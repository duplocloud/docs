---
description: Deploy a full DuploCloud infrastructure stack using Pulumi
---

# Deploying a Complete DuploCloud Stack with Pulumi

This page demonstrates how to deploy a full infrastructure stack using the DuploCloud Pulumi provider. It includes setting up the infrastructure, creating a Tenant, provisioning an EKS node, deploying a web application, and configuring a load balancer. Code samples are provided in Python, Go, TypeScript, and C#.

## Prerequisites

Before you begin, make sure you have completed the steps in the [Getting Started with Pulumi](getting-started-with-pulumi-for-duplocloud.md) and DuploCloud guide.

You must also have:

* A valid AWS certificate ARN to use for the HTTPS load balancer.
* An active DuploCloud API token set in your environment or configuration.

### What This Example Does

This example Pulumi project will:

* Create DuploCloud infrastructure (VPC, subnets, region)
* Create a DuploCloud tenant
* Provision an EKS worker node using `AwsHost`
* Deploy an `nginx` service inside Kubernetes
* Expose the service using a DuploCloud-managed load balancer

## Example: Deploying a Full Stack in Multiple Languages

An example demonstrating the deployment of DuploCloud infrastructure, tenant, EKS node, and web application on Kubernetes using the DuploCloud Pulumi provider across multiple language SDKs. Replace any placeholder values with values from your actual environment.

{% hint style="warning" %}
**Note:** In each code example, replace the placeholder variable (`cert_arn` or `certArn`) with your actual AWS certificate ARN.
{% endhint %}

### Go

```go
package main

import (
	"github.com/duplocloud/pulumi-duplocloud/sdk/go/duplocloud"
	"github.com/pulumi/pulumi/sdk/v3/go/pulumi"
)

func main() {
	pulumi.Run(func(ctx *pulumi.Context) error {
		// Set up the infrastructure.

		infra, err := duplocloud.NewInfrastructure(ctx, "infra", &duplocloud.InfrastructureArgs{
			InfraName:       pulumi.String("pulumi-infra"),
			Cloud:           pulumi.Int(0),
			Region:          pulumi.String("us-east-2"),
			Azcount:         pulumi.Int(2),
			SubnetCidr:      pulumi.Int(24),
			EnableK8Cluster: pulumi.Bool(true),
			AddressPrefix:   pulumi.String("10.22.0.0/16"),
		})
		if err != nil {
			return err
		}
		ctx.Export("infraName", infra.InfraName)
		ctx.Export("vpcId", infra.VpcId)

		// Create DuploCloud Tenant
		tenant, err := duplocloud.NewTenant(ctx, "dev", &duplocloud.TenantArgs{
			AccountName:   pulumi.String("dev"),
			PlanId:        infra.InfraName,
			AllowDeletion: pulumi.Bool(true),
		}, pulumi.DependsOn([]pulumi.Resource{infra}))
		if err != nil {
			return err
		}
		ctx.Export("tenantId", tenant.ID())

		// Get native image
		image := duplocloud.GetNativeHostImageOutput(ctx, duplocloud.GetNativeHostImageOutputArgs{
			TenantId:     tenant.TenantId,
			IsKubernetes: pulumi.Bool(true),
		}, nil)

		// Create EKS Node
		node, err := duplocloud.NewAwsHost(ctx, "node", &duplocloud.AwsHostArgs{
			TenantId:      tenant.TenantId,
			FriendlyName:  pulumi.String("node01"),
			ImageId:       image.ImageId(),
			Capacity:      pulumi.String("t3a.medium"),
			AgentPlatform: pulumi.Int(7),
			Zone:          pulumi.Int(0),
			Metadatas: duplocloud.AwsHostMetadataArray{
				&duplocloud.AwsHostMetadataArgs{
					Key:   pulumi.String("OsDiskSize"),
					Value: pulumi.String("20"),
				},
			},
		}, pulumi.DependsOn([]pulumi.Resource{tenant, infra}))
		if err != nil {
			return err
		}

		// Create a service
		webapp, err := duplocloud.NewDuploService(ctx, "web-app", &duplocloud.DuploServiceArgs{
			TenantId:      tenant.TenantId,
			Name:          pulumi.String("web-app"),
			AgentPlatform: pulumi.Int(7),
			DockerImage:   pulumi.String("nginx:latest"),
			Replicas:      pulumi.Int(1),
		}, pulumi.DependsOn([]pulumi.Resource{node, tenant, infra}))
		if err != nil {
			return err
		}

		// Configure Load Balancer
		cert_arn := "arn:aws:acm:<region>:<account-id>:certificate/<certificate-id>"
		_, err = duplocloud.NewDuploServiceLbconfigs(ctx, "web-app-lb", &duplocloud.DuploServiceLbconfigsArgs{
			TenantId:                  webapp.TenantId,
			ReplicationControllerName: webapp.Name,
			Lbconfigs: duplocloud.DuploServiceLbconfigsLbconfigArray{
				&duplocloud.DuploServiceLbconfigsLbconfigArgs{
					ExternalPort:   pulumi.Int(443),
					HealthCheckUrl: pulumi.String("/"),
					IsNative:       pulumi.Bool(false),
					LbType:         pulumi.Int(1),
					Port:           pulumi.String("80"),
					Protocol:       pulumi.String("http"),
					CertificateArn: pulumi.String(cert_arn),
					HealthCheck: &duplocloud.DuploServiceLbconfigsLbconfigHealthCheckArgs{
						HealthyThreshold:   pulumi.Int(4),
						UnhealthyThreshold: pulumi.Int(4),
						Timeout:            pulumi.Int(50),
						Interval:           pulumi.Int(30),
						HttpSuccessCodes:   pulumi.String("200-399"),
					},
				},
			},
		}, pulumi.DependsOn([]pulumi.Resource{webapp, node, tenant, infra}))
		if err != nil {
			return err
		}
		return nil
	})
}
```

### Python

```python
import pulumi
import pulumi_duplocloud as duplo

# Create DuploCloud Infrastructure
infra = duplo.infrastructure.Infrastructure(resource_name="pulumi-infra",
    infra_name="pulumi-infra",
    cloud=0,
    region="us-east-2",
    azcount=2,
    subnet_cidr=24,
    address_prefix="10.22.0.0/16",
    enable_k8_cluster=True,  # Enable Kubernetes
)

# Export the outputs
pulumi.export("vpc_id", infra.vpc_id)

# Create Tenant
tenant = duplo.tenant.Tenant(resource_name="dev",
    account_name="dev",
    plan_id=infra.infra_name,
)

# Export the outputs
pulumi.export("tenantId", tenant.tenant_id)

# Create EKS Node
image = duplo.get_native_host_image_output(tenant_id=tenant.tenant_id,
            is_kubernetes=True)

node = duplo.AwsHost(resource_name="Node01",
    tenant_id=tenant.tenant_id,
    friendly_name="Node01",
    image_id=image.image_id,
    capacity="t3a.medium",
    agent_platform=7,
    zone=0,
    metadatas=[{
        "key": "OsDiskSize",
        "value": "20",
    }]
)

# Deploy nginx service on EKS

cert_arn = "arn:aws:acm:<region>:<account-id>:certificate/<certificate-id>"
app_service = duplo.duplo_service.DuploService(resource_name="web-application",
    opts=pulumi.ResourceOptions(depends_on=[node]),
    tenant_id=tenant.tenant_id,
    name="web-app",
    docker_image="nginx:latest",
    replicas=1,
    agent_platform=7,
)

# Configure Load Balancer
app_lbconfigs = duplo.DuploServiceLbconfigs(resource_name="web-application-lb",
    tenant_id=tenant.tenant_id,
    replication_controller_name=app_service.name,
    lbconfigs=[{
        "external_port": 443,
        "health_check_url": "/",
        "is_native": False,
        "lb_type": 1,
        "port": "80",
        "protocol": "http",
        "certificate_arn":  cert_arn,
        "health_check": {
            "healthy_threshold": 4,
            "unhealthy_threshold": 4,
            "timeout": 10,
            "interval": 30,
            "http_success_codes": "200-399",
        },
    }]
)

```

### TypeScript

```typescript
import * as duplocloud from "@duplocloud/pulumi";

const certArn = "arn:aws:acm:<region>:<account-id>:certificate/<certificate-id>";

// Create DuploCloud infrastructure
const infra = new duplocloud.Infrastructure("infra", {
    infraName: "pulumi-infra",
    cloud: 0,
    region: "us-east-2",
    azcount: 2,
    subnetCidr: 24,
    enableK8Cluster: true,
    addressPrefix: "10.22.0.0/16",
});

export const vpcId = infra.vpcId;

// Create DuploCloud tenant
const tenant = new duplocloud.Tenant("dev", {
    accountName: "dev",
    planId: infra.infraName,
}, { dependsOn: [infra] });

export const tenantId = tenant.tenantId;

const image = duplocloud.getNativeHostImageOutput({
    tenantId: tenant.tenantId,
    isKubernetes: true,
});

// Create DuploCloud node
const node = new duplocloud.AwsHost("Node01", {
    tenantId: tenant.tenantId,
    friendlyName: "Node01",
    imageId: image.imageId,
    capacity: "t3a.medium",
    agentPlatform: 7,
    zone: 0,
    metadatas: [{
        key: "OsDiskSize",
        value: "20",
    }],
}, { dependsOn: [tenant] });

// Create DuploCloud service
const app_service = new duplocloud.DuploService("web-application", {
    tenantId: tenant.tenantId,
    name: "web-app",
    agentPlatform: 7,
    dockerImage: "nginx:latest",
    replicas: 1,
}, { dependsOn: [node] });

// Create DuploCloud load balancer
const appLbconfigs = new duplocloud.DuploServiceLbconfigs("web-application-lbconfigs", {
    tenantId: app_service.tenantId,
    replicationControllerName: app_service.name,
    lbconfigs: [{
        externalPort: 80,
        healthCheckUrl: "/",
        isNative: false,
        lbType: 1,
        port: "80",
        protocol: "http",
        certificateArn: certArn,
        healthCheck: {
            healthyThreshold: 4,
            unhealthyThreshold: 4,
            timeout: 50,
            interval: 30,
            httpSuccessCodes: "200-399",
        },
    }],
});
```

### C\#

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Pulumi;
using Duplocloud = DuploCloud.Pulumi;

return await Deployment.RunAsync(() =>
{

    // Create a new infrastructure in AWS
    var infra = new Duplocloud.Infrastructure("pulumi-infra", new Duplocloud.InfrastructureArgs
    {
        InfraName = "pulumi-infra",
        Cloud = 0,
        Region = "us-east-2",
        Azcount = 2,
        EnableK8Cluster = true,
        AddressPrefix = "10.22.0.0/16",
        SubnetCidr = 24,
    });
    infra.VpcId.Apply(id =>
    {
        Pulumi.Log.Info($"VPC ID : {id}");
        return id;
    });

    // Create tenant
    var tenant = new Duplocloud.Tenant("dev", new()
    {
        AccountName = "dev",
        PlanId = infra.InfraName,
    },
    new CustomResourceOptions { DependsOn = { infra } });

    tenant.TenantId.Apply(id =>
    {
        Pulumi.Log.Info($"Tenant ID : {id}");
        return id;
    });

    var imageOutput = Duplocloud.GetNativeHostImage.Invoke(new()
    {
        TenantId = tenant.TenantId,
        IsKubernetes = true,
    });

     imageOutput.Apply(image =>
    {
        Pulumi.Log.Info($"AMI ID : {image.ImageId}");
        return image.ImageId;
    });

    // Create EKS Node
    var host = new Duplocloud.AwsHost("Node01", new()
    {
        TenantId = tenant.TenantId,
        FriendlyName = "Node01",
        ImageId = imageOutput.Apply(image => image.ImageId),
        Capacity = "t3a.small",
        AgentPlatform = 7,
        Zone = 0,
        Metadatas = new[]
        {
            new Duplocloud.Inputs.AwsHostMetadataArgs
            {
                Key = "OsDiskSize",
                Value = "20",
            },
        },
    },
    new CustomResourceOptions { DependsOn = { tenant } });

    // Create EKS Deployment
    var certArn = "arn:aws:acm:<region>:<account-id>:certificate/<certificate-id>";
    var appService = new Duplocloud.DuploService("web-application", new()
    {
        TenantId = tenant.TenantId,
        Name = "web-application",
        AgentPlatform = 7,
        DockerImage = "nginx:latest",
        Replicas = 1,
    },
    new CustomResourceOptions { DependsOn = { host } });

    // Create EKS Service
    var appLBConfigs = new Duplocloud.DuploServiceLbconfigs("web-application-lb", new()
    {
        TenantId = appService.TenantId,
        ReplicationControllerName = appService.Name,
        Lbconfigs = new[]
        {
            new Duplocloud.Inputs.DuploServiceLbconfigsLbconfigArgs
            {
                ExternalPort = 443,
                HealthCheckUrl = "/",
                IsNative = false,
                LbType = 1,
                Port = "80",
                Protocol = "http",
                CertificateArn = certArn,
                HealthCheck = new Duplocloud.Inputs.DuploServiceLbconfigsLbconfigHealthCheckArgs
                {
                    HealthyThreshold = 4,
                    UnhealthyThreshold = 4,
                    Timeout = 10,
                    Interval = 30,
                    HttpSuccessCodes = "200-399",
                },
            },
        },
    },
    new CustomResourceOptions { DependsOn = { appService } });

    return new Dictionary<string, object>
    {
        { "VpcId",  infra.VpcId },
        { "tenantId",  tenant.TenantId },
    };
});
```

## Outputs

Each example exports the following Pulumi outputs:

* `vpcId`: The ID of the created VPC
* `tenantId`: The ID of the DuploCloud tenant

These outputs can be used in other Pulumi stacks, referenced in CI/CD workflows, or passed into downstream infrastructure, for example, to attach additional services to the same VPC or to deploy applications into the created tenant.

### Additional Resources

* [DuploCloud Pulumi Provider GitHub Repository](https://github.com/duplocloud/pulumi-duplocloud)
* [Pulumi Documentation](https://www.pulumi.com/docs/)
* [Getting Started with Pulumi and DuploCloud](getting-started-with-pulumi-for-duplocloud.md)
* [Using API Tokens in DuploCloud](../access-control/api-tokens.md)
