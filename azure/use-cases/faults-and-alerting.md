# Faults and alerting

## Introduction <a href="#0-toc-title" id="0-toc-title"></a>

Faults that happen in the system be it Infrastructure creation, Container deployments or Application health checks can be tracked in the DuploCloud portal under Faults Menu.

## Viewing faults <a href="#1-toc-title" id="1-toc-title"></a>

You can look at Tenant specific faults under **Deployments > Faults** or all the faults in the system under **Admin > Faults**. In addition to notifying you about the faults, DuploCloud integrates with Sentry, which will send an Email alert for the fault and also acts as a single place to look at all the events.

![](https://duplocloud.com/wp-content/uploads/2021/11/deploy-faults.png)

## Configuring Sentry alerts <a href="#2-toc-title" id="2-toc-title"></a>

To configure Sentry, go to the [Sentry website](https://sentry.io). Under projects create a new project. Then go to **Settings > Projects > \[project-name] > Client keys (DSN)**. Click on **show deprecated DSN**, Get the deprecated DNS name and add it under **Deployments > Metrics > Sentry DSN**.

![](https://duplocloud.com/wp-content/uploads/2021/11/sentry.png)

![](https://duplocloud.com/wp-content/uploads/2021/11/duplo-sentry.png)
