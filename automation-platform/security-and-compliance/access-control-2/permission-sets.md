---
description: Configure Permission Sets in DuploCloud for granular access control
---

# Permission Sets

Permission Sets in DuploCloud provide fine-grained access control for users. They define which APIs/resource types a user can access within specific Tenants. Permission Sets can be assigned directly to users or bundled into Permission Groups for easier management.

A **Permission Set** is a collection of allow or deny policies applied to users. These policies define which APIs, resource types, and HTTP methods a user can access within specific Tenants. Permission Sets are evaluated by priority, with lower numbers overriding higher numbers. Permission Sets can be system-wide, assigned directly to users, or assigned to user groups.

A **Permission Group** is a bundle of users assigned one or more Permission Sets. Groups simplify administration by giving multiple users the same access rules and are ideal for managing permissions by team or role. Users inherit all permissions from the Permission Sets assigned to the group. Users can belong to multiple groups, and all permissions from their assigned groups are combined.

## Configuring Permission Sets in DuploCloud

1. In the DuploCloud Portal, navigate to **Administrator** → **Permissions**.
2. Select the **Sets** tab.&#x20;
3.  Click **Add**. The **Add Permission Set** pane displays. \


    <figure><img src="../../../.gitbook/assets/Screenshot (765).png" alt=""><figcaption><p><strong>Add Permission Set</strong> pane</p></figcaption></figure>
4. Complete the following fields:

<table data-header-hidden><thead><tr><th width="212.22216796875"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a meaningful name for the Permission Set (e.g., <code>deny-k8s-job</code>).</td></tr><tr><td><strong>Scope</strong></td><td>Select the appropriate scope for the Permission Set (e.g., <strong>User</strong> or <strong>System Wide</strong>).<br><strong>Note:</strong> Choosing <strong>System Wide</strong> creates a Permission Set that applies to all users. This can be used for default allow-all permissions or to enforce explicit deny rules across the platform.</td></tr><tr><td><strong>Priority</strong></td><td>Enter a numeric value; lower numbers take higher precedence. (Tip: start with higher numbers like 50 for flexibility.)</td></tr><tr><td><strong>Applicable Tenants</strong></td><td>Select the applicable Tenants or choose <strong>All Tenants</strong>.</td></tr><tr><td><strong>Allow or Deny Policy</strong></td><td><p>Click <strong>Add Allow Policy</strong> or <strong>Add Deny Policy</strong> and complete the following fields:   <br></p><ul><li><strong>Resource Type RegEx:</strong> Enter the resource type (e.g., <code>k8s/job</code>).</li><li><strong>API Name RegEx:</strong> Enter a regex matching the API (e.g., <code>.*k8s/job.*</code>).</li><li><strong>Method:</strong> Choose <strong>GET</strong>, <strong>POST</strong>, <strong>PUT</strong>, <strong>DELETE</strong>, or <strong>ALL</strong>.</li></ul></td></tr></tbody></table>

5. Click **Save** to create the Permission Set.

## Assigning Users to a Permission Set

After creating a Permission Set, assign specific users to it:

1. In the **DuploCloud Portal**, navigate to **Administrator** → **Permissions**.
2. Select the **Sets** tab.
3.  Select the Permission Set from the **NAME** column. The Permission Set details page displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/image (462).png" alt=""><figcaption><p>Adding users to the permission set</p></figcaption></figure></div>
4. Select the **Users** tab.
5. Select the users to whom the Permission Set should apply.
6. Click **Save**.

## Creating a User Group

User Groups allow you to assign multiple users the same set of permissions at once.

1. Navigate to **Administrator** → **Permissions**.
2. Select the **Groups** tab.
3.  Click **Add**. The **Add Permission Group** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (847).png" alt=""><figcaption><p><strong>Add Permission Group</strong> pane</p></figcaption></figure></div>
4. Complete the fields:

<table data-header-hidden><thead><tr><th width="169.5555419921875"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a descriptive name for the Permission Group.</td></tr><tr><td><strong>Users</strong></td><td>Select one or more users to include in the group.</td></tr><tr><td><strong>Permissions</strong></td><td><p>Click <strong>Add</strong> under Permissions. The <strong>Add Permissions</strong> pane displays:<br></p><ul><li><strong>Select one or more Permission Sets</strong> to assign to the group.</li><li><strong>Click Add</strong> to confirm the selection.</li></ul></td></tr></tbody></table>

5. Click **Add** to create the Permission Group.

{% hint style="info" %}
#### Notes on User Groups

* Users inherit all permissions from the assigned Permission Sets.
* Users can belong to multiple groups; all permissions are combined.
{% endhint %}

## Handling Conflicting Permissions

It is possible for a user to be assigned multiple Permission Sets that contain contradictory rules. DuploCloud resolves conflicts using the following logic:

* **Priority Evaluation:** Permission Sets are evaluated in ascending priority (lower numbers first).
* **First Match Wins:** The first matching policy (allow or deny) determines access.
* **Default Deny:** If no policy matches, access is denied by default (`400` error).

**Example:**

* `Permission Set A` (priority 5) denies `GetSecretData`
* `Permission Set B` (priority 10) allows `GetSecretData`
* **Result:** access is denied because `Permission Set A` has higher precedence.

**Best Practices:**

* Assign careful priority numbers to Permission Sets to ensure intended behavior.
* Use Permission Groups to simplify management, but check for overlapping sets with conflicting rules.

## Testing Permission Set or User Group Configuration

1. Log in as a user assigned to a Permission Set or a User Group.
2. Attempt actions governed by the assigned Permission Set(s).
3. Verify that access is granted or denied according to the rules.&#x20;
