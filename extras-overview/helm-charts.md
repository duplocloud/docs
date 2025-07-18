---
description: Information for using Helm Charts with DuploCloud
---

# Deploying Helm Charts

## Introduction

Helm Charts are packages of pre-configured Kubernetes resources that help you define, install, and upgrade Kubernetes applications. You can integrate Helm Charts with DuploCloud to deploy applications onto the Kubernetes clusters you've created in DuploCloud. This section includes general guidance and best practices for using Helm Charts.

For instructions on how to deploy Helm Charts from the DuploCloud Platform, see the [Helm Chart documentation](../kubernetes-overview/helm/helm-charts.md) in the Kubernetes User Guide.

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

Yes. Refer to this document to create an [Ingress](../kubernetes-overview/ingress-loadbalancer/adding-ingress.md). Note the generated Ingress class. Refer to the [Helm ](https://helm.sh/docs/)documentation, for information about how to enable Ingress and add a class for the Ingress.&#x20;

{% hint style="info" %}
For EKS, refer to the [EKS Ingress Annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.7/guide/ingress/annotations/) document for information on customizing annotations to your specific needs.
{% endhint %}

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
