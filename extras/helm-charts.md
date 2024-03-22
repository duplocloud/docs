---
description: Deploying Helm Charts in DuploCloud
---

# Helm Charts

## Introduction

Helm Charts are packages of pre-configured Kubernetes resources that help you define, install, and upgrade Kubernetes applications. You can integrate Helm Charts with DuploCloud to deploy applications onto the Kubernetes clusters you've created in DuploCloud.

## Deploying Helm Charts

### **Step 1. Prepare Your Environment**:

* Ensure you have a Kubernetes cluster set up in DuploCloud.&#x20;
* Install Helm on your local machine or a machine with access to your Kubernetes cluster.

### **Step 2. Choose or Create Helm Charts**:

* Identify the Helm charts you want to use for deploying your applications or services. You can use community-maintained charts from public repositories like Helm Hub, or you can create your own custom charts tailored to your specific needs.

### **Step 3. Customize Helm Charts**:

* Modify the values.yaml file or create custom templates as necessary. This might involve configuring resource limits, environment variables, or other settings specific to your deployment.&#x20;
* The following YAML is an example of a values file modified to deploy using the API key: DUPLO\_API\_SECRET, on the cluster: DUPLO\_CLUSTER cluster, in the awsprod environment: &#x20;

```yaml
duplocloud:
  apiKeyExistingSecret: DUPLO_API_SECRET
  apm:
    portEnabled: true
  clusterName: DUPLU_CLUSTER
  logs:
    enabled: true
    containerCollectAll: true
    containerCollectUsingFiles: false
  tags:
  - env:awsprod
```

* You can also modify Helm Chart values using the node selector. This is the most common method. For example, to deploy a chart into the duploservices-mytenant Tenant using the node selector, give:

{% code fullWidth="false" %}
```yaml
nodeSelector:
  tenantname: duploservices-mytenant
```
{% endcode %}

* To specify which hosts the chart should run on using the node selector with  allocation tags, give:

```yaml
nodeSelector:
  tenantname: duploservices-mytenant
  allocationtags: mychart
```

### &#x20;**Step 4. Add Helm Repositories (if using external charts)**:

* If you're using Helm charts from external repositories, add the repositories to your Helm configuration using the helm repo add command:

`helm repo add`` `_**`REPOSITORY_NAME REPOSITORY_URL`**_&#x20;

### **Step 5. Update Helm Repositories**:

* Update your Helm repositories to ensure you have the latest versions of the charts available locally using the helm repo update command:

`helm repo update`

### **Step 6. Deploy Helm Charts**:

* Use the helm install command to deploy the Helm charts onto your Kubernetes cluster. Specify the release name, chart name, and any additional configuration values as needed.

`helm install`` `_**`[RELEASE_NAME] [CHART] [FLAGS]`**_

### **Step 7. Monitor Deployments**:

* Monitor the status of your deployments in DuploCloud by navigating to the Services page. Services deployed via Helm Chart are displayed in the Services list in read-only mode. Although you can't make changes to a Helm Service in DuploCloud, you can view the Service details to verify that it has deployed successfully and is running as expected.&#x20;

## Helm Chart Best Practices

### Namespaces

Give your Helm Chart a duploservices-tenant namespace to deploy into. If you create your own namespace, you will have to manage those resources outside of DuploCloud. It may be helpful to create a single-purpose Tenant to use with your chart or use allocation tags to assign different node types to your chart's Pods.

### Customizing values

The node selector is the most common method for customizing Helm Chart values. For an example of using the node selector to modify chart values, see the syntax above under Step 3.&#x20;

If the chart you are deploying has interactions with Kubernetes resources (Pods, jobs, etc.) ServiceAccounts may be needed. Generally, the default ServiceAccounts chart configuration is sufficient.

When creating a Load Balancer in DuploCloud, ensure that the Helm Chart is not creating a Kubernetes Service with the same name as the deployment. This can cause a naming conflict since DuploCloud needs to manage the Kubernetes Service for the Load Balancer to work.&#x20;

### Viewing Helm deployments in the DuploCloud portal

DuploCloud Helm Chart deployments are displayed in the list of Services, in read-only mode. You can attach a Load Balancer to the Service via the Service details page Load Balancer tab, but you cannot update the Service (e.g., change the replica count or image) from within the DuploCloud UI. Those changes must be done through Helm.

### Creating a Load Balancer in DuploCloud: do I need Ingress?

Yes. Refer to this document to create an [Ingress](../aws/aws-services/adding-ingress.md). Note the generated Ingress class. Refer to the [Helm ](https://helm.sh/docs/)documentation, for information about how to enable Ingress and add a class for the Ingress.&#x20;

{% hint style="info" %}
For EKS, refer to the [EKS Ingress Annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.7/guide/ingress/annotations/) document for information on customizing annotations to your specific needs.
{% endhint %}

{% code title="" %}
```yaml
ingress: 
  enabled: true
  className: alb
  annotations: 
    # name the alb and group so more than one ingress single alb
    alb.ingress.kubernetes.io/load-balancer-name: myapp
    alb.ingress.kubernetes.io/group.name: myapp
    
    # use tenant alb security groups and networking
    alb.ingress.kubernetes.io/security-groups: ${alb_security_groups}
    alb.ingress.kubernetes.io/target-type: "ip"
    
    # enable https
    alb.ingress.kubernetes.io/certificate-arn: ${cert_arn}
    alb.ingress.kubernetes.io/listen-ports: "[{\"HTTPS\": 443}]"
    
    # makes a private alb
    alb.ingress.kubernetes.io/scheme: "internal"
    alb.ingress.kubernetes.io/subnets: ${internal_subnets}
  hosts:
  - host: myapp.${domain}
    paths:
    - path: /*
      pathType: ImplementationSpecific
      port: 3301
```
{% endcode %}
