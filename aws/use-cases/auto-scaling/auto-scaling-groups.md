# Auto Scaling Groups

Configure Auto Scaling Group to ensure the application load is scaled based on the number of EC2 instances configured. Auto Scaling detects unhealthy instances and launches new EC2 instances. ASG is also cost-effective as EC2 Instances are dynamically created as per the application requirement within minimum and maximum count limits.

## Creating Auto Scaling Group (ASG)

Navigate **DevOps** > **Hosts** > **ASG** to create an auto-scaling group.

* **Name** - Name for the Auto Scaling Group
* **Instance Count** - Desired capacity for the autoscaling group.
* **Minimum Instances** - Minimum Instance Count. The Auto Scaling group will make sure that the total number of instances will always be greater than or equal to the minimum count.
* **Maximum Instances** - Maximum Instance Count. The Auto Scaling group will make sure that the total number of instances will always be less than or equal to the maximum count.
* **Platform** - Select container orchestration platform.
  1. _Linux Docker/Native_**:** Select this option if you want to run docker native services which are Linux based.
  2. _EKS Linux_**:** Select this option if you want to run services on the Kubernetes Cluster\


![](<../../../.gitbook/assets/image (12) (1).png>)

View the Hosts created as part of ASG creation from ASG View Details Page.\


![](<../../../.gitbook/assets/image (11) (1).png>)

## **Creating an Amazon EC2 Auto Scaling policy**

Refer to AWS [Documentation](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scale-based-on-demand.html#as-how-scaling-policies-work) for detailed steps on creating Scaling policies for the Auto Scaling Group created



## **Creating Services using Auto Scaling Group**

DuploCloud Portal provides the ability to configure Services based on the Platform - _EKS_ _Linux_ and _Linux Docker/Native_.  Select the ASG based on the platform used while creating service and auto scaling group

### **Service with Platform - EKS Linux**

![](<../../../.gitbook/assets/image (17) (1).png>)

### **Service with Platform - Linux Docker/Native**

![](<../../../.gitbook/assets/image (13) (1).png>)
