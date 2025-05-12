---
description: Working with the Advanced Observability Suite (AOS) dashboards in DuploCloud
---

# Dashboards

The DuploCloud AOS dashboards are a gateway to the detailed Grafana dashboards, serving two purposes:

* **SSO and Authentication Proxy**: The Grafana dashboards reside on a private network. DuploCloud acts as an authentication layer, connecting the same single sign-on (the DuploCloud login) to a Grafana session.
* **Summarizing Links**: While AOS contains many pre-configured Grafana dashboards, you can create quick links with descriptions of the ones you use most frequently.  See [Customizing Dashboards](customizing-dashboards.md) for more information.&#x20;

## Administrator and Tenant AOS Dashboards

Depending on your [role ](../../../access-control/)(Administrator or User), you can access the Advanced Observability Suite dashboard from two locations in the DuploCloud Portal.

1. The [Administrator AOS Dashboard](administrator-dashboard.md) displays cloud data across all resources and allows you to select DuploCloud Infrastructures. To use it, navigate to  **Administrator** -> **Observability** -> **Advanced** -> **Dashboard** in the DuploCloud Portal.&#x20;
2. The [Tenant AOS Dashboard](tenant-dashboard.md) displays data by Tenant. To use it, navigate to **Observability** -> **Advanced** -> **Dashboard** in the DuploCloud Portal. &#x20;

## Grafana Dashboards

The integration between DuploCloud AOS and Grafana ensures that you can seamlessly transition between high-level monitoring and detailed data analysis. Whether you need to troubleshoot a log entry, trace a request’s path, monitor resource usage, or track performance metrics, the ability to click through from the AOS Dashboard to the corresponding Grafana dashboards makes it easier to investigate and resolve issues.

From the DuploCloud AOS Dashboards, you can navigate directly to the Grafana dashboards for detailed data:&#x20;

* **Service Overview Dashboard**: Click the Grafana link from the AOS dashboard and navigate to **Integration-APM** -> **Service Overview Dashboard.** This dashboard provides a high-level summary of the performance of your services, showing key metrics such as request rates, error rates, and other service-level indicators. It allows you to monitor the health of your services and quickly identify any issues that may need attention.
* From the **DuploCloud AOS Dashboard**, you can easily navigate to corresponding **Grafana dashboards** for deeper insights. Simply click the links in the following panels to access detailed data:
  * **Logs**: Dive into the **Grafana Logging Dashboard** for log analysis and troubleshooting.
  * **Tracing**: Explore request flows and trace performance issues using the **Grafana Tracing Dashboard**.
  * **Metrics**: Click through to the **Grafana Metrics Dashboards** to analyze key performance metrics.
  * **K8s/Docker**: Monitor Kubernetes clusters and Docker containers by accessing the **Grafana Kubernetes Dashboards**.
  * **Profiles**: Track service, user, and tenant activity via the **Grafana Profiles Dashboards**.
