---
description: >-
  Define custom input parameters and use built-in substitution keys to enhance
  Stacks deploy templates
---

# Customize deploy templates

## Customizing deploy templates

### Disclaimer

These customization options are intended for advanced users familiar with JSON editing and deployment workflows. Improper modifications can break the template, potentially making it difficult to troubleshoot and restore. To avoid issues, always maintain a version history or backup of the original template before making changes. While some features, like adding custom input parameters, are straightforward and significantly enhance template utility, use caution when making complex edits.

### In-line editing of parameter fields

For example, you can use a different instance size for a node.

### Creating custom input parameters

Custom template input variables enhance template reusability by allowing dynamic values to be defined and inserted during use. To create a custom variable, wrap its name with double curly braces, like this: `{{My Parameter Name}}`. When the template is processed, you will be prompted to provide a value for each custom variable. This makes your templates more flexible and adaptable to different scenarios.

### Using substitution keys

Substitution keys are predefined strings that are automatically replaced with corresponding values during template processing. Unlike custom template parameters, substitution keys do not require wrapping with special characters like double curly braces and are not listed in the pop-up dialog for custom input parameters. They can be inserted directly into the JSON template and will resolve dynamically. Below is a list of available built-in substitution keys and their descriptions.

| Substitution Key                | Value                                                                                                                                                                                     |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ref.duplo!tenantid`            | Tenant ID                                                                                                                                                                                 |
| `ref.duplo!tenantname`          | Tenant name                                                                                                                                                                               |
| `ref.duplo!tenantinfraname`     | Infrastructure name                                                                                                                                                                       |
| `ref.duplo!tenantregion`        | Tenant region (e.g., us-east-1).                                                                                                                                                          |
| `ref.duplo!k8sclustername`      | K8s cluster name (the cluster deployed under the Tenant's Plan).                                                                                                                          |
| `ref.duplo!eksami`              | AWS AMI ID for the latest EKS Node Image compatible with the Tenant's cluster version.                                                                                                    |
| `ref.duplo!dnssuffix`           | External DNS Suffix for the Tenant's Plan.                                                                                                                                                |
| `ref.duplo!duplocloudusertoken` | User Token                                                                                                                                                                                |
| `ref.duplo!duplocloudportalurl` | Duplocloud Portal URL                                                                                                                                                                     |
| `ref.duplo!s3bucketnameprefix`  | S3 bucket prefix                                                                                                                                                                          |
| `ref.duplo!jwtpublickey`        | JWT Public key                                                                                                                                                                            |
| `ref.duplo!awsaccountid`        | AWS account id                                                                                                                                                                            |
| `ref.duplo!plancertificate`     | To use plan certificates. Here user can check the array of certificates in portal , and use index in same order. (example. ref.duplo!plancertificate\[0], ref.duplo!plancertificate\[0] ) |

### Removing a resource

You can remove a resource from a deployment template to exclude it permanently. While this functions the same as unchecking a resource in the tree displayed just before deployment, the key difference is that the resource will no longer appear in the list at all.

