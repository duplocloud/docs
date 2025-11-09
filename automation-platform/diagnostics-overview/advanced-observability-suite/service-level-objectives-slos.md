---
description: >-
  Using Service Level Objectives (SLOs) in the DuploCloud Advanced Observability
  Suite (AOS)
---

# Service Level Objectives (SLOs)

Service Level Objectives (SLOs) are metrics that define the desired reliability and performance targets for a service. Powered by Service Level Indicators (SLIs) such as latency, availability, and error rates, SLOs provide a precise measure of whether your service is meeting its goals. With SLOs integrated into DuploCloud’s Advanced Observability Suite (AOS), you benefit from automated dashboards, real-time performance monitoring, and proactive alerting. These capabilities empower you to continuously monitor and optimize your service's health for a seamless user experience.

DuploCloud streamlines the management of SLOs by integrating them with Grafana, where users can easily create and modify SLO configurations. Instead of manually editing backend files or complex configurations, DuploCloud uses a business form to simplify the process. This form is available in the DuploCloud UI through Grafana, where you can submit your SLO request with a few clicks.

Once submitted, the request is automatically processed by the Duplo-automation service. This powerful service takes care of creating and configuring the necessary backend resources, rules, and alerts based on your input. This automation reduces manual intervention and ensures that your SLO setup is quick, efficient, and error-free.

## Displaying SLOs in the DuploCloud AOS

The **SLO Overview** dashboard provides a comprehensive view of service performance. It contains high-level data and key metrics for your defined Service Level Objectives (SLO). For each SLO, it tracks the SLI percentage, shows the remaining error budget, and visualizes the SLI percentage as a graph, offering a clear trend of service performance over time.&#x20;

1. From the DuploCloud Portal, **Navigate to Observability** -> **Advanced** -> **Dashboard**
2. Click the **SLO** link in the Metrics data card or navigate to the **SLO Overview** dashboard in Grafana. The Grafana **SLO Overview** dashboard displays.&#x20;

<figure><img src="../../../.gitbook/assets/SLO Overview.png" alt=""><figcaption><p>The <strong>SLO Overview</strong> dashboard in Grafana</p></figcaption></figure>

## **Viewing SLO details**

You can dive deeper into the details of any individual SLO by clicking the **View Dashboard** button for that SLO on the left-hand side of the **SLO Overview** dashboard. The SLO details provide a more comprehensive view of the SLO's performance metrics such as the SLO percentage, error budget trend, burn rate, remaining error budget, current burn rate, event rate, etc.

<figure><img src="../../../.gitbook/assets/SLO Details.png" alt=""><figcaption><p>The details dashboard for the productcatalogue SLO.</p></figcaption></figure>

## **Creating an SLO**

To create an SLO in Grafana, follow the steps below. For more information, see the [Grafana SLO documentation](https://grafana.com/docs/grafana-cloud/alerting-and-irm/slo/create/).

1. From the DuploCloud Portal, **Navigate to Observability** -> **Advanced** -> **Dashboard**
2. Click the **SLO** link in the Metrics data card or navigate to the **SLO Overview** dashboard in Grafana. The Grafana **SLO Overview** dashboard displays.&#x20;
3.  Click on the **Create SLO** button located at the top-right corner of the screen. The **Dashboard for Managing SLO** displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (41).png" alt=""><figcaption><p>The form for managing SLOs in Grafana.</p></figcaption></figure></div>
4. Enter the following information about the SLO:
   * **Name**: The name of the SLO.
   * **Description**: A brief description of the SLO.
   * **Objective**: The target goal for the SLO (e.g., 99.9% uptime).
   * **Time Window**: The period over which the SLO is measured.
   * **Success Metric**: The metric used to track success.
   * **Total Metric**: The total metric used to evaluate the SLO.
5. Click **Create/Update SLO.** The SLO is created and added to the SLO Overview Dashboard.

## Editing or Deleting an SLO

1. Navigate to the **SLO Overview** dashboard.
2. Locate the SLO you wish to modify in the list on the left side, and click **Edit SLO**.
3. The **Dashboard for Managing SLO** will appear, displaying the same fields as when you created an SLO. You can now make the necessary changes, such as updating the name, description, objective, time window, type, success metric, and total metric.
4. After making your changes, click **Create/Update SLO** to save the updates.
5. If you wish to delete the SLO, click **Delete SLO**.

## Viewing SLO Alert Rules

DuploCloud automatically creates alert rules for each SLO, including **Critical** and **Warning** alerts. You can view them in Grafana to understand their configurations.

1. From your **Grafana** home page, navigate to **Alerting -> Alert rules**. The **Alert rules** page displays.
2. Locate and click the specific **SLO** (e.g., `duplo_slo_slo-auto-14:rjgsrnj6hyf1jef10bf91`).
3.  The associated recording and normal alert rules display.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (43).png" alt=""><figcaption><p>Alert rules for the selected SLO on the <strong>Alert rules</strong> page in Grafana.</p></figcaption></figure></div>
4. Click on any alert rule to review the alert conditions, thresholds, and labels.

<figure><img src="../../../.gitbook/assets/Alert rule in detail.png" alt=""><figcaption><p>Alert rule details in Grafana.</p></figcaption></figure>

## **Setting Up Notification Policies:**

To manage how these alerts are routed, create notification policies based on the SLO service name (e.g., `cartservice`). You can specify which channels (e.g., Slack, PagerDuty) alerts should be sent to based on the labels of the SLO.

For detailed steps on setting up notification policies, refer to the [Grafana Notification Policies](https://grafana.com/docs/grafana/latest/alerting/configure-notifications/create-notification-policy/). documentation.
