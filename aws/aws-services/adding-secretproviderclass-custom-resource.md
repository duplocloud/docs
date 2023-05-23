# SecretProviderClass custom resource

DuploCloud Portal provides the ability to create Custom Resource `SecretProvider` Class.

This capability allows Kubernetes to mount secrets stored in external secrets stores into the pods as volumes. After the volumes are attached, the data is mounted into the container’s file system.

### Step1: Enable Secret Provider Class

As a pre-requisite, Administrator needs to set the Infrastructure setting for `Enable Secrets CSI Driver` as `True`**.** This setting is available (Admin > Infrastructure > select your infrastructure > Settings).

### Step2: Create K8s Secret Provider Class

Navigate to DevOps > Container > EKS/Native > **K8s Secret Provider Class.**

You can map the `AWS Secrets` and `SSM Parameters` configured in DuploCloud Portal (DevOps > App Integration ) under the Parameters section of the configuration.

Use the optional **Secret Objects** field to define the desired state of the synced Kubernetes secret objects.

The following is an example SecretProviderClass configuration where AWS secrets and Kubernetes Secret Objects are configured.

![K8s Secret Provider Class Page](<../../.gitbook/assets/image (52) (1).png>)

### **Step3:** Mount Volumes based on the configured secrets

To ensure your application is using the Secrets Store CSI driver, you need to configure your deployment to use the  reference of the `SecretProviderClass` resource created in the previous step.

The following is an example of how to configure a pod to mount a volume based on the SecretProviderClass created in prior steps to retrieve secrets from Secrets Manager.

While creating **Service** (DevOps > Containers > EKS/Native > Service),&#x20;

{% hint style="info" %}
Select **Cloud Credentials** value as `From Kubernetes`
{% endhint %}

![Select Cloud Credentials](<../../.gitbook/assets/image (41) (3).png>)

![Advance Options Service Page](<../../.gitbook/assets/image (65).png>)

* Add **Other Pod Config** field as the following example.

{% code title="Other Pod Config field" %}
```yaml
Volumes:
  - Name: secretvolume-name
    Csi:
      driver: secrets-store.csi.k8s.io
      readOnly: true
      VolumeAttributes:
        secretProviderClass: my-secret-provider-class

```
{% endcode %}

* Add mount details in **Other Container Config** field

{% code title="Other Container Config field" %}
```yaml
VolumesMounts:
  - Name: secretvolume-name
    MountPath: /mnt/secrets
    readOnly: true

```
{% endcode %}

### Using SecretObjects

#### Configuring Secret Objects

You can use the optional secretObjects field to define the desired state of your synced Kubernetes secret objects. The volume mount is required for the sync.

Referring to the example which we are following from prior steps, we have defined `SecretObjects` in **Secret Object** field (K8s Secret Provider Class).

&#x20;The following is an example SecretProviderClass custom resource that will sync a secret from AWS Secrets Manager to a Kubernetes secret:

<div align="left">

<img src="../../.gitbook/assets/image (37) (2).png" alt="K8s Secret Provider Class Page">

</div>

#### Configuring Secret Objects in deployment

Create Service with all the configurations specified in [Step3](adding-secretproviderclass-custom-resource.md#step3-mount-volumes-based-on-the-configured-secrets)

In **Other Container Config** field, you can specify mount details with the object name. Refer following example.

{% code title="Other Container Config field" %}
```yaml
VolumesMounts:
  - Name: secretvolume-name
    MountPath: /mnt/secrets
    readOnly: true
EnvFrom:
  - SecretRef:
      Name: secretobject-name
```
{% endcode %}

#### Configuring Secret Objects in Environment Variables

Set environment variables in your deployment to refer your new Kubernetes secrets.

Refer following example. Specify below in **Environment Variables** field

{% code title="Environment Variables field" %}
```yaml
- name: SECRET_USERNAME
  valueFrom:
    secretKeyRef:
      name: secretobject-name
      key: secret-text
```
{% endcode %}

