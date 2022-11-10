# JIT Access

DuploCloud allows Just-In-Time (JIT) to AWS for a user. This access is restricted to the resources in scope of access to the user in the DuploCloud portal. For admin users, JIT access at an Admin level is also available. This access is generated real time and revoked in 1 hour.

## Access through UI

AWS JIT access is possible directly from the DuploCloud UI. Simply goto your user profile and click to generate the JIT access keys.  This page also links directly to the AWS Console

<figure><img src="../../.gitbook/assets/Screen Shot 2022-08-22 at 11.05.10 PM.png" alt=""><figcaption></figcaption></figure>

## Access through command line

Download the latest ZIP from [https://github.com/duplocloud/duplo-aws-jit/releases](https://github.com/duplocloud/duplo-aws-jit/releases) based on your Operating System. Extract the ZIP, and add **duplo-aws-credential-process** to your $PATH environment variable.

duplo-aws-credential-process needs to obtain an AWS JIT session using a DuploCloud [API token](https://docs.duplocloud.com/docs/administrators/access-control/api-tokens). This token can either be specified by you as part of your local AWS config or could obtained interactively using your DuploCloud portal session. Both options are specified below

### Obtain credentials using an API Token

First, obtain the DUPLO\_TOKEN using [this](https://docs.duplocloud.com/docs/administrators/access-control/api-tokens) process.&#x20;

Edit AWS Config file **\~/.aws/config** and add the below content

```
[profile ENV_NAME]
region=us-west-2
credential_process=duplo-aws-credential-process --admin --host https://ENV_NAME.duplocloud.net --token <DUPLO_TOKEN>
```

**Test you access**

`AWS_PROFILE=ENV_NAME aws ec2 describe-instances`

**Obtain the AWS Console Url**

If you want to obtain a link to the AWS Console, you can run the following, which will copy the Console Url to your clipboard which you can use in any browser window:

```
duplo-aws-credential-process --admin --host "https://ENV_NAME.duplocloud.net" --token <DUPLO_TOKEN> | jq -r .ConsoleUrl | pbcopy
```

### Obtain credentials interactively

Edit AWS Config file (example:`~/.aws/config)` **** and add the below content

#### **Access as ADMIN role**

```
[profile ENV_NAME]
region=us-west-2
credential_process=duplo-aws-credential-process --admin --host https://ENV_NAME.duplocloud.net --interactive
```

#### **Access as USER role**

If you are getting JIT access as a User role and not Admin, make sure you you replace `--admin` above with `--tenant THE-TENANT-YOU-ARE-USING`

Replace the `ENV_NAME` with your account name. You can make AWS API calls using this profile:

Add the appropriate value of `REGION` (for example: `us-west-2`)

#### **Test your access**

`AWS_PROFILE=ENV_NAME aws ec2 describe-instances`

_<mark style="color:blue;"></mark>_\
_<mark style="color:blue;"></mark>_When you first make the AWS call, you will be prompted to authorize through your DuploCloud portal as below. Upon successful authorization, A just-in-time token is given which is valid for 1 hour. When ever the token expires, you will be prompted to re-authorize the request.

![](<../../.gitbook/assets/image (18) (1).png>)

### Configure session timeout

By default, JIT sessions expire after one hour. This can be configured in the admin section for a tenant. On the Admin->Tenants page, select a tenant and go to the _Settings_ tab. Then you can add the setting to customize the timeout. The timeout is configured in seconds.\
![](<../../.gitbook/assets/image (2).png>)

If you are increasing the session timeout beyond the AWS default of 1 hour, you will also need to update the maximum session duration value for the IAM role assigned to your DuploCloud tenant. You can get access to AWS Console as an admin using the instructions above. Then you can goto IAM->Roles and modify the value for that tenant.&#x20;

For example: If your tenant is named "dev01", and you need to set the timeout to 2 hours. Find the IAM role called "duploservices-dev01" and modify the value for "Maximum session duration" to 2 hours.

