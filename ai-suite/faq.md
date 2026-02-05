# FAQ

### Getting Started and Infrastructure

**What is the infrastructure cost of running the DuploCloud AI Suite?**

Infrastructure costs (EC2 instances, load balancers, S3 buckets, Bedrock LLM cost) are typically estimated at $80-150 per month. LLM/Bedrock costs will only apply when you actively use the features and will be a few dollars per month. Additional costs may apply depending on your specific use case.

### Available Agents and Customization

**What agents are available out-of-the-box?**

We provide several pre-built agents including Kubernetes troubleshooting, Private GPT, Architecture Diagram generation, and Observability. Full documentation is available in the [out-of-the-box agents](ai-helpdesk/out-of-the-box-agents.md) section.

**Can we get custom agents built for our specific use cases?**

Yes, we can develop custom agents tailored to your specific DevOps use cases.

**What is Private GPT and why should we use it?**

Private GPT is a ChatGPT-like interface that keeps all your data within your AWS account. It's ideal for organizations with data security requirements that prevent using public AI services.

### AI Models and Framework

**Does DuploCloud use Artificial Intelligence (AI) models?**

Yes. DuploCloud AI Suite is a framework to build and deploy AI agents. These agents will use LLMs to respond to users, take action, etc.&#x20;

**What Model Providers do you support?**

The default Model Provider will be AWS Bedrock to keep the data within your cloud account. With our PreBuilt Agent option any Model Provider can be used.

**What is the purpose of these AI models?**

The models, provided through AWS Bedrock inside your own AWS account, are used to power your custom AI agents. They generate intelligent responses to support DevOps workflows, troubleshooting, and automation.

**What type of output do the models generate?**

Outputs include infrastructure provisioning commands, log analysis, troubleshooting recommendations, and other data that help DevOps teams operate more efficiently.

### Data and Training

**What data is used to train the AI models?**

We do not train models. DuploCloud uses foundational models from AWS Bedrock. Your data is never used to train or improve these models.

**What data is input into the models?**

The platform provides context about your infrastructure (e.g., Kubernetes cluster names, namespaces, application logs) so the model can assist with relevant operations.

**Does DuploCloud's AI process personal information?**

No. The AI agents do not process personal or sensitive personal information.

**How does DuploCloud ensure the security of my data in DuploCloud AI Suite?**

The DuploCloud Platform has always been a self-hosted solution that lives inside your Cloud - The DuploCloud AI Suite follows the same pattern.  The AI Agent, any knowledge sources (VectorDBs), and the LLM are all hosted inside your cloud account.&#x20;

<figure><img src="../.gitbook/assets/Self Hosted.png" alt=""><figcaption></figcaption></figure>

### System Integration and Oversight

**What systems do AI agents connect to?**

DuploCloud's AI agents interact with your DevOps and infrastructure systems (such as AWS, Datadog, and application logs) to perform tasks and provide insights.

**Is there human oversight of AI actions?**

Yes. The DuploCloud AI HelpDesk is designed with human-in-the-loop oversight. Users can review, approve, or reject actions the AI proposes before execution, ensuring control and safety.

### Business Value

**Why should we try the Agentic Help Desk?**

The Agentic Help Desk tackles the biggest DevOps headaches with AI-driven workflows:

* **Ticket overload** → Automates repetitive tasks so engineers focus on higher-value work
* **Troubleshooting bottlenecks** → Provides end-to-end visibility to accelerate root cause analysis
* **Deployment delays** → Manages rollbacks, approvals, and scaling with human-in-the-loop safeguards
* **Knowledge silos** → Captures and retains critical expertise, ensuring continuity when people leave

With agents for Kubernetes, observability, and log analysis, teams already see faster fixes, safer launches, and less burnout.

### Future Development

**What's coming next? What more can I expect?**

We're expanding the HelpDesk with more prebuilt agents to tackle problems across your infrastructure, and new capabilities designed to deliver long-term value for your growth and modernization journey.



