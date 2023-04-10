---
description: Mounting Kubernetes ConfigMaps as files
---

# Mounting Config as Files

In Kubernetes, you can mount application configuration or secrets as files.

## Mount a Kubernetes ConfigMap

The basic steps are:

1. Create a Kubernetes ConfigMap
2. Edit the Service, and add a volume that refers to the config map

### Create the Kubernetes ConfigMap&#x20;

Navigate to the **DevOps -> Containers -> EKS / Native** page and click the **Kubernetes Config Maps** tab.  Click the blue **+ Add** button to open the 'Add Kubernetes Config Map' form.

![](<../../../../.gitbook/assets/Screen Shot 2022-03-21 at 11.39.39 AM.png>)

* Give your config map a name, such as `my-config-map`.
* Add a data key / value pair for each file that you want to have in your config map.  The key will be the file name, and the value will be the file contents.

Click **Create** to create the config map.

### Mount the Kubernetes ConfigMap as a volume

Navigate to the **DevOps -> Containers -> EKS / Native** page and click the **Services** tab.   In the **Actions** column, click the ![](<../../../../.gitbook/assets/Screen Shot 2022-03-21 at 11.44.25 AM.png>) edit icon for the service that you want to edit.&#x20;

The volume configuration is on the second _(Advanced Options)_ page, so click the **Next ->** button to skip to that page.

![](<../../../../.gitbook/assets/Screen Shot 2022-03-21 at 11.48.48 AM.png>)

In the _Volumes_ field, enter configuration YAML to mount your config map as a volume.  For example, to mount a config map named `my-config-map` to a directory named `/app/my-config`, you could use the following YAML:

```yaml
- Name: my-config
  Path: /app/my-config
  Spec:
    ConfigMap:
      Name: my-config-map
```

#### Optional Settings for Mounting ConfigMaps

If you want to pick and choose individual ConfigMap items and specify the subpath it will be mounted at, you can use different configuration.  For example, if you want the key named `my-file-name` to mounted to `/app/my-config/config-file` , you could use the following YAML:

```yaml
  Path: /app/my-config
  Spec:
    ConfigMap:
      Name: my-config-map
      Items:
      - Key: my-file-name
        Path: config-file
```

## Mount a Kubernetes Secret

The basic steps are:

1. Create a Kubernetes Secret
2. Edit the Service, and add a volume that refers to the secret

### Create the Kubernetes Secret&#x20;

Navigate to the **DevOps -> Containers -> EKS / Native** page and click the **Kubernetes Secrets** tab.  Click the blue **+ Add** button to open the 'Add Kubernetes Secret' form.

![](<../../../../.gitbook/assets/Screen Shot 2022-03-21 at 12.50.14 PM.png>)

* Give your secret a name, such as `my-secret-files`.
* Add a data key / value pair for each file that you want to have in your secret.  The key will be the file name, and the value will be the file contents.

Click **Add** to create the secret.

### Create a multi-line Kubernetes Secret

See below example:

![](<../../../../.gitbook/assets/Screen Shot 2022-08-10 at 4.25.05 PM.png>)

### Mount the Kubernetes Secret as a volume

Navigate to the **DevOps -> Containers -> EKS / Native** page and click the **Services** tab.   In the **Actions** column, click the ![](<../../../../.gitbook/assets/Screen Shot 2022-03-21 at 11.44.25 AM.png>) edit icon for the service that you want to edit.&#x20;

The volume configuration is on the second _(Advanced Options)_ page, so click the **Next ->** button to skip to that page.

![](<../../../../.gitbook/assets/Screen Shot 2022-03-21 at 12.52.19 PM.png>)

In the _Volumes_ field, enter configuration YAML to mount your secret as a volume.  For example, to mount a secret named `my-secret-files` to a directory named `/app/my-config`, you could use the following YAML:

```yaml
- Name: my-config
  Path: /app/my-config
  Spec:
    Secret:
      SecretName: my-secret-files
```

#### Optional Settings for Mounting Secrets

If you want to pick and choose individual Secret items and specify the subpath it will be mounted at, you can use different configuration.  For example, if you want the key named `secret-file` to mounted to `/app/my-config/config-file` , you could use the following YAML:

```yaml
- Name: my-config
  Path: /app/my-config
  Spec:
    Secret:
      SecretName: my-secret-files
      Items:
      - Key: secret-file
        Path: config-file
```
