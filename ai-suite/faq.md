# FAQ



### What is the infrastructure cost of running the DuploCloud AI Suite?

Infrastructure costs (EC2 instances, load balancers, S3 buckets) will be approximately $30-50 per month. LLM/Bedrock costs will only apply when you actively use the features and will be a few dollars per month.&#x20;

### What agents are available out-of-the-box?

We provide several pre-built agents including Kubernetes troubleshooting, Private GPT, Architecture Diagram generation, and Observability. Full documentation is available in the [out-of-the-box agents section](ai-helpdesk/out-of-the-box-agents.md).

### What is Private GPT and why should we use it?

Private GPT is a ChatGPT-like interface that keeps all your data within your AWS account. It's ideal for organizations with data security requirements that prevent using public AI services.

### Can we get custom agents built for our specific use cases?

Yes, we can develop custom agents tailored to your specific DevOps use cases.

### How does DuploCloud ensure the security of my data in DuploCloud AI Suite?

The DuploCloud Platform has always been a self-hosted solution that lives inside your Cloud - The DuploCloud AI Suite follows the same pattern.  The AI Agent, any knowledge sources (VectorDBs), and the LLM are all hosted inside your cloud account.&#x20;

<figure><img src="../.gitbook/assets/Self Hosted.png" alt=""><figcaption></figcaption></figure>

### What Model Providers do you support?

The default Model Provider will be AWS Bedrock to keep the data within your cloud account.  With our PreBuilt Agent option any Model Provider can be used.&#x20;



