# Skills

Skills are what your AI engineer knows how to do—think Kubernetes operations, CI/CD workflows, or security tasks. Create skills from scratch, link to external packages, or upload your own. To simplify, group multiple skills into Personas representing specific roles (like DevOps or Full Stack).&#x20;

At its core, a skill is a folder containing a SKILL.md file. This file includes metadata (name and description, at minimum) and instructions that tell an agent how to perform a specific task. Skills can also bundle scripts, templates, and reference materials.

[Learn more about skills here](https://agentskills.io/what-are-skills).



There are 3 ways to give your engineer skills:

1. Duplo Platform provides some pre-built skills that you can use to create your first engineer.&#x20;
2.  Alternately, you can use skills from 3rd party vendors directly in the Duplo Platform. Here are some examples of skills you can use:&#x20;

    [Pulumi Agent Skills](https://github.com/pulumi/agent-skills/) | [HashiCorp Agent Skills](https://github.com/hashicorp/agent-skills/) | [Azure Agent Skills](https://github.com/microsoft/skills/)
3. You can write your own skills from scratch to suit the needs of your organisation



Steps to add skills to your Engineer:&#x20;

**Step 1:** Head to the Skills section and add a new skill. Enter a name and detailed description.

<figure><img src="../../.gitbook/assets/unknown (8).png" alt=""><figcaption></figcaption></figure>



**Step 2:** Choose the skill type—link an external package (URL) or upload a custom skill.

<figure><img src="../../.gitbook/assets/unknown (9).png" alt=""><figcaption></figcaption></figure>



**Step 3:** For Custom skills, you can either upload/ paste a [Skill.md](http://skill.md) file or you can upload a Skill Package in .zip format. Click update, when done.&#x20;



A typical skill file would look something like this:

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



A typical Skill folder would be structured like this:&#x20;

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

<br>



<br>



