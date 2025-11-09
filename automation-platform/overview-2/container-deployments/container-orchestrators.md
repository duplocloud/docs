---
description: Support orchestration technologies
---

# Container Orchestration Features

DuploCloud abstracts the complexity of container orchestration technologies, allowing you to focus on deploying, updating, and debugging your application.&#x20;

Among the technologies supported are:

* **Azure Kubernetes Service (AKS)**: AKS with DuploCloud provides a user-friendly interface that conceals the complexities of Kubernetes (K8s). You can use the DuploCloud UI to add Kubernetes configurations around Pods, Containers, Secrets, and more.&#x20;
* **Built-in (DuploCloud)**: DuploCloud platform's built-in container management has the same interface as the `docker run` command, except that it can be scaled to hundreds of containers across many Hosts, providing capabilities such as associated Load Balancers, DNS, and more.

## Container Orchestration Feature Matrix

Use the feature matrix below to compare the orchestration technologies that DuploCloud supports. DuploCloud helps you implement whichever option you choose through the DuploCloud Portal or the Terraform API.

{% hint style="info" %}
One dot indicates a low rating, two dots a medium rating, and three dots a high rating. For example, Kubernetes has a low ease-of-use rating, but a high rating for stateful application support.
{% endhint %}



<table><thead><tr><th width="276.71428571428567" align="center">Feature</th><th width="150" data-type="rating" data-max="3">AKS</th><th width="150" data-type="rating" data-max="3">Built-In</th><th data-hidden data-type="rating" data-max="3">ACI</th></tr></thead><tbody><tr><td align="center">Ease of use</td><td>1</td><td>3</td><td>1</td></tr><tr><td align="center">Features and ecosystem Tools</td><td>3</td><td>1</td><td>1</td></tr><tr><td align="center">Suitability for stateful apps</td><td>3</td><td>1</td><td>1</td></tr><tr><td align="center">Stability and maintenance</td><td>2</td><td>3</td><td>2</td></tr><tr><td align="center">Azure cost</td><td>1</td><td>3</td><td>3</td></tr><tr><td align="center">Multi-cloud (w/o DuploCloud)</td><td>3</td><td>null</td><td>null</td></tr></tbody></table>

### **Feature Definitions**

The descriptions below explain how each feature in the matrix is evaluated and why each technology receives its respective rating.

* **Ease of Use**:&#x20;
  * AKS is extensible and customizable, but not without a cost in ease of use. The DuploCloud platform reduces the complexities of Kubernetes, making it comparable with other container orchestration technologies in ease of adoption.
  * DuploCloud's Built-in orchestration mirrors `docker run`. You can SSH into a virtual machine (VM) and run `docker` commands to debug and diagnose. If you have an application with a few stateless microservices or configurations that use environment variables or Azure VM extensions, Azure Blob, or Azure Key Vault, consider using DuploCloud's Built-in container orchestration.
* **Features and Ecosystem Tools**:&#x20;
  * AKS, based on Kubernetes, offers a wide range of built-in features and ecosystem tools, such as Secrets Management, ConfigMaps, and support for Helm Charts. These features make it ideal for complex, extensible applications, especially since many third-party tools are designed for Kubernetes.
  * DuploCloud’s Built-In orchestration provides a simpler alternative, relying on native Azure services for features like secrets and configurations. While it doesn’t support Kubernetes-native tools like Helm, it is ideal for lighter-weight deployments where Kubernetes complexity is not needed.
* **Suitability for Stateful apps**:&#x20;
  * AKS (Kubernetes) effectively supports stateful workloads through StatefulSets and Volumes, which integrate directly with Azure-managed storage. This makes Kubernetes the preferred option when cloud-managed storage isn’t feasible due to cost or architecture constraints.
  * DuploCloud's Built-In orchestration can also run stateful applications, but relies on mounting shared file systems (like Azure Files), which may not offer the same capabilities or automation as Kubernetes volumes.
* **Stability and Maintenance**:&#x20;
  * Although Kubernetes is highly stable, it is an open-source product. The native customizability and extensibility can lead to points of failure when a mandatory cluster upgrade is needed, for example. This complexity often leads to support costs from third-party vendors. Maintenance can also be especially costly with AKS, as versions are deprecated frequently, requiring upgrades to the control plane and data nodes. While DuploCloud automates this upgrade process, it still requires careful planning and execution.
  * DuploCloud’s Built-in orchestration is simpler to manage. It does not require cluster-level upgrades or frequent patching, reducing the operational overhead and risk.
* **Azure Cost**:&#x20;
  * While the Azure control plane cost is relatively low, running AKS typically requires a business support plan, which adds to the overall cost. AKS users often incur additional charges for features like monitoring, logging, and load balancers. Small businesses may be able to manage costs by adding the support tier only when needed. &#x20;
  * DuploCloud’s Built-in orchestration generally has a lower cost profile. It avoids AKS-specific charges and uses simpler infrastructure components, making it more cost-effective for smaller environments or teams with limited budgets.
* **Multi-Cloud**:&#x20;
  * For many enterprises and independent software vendors, multi-cloud support is a current or future requirement. Kubernetes natively supports multi-cloud environments, allowing you to deploy across different cloud providers. However, managing multi-cloud with Kubernetes can be complex and requires specialized knowledge.
  * DuploCloud simplifies multi-cloud deployments, making it easier to maintain and implement than with Kubernetes.
