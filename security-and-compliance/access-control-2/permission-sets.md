---
description: Configure Granular Access Control in DuploCloud
---

# Permission Sets

DuploCloud provides a comprehensive access control mechanism, allowing administrators to assign scoped and granular permissions to Tenant resources for users.

## **DuploCloud Access Control Key Features**

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

* **Deny Takes Precedence:** If a _deny_ policy exists, it overrides any _allow_ rule.
* **Tenant-Specific Application:** Each Permission Set applies to a defined set of Tenants.
* **User Mapping:** Each DuploCloud user is associated with one or more PermissionSets.

#### **Policy Structure**

Each policy within a Permission Set defines access rules based on the following parameters:

* **ResourceTypeRegex:** Specifies the resource type the policy applies to (e.g., `aws/s3`, `k8s/job`).
* **ApiNameRegex:** Matches specific API names to control access (e.g., `GetSecretData`).
* **HttpMethodRegex:** Defines which HTTP methods are allowed or denied (e.g., `GET`, `PUT`, `POST`, `DELETE`).

#### **Matching Logic**

When a user attempts to access resources, DuploCloud evaluates permissions based on their assigned Permission Sets. The system then follows these steps to determine access:

* **Tenant Filtering:** Checks if the Permission Set applies to the current Tenant. If not, it is ignored.
* **Explicit Deny Check:** If a _deny_ rule exists for the request, access is immediately blocked with a **400** error.
* **Allow Check:** If no _deny_ rule is found and an _allow_ rule exists, access is granted.
* **Default Deny:** If there is no explicit _allow_ rule, access is denied by default (**400**).

#### **System-Wide Permission Set**

A System-Wide Permission Set applies globally across all DuploCloud users. It is typically used in the following scenarios:

* **Allow-All Permission:** Set a system-wide _allow-all_ permission for backward compatibility.
* **Explicit Deny Rules:** Introduce specific _deny_ rules for individual resources as necessary, overriding the global allow settings.

## Configuring Permission Sets in DuploCloud

Configure Permission Sets and apply access restrictions in DuploCloud to manage user access. The example below uses a _deny_ policy to restrict users from accessing Kubernetes Jobs in the DuploPortal.

1. In the **DuploCloud Portal**, navigate to **Administrator** → **Permissions**.
2.  Click **Add Permission Set**. The **Add Permission Set** pane displays. \


    <figure><img src="../../.gitbook/assets/image (461).png" alt=""><figcaption><p>Example of adding a <strong>Deny Policy</strong></p></figcaption></figure>
3. Enter a meaningful **Name** (e.g., `deny-k8s-job`).
4. From the **Scope** list box, select the appropriate scope for the Permission Set (e.g., **User**).
5. In the **Applicable Tenants** field, select the applicable **Tenants** or choose **All Tenants**.
6. Click **Add Allow Policy** or **Add Deny Policy**, and configure the policy details:&#x20;
   * **Resource Type Regex:** Enter the resource type the policy will apply to. For example, `k8s/job` to target Kubernetes Jobs.
   * **API Name Regex:** Enter a regular expression that matches the API name for the resource. For example, `.*k8s/job.*` will match any API calls related to Kubernetes Jobs. This field defines which API operations are covered by the policy.
   * **HTTP Method:** Choose the HTTP method for which the policy applies. Options include `GET`, `POST`, `PUT`, `DELETE`, or `ALL` to apply to all methods. This field defines the HTTP methods that the policy will restrict.
7. Click **Save** to create the **Permission Set**.

## Assigning Users to a Permission Set

After creating a Permission Set, assign specific users to it:

1. In the **DuploCloud Portal**, navigate to **Administrator** → **Permissions**.
2.  Select the Permission Set from the **NAME** column. The Permission Set details page displays.\


    <figure><img src="../../.gitbook/assets/image (462).png" alt=""><figcaption><p>Adding users to the permission set</p></figcaption></figure>
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

<figure><img src="../../.gitbook/assets/image (463).png" alt=""><figcaption><p>An error message denying user access to a K8s Job</p></figcaption></figure>

&#x20;
