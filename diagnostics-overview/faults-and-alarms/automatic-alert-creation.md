---
description: Create and customize automatic alerts
---

# Automatic alert creation

DuploCloud allows you to set up automatic alerts for resources in a tenant. These alerts help monitor system health and performance by applying standard thresholds (e.g., CPU usage) to supported resource types like EC2, RDS, and others.

Alerts can be customized using exclusion rules, giving you control over which resources are included in auto alerting.

## Creating an Automatic Alert

1. Select the **Alerting** tab
2. Click **Enable Alerting** to generate a default alert template. This template includes predefined rules for common AWS namespaces and metrics.
3. Review the generated rules and update the thresholds or evaluation periods as needed to match your alerting requirements.
4.  Click **Update** to save the alert configuration.<br>

    <figure><img src="../../.gitbook/assets/Screenshot (241).png" alt=""><figcaption></figcaption></figure>

## **Enabling Alerting**

Enable automatic alerting for your Tenant.

1. In the DuploCloud Portal, navigate to **Administrator** → **Tenants**.
2. Select your **Tenant** from the **NAME** column.
3. Select the **Alerting** tab.
4. Click **Click Here** or **Enable Alerting**. Once enabled, DuploCloud’s predefined out-of-the-box alert rules are enabled for the Tenant.

<figure><img src="../../.gitbook/assets/Screenshot (1085) (1).png" alt=""><figcaption></figcaption></figure>

## Customizing Alerts by Excluding Resources

Automatic alerts in DuploCloud apply to all resources of a given type, like all EC2 instances or all RDS databases. Sometimes, you may want to exclude specific resources from these alerts. This is done by adding an `ExcludeDimensions` rule to the alert configuration.

To exclude a resource from an alert:

1. Go to **Administrator** → **Tenants** in the DuploCloud portal.
2. Select the name of the Tenant from the **NAME** column.
3. In the **Alerting** tab, check whether alerting has already been enabled:
   * If not, click **Enable Alerting**. A default alert template will be generated with predefined rules for supported AWS namespaces and metrics.
   * If alerting is already enabled, click the **edit** icon in the **Alert Template JSON** section to modify the existing rules.
4. In the alert template, locate the rule where you want to add the `excludedDimensions` block. You can identify rules by their `metricName` or `namespace`.
5. Add an `ExcludeDimensions` block with the resource’s:
   * **Name**: The type of ID used for the resource (like `InstanceId` for EC2), and
   * **Value:** The exact resource ID or name you want to exclude.
6. Click **Update** to save the changes.

### **Example**

The following configuration excludes the EC2 instance with ID `i-0a1b2c3d4e5f6g7h8` from CPUUtilization alerts:

```json
{
  "HOSTS": [
    {
      "ExcludeDimensions": [
        {
          "Name": "InstanceId",
          "Value": "i-0a1b2c3d4e5f6g7h8"
        }
      ],
      "Severity": 0,
      "Cloud": 0,
      "ComparisonOperator": "GreaterThanOrEqualToThreshold",
      "Dimensions": [],
      "EvaluationPeriods": 1,
      "MetricName": "CPUUtilization",
      "Namespace": "AWS/EC2",
      "Period": 300,
      "StateTransitionedTimestamp": "0001-01-01T00:00:00",
      "Statistic": "Average",
      "Threshold": 70
    }
  ]
}
```

### Common Resource Types and IDs

| Resource Type           | Name                   | Example Value                 |
| ----------------------- | ---------------------- | ----------------------------- |
| EC2 Instance            | `InstanceId`           | `i-0123456789abcdef0`         |
| RDS Database            | `DBInstanceIdentifier` | `my-database-1`               |
| ECS Cluster             | `ClusterName`          | `my-ecs-cluster`              |
| Lambda Function         | `FunctionName`         | `my-function`                 |
| SQS Queue               | `QueueName`            | `my-queue`                    |
| Redis Cache             | `CacheClusterId`       | `my-redis-cache`              |
| Load Balancer (ALB/NLB) | `TargetGroup`          | `targetgroup/my-tg/abcdef123` |

{% hint style="info" %}
**Resource Exclusion Tips:**

* To exclude the same resource from multiple alerts, add the exclusion to each alert rule individually.
* If a `Name` value is invalid or unsupported, it will be ignored and the resource will not be excluded.
* The `Dimensions` field is not currently used for _including_ resources. It only applies to exclusions.
* Not sure which dimension name to use? Refer to the AWS CloudWatch documentation for your specific resource type.
{% endhint %}
