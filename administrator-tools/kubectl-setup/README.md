---
description: Accessing Kubectl on your local computer with the Administrator role
---

# Kubectl setup for administrators

As an Administrator, you can access `kubectl`on a local computer to a Kubernetes cluster with `cluster-admin` privileges to download and run `kubeconfig`.

## Downloading kubeconfig&#x20;

1. In the DuploCloud Portal, navigate to **Administrators** -> **Infrastructure.**
2. In the Name column, select the Infrastructure in which you want to set up `kubectl`.&#x20;
3. Click the **EKS** (for AWS and GCP) tab or the **AKS** (for Azure) tab.
4. Click **Download Kube Config** to download the `kubeconfig` file.

![EKS tab with Download Kube Config button](../../.gitbook/assets/kubectl-config-download.jpg)

## Installing kubectl on your local computer

1. Use these [tools ](https://kubernetes.io/docs/tasks/tools/)to install `kubectl` locally.
2. Run these commands to enable `kubectl` to use the downloaded `kubeconfig`.

* For Linux or macOS:

```shell
export KUBECONFIG=/home/duplo/duploinfra-INFRASTRUCTURE_NAME.yaml # INFRASTRUCTURE_NAME is your DuploCloud Infrastructure name.
```

* For Windows:

```powershell
setx KUBECONFIG "%USERPROFILE%\Downloads\duploinfra-INFRASTRUCTURE_NAME.yaml" # INFRASTRUCTURE_NAME is your DuploCloud Infrastructure name.
```

