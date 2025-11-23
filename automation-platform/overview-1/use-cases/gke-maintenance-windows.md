---
description: Configuring GKE maintenance windows in the DuploCloud Portal
---

# GKE Maintenance Windows

You can configure maintenance windows and maintenance exclusions for your GKE clusters in the DuploCloud Portal. This lets you define when automatic upgrades and maintenance tasks are allowed, giving you more control over downtime and deployment planning.

## Configuring GKE Maintenance Windows

1. In the DuploCloud Portal, navigate to **Administrator** → **Infrastructure**.
2. In the **NAME** column, click your Infrastructure name.
3. Select the **GKE** tab.
4.  Open the **Actions** menu, and select **Edit GKE Maintenance Policy**. The **Edit GKE Maintenance Policy** pane displays. <br>

    <figure><img src="../../../.gitbook/assets/Screenshot (440).png" alt=""><figcaption><p>The <strong>Edit GKE Maintenance Policy</strong> pane</p></figcaption></figure>
5. Complete the following fields:

<table data-header-hidden><thead><tr><th width="198">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Recurrence Start Time</strong></td><td>Select the maintenance window start time (e.g., <code>2025-05-26 00:00</code>).</td></tr><tr><td><strong>Recurrence End Time</strong></td><td>Select the maintenance window end time (e.g., <code>2025-05-26 04:00</code>).</td></tr><tr><td><strong>Recurrence Rule</strong></td><td>Enter an RFC 5545 recurrence rule, (e.g., <code>FREQ=WEEKLY;BYDAY=MO,WE,FR</code>).</td></tr></tbody></table>

6. Optionally, click the add button (**+**) next to **Configure Maintenance Exclusions**. Maintenance exclusions prevent GKE upgrades during specified periods, which is especially useful when your business needs require zero downtime during certain periods.&#x20;
7. Configure maintenance exclusions, as needed:

<table data-header-hidden><thead><tr><th width="133.111083984375">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Scope</strong></td><td>Configure your maintenance exclusion scope, e.g., <strong>No upgrades</strong> , <strong>No minor upgrades</strong>, or <strong>No minor or node upgrades</strong>.</td></tr><tr><td><strong>Start Time</strong></td><td>Set the time when the exclusion period begins (e.g., <code>2025-05-28 09:00</code>).</td></tr><tr><td><strong>End Time</strong></td><td>Set the time when the exclusion period ends (e.g., <code>2025-05-28 17:00</code>).</td></tr></tbody></table>

7. Click **Save** to save your maintenance policy.

<figure><img src="../../../.gitbook/assets/Screenshot (473).png" alt=""><figcaption><p>The <strong>GKE</strong> tab for the DuploCloud <strong>Auto</strong> Infrastructure with the Maintenance Policy configuration highlighted </p></figcaption></figure>

## Viewing, Editing, or Disabling GKE Maintenance Policies

1. In the DuploCloud Portal, go to **Administrator** → **Infrastructure**.
2. From the **NAME** column, select the Infrastructure where your GKE cluster is defined.
3. Select the **GKE** tab.&#x20;
4.  View the current GKE Maintenance Policy details in the **Maintenance Policy** area near the bottom of the screen. <br>

    <figure><img src="../../../.gitbook/assets/Screenshot (444).png" alt=""><figcaption><p>The GKE tab on the Infrastructure page with the Actions menu options highlighted</p></figcaption></figure>
5. Click the **Actions** menu in the upper-right corner for additional options:
   * **Edit GKE Maintenance Policy**:\
     Opens the **Edit GKE Maintenance Policy** pane where you can define or update the maintenance window for your GKE cluster.
   * **Disable GKE Maintenance Policy**:\
     Removes the current maintenance policy. GKE will then allow maintenance at any time.
6. After saving your changes or disabling the policy, the new configuration will apply to your GKE cluster.
