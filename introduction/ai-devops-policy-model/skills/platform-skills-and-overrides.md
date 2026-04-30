# Platform Skills and Overrides

## Platform Default Skills

DuploCloud ships a set of platform default skills — pre-built agent instruction sets that are available to every workspace without any custom configuration.

**duplo-project-management** guides the agent through a three-phase project workflow: Spec (define what and why), Plan (define how, with TDD tasks), and Execution (generate a StageBoard-ready JSON of stages and tasks with UUIDs). The agent loads only the file for the active phase and never transitions automatically — the user drives progression via ticket type.

**duplo-aws-infra** provisions and manages AWS infrastructure baselines. It routes to sub-skills for network baseline (VPC, subnets, security groups), cluster baseline (EKS), and resource provisioning — producing structured outputs the platform can act on.

**duplo-dashboard** builds observability dashboards end-to-end. It covers template authoring, live data runs, and script generation across Grafana/Prometheus, AWS CloudWatch, and Kubernetes datasources.

All three follow the same pattern: a `SKILL.md` index routes the agent to the correct phase file based on ticket context, keeping instructions modular and token-efficient. They are seeded at startup and are protected from deletion — they form the baseline capability layer every DuploCloud AI Suite deployment starts with.

---

## Skill Mapping

Skill Mapping lets you override the platform default skills for a specific Origin Type and Sub Type combination. When a ticket is created that matches the override, the agent loads the mapped skill instead of the platform default — without any change to the project or ticket configuration.

### Viewing the Platform Defaults

Go to **AI Admin → Skill Mapping** and click **View Default Skills** to see the full table of default mappings. Each row shows an Origin Type, its Sub Type, and the platform default skill assigned to it.

![](<../../../.gitbook/assets/skill-mapping-step-01.png>)

### Why Override?

Let's consider a scenario. The image shows a copy of the current project platform default skill, which covers three phases: Spec, Plan, and Execution.

![](<../../../.gitbook/assets/skill-mapping-step-02.png>)

The team wants to use a skill that extends this workflow — like adding a dedicated **Review** phase — you can map it as an override so that project tickets automatically use the richer skill instead. This would not be possible without override.

![](<../../../.gitbook/assets/skill-mapping-step-03.png>)

### Guide to Skill Mapping

### Step 1 — Navigate to Skill Mapping

In **AI Admin → Skills**, open the **Skills** dropdown and select **Skill Mapping**. The page opens showing all active overrides — it is empty until the first override is added.

![](<../../../.gitbook/assets/skill-mapping-step-04.png>)

### Step 2 — Add a Skill Mapping Override

Click **+ Add**. In the form that appears:

- **Origin Type** — select the ticket origin (e.g. `Project`)
- **Sub Type** — select the sub type within that origin (e.g. `project-planner`)
- **Override Skills** — select the skill to use instead of the platform default

The platform default for the selected combination is shown for reference. Open the **Override Skills** dropdown and choose the skill to substitute.

![](<../../../.gitbook/assets/skill-mapping-step-05.png>)

Select the override skill — here, `Project-lifecycle` — then click **Create**.

![](<../../../.gitbook/assets/skill-mapping-step-06.png>)

---

### Verifying the Override

To confirm the override is active, create a project and open its AI Planner. The agent will now load the overridden skill rather than the platform default.

Create a new project under **Projects** with the relevant scopes.

![](<../../../.gitbook/assets/skill-mapping-step-07.png>)

The project is created with the standard three-phase workflow (Specification, Plan, Execution). The override takes effect when the AI Planner session starts — the agent reads the overridden skill and follows its instruction set.

![](<../../../.gitbook/assets/skill-mapping-step-08.png>)

Open the AI Planner and progress through the workflow. When you prompt the agent to move to the review phase, it transitions into the Review phase defined in the overridden skill — a phase that does not exist in the platform default.

![](<../../../.gitbook/assets/skill-mapping-step-09.png>)

The agent generates a full review document — in this example covering observability, cost optimisation, and SOC2 security — confirming that the `duplo-project-lifecycle` skill is active and the override is working correctly.

![](<../../../.gitbook/assets/skill-mapping-step-10.png>)
