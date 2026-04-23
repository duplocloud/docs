# Amazon Web Services (AWS)

The AWS Cloud Provider lets DuploCloud AI agents interact with your AWS account — querying resources, running CLI commands, and managing infrastructure on your behalf. There are two ways to authenticate: using an **IAM Role** (recommended) or using an **Access Key**.

> Use this [CloudFormation Template](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/review?templateURL=https://duploservices-ai-access-227120241369.s3.us-west-2.amazonaws.com/aws.yaml) to easily create the AWS and Kubernetes Credentials you can use to connect with DuploCloud.&#x20;

***

## Step 1 — Add the AWS Provider

Navigate to **Providers** in the left sidebar, select your tenant (e.g. **IT**), and click the **Cloud** tab. Click **+ Add** in the top-right corner.

![Cloud providers list](../../.gitbook/assets/aws-step-01.png)

Fill in the **Add Provider** form:

* **Name** — a name for this provider (e.g. `AWS-test`)
* **Type** — select `AWS`
* **Account ID** — your AWS account ID (12-digit number)

Click **Create Provider**.

![Add Provider form](../../.gitbook/assets/aws-step-02.png)

The provider appears in the list with a success notification.

![Provider created successfully](../../.gitbook/assets/aws-step-03.png)

***

## Method 1 — IAM Role

Using an IAM Role is the recommended approach. Instead of storing long-term credentials, DuploCloud assumes a role in your AWS account to perform actions.

> **Important:** You must add the AWS account used by DuploCloud as a **trusted entity** in your IAM role's trust policy. Without this, the role assumption will fail and the agent will not be able to access your AWS resources.

### Step 2 — Add an IAM Role Credential

Click on your new provider to open it, then go to the **Credentials** tab. Click **+ Add**.

In the **Add Credential** modal:

* **Name** — a name for this credential (e.g. `AWS-test-IAM`)
* **Credential Type** — select `IAM Role`
* **IAM Role ARN** — the full ARN of the IAM role to assume (e.g. `arn:aws:iam::774157348504:role/duplocloud-test-role`)

Click **Create**.

![Add IAM Role credential](../../.gitbook/assets/aws-step-04.png)

The credential is created and you are returned to the **Scope** tab.

![IAM Role credential created](../../.gitbook/assets/aws-step-05.png)

### Step 3 — Add a Scope

With the credential in place, click **+ Add** on the **Scope** tab to define what region and resources this scope covers.

* **Name** — a name for this scope (e.g. `AWS-test-IAM-role`)
* **Credential** — select the IAM Role credential you just created
* **Region** — select the AWS region (e.g. `US East (N. Virginia) | us-east-1`)
* **Resource Types** — select specific resource types or choose `All Resources`
* **Tags** — optionally filter by resource tags

Click **Create**.

![Add Scope for IAM Role](../../.gitbook/assets/aws-step-06.png)

### Step 4 — Use the Scope in a Ticket

Go to **HelpDesk** and create a new ticket. In the scope selector, choose the IAM Role scope you created under your provider.

![Selecting the IAM Role scope](../../.gitbook/assets/aws-step-07.png)

Type your request and click **Create Ticket**.

![Ticket with IAM Role scope selected](../../.gitbook/assets/aws-step-08.png)

### Step 5 — Output

The agent uses the IAM Role to authenticate with AWS and execute the request. Results appear in the ticket thread.

![Agent processing with IAM Role](../../.gitbook/assets/aws-step-09.png)

![S3 bucket list output — IAM Role method](../../.gitbook/assets/aws-step-10.png)

***

## Method 2 — Access Key

You can also authenticate using an AWS Access Key ID and Secret Access Key. This creates long-term credentials stored in DuploCloud.

### Step 2 — Add an Access Key Credential

On the **Credentials** tab of your provider, click **+ Add**.

In the **Add Credential** modal:

* **Name** — a name for this credential (e.g. `AWS-test-key`)
* **Credential Type** — select `Access Key`
* **Access Key ID** — your AWS Access Key ID (e.g. `AKIA3IP27V2ME5MWITWV`)
* **Password** — enter your **Secret Access Key** here

> **Note:** The **Password** field in the Access Key credential form corresponds to your AWS Secret Access Key. For added safety, it is also recommended to add the Secret Access Key as an additional **Credential Field** (key: `secretaccesskey`, type: `String`, sensitive: on) so that it is explicitly available to the agent.

Click **Create**.

![Add Access Key credential](../../.gitbook/assets/aws-step-13.png)

### Step 3 — Add a Scope

On the **Scope** tab, click **+ Add**. The existing IAM Role scope (if created) will already be listed.

![Scope tab with existing IAM Role scope](../../.gitbook/assets/aws-step-14.png)

Fill in the scope form for the Access Key credential:

* **Name** — a name for this scope (e.g. `AWS-test-key`)
* **Credential** — select the Access Key credential you just created
* **Region** — select the AWS region
* **Resource Types** — select specific resource types or `All Resources`

Click **Create**.

![Add Scope for Access Key](../../.gitbook/assets/aws-step-15.png)

### Step 4 — Use the Scope in a Ticket

Go to **HelpDesk** and create a new ticket. In the scope selector, choose the Access Key scope. Both the IAM Role and Access Key scopes for your provider will appear in the dropdown.

![Selecting the Access Key scope](../../.gitbook/assets/aws-step-16.png)

Type your request and click **Create Ticket**.

![Ticket with Access Key scope selected](../../.gitbook/assets/aws-step-17.png)

### Step 5 — Output

The agent authenticates using the Access Key and returns results in the ticket thread.

![S3 bucket list output — Access Key method](../../.gitbook/assets/aws-step-18.png)
