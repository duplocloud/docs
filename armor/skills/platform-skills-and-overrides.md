# Platform Skills and Overrides

## Platform Default Skills

DuploCloud ships a set of built-in skills. The platform loads one of them automatically when it creates a ticket for a resource or a project. For example, a ticket that provisions an AWS network gets `duplo-aws-infra`, and a project's AI Planner gets `duplo-project-management`. You don't attach these skills yourself.

| Skill | What it does |
|---|---|
| `duplo-project-management` | Guides a project through three phases: Spec (what and why), Plan (how, broken into stages and test-driven tasks), and Execution (a JSON list of stages and tasks for the project board). The agent reads only the file for the current phase and never moves to the next phase on its own. |
| `duplo-aws-infra` | Provisions AWS baselines: VPC networks, EKS or ECS clusters, cluster add-ons, resource groups (IAM, KMS, security groups), and plans. |
| `duplo-aws-resources` | Provisions AWS resources inside an existing resource group, such as RDS instances, RDS clusters and ElastiCache. |
| `duplo-azure-infra` | Provisions Azure baselines: VNets, AKS clusters, cluster add-ons and resource groups. |
| `duplo-azure-resources` | Provisions Azure resources inside an existing resource group, such as virtual machines. |
| `duplo-kubernetes-infra` | Provisions Kubernetes resources such as namespaces and node groups, on any cloud. |
| `duplo-dashboard` | Builds dashboard templates, runs them with live data, and writes the fetch script. Covers Grafana/Prometheus, AWS CloudWatch, Kubernetes and MCP-backed datasources. |
| `duplo-iac-terraform-import` | Imports existing Terraform repositories and runs Terraform actions for them. |
| `duplo-extension-ticket` | Runs the provisioning ticket for an extension. |

Built-in skills are seeded when the platform starts, and they can't be edited or deleted. To see them, go to **AI Admin → Skills → Skills** and turn on **Show Built-In**.

![Skills list with Show Built-In turned on](<../../.gitbook/assets/platform-skills-02-built-in-skills.png>)

### Which skill runs for which ticket

Each ticket the platform creates has an **Origin Type** (what created it, such as `Project`, `Network` or `AWSRdsInstance`) and a **Sub Type** (the specific job, such as `project-planner` or `aws-network-baseline`). The platform default table maps each Origin Type and Sub Type pair to a skill, and to provision and deprovision timeouts.

To see the table, go to **AI Admin → Skills → Skill Mapping** and click **View Defaults**.

![Platform Default Skill Mappings](<../../.gitbook/assets/platform-skills-01-defaults-modal.png>)

---

## Skill Mapping Overrides

A skill mapping override replaces the platform default skill for one Origin Type and Sub Type pair. Use it when your team wants a different instruction set for a ticket type. For example, you might use your own project workflow that adds a review phase, or an AWS skill that enforces your tagging policy.

{% hint style="warning" %}
**An override applies to the whole platform.** There is one override per Origin Type and Sub Type pair, and it applies to every workspace. The platform looks the mapping up each time the agent starts work on a ticket, so an override also changes existing tickets of that type, not just new ones. Test your skill before you map it.
{% endhint %}

An override can also set its own provision and deprovision timeouts. Any timeout you leave blank keeps the platform default.

### Before you start

The skill you want to use must already exist. The **Override Skills** list shows every skill in the system, including the built-in skills. If you haven't created your skill yet, see [Creating a Skill](README.md#creating-a-skill).

### Add an override

1. Go to **AI Admin → Skills → Skill Mapping**. The page lists existing overrides, with a summary of how many there are and how many set their own timeouts. Click **Add Override**.

    ![Skill Mapping page](<../../.gitbook/assets/platform-skills-03-skill-mapping-list.png>)

2. Select the **Origin Type** and **Sub Type**. The form shows the platform default skill for that pair.

    ![Add Skill Mapping Override form showing the platform default](<../../.gitbook/assets/platform-skills-05-add-override-default.png>)

3. Open **Override Skills** and select the skill to use instead. You can select more than one skill.

    ![Override Skills list](<../../.gitbook/assets/platform-skills-06-override-skills.png>)

4. Optionally, enter a **Provision Timeout** or **Deprovision Timeout** in seconds. Leave them blank to keep the platform defaults shown under each field.

5. Click **Create**.

    ![Completed override form](<../../.gitbook/assets/platform-skills-07-add-override-filled.png>)

### Confirm the override

**In the Skill Mapping list.** The new row shows the platform default under **Default Skills** and your skill under **Override Skills**. A timeout you changed shows an **Override** badge.

![New override in the Skill Mapping list](<../../.gitbook/assets/platform-skills-08-override-in-list.png>)

**In a ticket.** Open a ticket of that type and click **Details**. The **Skills** section shows the skill the platform loads by default.

Before the override, a project's AI Planner ticket shows `duplo-project-management`:

![Ticket Details before the override](<../../.gitbook/assets/platform-skills-04-ticket-before.png>)

After the override, the same ticket shows the override skill:

![Ticket Details after the override](<../../.gitbook/assets/platform-skills-09-ticket-after.png>)

The agent follows the override skill from its next reply onwards. In this example, the override skill tells the agent to start every reply by naming the skill:

![Agent reply using the override skill](<../../.gitbook/assets/platform-skills-10-agent-reply.png>)

### Edit or remove an override

Open the menu (**⋮**) on the override's row and choose **Edit** or **Delete**. When you edit, you can change the skills and timeouts, but not the Origin Type or Sub Type. To move an override to a different pair, delete it and create a new one.

Deleting an override returns that Origin Type and Sub Type to the platform default right away, including for existing tickets.
