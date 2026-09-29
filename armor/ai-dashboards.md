# AI Dashboards

DuploCloud's agentic dashboarding lets you create purpose-built dashboards for any data source connected as a provider — cloud accounts, Kubernetes clusters, incident management systems, cost tracking platforms, and more. Dashboards can be organized into categories such as **Observability**, **Security & Compliance**, and **Cost**, and scoped to specific environments or shared globally across your organization.

The workflow is template-driven. An AI agent builds a reusable **Dashboard Template** that defines the layout, panels, and data-fetching logic. Once a template is published it can be instantiated as many times as needed — each instance connected to a different scope (a different cloud account, cluster, or environment) — without rerunning the agent.

## Dashboard Primitives

Every dashboard is composed of four panel types:

| Primitive         | Description                                                              |
| ----------------- | ------------------------------------------------------------------------ |
| **Single Values** | A single metric displayed prominently, with optional trend indicators    |
| **Tables**        | Tabular views of multi-row data such as service lists or cost breakdowns |
| **Alerts**        | Active alert feeds pulled from connected monitoring systems              |
| **Insights**      | AI-generated narrative analysis surfaced alongside the metrics           |

When building a template, the agent uses the built-in **Dashboarding skill** to choose the right primitive for each metric it discovers, based on the nature and volume of the data.

## Viewing Dashboards

Dashboards are accessible under **Analytics** in the left sidebar, grouped by category — **Observability**, **Security**, or **Cost** — depending on which category the dashboard belongs to. Navigate to the relevant category and select **Dashboards**. Each published and instantiated dashboard appears as a tab at the top of the page, letting you switch between dashboards for different environments or use cases at a glance.

![Dashboards overview](../.gitbook/assets/dashboards-step-02.png)

## Dashboard Templates

Templates define the panel structure, filters, and data-fetching script for a dashboard. Navigate to **Analytics → Observability → Dashboard Templates** to see all available templates.

![Dashboard Templates list](../.gitbook/assets/dashboards-step-03.png)

Each row shows the template name, description, scope (Global or Workspace), publication status, and the number of filters it exposes.

## Creating a Dashboard Template

### 1. Open the New Template modal

Click **+ New Template** in the top-right corner of the Dashboard Templates page.

![New Template modal — base template selection](../.gitbook/assets/dashboards-step-05.png)

Give the template a name. Optionally select a **Base Template** to start from an existing structure, or choose **None / Blank** to build from scratch. Click **Create**.

![New Template modal — filled](../.gitbook/assets/dashboards-step-06.png)

The template detail page opens. The panel slots — Filters, Stats Panel, Timeseries Panel, and Recent Panel — are empty until the agent populates them.

![Empty template detail](../.gitbook/assets/dashboards-step-07.png)

### 2. Open an agent session

Click **Edit with Agent** on the template detail page. Select an agent and a workspace scope that grants access to the data sources you want to include in the dashboard.

![Edit with Agent — agent selection](../.gitbook/assets/dashboards-step-09.png)

![Edit with Agent — scope selected](../.gitbook/assets/dashboards-step-10.png)

Click **Start Session**.

### 3. Describe the dashboard to the agent

In the chat, describe what the dashboard should show — the data sources to draw from, the metrics that matter, and any focus areas such as cost breakdown, reliability indicators, deployment frequency, or security posture. Be as specific or as broad as suits your needs.

![Agent session — user prompt](../.gitbook/assets/dashboards-step-11.png)

The agent queries the connected data sources, analyses what is available, and determines the best panel structure for your requirements.

![Agent — fetching data](../.gitbook/assets/dashboards-step-13.png)

### 4. Review the generated template

As the agent works, the YAML template definition and panel list appear in the right-hand pane. The agent explains each panel, the metric it tracks, and why it was included.

![Template structure generated](../.gitbook/assets/dashboards-step-15.png)

### 5. Preview with live data

Once the structure is ready, the agent runs the data-fetching logic against your connected providers and populates a **Dashboard Preview** with real values. This lets you validate that every panel is showing the right data before committing.

![Dashboard Preview with live data](../.gitbook/assets/dashboards-step-18.png)

### 6. Review findings and persist the fetch script

After the preview, the agent surfaces a summary of key findings across the panels. It then generates a reusable **fetch script** that will run automatically on every future refresh of the dashboard — so the agent does not need to be invoked again after the initial build.

![Agent summary and fetch script](../.gitbook/assets/dashboards-step-21.png)

### 7. Save the template

Click **Save Dashboard Template**. A confirmation message confirms the template and its fetch script have been persisted.

![Template saved confirmation](../.gitbook/assets/dashboards-step-23.png)

## Publishing a Template

Return to the dashboard template you just created. Set its status to **Published** to make it available for instantiation across the workspace.

![Template published](../.gitbook/assets/dashboards-step-25.png)

## Creating a Dashboard from a Template

Open the template detail page and click **Create Dashboard**.

![Template detail — Create Dashboard button](../.gitbook/assets/dashboards-step-28.png)

In the **Create Dashboard** modal, provide a name for this dashboard instance and select the **Scopes** you want to connect — a cloud account, cluster, or other environment. Scope selection accepts more than one, so a single dashboard can draw on several sources at once, and is optional if the template's panels don't need credentials. Configure any filters such as date range, then click **Create Dashboard**.

![Create Dashboard modal — filled](../.gitbook/assets/dashboards-step-30.png)

The dashboard is instantiated and appears as a new tab on the Dashboards page, automatically populated with live data from the selected scopes.

![New dashboard tab with live data](../.gitbook/assets/dashboards-step-32.png)

## Reusing a Template Across Multiple Scopes

Because the template and its fetch script are reusable, one template can back as many dashboards as you need without any additional agent work. There are two ways to combine scopes:

* **Several scopes on one dashboard** — select multiple scopes when creating the instance. The panels draw on all of them together, which suits an aggregate view across accounts or clusters.
* **One dashboard per scope** — repeat the **Create Dashboard** step, selecting a different scope each time. Each instance shows the same panel structure populated from its own environment, for example one tab for development and another for production.

![Multiple dashboards from the same template](../.gitbook/assets/dashboards-step-37.png)

This makes Dashboard Templates a scalable building block: define the structure once and connect it to as many environments as your organization needs.

## Inspecting a Template's Definition

Everything a template holds — its filters, system prompt, panel layout, and the metric definitions behind each panel — is stored as a structured document you can read directly. Open the template and click **View YAML**.

![Template detail page](../.gitbook/assets/dashboards-v2-template-detail.png)

The dialog shows the full saved definition, with a **YAML** / **JSON** toggle and buttons to copy or download it.

![View YAML dialog](../.gitbook/assets/dashboards-v2-view-yaml.png)

This is useful for reviewing exactly what the agent generated, for copying a panel definition between templates, or for keeping a copy of a template's structure outside the platform. Individual panels also have their own **Edit YAML** action for changing one panel without regenerating the whole template.
