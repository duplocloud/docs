---
description: >-
  Deploy DuploCloud AI HelpDesk on AWS EKS, on-premises k3s, Azure AKS, and GCP
  GKE.
---

# Systems Integrator Installation Guide

This guide provides deployment paths for AWS EKS, self-managed k3s, Azure AKS, and Google Kubernetes Engine (GKE), followed by platform-agnostic requirements and operational guidance.

### Choose a deployment path

| Environment                                       | Use this section                                                                                        |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| AWS EKS with Amazon Bedrock and IRSA              | [AWS EKS](systems-integrator-installation-guide.md#part-a--aws-eks-tested-walkthrough)                  |
| Self-managed or on-premises Kubernetes            | [On-premises k3s](systems-integrator-installation-guide.md#part-a2--on-premises-k3s-tested-walkthrough) |
| Azure Kubernetes Service with Azure AI            | [Azure AKS](systems-integrator-installation-guide.md#part-a3--azure-aks-tested-walkthrough)             |
| Google Kubernetes Engine with Bedrock credentials | [GCP GKE](systems-integrator-installation-guide.md#part-a4--gcp-gke-tested-walkthrough)                 |

{% hint style="info" %}
Replace every value in angle brackets, such as `<ADMIN_EMAIL>`, before applying commands or values files. Do not commit credentials, OAuth secrets, or MongoDB passwords to source control.
{% endhint %}

***

### Part A — AWS EKS walkthrough

#### A.1 Prerequisites and variables

#### Install the following:

* AWS CLI v2
* `kubectl` 1.26 or later
* Helm 3.12 or later
* `eksctl` 0.165 or later
* `jq` 1.6 or later
* OpenSSL 3
* AWS permissions to create EKS, IAM, EFS, and ACM resources

#### Before continuing, obtain:

* An AWS account and a Bedrock-capable region&#x20;
* Google OAuth client ID and secret
* Frontend and API hostnames
* A DNS zone and ACM certificate ARN
* Two public subnet IDs for the internet-facing Application Load Balancer

```bash
aws configure

# Or, with AWS IAM Identity Center:
aws sso login --profile <PROFILE>
export AWS_PROFILE=<PROFILE>

aws sts get-caller-identity
export AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
export AWS_REGION=us-west-2
```

#### A.2 Create the EKS cluster

```bash
eksctl create cluster \
  --name=helpdesk \
  --region=${AWS_REGION} \
  --version=1.35 \
  --nodegroup-name=hd-workers \
  --node-type=t3a.medium \
  --nodes=2 \
  --nodes-min=2 \
  --nodes-max=6 \
  --managed \
  --asg-access \
  --with-oidc

kubectl get nodes
kubectl cluster-info

export OIDC_PROVIDER=$(aws eks describe-cluster \
  --name helpdesk \
  --region ${AWS_REGION} \
  --query "cluster.identity.oidc.issuer" \
  --output text | sed 's|https://||')

export VPC_ID=$(aws eks describe-cluster \
  --name helpdesk \
  --region ${AWS_REGION} \
  --query "cluster.resourcesVpcConfig.vpcId" \
  --output text)
```

#### A.3 Install the AWS Load Balancer Controller

```bash
curl -o /tmp/alb-iam-policy.json \
  https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.7.1/docs/install/iam_policy.json

aws iam create-policy \
  --policy-name AWSLoadBalancerControllerIAMPolicy \
  --policy-document file:///tmp/alb-iam-policy.json

eksctl create iamserviceaccount \
  --cluster=helpdesk \
  --region=${AWS_REGION} \
  --namespace=kube-system \
  --name=aws-load-balancer-controller \
  --attach-policy-arn=arn:aws:iam::${AWS_ACCOUNT_ID}:policy/AWSLoadBalancerControllerIAMPolicy \
  --approve \
  --override-existing-serviceaccounts

helm repo add eks https://aws.github.io/eks-charts
helm repo update eks

helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
  --namespace kube-system \
  --set clusterName=helpdesk \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller \
  --set region=${AWS_REGION} \
  --set vpcId=${VPC_ID}
```

#### A.4 Configure shared EFS storage

Create the EFS CSI service account and add-on:

```bash
eksctl create iamserviceaccount \
  --cluster=helpdesk \
  --region=${AWS_REGION} \
  --namespace=kube-system \
  --name=efs-csi-controller-sa \
  --attach-policy-arn=arn:aws:iam::aws:policy/service-role/AmazonEFSCSIDriverPolicy \
  --approve \
  --override-existing-serviceaccounts

export EFS_CSI_ROLE_ARN=$(aws cloudformation describe-stacks \
  --region ${AWS_REGION} \
  --query "Stacks[?StackName=='eksctl-helpdesk-addon-iamserviceaccount-kube-system-efs-csi-controller-sa'].Outputs[0].OutputValue" \
  --output text)

aws eks create-addon \
  --cluster-name helpdesk \
  --region ${AWS_REGION} \
  --addon-name aws-efs-csi-driver \
  --service-account-role-arn ${EFS_CSI_ROLE_ARN}
```

Create an encrypted EFS file system, permit NFS from the VPC, and create mount targets:

```bash
export VPC_CIDR=$(aws ec2 describe-vpcs \
  --vpc-ids ${VPC_ID} \
  --query "Vpcs[0].CidrBlock" \
  --output text)

export EFS_SG_ID=$(aws ec2 create-security-group \
  --group-name helpdesk-efs-sg \
  --description "Security group for HelpDesk EFS" \
  --vpc-id ${VPC_ID} \
  --query "GroupId" \
  --output text)

aws ec2 authorize-security-group-ingress \
  --group-id ${EFS_SG_ID} \
  --protocol tcp \
  --port 2049 \
  --cidr ${VPC_CIDR}

export EFS_FS_ID=$(aws efs create-file-system \
  --creation-token helpdesk-efs \
  --performance-mode generalPurpose \
  --throughput-mode bursting \
  --encrypted \
  --region ${AWS_REGION} \
  --tags Key=Name,Value=helpdesk-efs \
  --query "FileSystemId" \
  --output text)

SUBNET_IDS=$(aws ec2 describe-subnets \
  --filters "Name=vpc-id,Values=${VPC_ID}" \
    "Name=tag:kubernetes.io/role/internal-elb,Values=1" \
  --query "Subnets[*].SubnetId" \
  --output text)

for SUBNET_ID in ${SUBNET_IDS}; do
  aws efs create-mount-target \
    --file-system-id ${EFS_FS_ID} \
    --subnet-id ${SUBNET_ID} \
    --security-groups ${EFS_SG_ID} || true
done
```

Create `efs-sc.yaml`:

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: efs-sc
provisioner: efs.csi.aws.com
parameters:
  provisioningMode: efs-ap
  fileSystemId: "${EFS_FS_ID}"
  directoryPerms: "700"
  gidRangeStart: "1000"
  gidRangeEnd: "2000"
  basePath: "/helpdesk"
mountOptions:
  - tls
```

```bash
kubectl apply -f efs-sc.yaml
```

#### A.5 Configure the EBS CSI driver

MongoDB requires block storage. Install the EBS CSI driver and retain `gp2` as the default storage class.

```bash
eksctl create iamserviceaccount \
  --cluster=helpdesk \
  --region=${AWS_REGION} \
  --namespace=kube-system \
  --name=ebs-csi-controller-sa \
  --attach-policy-arn=arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy \
  --approve \
  --override-existing-serviceaccounts

export EBS_CSI_ROLE_ARN=$(aws cloudformation describe-stacks \
  --region ${AWS_REGION} \
  --query "Stacks[?StackName=='eksctl-helpdesk-addon-iamserviceaccount-kube-system-ebs-csi-controller-sa'].Outputs[0].OutputValue" \
  --output text)

aws eks create-addon \
  --cluster-name helpdesk \
  --region ${AWS_REGION} \
  --addon-name aws-ebs-csi-driver \
  --service-account-role-arn ${EBS_CSI_ROLE_ARN}

kubectl annotate storageclass gp2 \
  storageclass.kubernetes.io/is-default-class=true --overwrite

kubectl annotate storageclass efs-sc \
  storageclass.kubernetes.io/is-default-class=false --overwrite
```

#### A.6 Install Cluster Autoscaler

```bash
helm repo add autoscaler https://kubernetes.github.io/autoscaler
helm repo update autoscaler

helm install cluster-autoscaler autoscaler/cluster-autoscaler \
  --namespace kube-system \
  --set autoDiscovery.clusterName=helpdesk \
  --set awsRegion=${AWS_REGION} \
  --set rbac.serviceAccount.name=cluster-autoscaler \
  --set rbac.serviceAccount.annotations."eks\.amazonaws\.com/role-arn"="" \
  --set extraArgs.balance-similar-node-groups=true \
  --set extraArgs.skip-nodes-with-system-pods=false
```

#### A.7 Create the Bedrock IRSA role

Save the following trust policy as `/tmp/bedrock-trust-policy.json`.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Federated": "arn:aws:iam::${AWS_ACCOUNT_ID}:oidc-provider/${OIDC_PROVIDER}"
      },
      "Action": "sts:AssumeRoleWithWebIdentity",
      "Condition": {
        "StringEquals": {
          "${OIDC_PROVIDER}:aud": "sts.amazonaws.com"
        },
        "StringLike": {
          "${OIDC_PROVIDER}:sub": "system:serviceaccount:helpdesk:*"
        }
      }
    }
  ]
}
```

Save the following permissions policy as `/tmp/bedrock-permissions-policy.json`.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "BedrockInvoke",
      "Effect": "Allow",
      "Action": [
        "bedrock:InvokeModel",
        "bedrock:InvokeModelWithResponseStream"
      ],
      "Resource": [
        "arn:aws:bedrock:*::foundation-model/*",
        "arn:aws:bedrock:*:${AWS_ACCOUNT_ID}:inference-profile/*"
      ]
    },
    {
      "Sid": "BedrockList",
      "Effect": "Allow",
      "Action": [
        "bedrock:ListFoundationModels",
        "bedrock:ListInferenceProfiles",
        "bedrock:GetFoundationModel"
      ],
      "Resource": "*"
    }
  ]
}
```

```bash
aws iam create-role \
  --role-name helpdesk-bedrock-role \
  --assume-role-policy-document file:///tmp/bedrock-trust-policy.json \
  --description "IRSA role for HelpDesk duplo-agent Bedrock access"

aws iam put-role-policy \
  --role-name helpdesk-bedrock-role \
  --policy-name BedrockInvokePolicy \
  --policy-document file:///tmp/bedrock-permissions-policy.json

export BEDROCK_ROLE_ARN="arn:aws:iam::${AWS_ACCOUNT_ID}:role/helpdesk-bedrock-role"
```

#### A.8 Create AWS Helm values

Create `values.yaml`.

```yaml
config:
  authFrontendBaseUrl: "https://<HELPDESK_FRONTEND_HOST>"
  authAllowedOrigins: "https://<HELPDESK_FRONTEND_HOST>"
  authSuperUsers: "<SUPER_ADMIN_EMAIL>"
  infraRegion: "us-west-2"
  aiStudioIsMasterDisabled: true
secrets:
  googleClientId: "<GOOGLE_CLIENT_ID>"
  googleClientSecret: "<GOOGLE_CLIENT_SECRET>"
mongodb:
  auth:
    enabled: true
    rootUser: "root"
    rootPassword: "<MONGODB_ROOT_PASSWORD>"
mongodbBackup:
  enabled: true
backend:
  persistence:
    storageClass: "efs-sc"
    accessModes:
      - ReadWriteMany
duploAgent:
  persistence:
    storageClass: "efs-sc"
    accessModes:
      - ReadWriteMany
  serviceAccount:
    irsaRoleArn: "arn:aws:iam::<AWS_ACCOUNT_ID>:role/helpdesk-bedrock-role"
  extraEnv:
    - name: CLAUDE_MODEL
      value: "us.anthropic.claude-sonnet-4-20250514-v1:0"
    - name: AWS_REGION
      value: "us-west-2"
ingress:
  enabled: true
  className: "alb"
  annotations:
    alb.ingress.kubernetes.io/certificate-arn: "<ACM_CERTIFICATE_ARN>"
    alb.ingress.kubernetes.io/listen-ports: '[{"HTTPS":443}]'
    alb.ingress.kubernetes.io/scheme: "internet-facing"
    alb.ingress.kubernetes.io/ssl-redirect: "443"
    alb.ingress.kubernetes.io/target-type: "ip"
    alb.ingress.kubernetes.io/subnets: "<SUBNET_1>,<SUBNET_2>"
  hosts:
    - host: "<HELPDESK_FRONTEND_HOST>"
      paths:
        - path: /
          pathType: Prefix
    - host: "<HELPDESK_API_HOST>"
      paths:
        - path: /
          pathType: Prefix
internalIngress:
  enabled: false
bedrockSubscription:
  enabled: true
  serviceAccount:
    irsaRoleArn: "arn:aws:iam::<AWS_ACCOUNT_ID>:role/helpdesk-bedrock-role"
slackBackend:
  enabled: false
teamsBackend:
  enabled: false
collector:
  enabled: false
coreMcp:
  enabled: false
clickhouse:
  enabled: false
```

#### A.9 Install and validate

{% hint style="info" %}
Do **not** use `--wait`; some components finish initialization asynchronously.
{% endhint %}

```bash
helm install helpdesk \
  oci://quay.io/duplocloud/helpdesk \
  --version 0.2.22 \
  --namespace helpdesk \
  --create-namespace \
  --values values.yaml \
  --timeout 10m

kubectl get pods -n helpdesk -w
kubectl get ingress -n helpdesk
```

Create DNS records for the frontend and API hosts that target the ALB hostname. Configure the identity provider with the appropriate callback, for example `https://<HELPDESK_FRONTEND_HOST>/signin-google`, then sign in as the configured superuser.

#### A.10 AWS validation checklist

* All pods in `helpdesk` become `Running` or complete successfully.
* Backend and agent persistent volumes bind to `efs-sc`.
* MongoDB uses the EBS-backed default storage class.
* The ALB has healthy targets and valid TLS.
* The configured Bedrock model is enabled in the chosen AWS Region.

***

### Part A2 — On-premises walkthrough

#### A2.1 Install k3s and Helm

The configuration is a single-server k3s deployment using NGINX Ingress, the chart-provided NFS server, a self-signed certificate, and static AWS credentials for Bedrock.

```bash
curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC='--disable traefik --tls-san <SERVER_PUBLIC_IP>' sh -

sudo kubectl get nodes

curl -sfL https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

sudo apt-get update
sudo apt-get install -y nfs-common
```

#### A2.2 Install NGINX Ingress

```bash
sudo helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

sudo helm install ingress-nginx ingress-nginx/ingress-nginx \
  -n ingress-nginx \
  --create-namespace \
  --set controller.hostNetwork=true \
  --set controller.service.type=ClusterIP \
  --set controller.kind=DaemonSet \
  --kubeconfig /etc/rancher/k3s/k3s.yaml
```

#### A2.3 Retrieve kubeconfig and create TLS material

```bash
scp user@<SERVER_IP>:/etc/rancher/k3s/k3s.yaml ./k3s-kubeconfig.yaml
sed -i 's/127.0.0.1/<SERVER_PUBLIC_IP>/g' k3s-kubeconfig.yaml

HOSTNAME="helpdesk.<SERVER_IP>.nip.io"
XTERM_HOSTNAME="xterm.<SERVER_IP>.nip.io"

openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout onprem-tls.key \
  -out onprem-tls.crt \
  -subj "/CN=$HOSTNAME" \
  -addext "subjectAltName=DNS:$HOSTNAME,DNS:$XTERM_HOSTNAME"

kubectl --kubeconfig k3s-kubeconfig.yaml create namespace helpdesk

kubectl --kubeconfig k3s-kubeconfig.yaml create secret tls helpdesk-tls \
  -n helpdesk \
  --cert=onprem-tls.crt \
  --key=onprem-tls.key
```

#### A2.4 Create on-premises Helm values

Create `values.yaml`. The AWS access keys must be permitted to invoke the selected Bedrock model.

```yaml
config:
  authFrontendBaseUrl: "https://helpdesk.<SERVER_IP>.nip.io"
  authAllowedOrigins: "https://helpdesk.<SERVER_IP>.nip.io"
  authSuperUsers: "<ADMIN_EMAIL>"
  infraRegion: "us-west-2"
  aiStudioIsMasterDisabled: true
secrets:
  googleClientId: "<GOOGLE_CLIENT_ID>"
  googleClientSecret: "<GOOGLE_CLIENT_SECRET>"
tolerations: []
mongodb:
  auth:
    rootUser: "authuser"
    rootPassword: "<MONGODB_PASSWORD>"
  persistence:
    enabled: true
    size: 8Gi
  tolerations: []
mongodbBackup:
  enabled: true
  schedule: "0 2 * * *"
  storage:
    size: 25Gi
  tolerations: []
nfs-server:
  enabled: true
  storageClass:
    name: "nfs"
  tolerations: []
backend:
  persistence:
    enabled: true
    accessModes:
      - ReadWriteMany
    size: 10Gi
duploAgent:
  persistence:
    storageClass: "nfs"
  extraEnv:
    - name: CLAUDE_MODEL
      value: "us.anthropic.claude-sonnet-4-6"
    - name: AWS_ACCESS_KEY_ID
      value: "<AWS_ACCESS_KEY>"
    - name: AWS_SECRET_ACCESS_KEY
      value: "<AWS_SECRET_KEY>"
    - name: AWS_REGION
      value: "us-west-2"
xterm:
  hostname: "xterm.<SERVER_IP>.nip.io"
ingress:
  enabled: true
  className: "nginx"
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
    nginx.ingress.kubernetes.io/proxy-body-size: "50m"
    nginx.ingress.kubernetes.io/proxy-buffer-size: "16k"
  tls:
    - secretName: "helpdesk-tls"
      hosts:
        - "helpdesk.<SERVER_IP>.nip.io"
        - "xterm.<SERVER_IP>.nip.io"
internalIngress:
  enabled: false
bedrockSubscription:
  enabled: false
slackBackend:
  enabled: false
teamsBackend:
  enabled: false
collector:
  enabled: false
coreMcp:
  enabled: false
clickhouse:
  enabled: false
```

#### A2.5 Install, grant agent privileges, and trust the certificate

```bash
helm install helpdesk \
  oci://quay.io/duplocloud/helpdesk \
  --version 0.2.22 \
  --namespace helpdesk \
  --values values.yaml \
  --kubeconfig k3s-kubeconfig.yaml \
  --timeout 10m

kubectl --kubeconfig k3s-kubeconfig.yaml patch deployment helpdesk-duplo-agent \
  -n helpdesk \
  --type=json \
  -p '[
    {
      "op": "add",
      "path": "/spec/template/spec/containers/0/securityContext/privileged",
      "value": true
    }
  ]'

kubectl --kubeconfig k3s-kubeconfig.yaml create configmap helpdesk-ca-cert \
  -n helpdesk \
  --from-file=ca.crt=onprem-tls.crt
```

Mount the CA ConfigMap into the agent and set `NODE_EXTRA_CA_CERTS`, `SSL_CERT_FILE`, and `REQUESTS_CA_BUNDLE` to `/etc/ssl/custom-certs/ca.crt`. Restart the agent deployment and validate pod health, OAuth sign-in, and an agent request.

***

### Part A3 — Azure AKS walkthrough

#### A3.1 Create the AKS cluster

```bash
az login

az group create \
  --name helpdesk-si-test \
  --location eastus

az aks create \
  --resource-group helpdesk-si-test \
  --name helpdesk-aks \
  --node-count 2 \
  --node-vm-size Standard_B4ms \
  --generate-ssh-keys \
  --enable-managed-identity \
  --network-plugin azure

az aks get-credentials \
  --resource-group helpdesk-si-test \
  --name helpdesk-aks
```

#### A3.2 Install NGINX Ingress

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

helm install ingress-nginx ingress-nginx/ingress-nginx \
  -n ingress-nginx \
  --create-namespace \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"="/healthz"
```

#### A3.3 Configure values for Azure AI

Use the same NFS, MongoDB, ingress, and TLS configuration pattern as the on-premises deployment. Set the HelpDesk endpoint and Azure AI credentials as follows:

```yaml
config:
  authFrontendBaseUrl: "https://<HELPDESK_FRONTEND_HOST>"
  authAllowedOrigins: "https://<HELPDESK_FRONTEND_HOST>"
  authSuperUsers: "<ADMIN_EMAIL>"
  infraRegion: ""
  azureBaseUrl: "https://<RESOURCE_NAME>.services.ai.azure.com/anthropic"
secrets:
  googleClientId: "<GOOGLE_CLIENT_ID>"
  googleClientSecret: "<GOOGLE_CLIENT_SECRET>"
  azureClientId: "<AZURE_CLIENT_ID>"
  azureClientSecret: "<AZURE_CLIENT_SECRET>"
duploAgent:
  extraEnv:
    - name: CLAUDE_MODEL
      value: "claude-sonnet-4-6"
    - name: AZURE_BASE_URL
      value: "https://<RESOURCE_NAME>.services.ai.azure.com/anthropic"
    - name: AZURE_CLIENT_ID
      value: "<AZURE_CLIENT_ID>"
```

Install the chart using the standard Helm command, then grant the agent the permissions required to manage its workload:

```bash
kubectl patch deployment helpdesk-duplo-agent \
  -n helpdesk \
  --type=json \
  -p '[
    {
      "op": "replace",
      "path": "/spec/template/spec/containers/0/securityContext",
      "value": {
        "privileged": true,
        "runAsUser": 0,
        "runAsGroup": 0,
        "seccompProfile": {
          "type": "Unconfined"
        },
        "capabilities": {
          "add": [
            "SYS_ADMIN",
            "NET_ADMIN"
          ]
        }
      }
    }
  ]'

kubectl exec -n helpdesk deploy/helpdesk-duplo-agent -- \
  sh -c "mkdir -p /home/appuser/.claude/projects && chown -R root:root /home/appuser"
```

### Part A4 — GCP GKE walkthrough

#### A4.1 Create the GKE cluster

```bash
gcloud auth login
gcloud config set project <PROJECT_ID>

gcloud container clusters create helpdesk-gke \
  --region us-central1 \
  --num-nodes 1 \
  --machine-type e2-standard-4 \
  --disk-size 100 \
  --enable-ip-alias

gcloud container clusters get-credentials helpdesk-gke \
  --region us-central1
```

#### A4.2 Install NGINX Ingress and HelpDesk

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

helm install ingress-nginx ingress-nginx/ingress-nginx \
  -n ingress-nginx \
  --create-namespace
```

Use the on-premises values pattern for NFS-backed RWX storage and supply static AWS credentials to `duploAgent.extraEnv` for Amazon Bedrock access. Create a TLS secret for the public frontend and xterm hostnames, install the chart, then apply the same privileged-agent and custom-CA configuration used for on-premises deployments.

```bash
gcloud container clusters delete helpdesk-gke \
  --region us-central1 \
  --quiet
```

***

### Part B — Platform-agnostic requirements and reference

#### B.1 Kubernetes and compute requirements

* Kubernetes 1.26 or later is required;&#x20;
* The Helm chart and images are `amd64`.
* Plan approximately **2.1 vCPU** and **2.2 GiB** of memory as a baseline, excluding workload growth.
* Start with at least two nodes where high availability is required. Configure autoscaling to a maximum of six or more nodes based on demand.

#### B.2 Storage requirements

HelpDesk backend and agent data require **ReadWriteMany (RWX)** storage. Plan at least 10 GiB with POSIX UID/GID `1000`; use a reclaim policy of `Retain` and volume expansion where supported. MongoDB requires a separate **ReadWriteOnce (RWO)** volume of at least 8 GiB, and backups require at least 25 GiB.

Supported patterns include Amazon EFS, Google Filestore, Azure Files NFS, NFS subdir provisioners, CephFS, Portworx Sharedv4, and Longhorn RWX.

#### B.3 Ingress, TLS, DNS, and egress

Ingress must support host routing, WebSockets, a 50 MiB request body, and a 16 KiB proxy buffer. Set long timeouts for interactive agent requests:

```yaml
nginx.ingress.kubernetes.io/proxy-buffer-size: "16k"
nginx.ingress.kubernetes.io/proxy-body-size: "50m"
nginx.ingress.kubernetes.io/proxy-read-timeout: "3600"
nginx.ingress.kubernetes.io/proxy-send-timeout: "3600"
```

TLS is mandatory. Provide distinct frontend and agent/xterm hostnames where applicable. Permit outbound access to Quay, Docker registries as needed, the configured LLM provider, and the identity provider. Air-gapped deployment is not validated by this guide.

#### B.4 Identity provider configuration

Google, Microsoft, Okta, and Keycloak are supported identity-provider patterns. Configure the callback URL exactly as:

```
https://<PRIMARY_HOSTNAME>/signin-<provider>
```

Set CORS origins to the exact public frontend origin, including the scheme, and configure at least one superuser before the first login.

#### B.5 Agent permissions

The agent needs `SYS_ADMIN` and `NET_ADMIN` capabilities. Some environments require a privileged container or an explicit Pod Security Admission exemption. Validate this requirement with the cluster security team before production rollout.

#### B.6 Model identifiers

Use the provider-specific model format:

| Provider                            | Example model identifier                     |
| ----------------------------------- | -------------------------------------------- |
| Amazon Bedrock                      | `us.anthropic.claude-sonnet-4-20250514-v1:0` |
| Azure AI / direct Anthropic pattern | `claude-sonnet-4-20250514`                   |

For Bedrock, the IAM policy must allow both foundation-model and inference-profile resources.

#### B.7 Taints and tolerations

When using dedicated nodes, define matching tolerations in the values file:

```yaml
hdTolerations: &hdTolerations
  - key: dedicated
    value: hd
    operator: Equal
    effect: NoSchedule
```

To explicitly override inherited tolerations:

```yaml
hdTolerations: &hdTolerations []
```

#### B.8 Helm lifecycle operations

Do not change an existing `encryptionMasterKey`. Preserve it through upgrades and restores.

```bash
helm install si oci://quay.io/duplocloud/helpdesk \
  --version 0.2.22 \
  --namespace si \
  --create-namespace \
  -f values.yaml

helm upgrade si oci://quay.io/duplocloud/helpdesk \
  --version <NEW_VERSION> \
  --namespace si \
  -f values.yaml

helm rollback si <REVISION> --namespace si

helm uninstall si --namespace si
```

#### B.9 Troubleshooting quick reference

| Symptom                                    | Check                                                                            |
| ------------------------------------------ | -------------------------------------------------------------------------------- |
| Pods remain `Pending`                      | Node capacity, matching tolerations, and storage provisioning                    |
| MongoDB cannot schedule                    | RWO storage class and zone affinity                                              |
| Bedrock `AccessDenied`                     | Region access, model enablement, and inference-profile IAM resources             |
| Ingress returns 413 or header errors       | 50 MiB body size and 16 KiB proxy buffer annotations                             |
| Agent cannot perform privileged operations | Pod Security Admission policy, `privileged`, `SYS_ADMIN`, and `NET_ADMIN`        |
| Certificate errors in the agent            | Mounted CA bundle and `NODE_EXTRA_CA_CERTS`/`SSL_CERT_FILE`/`REQUESTS_CA_BUNDLE` |
| OAuth callback fails                       | Exact callback URL and exact CORS origin                                         |
| Image pull failures                        | Egress access to Quay and required registries                                    |

#### B.10 Support handoff commands

Collect the following before escalating an installation issue:

```bash
kubectl get events -n si --sort-by='.lastTimestamp'
kubectl get pods -n si -o wide
kubectl logs -n si <POD_NAME> --tail=200
kubectl logs -n si <POD_NAME> --previous --tail=200
kubectl describe pod -n si <POD_NAME>
kubectl get pvc -n si
helm status si -n si
helm get values si -n si
kubectl get ingress -n si -o yaml
```

Include the chart version, Kubernetes version, cloud region, sanitized values file, relevant events, and pod logs in the handoff.

#### B.11 Where to Send It

| Channel                             | Use When                                      |
| ----------------------------------- | --------------------------------------------- |
| DuploCloud Slack #si-support        | First-line support; most issues resolved here |
| DuploCloud support portal           | Formal ticket with SLA tracking               |
| GitHub Issues (duplocloud/helpdesk) | Bug reports with reproduction steps           |

<br>
