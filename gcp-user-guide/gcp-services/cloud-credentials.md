---
description: Add GCP subscription details
---

# Cloud Credentials

The DuploCloud rules-based expert system requires GCP Subscription details to effectively manage cloud resources. By adding Cloud Credentials in the DuploCloud Portal, you provide the necessary subscription details for this management.

## Adding Cloud Credentials for GCP Subscriptions

To integrate GCP project cloud credentials into DuploCloud, follow these steps:

1. In the DuploCloud Portal, navigate to **Administrator** -> **Cloud Credentials**. The **Cloud Credentials** page displays.
2. Click **Add** to initiate the creation of new cloud credentials.&#x20;
3. Ensure **Google** is selected from the **Cloud** list box as your cloud provider.
4. Enter your Google Project ID in the **Project ID** field. This ID uniquely identifies your GCP project.
5. Provide the Service Account email in the **Service Account Email** field. Service accounts are crucial for applications or compute workloads to interact with GCP services, managed through Identity and Access Management (IAM).
6. In the **Service Account Private Key** field, paste the private key associated with your service account. To extract and copy the private key from a JSON file, you can use the command `jq -r .private_key < filename.json | pbcopy`.

    <figure><img src="../../.gitbook/assets/gcp_cc2.png" alt=""><figcaption><p><strong>Add Cloud Credentials</strong> page in the DuploCloud Portal</p></figcaption></figure>

7. Click **Submit** to save your credentials, which are then displayed on the **Cloud Credentials** page.

<figure><img src="../../.gitbook/assets/gcp_cc.png" alt=""><figcaption><p>GCP <strong>Cloud Credentials</strong> page in the DuploCloud Portal</p></figcaption></figure>

For enhanced integration, consider creating a GitHub Actions secret named `CLOUD_CREDENTIALS` with the JSON credentials and a GitHub Actions variable named `CLOUD_ACCOUNT` with the project ID or name. This facilitates further integrations and automations within your CI/CD pipelines.

**Note:** When providing cloud credentials, it's essential to create a service account with the IAM Admin Service Accounts role and grant it the Owner role. Generate a new private key for this account, selecting JSON as the key type, and download the JSON file. The Project ID and Service Account Email can be directly copied from this JSON file, simplifying the process of adding cloud credentials in DuploCloud.

Should you require any assistance during this process, DuploCloud customer support is available to help.