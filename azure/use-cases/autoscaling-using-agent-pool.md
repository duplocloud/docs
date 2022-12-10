# AutoScaling using Agent Pool

Azure Kubernetes AutoScaling use case can be achieved by setting up the capacity in Agent Pool required for your application. Further Kubernetes Horizontal Pod Autoscaling can be configured under services to scale your application.

### Step1: Create Azure Agent Pool

Agent pools can be scaled when **Enable Autoscaling** option is enabled in DuploCloud Portal. Each agent pool will contain nodes backed by the virtual host machines.

Navigate to DevOps --> Hosts --> Azure Agent Pool. Provide inputs for Instance Type and Minimum/Maximum Capacity to scale the pool.

![Agent Pool Screen](<../../.gitbook/assets/image (59).png>)

### Step2: Configure Service with HPA

Refer to these steps to [configure Service Deployment with Horizontal Pod Autoscaling (HPA) ](../../aws/use-cases/auto-scaling/kubernetes-scaling-options.md#kubernetes-horizontal-pod-autoscaler-hpa)from DuploCloud portal.
