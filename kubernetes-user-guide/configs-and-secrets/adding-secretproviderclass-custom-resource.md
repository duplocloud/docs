# SecretProviderClass custom resource

DuploCloud Portal provides the ability to create Custom Resource `SecretProvider` Class.

This capability allows Kubernetes to mount secrets stored in external secrets stores into the pods as volumes. After the volumes are attached, the data is mounted into the container’s file system.

### Step 1: Enable Secret Provider Class

As a pre-requisite, Administrator needs to set the Infrastructure setting for `Enable Secrets CSI Driver` as `True`. This setting is available by navigating to **Administrator** -> **Infrastructure**, selecting your Infrastructure, and clicking **Settings**).

### Step 2: Create K8s Secret Provider Class

Navigate to **Kubernetes** -> **Sec. Provider Class.**

You can map the `AWS Secrets` and `SSM Parameters` configured in DuploCloud Portal (**Cloud Services** -> **App Integration**) under the **Parameters** section of the configuration.

Use the optional **Secret Objects** field to define the desired state of the synced Kubernetes secret objects.

The following is an example SecretProviderClass configuration where AWS secrets and Kubernetes Secret Objects are configured.

![K8s Secret Provider Class Page](<../../.gitbook/assets/image (52) (1).png>)

### **Step 3:** Mount Volumes based on the configured secrets

To ensure your application is using the Secrets Store CSI driver, you need to configure your deployment to use the reference of the `SecretProviderClass` resource created in the previous step.

It's important to note that SPC timeouts can occur due to issues related to Secret Auto Rotation, which is enabled by default. This feature checks every two minutes if the secrets need to be updated from the values in AWS Secrets Manager. During a service deployment, if a secret is deleted due to a redeployment while a rotation check is attempted, it can lead to timeouts. This deletion happens because the secret is generated from the volume mount in the service pod, and when the pod is destroyed, the secret is also destroyed.

While creating **Service** (**Kubernetes** -> **Service**),

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

<div align="left">

<img src="../../.gitbook/assets/image (37) (2).png" alt="K8s Secret Provider Class Page">

</div>

#### Configuring Secret Objects in deployment

Create Service with all the configurations specified in [Step 3](adding-secretproviderclass-custom-resource.md#step3-mount-volumes-based-on-the-configured-secrets)

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

This integration of secrets into Kubernetes deployments, while powerful, requires careful management to avoid issues such as SPC timeouts. Understanding the underlying mechanisms, such as Secret Auto Rotation and the lifecycle of secrets in pod deployments, is crucial for smooth operations.