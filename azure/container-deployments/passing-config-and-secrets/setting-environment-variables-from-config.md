---
description: Set EVs from the Kubernetes ConfigMap
---

# Setting Environment Variables (EVs) from a ConfigMap or Secret

In Kubernetes, you populate environment variables from application configurations or secrets.

## Setting Environment Variables from a Kubernetes ConfigMap

{% hint style="info" %}
Before you create the Kubernetes [ConfigMap](https://kubernetes.io/docs/concepts/configuration/configmap/), you must create a DuploCloud [Service](../../azure-services/containers/).&#x20;
{% endhint %}

### Create the Kubernetes ConfigMap&#x20;

1. In the DuploCloud Portal, navigate to the **DevOps** -> **Containers** -> **AKS / Native** page.
2. Click the **K8S Config Maps** tab.&#x20;
3. Click **Add**. The **Add Kubernetes Config Map** pane displays.&#x20;
4. Name the ConfigMap you want to create, such as `my-config-map`.&#x20;
5. Add a **Data** key/value pair for each file in your ConfigMap, separated by a colon (**`:`**). The key is the file name, and the value is the file's contents.&#x20;
6. Click **Create**.

![Add Kubernetes Config Map pane](<../../../.gitbook/assets/Screen Shot 2022-03-21 at 12.04.45 PM.png>)

### Editing the DuploCloud Service

1. In the DuploCloud Portal, navigate to the **DevOps -> Containers -> AKG/ Native** page.
2. Click the **Services** tab.
3. Select the service you want to modify from the **Name** column.
4. Click the **Actions** menu and select **Edit**.

### Configure Environment Variables

You can import the entire ConfigMap as Environment Variables or choose specific keys to import as environment variables.

#### Import the entire ConfigMap as Environment Variables

The most straightforward approach is to import the entire ConfigMap as environment variables.  Using this approach, your service will recognize each key in the ConfigMap defined as an environment variable.

1. On the **Edit Service: **_**service\_name**_** Basic Options** page, click **Next** to navigate to the **Advanced Options** page.
2. On the **Advanced Options** page, in the **Other Container Config** field, enter the configuration YAML to import environment variables from a ConfigMap.  For example, to import all environment variables from a ConfigMap named `my-env-vars`, use the following YAML:&#x20;

```yaml
EnvFrom:
- ConfigMapRef:
    Name: my-env-vars
```

![Defining Other Container Config on the Advanced Options page ](<../../../.gitbook/assets/Screen Shot 2022-03-21 at 12.15.35 PM.png>)

{% hint style="info" %}
To import from additional ConfigMaps, duplicate the YAML from lines 2 and 3 in the above example for each config map that you want to import from.
{% endhint %}

#### Select individual Environment Variable from a Config Map

Another approach is to select which keys to import from the ConfigMap as environment variables.  This method gives you complete control over each environment variable as well as its name,  but it requires you to perform more manual configuration.

1. [Edit the DuploCloud Service](setting-environment-variables-from-config.md#editing-the-duplocloud-service).
2. On the **Edit Service: **_**service\_name**_** Basic Options** page, in the **Environment Variables** field, enter the configuration for choosing environment variables to import from a ConfigMap.  For example, to set a single environment variable (`ENV_VAR_ONE)` to the value of the `MY_ENV_VAR` key in the `my-env-vars` config map, use the following YAML:

```yaml
- Name: ENV_VAR_ONE
  ValueFrom:
    ConfigMapKeyRef:
      Name: my-env-vars
      Key: MY_ENV_VAR
```

{% hint style="info" %}
To add additional environment variables, duplicate the YAML from lines 2 through 5 in the above example for each environment variable that you want to add.
{% endhint %}

## Setting Environment Variables from a Kubernetes Secret

You can import Kubernetes Secrets as Environment Variables.&#x20;

### Create the Kubernetes Secret

1. In the DuploCloud Portal, navigate to the **DevOps -> Containers -> AKG/ Native** page.
2. Click the **K8S Secrets** tab.
3. Click **Add**. The **Add Kubernetes Secret** page opens.
4. Create a Secret Name, such as `my-env-vars`.
5. From the **Secret Type** list box, select **Opaque**.
6. In the **Secret Details** field, Add **Data** key/value pairs for each Environment Variable in your ConfigMap, separated by a colon (**`:`**). The key is the Environment Variable name, and the value is the Environment Variable's value.
7. Click **Add to create the secret.**

![Add Kubernetes Secret page](<../../../.gitbook/assets/Screen Shot 2022-03-21 at 12.34.20 PM.png>)

### Configure Environment Variables

{% hint style="info" %}
Before you configure Environment Variables, you must create a DuploCloud [Service](../../azure-services/containers/).
{% endhint %}

#### Import the entire Secret as Environment Variables

The most straightforward approach is to import the entire Secret as environment variables.  Using this approach, your service will recognize each key in the Secret defined as an environment variable.

1. [Edit the DuploCloud Service](setting-environment-variables-from-config.md#editing-the-duplocloud-service).
2. On the **Edit Service: **_**service\_name**_** Basic Options** page, click **Next** to navigate to the **Advanced Options** page.
3. On the **Advanced Options** page, in the **Other Container Config** field, enter the configuration YAML to import environment variables from a Secret.  For example, to import all environment variables from a secret named `my-env-vars`, use the following YAML:&#x20;

```yaml
EnvFrom:
- SecretRef:
    Name: my-env-vars
```

![Defining Other Container Config on the Advanced Options page ](<../../../.gitbook/assets/Screen Shot 2022-03-21 at 12.39.58 PM.png>)

{% hint style="info" %}
To import from additional secrets, duplicate the YAML from lines 2 and 3 in the above example for each secret that you want to import.
{% endhint %}

#### Select individual Environment Variables from a Secret

Another approach is to select which keys to import from the Secret as environment variables.  This method gives you complete control over each environment variable as well as its name, but it requires you to perform more manual configuration.

1. [Edit the DuploCloud Service](setting-environment-variables-from-config.md#editing-the-duplocloud-service).
2. On the **Edit Service: **_**service\_name**_** Basic Options** page, in the **Environment Variables** field, enter the configuration for choosing specific environment variables to import from a Secret.  For example, to set a single environment variable (`ENV_VAR_ONE)` to the value of the `SECRET_ENV_VAR` key in the `my-env-vars` secret, use the following YAML:

```yaml
- Name: ENV_VAR_ONE
  ValueFrom:
    SecretKeyRef:
      Name: my-env-vars
      Key: SECRET_ENV_VAR
```

{% hint style="info" %}
To import from additional secrets, duplicate the YAML from lines 2 and 5 in the above example for each secret that you want to import.
{% endhint %}
