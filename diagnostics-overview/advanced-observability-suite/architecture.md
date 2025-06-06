---
description: >-
  How the Advanced Observability Suite and OpenTelemetry integrate with
  DuploCloud
---

# Architecture

Advanced Observability Suite (AOS) is based on OpenTelemetry. The following graphic shows the various components.

{% hint style="info" %}
The OTel stack consists of 50 or more components and hundreds of configurations. If you need to change your OpenTelemetry configuration, contact your DuploCloud support team.
{% endhint %}

<figure><img src="../../.gitbook/assets/OAS_Arch.png" alt=""><figcaption><p>DuploCloud Advanced Observability Suite Architecture</p></figcaption></figure>

## Viewing the DuploCloud Deployment of the OpenTelemetry Stack

To view the complete deployment of the OpenTelemetry stack:

1. In the DuploCloud Portal, navigate to **Administrator** -> **Observability** -> **Advanced** -> **Dashboard**.
2. In the **Observability** area, click the **K8s/Docker** card. The Grafana K8s Resource Monitoring dashboard launches, giving you a detailed view of resources and monitoring for Kubernetes nodes, Docker containers, and Pods.

<figure><img src="../../.gitbook/assets/otel1.png" alt=""><figcaption><p>The AOS <strong>Dashboard</strong> containing the <strong>K8s/Docker</strong> card</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/garf1.png" alt=""><figcaption><p>The Grafana <strong>K8s Resource Monitoring</strong> dashboard</p></figcaption></figure>

## Viewing OpenTelemetry Data in DuploCloud

OpenTelemetry data is stored in S3 Buckets, which you can view in the DuploCloud Portal.

{% hint style="info" %}
OpenTelemetry data is stored in S3 Buckets in a Tenant that DuploCloud preconfigures for you during Onboarding. DuploCloud documentation refers to this Tenant as _**OpenTelemetry\_Tenant**_ (in bold italics), but the name may vary if a different name was chosen during setup.
{% endhint %}

1. In the DuploCloud Portal, select the _**OpenTelemetry\_Tenant**_ from the **Tenant** list box at the top of the Portal.
2. Navigate to **Cloud Services** -> **Storage** and select the **S3** tab to view the data. This data setup is deployed and managed via [Flux Helm](architecture.md#viewing-the-duplocloud-deployment-of-the-opentelemetry-stack) release infrastructure.

<figure><img src="../../.gitbook/assets/Screenshot (305).png" alt=""><figcaption><p><strong>S3 Bucket</strong> containing OpenTelemetry data in the OpenTelemetry Tenant</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/S3 to edit (3).png" alt=""><figcaption><p>S3 Buckets in the <strong>OpenTelemetry_Tenant</strong> Tenant</p></figcaption></figure>

To view a complete list of Kubernetes Services in an OpenTelemetry deployment, select the _**OpenTelemetry\_Tenant**_ from the **Tenant** list box at the top of the Portal and navigate to **Kubernetes** -> **Services**.

<figure><img src="../../.gitbook/assets/Screenshot (306).png" alt=""><figcaption><p> Kubernetes deployments, containers, and S3 buckets in an OpenTelemetry Tenant</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (10) (2).png" alt=""><figcaption><p>Services in the <strong>OpenTelemetry_Tenant</strong> Tenant</p></figcaption></figure>

To view a complete list of Docker Containers in an OpenTelemetry deployment, select the **OpenTelemetry\_Tenant** from the **Tenant** list box at the top of the Portal and navigate to **Kubernetes** -> **Containers**.

<figure><img src="../../.gitbook/assets/Screenshot (307).png" alt=""><figcaption><p>Docker Containers in the OpenTelemetry Tenant</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11) (2).png" alt=""><figcaption><p>Containers in the <strong>OpenTelemetry_Tenant</strong> Tenant</p></figcaption></figure>
