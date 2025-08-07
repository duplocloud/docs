---
description: Configure Permission Sets in DuploCloud for granular access control
---

# Permission Sets

Permission Sets with DuploCloud provide a comprehensive access-control mechanism, allowing administrators to assign fine-grained permissions to users. This allows administrators to provide individual users access to specific resources.&#x20;

## Key Features of DuploCloud Access Control

* **API-Level Permissions:** Administrators can define permissions at the API level. For example, _user1@duplocloud.com_ can be denied access to read secrets in the _prod01_ Tenant while still having full Kubernetes permissions.
* **Granular Access Control:** Permissions can be granted or denied at different levels:
  * **API Level:** Allows or denies access to specific APIs.
  * **Resource Type Level:** Restricts access to resource types such as _S3_, _SQS_, etc.
* **Regular Expression Support:** Policies can utilize regex patterns for _ApiNames_, _HttpMethods_, and _resource types_ to define flexible access rules.
* **Tenant-Based Access:** Policies can be scoped to one, multiple, or all Tenants.
* **User-Based Assignment:** Permissions can be directly assigned to users.

## Permission Set Concepts

#### **Permission Set**

A **Permission Set** defines access rules through a combination of _allow_ and _deny_ policies:

* **Policy Precedence:** Each Permission Set has a numeric priority value. The lower the number, the higher the precedence (e.g., a Permission Set with priority value 5 overrides one with priority value 10. If multiple Permission Sets are assigned to a user, the policies in the set with the lowest number will override those in others. _We recommend starting with a higher priority value (e.g., 50) so you can add higher-priority Permission Sets later if needed._
* **Tenant-Specific Application:** Each Permission Set applies to a defined set of Tenants.
* **User Mapping:** Each DuploCloud user is associated with one or more PermissionSets.

#### **Policy Structure**

Each policy within a Permission Set defines access rules based on the following parameters:

* **ResourceTypeRegex:** Specifies the resource type the policy applies to (e.g., `aws/s3`, `k8s/job`).
* **ApiNameRegex:** Matches specific API names to control access (e.g., `GetSecretData`).
* **HttpMethodRegex:** Defines which HTTP methods are allowed or denied (e.g., `GET`, `PUT`, `POST`, `DELETE`).

#### **Matching Logic**

DuploCloud evaluates all Permission Sets assigned to the user and uses the following logic:

* **Tenant Filtering:** Permission Sets not applicable to the current Tenant are ignored.
* **Priority Evaluation:** All applicable Permission Sets are sorted by their priority. Lower priority numbers are evaluated first.
* **Policy Match:** The first matching policy (deny or allow) found in the sorted list determines the result.
* **Default Deny:** If no matching policy is found, access is denied by default with a 400 error.

#### **System-Wide Permission Set**

A System-Wide Permission Set applies globally across all DuploCloud users. It is typically used in the following scenarios:

* **Allow-All Permission:** Set a system-wide _allow-all_ permission for backward compatibility.
* **Explicit Deny Rules:** Introduce specific _deny_ rules for individual resources as necessary, overriding the global allow settings.

## Configuring Permission Sets in DuploCloud

Configure Permission Sets and apply access restrictions in DuploCloud to manage user access. The example below uses a _deny_ policy to restrict users from accessing Kubernetes Jobs in the DuploPortal.

1. In the **DuploCloud Portal**, navigate to **Administrator** → **Permissions**.
2.  Click **Add Permission Set**. The **Add Permission Set** pane displays. \


    <figure><img src="../../.gitbook/assets/Screenshot (765).png" alt=""><figcaption><p><strong>Add Permission Set</strong> pane</p></figcaption></figure>
3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="212.22216796875"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a meaningful name for the Permission Set (e.g., <code>deny-k8s-job</code>).</td></tr><tr><td><strong>Scope</strong></td><td>From the Scope list box, select the appropriate scope for the Permission Set (e.g., <strong>User</strong>).</td></tr><tr><td><strong>Priority</strong></td><td>Enter a numerical value greater than 0. Lower values give this Permission Set higher precedence when multiple are assigned to the same user.</td></tr><tr><td><strong>Applicable Tenants</strong></td><td>Select the applicable Tenants or choose <strong>All Tenants</strong>.</td></tr><tr><td><strong>Allow or Deny Policy</strong></td><td>Click <strong>Add Allow Policy</strong> or <strong>Add Deny Policy</strong>, and configure the following fields:</td></tr><tr><td><strong>Resource Type RegEx</strong></td><td>Enter the resource type the policy will apply to. For example, <code>k8s/job</code> to target Kubernetes Jobs.</td></tr><tr><td> <strong>API Name RegEx</strong></td><td>Enter a regular expression that matches the API name for the resource. For example, <code>.*k8s/job.*</code> will match any API calls related to Kubernetes Jobs.</td></tr><tr><td> <strong>Method</strong></td><td>Choose the HTTP method for which the policy applies: <strong>GET</strong>, <strong>POST</strong>, <strong>PUT</strong>, <strong>DELETE</strong>, or <strong>ALL</strong>.</td></tr></tbody></table>

4. Click **Save** to create the **Permission Set**.

## Assigning Users to a Permission Set

After creating a Permission Set, assign specific users to it:

1. In the **DuploCloud Portal**, navigate to **Administrator** → **Permissions**.
2.  Select the Permission Set from the **NAME** column. The Permission Set details page displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/image (462).png" alt=""><figcaption><p>Adding users to the permission set</p></figcaption></figure></div>
3. Click on the **User** tab.
4. Add the list of users to whom the Permission Set should apply. In the example, **userA** and **userB** are explicitly denied access to **Kubernetes Jobs** across the selected Tenants.
5. Click **Save**.

## Testing Permission Set Configuration

To test if a Permission Set is correctly applied, follow these steps:

1. Have the specific users attempt to access a resource the Permission Set applies to (e.g., **userA** or **userB** attempt to access the **Kubernetes Jobs** section in the DuploCloud portal).
2. Verify that they receive an error message, such as:\
   \
   `Access Denied: You do not have permission to access Kubernetes Jobs`. \
   \
   If the error appears, it confirms that the policy has been successfully applied, blocking unauthorized access to the resource.

<div align="left"><figure><img src="../../.gitbook/assets/image (463).png" alt="" width="533"><figcaption><p>An error message denying user access to a K8s Job</p></figcaption></figure></div>

