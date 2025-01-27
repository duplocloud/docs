---
description: >-
  Create a re-usable template to deploy resources using the DuploCloud Stacks
  feature.
---

# Create a deploy template

Create a re-usable template to deploy resources (Nodes, Hosts, Services, Secrets, storage, etc.) using the DuploCloud Stacks feature.

1. Select the Tenant from the **Tenant** list box that owns the resources that will act as a baseline for the new template.&#x20;
2. Navigate to **Automation** -> **Stacks**.
3. Select the **Templates** tab.
4. Click **Generate**. The **Generate Deployment Template** pane displays.
5. Enter a name for the template in the **Name** field.
6. Select all applicable scopes in the **Scopes** field. If unsure, you can safely add any scope, as it only affects the resource lists shown on the next page. The following scopes are currently available, with more to be added as new resource types are supported:
   * Kubernetes
   * Admin / Reverse Proxy
   * Admin / System Config
   * Admin / Tenant Security
   * Cloud / Host&#x20;
   * Cloud / Load Balancer
   * Cloud / Storage
   * Docker&#x20;
7. Click **Next**. A page allowing you to edit the template configurations displays.&#x20;
8. Edit the template configurations as needed:
   * The left panel displays resources and their components (e.g., **Kubernetes**, **Service**, and **filebeat-k8s-duploinfrasvc)** organized hierarchically.
     * Subcomponents can be toggled on or off, controlling their inclusion in the template.
     * Selecting a parent node (e.g., **Kubernetes**) includes all its child components, while deselecting it removes them.
   * The right panel displays JSON that dynamically reflects the selections made on the left.
     * Adding or removing components on the left modifies the corresponding nodes and payloads in the JSON.
     * Advanced users can click **Edit** to [fine-tune the JSON manually](customize-deploy-templates.md#customizing-deploy-templates).
     * Click **Save** to save your changes.
9. Click the **Download** button to save the template file to your local machine for further use or modifications.\
