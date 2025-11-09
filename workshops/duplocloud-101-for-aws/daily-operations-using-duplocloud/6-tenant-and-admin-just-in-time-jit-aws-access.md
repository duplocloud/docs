---
description: Using JIT to access the AWS Portal from DuploCloud
---

# 6 - Tenant and Admin Just-In-Time (JIT) AWS Access

## JIT Access from the DuploCloud Portal

Navigate to **User** -> **Profile** to view options for obtaining JIT credentials with the **JIT AWS Console** button.

{% hint style="info" %}
This method uses Tenant-level AWS permissions.
{% endhint %}

<figure><img src="../../../.gitbook/assets/PROFILE.png" alt=""><figcaption><p>The <strong>JIT AWS Console</strong> button on the <strong>Profile</strong> page</p></figcaption></figure>

## CLI

DuploCloud uses `duplo-jit` to access the CLI. You can use `duplo-jit` to retrieve Tenant-scoped temporary credentials.&#x20;

Documentation for installation and setup can be found [here](../../../automation-platform/overview/use-cases/jit-access.md).

## Accessing the AWS CLI for Admin and Tenant Scopes

{% code fullWidth="false" %}
```bash
[profile duplo-prod]
region=us-west-2
credential_process=duplo-jit aws --admin --host https://prod.duplocloud.net --interactive
```
{% endcode %}

```
[profile test-04]
region=us-west-2
credential_process=duplo-jit aws -tenant devab01 --host https://test04.duplocloud.net --interactive
```

## Accessing Kubectl&#x20;

Administrators can obtain a cluster-wide `kubeconfig` file by navigating to **Administrator** -> **Infrastructure.**&#x20;

Select the Infrastructure, and in the **EKS** tab, click the **Download Kube Config** button.

<figure><img src="../../../.gitbook/assets/apicode.png" alt=""><figcaption><p>The <code>kubeconfig</code> file downloaded from DuploCloud</p></figcaption></figure>
