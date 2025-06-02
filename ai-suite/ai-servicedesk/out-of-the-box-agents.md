# Out of the Box Agents

DuploCloud’s AI Suite comes with several built-in, domain-specific agents that help you troubleshoot and manage your infrastructure. These out-of-the-box agents provide immediate support for Kubernetes, AWS, and Observability environments.

To get started with any agent, navigate to **AI Suite** -> **ServiceDesk**, select your **Tenant**, and choose the agent that best fits your needs. See the [Tickets documentation](ticket.md) to learn more about working with ServiceDesk tickets.

## Kubernetes

The Kubernetes agent assists with Kubernetes-related tasks, from debugging pods to managing Helm applications. It understands Kubernetes concepts and can walk you through cluster operations with suggested `kubectl` commands.

To access the Kubernetes agent from the DuploCloud Platform, select your Tenant from the **Tenant** list box, go to **AI Suite** -> **ServiceDesk**, and choose the **`k8s` Agent** and **Instance**. You can describe a problem or ask a question, and the agent will respond with diagnostic steps, command suggestions, and optional follow-up actions like restarting the pod or checking logs. It can also assist with Helm chart management, including converting Docker Compose files into Helm templates.

## AWS

The AWS agent helps you explore and manage your AWS environment using AWS CLI commands. It understands natural-language requests and can translate them into actionable commands that query or modify AWS resources.

To access the AWS agent from the DuploCloud Platform, select your Tenant from the **Tenant** list box, go to **AI Suite** -> **ServiceDesk**, and choose the `aws` **Agent** and **Instance.** Then, start the interaction by describing your problem or asking a question like _(_&#x66;or example, `What was the last S3 bucket I created?`_)._ The agent will suggest and execute CLI commands, show the output, and suggest what to do next, such as inspecting the bucket’s contents or permissions.

## Observability

The Observability agent focuses on metrics and performance monitoring. Rather than suggesting CLI commands, it generates Grafana dashboard URLs and ready-made queries to help you visualize issues in real time.

To access the Observability agent from the DuploCloud Platform, select your Tenant from the **Tenant** list box, go to **AI Suite** -> **ServiceDesk**, and choose the `grafana-agent` for the **Agent** and **Instance**. You might type a prompt like `Show CPU usage for my backend service` and the agent will return a clickable URL that opens the Grafana Explorer with the relevant data preloaded. It can also offer suggestions for additional metrics to monitor or compare.

