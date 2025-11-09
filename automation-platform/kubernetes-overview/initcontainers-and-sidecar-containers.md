---
description: Use InitContainers and Sidecar Containers with DuploCloud
---

# InitContainers and Sidecar Containers

InitContainers and Sidecar Containers are special types of containers that enhance Kubernetes workloads. InitContainers run before the main application container starts, handling setup tasks like configuration or waiting for dependencies. Sidecar Containers run alongside the main application container, providing auxiliary services such as logging, monitoring, or proxying traffic.

Using these features in DuploCloud allows for more flexible and modular application design, improving automation and scalability.

## Configuring initContainers and additionalContainers (Sidecar Containers) in DuploCloud

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Services.**
2. Select **Add** to create a new Service, or click the menu icon in the row of the Service you want to configure, and select **Edit**. The **Add** **Service** or **Edit Service** page displays.&#x20;
3. Open the **Advanced Options** section and add your initContainers and additionalContainers configurations to the **Other Pod Config** field. See the following example:

```yaml
initContainers:
  - name: bootstrap
    image: busybox:1.28
    command:
      - sh
      - '-c'
      - echo duplo

additionalContainers:
  - name: init-myservice
    image: busybox:1.28
    restartPolicy: Always
    command:
      - sh
      - '-c'
      - ping 127.0.0.1
```

4. Click **Save** or **Create** to save and deploy the updated configuration.
