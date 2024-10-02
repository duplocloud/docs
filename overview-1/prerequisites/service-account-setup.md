# Service Account Setup

For each GCP project that is to be onboarded, we need to create a service account and a key.&#x20;

1. Disable restriction on Service Account Key Setup. Login to GCP console and make sure that the desired project is selected in the GCP project drop down at the top. Search for IAM and admin and on the left hand side select "IAM and Admin" and under that select "Organization Policies". Then on the right hand side select the filter and search for "iam.disableServiceAccountKeyCreation". Then click the 3 dots and select edit policy. Then add a Rule at the bottom turn off enablement

<img src="../../.gitbook/assets/image (434).png" alt="" data-size="original">" ![](<../../.gitbook/assets/image (435).png>)

2. Next we create a service account and key
