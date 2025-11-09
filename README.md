---
description: An overview and demo of DuploCloud's DevOps platform
cover: .gitbook/assets/banner dark.png
coverY: 0
---

# Overview

DuploCloud is an agentic Devsecops Automation platform that leverages AI for a wide range of Cloud Infrastructure automation needs. It encompasses Devops, security, compliance, Observability and CICD. The software can:

* Configure and update resources safely and securely
* Write IAC (Cursor like experience in an IDE)
* Troubleshoot incidents
* Perform several other functions like collect evidence for compliance audits, reporting, discover cloud resources to generate documentation and so on.&#x20;

![The DuploCloud Platform Features Diagram](.gitbook/assets/duplocloud-update-illustration-graphics-v2.png)

{% hint style="info" %}
Duplocloud platform is entirely self hosted in customer's cloud account. With an open architecture you can choose your own model, build your own agents and bring your own automation tools.
{% endhint %}

The platform broadly comprises of two parts:

* **Agentic Orchestration or AI Suite**: This module orchestrates AI agents that are specialized in different devops, in such a way that the overall system functions like an AI devops engineer to which users can delegate higher level tasks.\
  The primary user experience is that of an IT help Desk where users create a ticket, assign it to an AI agent that accomplishes the task in real time. The help desk interface can be accessed via a Web browser, slack/teams thread or an IDE Extension (Cursor like experience) &#x20;
*   **Automation Platform**: The AI agents need automation tools to interface with cloud infrastructure. For example for an AI observability functionality we need an observability solution underneath like a Datadog or Open telemetry. DuploCloud's automation platform provides a comprehensive tool set that include:

    * **Provisioning Tool kit** that has automation capability to create and manage hundreds of cloud services like EKS, AKS, GKE, S3, SQS, RDS, Azure SQL, Google Cloud SQL and so on. This tool lit is available to the agent in the form of MCP, Terraform provider, CLI and APIs.&#x20;
    * **Observability** is delivered using Open telemetry stack with functions like tracing, Logging, alerting, profiles, infrastructure metrics, RUM, SLO/SLA monitoring and so forth.
    * **Security** tooling includes SIEM, VA, AV, JIT, Access controls and so forth.
    * **CI/CD** we have argoCD and workflows as well as integrate with any other CI/CD system

    Teams can also bring their own automation tools whether built in-house or from a third party. &#x20;



{% hint style="info" %}
Users can interface directly with the automation tools without going through the AI functionality using the APIs, Terraform provider, CLI and Browser workflows.
{% endhint %}

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>



## AI Orchestration Demo

Check out a quick video of the AI functionality

{% embed url="https://player.vimeo.com/video/1085542812?h=de0470a8c2" %}

## Automation Platform Demo

Check out a 6-minute video overview of the comprehensive Automation Platform.

{% embed url="https://drive.google.com/file/d/1b0VYeix7vex7MxfCtRa4Yq5nHptb4nkA/view?usp=sharing" %}
