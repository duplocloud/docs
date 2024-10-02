# Service Account Setup

For each GCP project that is to be onboarded, we need to create a service account and a key.&#x20;

1. Disable restriction on Service Account Key Setup. Login to GCP console and make sure that the desired project is selected in the GCP project drop down at the top. Search for IAM and admin and on the left hand side select "IAM and Admin" and under that select "Organization Policies". Then on the right hand side select the filter and search for "iam.disableServiceAccountKeyCreation". Then click the 3 dots and select edit policy. Then add a Rule at the bottom turn off enablement

<img src="../../.gitbook/assets/image (434).png" alt="" data-size="original">" ![](<../../.gitbook/assets/image (435).png>)

2. Next we create a service account by clicking on Service Accounts menu on the left Nav bar under IAM and Admin. Give the account "owner" permission to the project

<div align="center">

<figure><img src="../../.gitbook/assets/image (436).png" alt=""><figcaption></figcaption></figure>

</div>

3. Click in the service account and create a new key of type json and download the json file and name it say "my-gcp-project-sa-key.json". Open a terminal window in your computer and navigate to the folder where you downloaded the file and run this command "jq -r .private\_key < my-gcp-project-sa-key.json| pbcopy" This will copy the key contents in your clip board. You can check by pasting it in a text editor.&#x20;
4. Now we need to add these keys to DuploCloud portal. Login to your duploCloud portal and navigate to Administrator --> CloudCredentials. Paste the key from clip board to private key box; give a friendly display name typically you can keep it same as the project; Get the project ID and Service Account Email from the json key file downloaded above and submit the form.\
   &#x20;&#x20;

<figure><img src="../../.gitbook/assets/image (437).png" alt=""><figcaption></figcaption></figure>
