# Skills

Skills define the tasks your AI Engineer can perform, like Kubernetes operations, CI/CD workflows, or security tasks. Multiple Skills can be grouped into Personas which represent specific roles (for example, DevOps Engineer or Full Stack Engineer).&#x20;

At its core, a Skill is a folder containing a `SKILL.md` file. This file includes required metadata (at minimum, name and description), and instructions that tell the Agent how to perform a specific task. A Skill can also include supporting assets such as scripts, templates, and reference materials. [Learn more about Skills here](https://agentskills.io/what-are-skills).

There are three ways to assign Skills to an Engineer:

**Pre-Built Skills**: The DuploCloud platform provides pre-built Skills that you can use to quickly create and configure your first Engineer.

**External Skills**: You can use Skills from third-party vendors directly within the platform. Examples include:

* [Pulumi Agent Skills](https://github.com/pulumi/agent-skills/)
* [HashiCorp Agent Skills](https://github.com/hashicorp/agent-skills/)
* [Azure Agent Skills](https://github.com/microsoft/skills/)

**Custom Skills**: You can create your own Skills from scratch to meet your organization’s specific requirements.

## Assigning Skills to an Engineer:&#x20;

1. Navigate to **Skills** and click **Add**.&#x20;
2. Enter a **Name** and detailed **Description**.

<figure><img src="../../.gitbook/assets/unknown (8).png" alt=""><figcaption></figcaption></figure>

3. Select the **Skill** **Type** (**External** or **Custom**).
4. Optionally, add a **Description** for the Skill.

<figure><img src="../../.gitbook/assets/unknown (9).png" alt=""><figcaption></figcaption></figure>

5. Specify the Skills package:

* &#x20;**External Packages:** Enter the link to the Skills package.
* **Custom** **Packages:** upload/paste a [`Skill.md`](http://skill.md) file or a Skill Package in `.zip` format into the **Package File** field.

6. Click **Update** to save.&#x20;

#### Example: Typical `SKILL.md` File

````
# Terraform Management Skill

## Description
Expert in Terraform infrastructure as code for AWS, Azure, and GCP.

## Capabilities
- Create and modify Terraform configurations
- Manage state files and remote backends
- Troubleshoot plan and apply errors
- Implement modules and workspaces
- Handle provider version constraints

## Best Practices
- Always run `terraform plan` before apply
- Use remote state with locking
- Implement proper variable validation
- Tag all resources appropriately
- Use modules for reusable components

## Common Commands
```bash
terraform init
terraform plan -out=tfplan
terraform apply tfplan
terraform destroy
terraform state list
```
## Error Handling
- Check for state lock issues
- Verify provider credentials
- Validate syntax with `terraform validate`
- Review dependency cycles
````

#### Example: Typical Skill Folder Structure

```
skills/
├── SKILLS.md
├── infrastructure/
│   ├── terraform.md
│   ├── kubernetes.md
│   └── cloud-provisioning.md
├── cicd/
│   ├── pipeline-management.md
│   └── deployment-strategies.md
├── observability/
│   ├── monitoring.md
│   └── logging.md
├── security/
│   ├── scanning.md
│   └── secrets-management.md
└── incident-response/
    ├── troubleshooting.md
    └── root-cause-analysis.md
```
