---
description: Kubectl setup on your local computer
---

# Kubectl setup

The goal of this section is to show how to set up Kubectl on a local computer pointing to Kubernetes cluster with cluster-admin privileges.

Navigate to the **Administrators -> Infrastructure** page and click the infrastructure in the list to go to a infrastructure to which Kubectl need to be set up. Within the infrastructure' detail page select the tab labeled 'EKS' and click the blue **+ Download Kube Config** button to download the kube-config file.

![](../.gitbook/assets/kubectl-config-download.jpg)

If you don't have Kubectl installed on your local computer. Follow the instruction in the below link to install Kubectl.

{% embed url="https://kubernetes.io/docs/tasks/tools" %}

Run the below command to point Kubectl to use the downloaded kube-config file.

* For linux or MacOS

```shell
export KUBECONFIG=/home/duplo/duploinfra-finance.yaml #CHANGE ME
```

* For Windows

```powershell
setx KUBECONFIG "%USERPROFILE%\Downloads\duploinfra-finance.yaml" #CHANGE ME
```

