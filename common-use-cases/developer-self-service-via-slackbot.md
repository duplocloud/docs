# DuploCloud — Slack-Native Infrastructure Provisioning

This walkthrough shows how developers can provision cloud infrastructure entirely from Slack — using the Duplo Slackbot to kick off a task, track progress, and close out a Jira ticket without switching tools.

---

## The Scenario

A developer needs to create a new S3 bucket for their order service analytics feature. Instead of filing a ticket and waiting, they handle it directly from Slack.

---

## Step 1 — Mention the Slackbot

The developer mentions the Duplo Slackbot in their Slack channel and refers it to the relevant Jira ticket.

![Mention bot and reference Jira ticket](../.gitbook/assets/demo3-03-mention-bot-jira.png)

---

## Step 2 — Set Workspace and Scopes

The developer enters a few details — workspace and scopes — directly in Slack to give DuploCloud the access it needs and set the task in motion.

![Enter workspace and scopes in Slack](../.gitbook/assets/demo3-04-workspace-scopes-slack.png)

---

## Step 3 — DuploCloud Creates a Ticket and Gets to Work

DuploCloud automatically creates a ticket and begins working on the task autonomously.

![DuploCloud ticket created](../.gitbook/assets/demo3-05-duplocloud-ticket-created.png)

Progress is streamed back to Slack in real time. You can also click **Open in AI DevOps** from the Slack message to jump directly into DuploCloud and see every action the agent is taking.

![Agent working, updates in Slack](../.gitbook/assets/demo3-06-agent-working-slack.png)

![Agent actions visible in DuploCloud in real time](../.gitbook/assets/demo3-07-view-in-duplocloud-realtime.png)

---

## Step 4 — Agent Reads the Jira Ticket

The agent reads the Jira ticket for context — the S3 bucket requirements, size, environment, and retention policy are all specified there. When permissions are needed, it asks before proceeding.

![Jira ticket with S3 specifications](../.gitbook/assets/demo3-08-jira-s3-specs.png)

---

## Step 5 — Terraform Files Generated

Once the agent has everything it needs, it proceeds to execution — generating all the Terraform files for the S3 bucket.

![Terraform files created](../.gitbook/assets/demo3-09-terraform-files-created.png)

---

## Step 6 — Pull Request Opened on GitHub

The agent opens a pull request on GitHub with the generated Terraform. The Slackbot notifies the developer and waits for the PR to be approved.

![GitHub PR created](../.gitbook/assets/demo3-10-github-pr-created.png)

![Slackbot waiting for PR approval](../.gitbook/assets/demo3-11-slackbot-waiting-approval.png)

---

## Step 7 — Merge the PR

The developer reviews and merges the pull request directly in GitHub.

![Merging the pull request](../.gitbook/assets/demo3-12-merging-pr.png)

Back in Slack, the bot confirms the PR has been merged and proceeds to apply the Terraform.

![PR merged — applying Terraform](../.gitbook/assets/demo3-13-pr-merged-apply-terraform.png)

---

## Step 8 — Task Complete, Visible in HelpDesk

The entire task is completed autonomously. The same work is also visible in DuploCloud's HelpDesk, giving the team full audit trail and visibility.

![Task completed and visible in HelpDesk](../.gitbook/assets/demo3-14-task-completed-helpdesk.png)

---

## Step 9 — Jira Ticket Closed Automatically

The developer asks the bot to update Jira. The ticket is marked as done with a comment that includes a full summary of everything the bot did — including the GitHub PR link.

![Jira ticket marked done with PR comment](../.gitbook/assets/demo3-15-jira-marked-done.png)

---

## Back to Writing Code

With the infrastructure provisioned, the PR merged, and Jira updated — all from Slack — the developer can go straight back to writing code.

![Developer back to writing code](../.gitbook/assets/demo3-16-developer-back-to-code.png)
