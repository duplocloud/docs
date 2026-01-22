# Viewing Kubernetes Apps

The **Apps** page in DuploCloud lets you view your Kubernetes resources grouped by application. You can see all applications, the number and type of resources in each application, and filter or sort resources to quickly find what you need. This page appears only after you have added App Names to one or more Kubernetes resources.

## Adding App Names to Kubernetes Resources <a href="#adding-app-names-to-kubernetes-resources" id="adding-app-names-to-kubernetes-resources"></a>

To group resources in the **Apps** dashboard, assign an app name to each resource. Use the same app name for all resources you want grouped together.

* **Services**: When adding or updating a Kubernetes Service, enter an app name in the **App Name** field.
* **Resources**: For other Kubernetes resources (Deployments, Helm releases, StatefulSets, Secrets, etc.), enter an app name in the **Labels** section using the following format: `app.duplocloud.net/app-name: "<app name>"`

## Viewing Resources by Application <a href="#viewing-resources-by-application" id="viewing-resources-by-application"></a>

After adding app names to your resources, you can view them on the **Apps** page.

1. Navigate to **Kubernetes** -> **Apps**.&#x20;
2. Select All to display all apps or use the **Search App** bar to search for a specific application.
3. Click on an app name to view its details.
4. Select **All** to see every resource in the app, or click **Select** **Resource Type** to view specific types (for example, Services or Secrets).

<figure><img src="../../.gitbook/assets/Screenshot (1080).png" alt=""><figcaption><p>Kubernetes <strong>Apps</strong> page in the DuploCloud Portal</p></figcaption></figure>
