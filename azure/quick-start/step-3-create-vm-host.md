# Step 3: Create VM Host

{% hint style="info" %}
Make sure you have switched the Tenant drop down to the desired tenant i.e. dev01 in this case.
{% endhint %}

Navigate DevOps > Hosts > Azure VM to create Azure Virtual Machine (VM).

You need to give the following inputs:

Name: host01

Instance Type: Select from the dropdown (4 CPU, 16GB)

Expand Advanced Option, Enter Username, and Password. Usernames must not include reserved words like admin, administrator, user, etc.

The host should get launched and soon get registered with Kubernetes and should show in `VM running` status in the DuploCloud UI as shown below

![Azure VM Screen](<../../.gitbook/assets/image (27) (1).png>)
