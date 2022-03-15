# Configuration scopes

## **Base Configuration** <a href="#0-toc-title" id="0-toc-title"></a>

This must be set up by the user outside DuploCloud and provided as an input to DuploCloud. This is a once in a lifetime configuration. This configuration includes one VPC and one subnet with appropriate routes. It is recommended that you setup at least 2 Availability Zones, one public and one private subnet in each availability zone. All resources (EC2 instances, RDS, Elastic-cache, etc.) are placed in the private subnet by default. ELB is placed in public or private subnet based on user (tenant) choice. DuploCloud provides a default cloud formation template that can be used if desired.

## **Plan Configuration** <a href="#1-toc-title" id="1-toc-title"></a>

Every tenant is part of one and only one plan. Configuration applied at the plan level is applies to all tenants in a plan. A plan can be used to denote say a dev environment, a class of tenants (private\public facing) etc. Following are the plan configurations. Except of VPC and subnets rest of the parameters can be changed at will. Plan parameters include:

```json5
{
  "Name": "devplan", /* Name of the plan */
  "Images": [ /* AMIs that are made available for the tenants */
    {
      "Name": "Duplo-Host-Docker-v1.17", /* User friendly Name of the AMI displayed to the user */
      "ImageId": "ami-0861ea68", /* AWS AMI ID */
      "OS": "Linux"
    },
    {
      "Name": "ubuntu-dev",
      "ImageId": "ami-d83af7b8",
      "OS": "Linux"
    },
    {
      "Name": "Windows-Docker-Fleet",
      "ImageId": "ami-1977d979",
      "OS": "Windows"
    },
    {
      "Name": "Unmanaged Ubuntu-16.04",
      "ImageId": "ami-5e63d13e",
      "OS": "Linux"
    }
  ],
  "Quotas": [ /* Limit of on the number of resources that be used by each tenant. If none is set for a given resource type, then there is no limit. */
    {
      "ResourceType": "ec2",
      "CumulativeCount": 2,
      "InstanceQuotas": [
        {
          "InstanceType": "t2.medium",
          "MetaData": "(2CPU, 4GB)",
          "Count": 2
        },
        {
          "InstanceType": "t2.small",
          "MetaData": "(1CPU, 2GB)",
          "Count": 2
        }
      ]
    },
    {
      "ResourceType": "rds",
      "CumulativeCount": 1,
      "InstanceQuotas": [
        {
          "InstanceType": "db.t2.small",
          "MetaData": "(1CPU, 1.7GB)",
          "Count": 1
        }
      ]
    },
    {
      "ResourceType": "ecache",
      "CumulativeCount": 1,
      "InstanceQuotas": [
        {
          "InstanceType": "cache.t2.small",
          "MetaData": "(1CPU, 1.7GB)",
          "Count": 1
        }
      ]
    },
    {
      "ResourceType": "s3",
      "CumulativeCount": 1,
      "InstanceQuotas": [
        {
          "InstanceType": "bucket",
          "MetaData": "bucket",
          "Count": 1
        }
      ]
    },
    {
      "ResourceType": "sqs",
      "CumulativeCount": 1,
      "InstanceQuotas": [
        {
          "InstanceType": "queue",
          "MetaData": "queue",
          "Count": 1
        }
      ]
    },
    {
      "ResourceType": "dynamodb",
      "CumulativeCount": 1,
      "InstanceQuotas": [
        {
          "InstanceType": "table",
          "MetaData": "table",
          "Count": 1
        }
      ]
    },
    {
      "ResourceType": "elb",
      "CumulativeCount": 2,
      "InstanceQuotas": [
        {
          "InstanceType": "elb",
          "MetaData": "elb",
          "Count": 1
        }
      ]
    },
    {
      "ResourceType": "sns",
      "CumulativeCount": 1,
      "InstanceQuotas": [
        {
          "InstanceType": "topic",
          "MetaData": "topic",
          "Count": 1
        }
      ]
    }
  ],
  "AwsConfig": {
    "VpcId": "vpc-1eafce79", /* VPC for this tenant */
    "AwsHostSg": "sg-c2d899ba", /* list of security groups separated by ;. All hosts will be placed in this security groups. */
    "AwsElbSg": "sg-b9d899c1", /* Security group in which the ELB will be placed. This applies to traffic into the extenal (VIP) of the elb. Internal Sg between hosts and ELB will be auo setup.  */
    "AwsPublicSubnet": "subnet-0066b449;subnet-24e25943", /* Subnets in which hpublic facing ELBs must be placed. Each subnet corresponds to an AZ. */
    "AwsInternalElbSubnet": "subnet-0e66b447;subnet-23e25944", /* Subnets in which internal resources like Ec2 hosts, rds ecaache etc will be placed. If you like hosts to be public facing then put the same public subnets here. */
    "AwsElastiCacheSubnetGrp": "duplo-cache-aww6gk5hsy4n",
    "AwsRdsSubnetGrp": "duplo-vpc-21-resources-dbsubnetduplo-z9fh3g59362z",
    "CommonPolicyARNs": "", /*Set of IAM policy ARNs that will be applied to all tenants. */
    "Domain name": "" /* Name of route 53  domain that will be used for tenant custom dns names*/
    "CertMgrResourceArns": "" /* List of certificate arns that wil be available to the tenant for SSL termination on the ELB. */
  },
  "UnrestrictedExtLB": false,
  "Capabilities": {
    "DisableNativeApps": false,
    "DisablePublicEps": false,
    "DisablePrivateElb": false,
    "AssignInstanceElasticIp": false,
    "BlockEbsOptimization": false,
    "DisableSumoIntegration": false,
    "DisableSignalFxIntegration": false,
    "EnableTenantExpiry": false
  }
}
```

## **Tenant Configuration** <a href="#2-toc-title" id="2-toc-title"></a>

These are the configuration that we covered in the deployment guide.
