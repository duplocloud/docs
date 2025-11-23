---
description: >-
  Create Kubernetes ConfigMaps to store non-sensitive information with
  DuploCloud
---

# Creating a Kubernetes ConfigMap

You can use Kubernetes ConfigMaps to store non-sensitive configuration data as key-value pairs. These values can later be mounted into containers as files or environment variables.

## Creating a Kubernetes ConfigMap

1. In the DuploCloud Portal, navigate to **Kubernetes** → **Config Maps**.
2.  Click **Add**. The **Add Config Map** pane displays.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (376).png" alt=""><figcaption><p>The <strong>Add Config Map</strong> pane</p></figcaption></figure>
3. Complete the fields:

<table data-header-hidden><thead><tr><th width="128.66668701171875"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the ConfigMap. (e.g., <code>my-config-map</code>).</td></tr><tr><td><strong>Data</strong></td><td>Add a key-value pair for each file to include in the ConfigMap, using a colon <code>:</code> to separate the key (filename) and value (file content).<br><strong>Example</strong>: <code>config.yaml: key1: value1</code></td></tr></tbody></table>

4. Click **Create** to create the ConfigMap.

To use this ConfigMap in your application,[ mount it as a volume in a container](mounting-config-as-files.md#mounting-a-kubernetes-configmap-as-a-volume).
