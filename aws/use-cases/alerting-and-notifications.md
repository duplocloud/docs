# Alerting and notifications

## Introduction <a href="#0-toc-title" id="0-toc-title"></a>

In addition to visibility of faults in the UI, DuploCloud also supports sending these notifications to the following systems:&#x20;

* Sentry
* PagerDuty

Both of these systems support sending emails for these faults. They also allow you to view the notifications in their dashboard. You will need to generate an integration key from Sentry or PagerDuty and provide that to DuploCloud to enable this integration.



## Sentry integration <a href="#1-toc-title" id="1-toc-title"></a>

To create a key for Sentry, visit Sentry website and manage your application Under projects create a new project. Then go to **Settings > Projects > \[project-name] > Client keys (DSN)**.

![](https://duplocloud.com/wp-content/uploads/2021/11/sentry.png)

## PagerDuty integration <a href="#2-toc-title" id="2-toc-title"></a>

In your PagerDuty account, go to the Service that should receive events. If a Service does not exist, you need to go through **Configuration > Services > Add Service.** Once the Service is created, go to **Service->Integrations->New Integration**. This will generate an integration key that you will need to provide to DuploCloud.

## Setting the key in DuploCloud <a href="#2-toc-title" id="2-toc-title"></a>

Add the integration key under **DevOps > Faults > Update Sentry Config**.&#x20;

![](<../../.gitbook/assets/Screen Shot 2022-03-20 at 3.06.51 PM.png>)
