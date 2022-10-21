# Alert notifications

## Introduction <a href="#0-toc-title" id="0-toc-title"></a>

In addition to visibility of faults in the UI, DuploCloud also supports sending these notifications to the following systems:&#x20;

* Sentry
* PagerDuty
* NewRelic
* OpsGenie

Both of these systems support sending emails for these faults. They also allow you to view the notifications in their dashboard. You will need to generate an integration key from Sentry or PagerDuty and provide that to DuploCloud to enable this integration.



## Sentry <a href="#1-toc-title" id="1-toc-title"></a>

To create a key for Sentry, visit Sentry website and manage your application Under projects create a new project. Then go to **Settings > Projects > \[project-name] > Client keys (DSN)**.

![](https://duplocloud.com/wp-content/uploads/2021/11/sentry.png)

## PagerDuty <a href="#2-toc-title" id="2-toc-title"></a>

In your PagerDuty account, go to the Service that should receive events. If a Service does not exist, you need to go through **Configuration > Services > Add Service.** Once the Service is created, go to **Service->Integrations->New Integration**. This will generate an integration key that you will need to provide to DuploCloud.

## NewRelic

In your NewRelic account, obtain an integration key to send events to NewRelic [Insights](https://docs.newrelic.com/docs/data-apis/ingest-apis/event-api/introduction-event-api/), generate an [API Key](https://docs.newrelic.com/docs/apis/intro-apis/new-relic-api-keys) and provide that to DuploCloud as below.

## OpsGenie

In your OpsGenie account, obtain an API Key to integrate DuploCloud faults with OpsGenie. Please review the OpsGenie [documentation](https://support.atlassian.com/opsgenie/docs/what-is-a-default-api-integration/) to obtain the key.

## Setting the key in DuploCloud <a href="#2-toc-title" id="2-toc-title"></a>

Add the integration key under **DevOps > Faults > Set Alert Notifications Config**&#x20;

&#x20;                                &#x20;

<figure><img src="../../../.gitbook/assets/Screen Shot 2022-10-20 at 7.11.57 PM.png" alt=""><figcaption></figcaption></figure>
