---
description: Install kubectl on your local computer for use with DuploCloud
---

# Install Kubectl

## Installing `kubectl`

Install `kubectl` on your local computer:

1. Use these [tools ](https://kubernetes.io/docs/tasks/tools/)to install `kubectl` locally.
2. Run these commands to enable `kubectl` to use the downloaded `kubeconfig`.

### **For Linux or macOS**

```shell
export KUBECONFIG=/home/duplo/duploinfra-INFRASTRUCTURE_NAME.yaml # INFRASTRUCTURE_NAME is your DuploCloud Infrastructure name.
```

### **For Windows**

```powershell
setx KUBECONFIG "%USERPROFILE%\Downloads\duploinfra-INFRASTRUCTURE_NAME.yaml" # INFRASTRU
```
