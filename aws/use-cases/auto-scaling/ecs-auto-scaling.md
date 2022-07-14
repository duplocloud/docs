# Using ECS Auto Scaling

ECS Auto Scaling has the ability to scale the desired count of tasks for the ECS Service configured in your infrastructure.  Average CPU/Memory metrics of your tasks are used to increase/decrease the desired count value.

## Step1: Add Auto-Scaling for Targets

Navigate to **DevOps** > **Containers** > **ECS** > Select the _ECS Task Definition_ where Auto Scaling needs to be enabled > **Add Scaling Target**

Set the Minimum Capacity (minimum value 2) and Maximum Capacity to complete the configuration.\


![](<../../../.gitbook/assets/image (24).png>)

## Step2: Add Scaling Policy

Once Auto Scaling for Targets is configured, Next we have to add Scaling Policy

Provide details below:

* **Policy Name** - The name of the scaling policy.
* **Policy Dimension** - The metric type tracked by the target tracking scaling policy.. Select from the dropdown
* **Target Value** -  The target value for the metric.&#x20;
* **Scalein Cooldown** - The amount of time, in seconds, after a scale in activity completes before another scale in activity can start.
* **ScaleOut Cooldown** -The amount of time, in seconds, after a scale out activity completes before another scale out activity can start.
* **Disable ScaleIn** - Disabling scale-in makes sure this target tracking scaling policy will never be used to scale in the Auto Scaling group

This step creates the target tracking scaling policy and attaches it to the Auto Scaling group

![](<../../../.gitbook/assets/image (5).png>)



## Step3: View Scaling Target and Policy

View the Scaling Target and Policy Details from the DuploCloud Portal. Update and Delete Operations are also supported from this view



![](<../../../.gitbook/assets/image (23).png>)
