# FAQ



### What is the infrastructure cost of running the DuploCloud AI Suite?

AI Suite will require the following infrastructure

| Infrastructure   | Cost          | Quantity |
| ---------------- | ------------- | -------- |
| Host (t3a.small) | $14/month     | 2        |
| Load Balancer    | $25/month     | 1        |
| S3 Bucket        | $.01/month    | 1        |
| AWS Bedrock      | \~ $100/month | NA       |

### How does DuploCloud ensure the security of my data in DuploCloud AI Suite?

The DuploCloud Platform has always been a self-hosted solution that lives inside your Cloud - The DuploCloud AI Suite follows the same pattern.  The AI Agent, any knowledge sources (VectorDBs), and the LLM are all hosted inside your cloud account.&#x20;

<figure><img src="../.gitbook/assets/Self Hosted.png" alt=""><figcaption></figcaption></figure>

### What Model Providers do you support?

The default Model Provider will be AWS Bedrock to keep the data within your cloud account.  With our PreBuilt Agent option any Model Provider can be used.&#x20;



