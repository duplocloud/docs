---
description: What you can expect during the DuploCloud onboarding process
---

# Onboarding

## Phase 1. Kickoff and Delivery

During Kickoff and Delivery, your Team learns about the DuploCloud onboarding flow and what to expect in each phase. Our Team works closely with yours to review your project scope and objectives, technical specifications and information, and important dates and deadlines.&#x20;

By the end of this phase, DuploCloud engineers will configure a DuploCloud Platform in your company's cloud account. We will ask your Team for any feedback about the onboarding approach to improve the process in the future.&#x20;

### Your Team Provides:&#x20;

* Project details, including objectives, technical specifications, and dates/deadlines.
* A list of project members and roles.
* A new cloud account with access for DuploCloud engineers.
* Read-only access to your existing accounts, documents, repositories, and artifacts.&#x20;

### DuploCloud Provides:

* Introduction to the onboarding process.
* A DuploCloud Platform in your new cloud account.

## Phase 2. Assessment and Project Planning

In the Assessment and Project Planning phase, DuploCloud engineers create and review a high-level block diagram of your project architecture, verify your containerization/migration needs, and confirm your service configurations, interdependencies, and data migration requirements. We also complete a compliance assessment to ensure your project meets all required compliance guidelines. Together, Teams choose a working-session cadence that aligns with your project needs and timeline.&#x20;

{% hint style="info" %}
In this phase we confirm if the Agents that are available out-of-the-box accomplish the required automation goals or we need to tweak those Agents or write new ones.&#x20;
{% endhint %}

By the conclusion of this phase, we will provide you with a DuploCloud Portal your Team can access and detailed information about the project plan. So far no new workload has been deployed or an existing infrastructure been imported into the Dev Environment.

### Your Team Provides:&#x20;

* Verification of your project's containerization needs, service configurations, interdependencies, and data migration requirements.
* Project plan questions or feedback.
* Input for the creation of a working session plan.

### DuploCloud Provides:

* List of in-scope services and their statuses.
* Project plan for the initial workload deployment.
* Confirmation of Tenant structure.
* Assessment of any new AI Agents that should be built (if any).
* A DuploCloud Portal with access for your Team.
* Recurring working session schedule.

## Phase 3. Initial Workload Deployment

In this phase, DuploCloud engineers deploy your Dev Environment, which includes all in-scope services and applications. During deployment working sessions, we provide your Team with comprehensive DuploCloud Platform training. Teams discuss and complete any necessary application-level changes and move on to app containerization, secret management, and Kubernetes configuration (where required). Finally, we review the Dev Environment and your Team's test plan.  &#x20;

If we are importing existing infrastructure then we would map out the existing Dev Namespaces, wire them to the DuploCloud observability and security solution as appropriate and test out agentic workflows. We aim to accomplish a majority of required use cases.&#x20;

{% hint style="info" %}
In large organizations during onboarding we only aim to achieve a representative set of use cases unlike a smaller organization where we can cover pretty much all use case and are ready to go live in a production environment fully managed by DuploCloud.
{% endhint %}

### Your Team Provides:&#x20;

* Necessary application changes.
* Dev Environment testing and signoff.

### DuploCloud Provides:

* A complete Dev Environment deployment for testing.
* Training on the DuploCloud Platform during deployment work sessions.
* Terraform code that can be used as a template for new environments, if needed.
* Custom AI Agent where applicable

## Phase 4. CI/CD & Release Management

The CI/CD & Release Management phase involves identifying Services and Tenants to implement pipelines, selecting and agreeing on a pipeline implementation logic, and building the pipelines. DuploCloud builds an operational CI/CD pipeline for each Service and trains your Team to add and modify CI/CD pipelines in the future. &#x20;

### Your Team Provides:&#x20;

* Input for CI/CD pipeline development.
* Participation in information/knowledge sharing, training, and demo.

### DuploCloud Provides:

* An operational CI/CD pipeline for each of the project’s Services.
* Training so your Team can add and modify pipelines.

## Phase 5. Production Deployment

The fifth phase, Production Deployment, focuses on the Production environment. During this phase, the DuploCloud Team works with your Team to confirm your high-availability requirements and apply any needed adjustments. We also review and update infrastructure component scale parameters (e.g., CPU and memory utilization) and monitoring and alerting configurations. Lastly, we review data migration requirements and formulate a production cutover plan.&#x20;

In large organization this covers only a subset of environments or use cases. The internal Teams take over from here and continue the process.

### Shared Responsibilities

* Deploy the Production environment
* Test the Production environment
* Stabilize production applications

## Phase 6. Onboarding Signoff

Onboarding Signoff ensures that your Team is prepared for the following stages of support and operations, where you’ll receive ongoing maintenance assistance. We review your ongoing support needs, discuss your plans for the next 3 to 6 months, and establish the next steps with the Operations Team to ensure a smooth handover and continuity of service. On top of that, the DuploCloud Team delivers an updated architecture diagram, providing a clear and current overview of the system's structure. Lastly, we ask you for feedback about the onboarding experience, which is crucial for assessing the process and identifying areas for improvement.

### Your Team Provides:&#x20;

* Feedback about the onboarding experience.

### DuploCloud Provides:

* An outline of your next steps with the Operations Team.
* An updated architecture diagram.
