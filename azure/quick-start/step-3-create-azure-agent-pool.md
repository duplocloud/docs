# Step 3: Create Azure Agent Pool

{% hint style="info" %}
Make sure you have switched the Tenant drop down to the desired tenant i.e. dev01 in this case.
{% endhint %}

Navigate DevOps > Hosts > Azure Agent Pool.  Each agent pool will contain nodes backed by the virtual host machines.

You need to give the following minimum user inputs like below:

Id, Minimum , Maximum and Desired Capacity. Lets give input as 1 , since we are deploying a small sample application for the tutorial.

Instance Type: Select from the dropdown (4 CPU, 16GB)

![](<../../.gitbook/assets/image (42).png>)

The node pools should get registered with Kubernetes and should show in `Connected` status in the DuploCloud UI.
