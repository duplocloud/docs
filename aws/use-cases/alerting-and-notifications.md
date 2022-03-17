# Alerting and notifications

## Introduction <a href="#0-toc-title" id="0-toc-title"></a>

In addition to notify you about the faults, DuploCloud integrates with Sentry, which will send an Email alert for the fault and acts as a single place to look at all the events.

## Configure Sentry <a href="#1-toc-title" id="1-toc-title"></a>

To configure Sentry, visit Sentry website and manage your application Under projects create a new project. Then go to **Settings > Projects > \[project-name] > Client keys (DSN)**.

![](https://duplocloud.com/wp-content/uploads/2021/11/sentry.png)

## Set Sentry config in DuploCloud <a href="#2-toc-title" id="2-toc-title"></a>

Click on show deprecated DSN, Get the deprecated DNS name and add it under **DevOps > Faults > Update Sentry Config**.

![](https://duplocloud.com/wp-content/uploads/2021/11/duplo-sentry.png)
