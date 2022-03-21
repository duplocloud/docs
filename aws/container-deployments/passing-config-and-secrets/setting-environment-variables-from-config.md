# Setting Environment Variables from Config

In Kubernetes, you can populate environment variables from application configuration or secrets.

## Setting Environment Variables from a Kubernetes ConfigMap

The basic steps are:

1. Create a Kubernetes ConfigMap
2. Edit the Service, and add configuration to import environment variables from the config map

### Create the Kubernetes ConfigMap&#x20;

Navigate to the **DevOps -> Containers -> EKS / Native** page and click the **Kubernetes Config Maps** tab.  Click the blue **+ Add** button to open the 'Add Kubernetes Config Map' form.

![](<../../../.gitbook/assets/Screen Shot 2022-03-21 at 12.04.45 PM.png>)

* Give your config map a name, such as `my-env-vars`.
* Add a data key / value pair for each environment variable in your config map.  The key will be the environment variable name, and the value will be the environment variable value.

Click **Create** to create the config map.

### Configure Environment Variables

Navigate to the **DevOps -> Containers -> EKS / Native** page and click the **Services** tab.   In the **Actions** column, click the ![](<../../../.gitbook/assets/Screen Shot 2022-03-21 at 11.44.25 AM.png>) edit icon for the service that you want to edit.&#x20;

#### Import the entire ConfigMap as Environment Variables

The simplest approach to import the entire ConfigMap as environment variables.  Your service will see each key in the config map defined as an environment variable - so you will not need to set environment variables one by one.

The option to import an entire ConfigMap is on the second _(Advanced Options)_ page, so click the **Next ->** button to skip to that page.

![](<../../../.gitbook/assets/Screen Shot 2022-03-21 at 12.15.35 PM.png>)

In the _Other Container Config_ section, enter the configuration for importing environment variables from a config map.  For example, to import all environment variables from a config map named `my-env-vars`, you could use the following YAML:

```yaml
EnvFrom:
- ConfigMapRef:
    Name: my-env-vars
```

To import from additional config maps, you can simply repeat the YAML from lines 2 and 3 above for each config map that you want to import from.

#### Pick and Choose individual Environment Variable from a Config Map

Another approach is to pick and choose which keys to import from the ConfigMap as environment variables.  This method gives you complete control over each environment variable as well as its name - but it requires more configuration on your part.

The option to set individual environment variables is on the first _(Basic Options)_ page.

In the _Environment Variables_ section, enter the configuration for choosing environment variables to import from a config map.  For example, to set a single environment variable `ENV_VAR_ONE` to the value of the `MY_ENV_VAR` key in the `my-env-vars` config map, you could use the following YAML:

```yaml
- Name: ENV_VAR_ONE
  ValueFrom:
    ConfigMapKeyRef:
      Name: my-env-vars
      Key: MY_ENV_VAR
```

To add additional environment variables, you can simply repeat the YAML from lines 2 through 5 above for each environment variable that you want to add.

## Setting Environment Variables from a Kubernetes Secret

The basic steps are:

1. Create a Kubernetes Secret
2. Edit the Service, and add configuration to import environment variables from the secret

### Create the Kubernetes Secret

Navigate to the **DevOps -> Containers -> EKS / Native** page and click the **Kubernetes Secrets** tab.  Click the blue **+ Add** button to open the 'Add Kubernetes Secret' form.

![](<../../../.gitbook/assets/Screen Shot 2022-03-21 at 12.34.20 PM.png>)

* Give your secret a name, such as `my-env-vars`.
* Pick the `Opaque` secret type.
* Add a data key / value pair for each environment variable in your config map.  The key will be the environment variable name, and the value will be the environment variable value.

Click **Add** to create the secret.

### Configure Environment Variables

Navigate to the **DevOps -> Containers -> EKS / Native** page and click the **Services** tab.   In the **Actions** column, click the ![](<../../../.gitbook/assets/Screen Shot 2022-03-21 at 11.44.25 AM.png>) edit icon for the service that you want to edit.&#x20;

#### Import the entire Secret as Environment Variables

The simplest approach to import the entire Secret as environment variables.  Your service will see each key in the secret defined as an environment variable - so you will not need to set environment variables one by one.

The option to import an entire Secret is on the second _(Advanced Options)_ page, so click the **Next ->** button to skip to that page.

![](<../../../.gitbook/assets/Screen Shot 2022-03-21 at 12.39.58 PM.png>)

In the _Other Container Config_ section, enter the configuration for importing environment variables from a secret.  For example, to import all environment variables from a secret named `my-env-vars`, you could use the following YAML:

```yaml
EnvFrom:
- SecretRef:
    Name: my-env-vars
```

To import from additional secrets, you can simply repeat the YAML from lines 2 and 3 above for each secret that you want to import from.

#### Pick and Choose individual Environment Variable from a Secret

Another approach is to pick and choose which keys to import from the Secret as environment variables.  This method gives you complete control over each environment variable as well as its name - but it requires more configuration on your part.

The option to set individual environment variables is on the first _(Basic Options)_ page.

In the _Environment Variables_ section, enter the configuration for choosing environment variables to import from a config map.  For example, to set a single environment variable `ENV_VAR_ONE` to the value of the `SECRET_ENV_VAR` key in the `my-env-vars` secret, you could use the following YAML:

```yaml
- Name: ENV_VAR_ONE
  ValueFrom:
    SecretKeyRef:
      Name: my-env-vars
      Key: MY_ENV_VAR
```

To add additional environment variables, you can simply repeat the YAML from lines 2 through 5 above for each environment variable that you want to add.
