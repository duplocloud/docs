# Cloud Console, API and CLI

DuploCloud manages access for users to the cloud provider. This is achieved by creating a session in the cloud provider who permissions are the same as the tenant's IAM role.&#x20;

* In case of AWS such sessions are transit and does require a username to be created in the cloud provider. When logged into AWS console the username will appear as \<tenantname>/\<emailaddress>. Note that this user has the same access as the tenant IAM role. Same principle is used for cli access. See the [JIT](../../aws-user-guide/use-cases/jit-access.md) section for more details.
* In case of GCP the session is generated and has the same permission as the Tenant's IAM role. The username itself does existing in GCP because its a gsuite user, but the permissions that are generated and associated are just-in-time for the duration of the session.
* In case of Azure each user is addess to the user access list for the resource group that the tenant is part of. The validity of this session is tied to validity of the user login. The access of the session is NOT transient and is permanently attached to the resource group for as long as the user has access to the tenant.

All user activity in the direct cloud provider is tracked in the cloud provider audit trail like cloud trail.&#x20;
