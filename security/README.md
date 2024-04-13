# Security

Automation, security and compliance are the three core value propositions of the DuploCloud platform. In fact majority of our clients buy DuploCloud for security and compliance first. Following are the fundamental tenants of DuploCloud's approach to security:

* **Self Hosted**: The platform lives completely within your cloud infrastructure. There is no call home or control plane outside. Our personnel support the client by having access to the environment with their permission.  This permission can be revoked anytime. Upgrades and patches can be downloaded and applied by clients themselves. But in almost all cases our clients tend to leverage us as valuable support resource and allow us to provide a managed service. DuploCloud is a SOC2 certified organization.
* **NIST 800-53 based Implementation: E**ven though well established frameworks like NIST exists, most organizations have an adhoc approach to security controls.

{% hint style="info" %}
They say .."_**We follow best practices**_". It ends up being a set of opinions because implementing framework is ardous, expensive and requires deep subject matter expertise
{% endhint %}

At DuploCloud we have codified NIST 800-53 control set in the platform. Any other standard is a subset. Thus further allows us to adapt easily to any industry specific compliance frameworks (PCI, HIPAA, SOC2 etc) because those controls (in the infrastructure context) are a subset of the NIST framework.   &#x20;

* **Shift left Approach**: Being a comprehensive automation solution allows the platform to control pretty much all aspects of the cloud infrastructure and hence make sure that controls are setup correctly at the configuration time. No rework in necessary. The monitoring systems placed post provisioning are consistently clear of alarms making security operations almost a no-op. In fact security is integrated so seamlessly that users don't have that even in their minds while they are focussed on building and operating the infrastructure in an application centric focus.
* **Post Provisioning Monitoring**: The platform calls native cloud provider APIs during provisioning time. During and after the provisioning process it integrates various 2nd (cloud provider) and 3rd Party (open source and ISV) tools for validation and monitoring of the security posture. This allows for an independent validation of the environment. This approach seamlessly integrates devops and secops functions in unified workflow with pane of glass visibility. A simple example is when a Kubernetes worker node is launched the platform implicitly triggers installation of a list of security agents and connects them to the SIEM.  &#x20;
