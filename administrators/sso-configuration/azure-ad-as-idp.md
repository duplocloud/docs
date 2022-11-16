# Azure AD as IdP

This section describes the steps to configure SSO for DuploCloud using Azure AD as IDP.&#x20;

## Configuration Steps

1\.     App Registration

2\.    Secret Creation

3\.    Assign API Permissions



## Step1: App Registration

As AD Administrator, login to your Azure AD Portal.&#x20;

1. Browse to _Manage->App Registrations->New registration_

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>App Registration 1</p></figcaption></figure>

__

1. Set the name of application, example: duplo-app1
2. In Supported account types: Select _“Accounts in any organizational directory (Any Azure AD directory - Multitenant)”_
3. In Redirect URI (optional): Select Web and add DuploCloud URL as below. Make sure to replace company with your company's DuploCloud deployment

[https://company.duplocloud.net/app/signin-microsofturl](https://companyx.duplocloud.net/app/signin-microsofturl)

1. Click on Register.
2. Note down the Application (Client) ID. example: _8a6acf76-555e-4782-a8a4-abcd283d889d_

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

## Step2: Secret Creation

1\. Click on Manage: Certification & Secrets.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

2\. In the Client Secret Tab, click on ‘New Client Secret’

<figure><img src="../../.gitbook/assets/Screen Shot 2022-11-15 at 6.52.29 PM.png" alt=""><figcaption></figcaption></figure>

3\. In Add a client Secret window, enter ‘Description’ and select 12 months for ‘Expires’ duration.

4\. Note down the ‘Value’ shown in the client secrets tab. example: hFFC8Q\~z.bHooBGcwftnh2LRgp53M62XJdLIrXxyz



<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>



## Step3: Assign API Permissions

1. Click on Manage: Add Permissions

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

2\. Select Microsoft Graph & Delegated Permissions



<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

3\. Select: User.Read(if not present), openid, email and profile. Click on Add permissions

4\. Click on the Grant admin consent for Default Directory and select “Yes”.



<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

## Setup Complete!

Give details of Application ID and Client Secret to DuploCloud to integrate Login Authentication with your Azure AD.
