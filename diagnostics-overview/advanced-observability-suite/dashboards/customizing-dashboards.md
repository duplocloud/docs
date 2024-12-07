---
description: Create your own Advanced Observability Suite (AOS) Dashboards
---

# Customizing Dashboards

{% hint style="info" %}
Note that each Kubernetes cluster has its own OpenTelemetry stack by default. If you need to share an OTEL stack across clusters, contact your DuploCloud support team, and they will set it up for you.
{% endhint %}

The OpenTelemetry part of the AOS dashboard has five cards that point to Grafana dashboards. These cards depend on the the links from under **Administrator --> SystemSettings -> System Config**. Search for "otel" and you will find a list of settings of type otel with links as shown in the picture below:

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Each entry maps to a card on the dashboard. An entry that starts with \<infraname>/ applies to the cards for that Infrastructure. Note that in admin dashboard all cards are in the context of the Infrastructure and there is a infrastructure drop down.

| Setting Name          | Card                            | Dashboard Type |
| --------------------- | ------------------------------- | -------------- |
| \<infraname>/proxyurl | Grafana button on the dashboard | Admin          |
| \<infraname>/logs     | Logs Button                     | Admin          |
| \<infraname>/metrics  | Metrics Button                  | Admin          |
| \<infraname>/traces   | Traces Button                   | Admin          |
| \<infraname>/k8s      | K8S Button                      | Admin          |

Also note that the settings can have place holders like \[\[TENANT\_NAME]] that get dynamically replaced by the platform when the user clicks on the respective button.

### Adding Custom Links to AOS Dashboards

Link external data sources to AOS dashboards by adding custom links to data cards.&#x20;

#### Adding Custom Links for Administrators

1. From the DuploCloud Portal, navigate to **Administrator** -> **Observability** -> **Advanced** -> **Dashboard**.
2. Click the link icon (<img src="../../../.gitbook/assets/new link icon.png" alt="" data-size="line">) in the header of the card to which you wish to add a custom link. The **All Admin Custom Links** pane displays.
3. Select the **Admin** tab to add a custom link only to the Administrator AOS Dashboard, or the **Common** tab to include the custom link on the Tenant AOS Dashboard.
4. Click Add. The **Add profiles Custom Link** pane displays.
5. Enter a **Name**, **URL**, and **Description** for the custom link.&#x20;
6. Click **Submit**. The custom link is added to the data card on the AOS Dashboard(s).&#x20;

<div align="left"><figure><img src="../../../.gitbook/assets/new logs.png" alt="" width="354"><figcaption><p>The <strong>Logs</strong> data card with the clink icon highlighted</p></figcaption></figure></div>

#### Adding Custom Links for Non-Administrators

1. From the DuploCloud Portal, navigate to **Observability** -> **Advanced** -> **Dashboard.**
2. Click the link icon (<img src="../../../.gitbook/assets/new link icon.png" alt="" data-size="line">) in the header of the card to which you wish to add a custom link. The **All Admin Custom Links** pane displays.
3. Click Add. The **Add profiles Custom Link** pane displays.
4. Enter a **Name**, **URL**, and **Description** for the custom link.&#x20;
5. Click **Submit**. The custom link is added to the data card on the Tenant AOS Dashboard.&#x20;

### Adding New Dashboards In Grafana

You can get the admin credentials for the grafana deployment from the tenant where the otel stack is deployed. It is the service called grafana-ui. Click edit on the service to get the credentials from the env.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
