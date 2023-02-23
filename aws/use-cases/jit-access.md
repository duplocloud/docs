# JIT Access

DuploCloud users can obtain Just-In-Time (JIT) access to AWS Console. This access is restricted to resources the user has access to in the DuploCloud portal. DuploCloud admin users have admin-level access in AWS Console. This access is generated in real time and revoked by default in 1 hour.

## Access through UI

AWS JIT access is possible directly from the DuploCloud UI. Go to your user profile and click _Get JIT AWS Access_ to generate the JIT access keys.  This page also links directly to the AWS Console.

<figure><img src="../../.gitbook/assets/Screen Shot 2022-08-22 at 11.05.10 PM.png" alt=""><figcaption><p>DuploCloud User Profile page</p></figcaption></figure>

## Access through command line

Download the latest ZIP from [https://github.com/duplocloud/duplo-aws-jit/releases](https://github.com/duplocloud/duplo-aws-jit/releases) based on your Operating System. Extract the ZIP, and add **duplo-aws-credential-process** to your $PATH environment variable.

**duplo-aws-credential-process** needs to obtain an AWS JIT session using a [DuploCloud API Token](https://docs.duplocloud.com/docs/administrator-tools/access-control/api-tokens). This token can either be specified as part of your local AWS config or could be obtained interactively using your DuploCloud portal session. Both options are specified below.

### Authentication

#### Obtain credentials using an API Token

First, [Obtain a DuploCloud API Token](https://docs.duplocloud.com/docs/administrator-tools/access-control/api-tokens).&#x20;

Second, Edit AWS Config file **\~/.aws/config** and add the below content

```
[profile ENV_NAME]
region=us-west-2
credential_process=duplo-aws-credential-process --admin --host https://ENV_NAME.duplocloud.net --token <DUPLO_TOKEN>
```

#### Obtain credentials interactively

Replace `--token <DUPLO_TOKEN>` in the API Token example with `--interactive`.

When you first make the AWS call, you will be prompted to authorize through your DuploCloud portal as below. Upon successful authorization, A just-in-time token is given which is valid for 1 hour. When the token expires, you will be prompted to re-authorize the request.

<figure><img src="../../.gitbook/assets/image (18) (1).png" alt="A prompt reads &#x22;The duplo-aws-credential-process application on your computer wants to access your Duplo credentials.&#x22; The options are a green button on the right for Authorize and a Red button on the left for Cancel."><figcaption><p>Local Access Requested prompt</p></figcaption></figure>

### Access AWS

**Access AWS from the CLI**

Example:

`AWS_PROFILE=ENV_NAME aws ec2 describe-instances`

As long as you use the AWS\_PROFILE matching the profile name set in the Authentication section above, AWS CLI obtains the access credentials it requires.

**Obtain the AWS Console Url**

If you want to obtain a link to the AWS Console, you can run the following, which will copy the Console URL to your clipboard which you can use in any browser window:

API Token:

```
duplo-aws-credential-process --admin --host "https://ENV_NAME.duplocloud.net" --token <DUPLO_TOKEN> | jq -r .ConsoleUrl | pbcopy
```

Interactive:

```
duplo-aws-credential-process --admin --host "https://ENV_NAME.duplocloud.net" --interactive | jq -r .ConsoleUrl | pbcopy
```

Or if you want to get really fancy, add this to your .zshrc:

```
function jitnow() {
  duplo-aws-credential-process --admin --no-cache --host "https://$1.duplocloud.net" --interactive | jq -r .ConsoleUrl | pbcopy
}
```

usage: `jitnow portalname`

``

### Other option flags

#### **Access as ADMIN role**

All of the examples above are written for admin access, passing the `--admin` flag.

#### **Access as USER role**

If you are getting JIT access as a User role and not Admin, make sure you you replace `--admin` above with `--tenant THE-TENANT-YOU-ARE-USING`

**No credential caching**

If you are getting errors retrieving credentials, try running the command with `--no-cache` added.\
_<mark style="color:blue;"></mark>_

### Configure session timeout

By default, JIT sessions expire after one hour. This can be configured in the admin section for a tenant. On the Admin->Tenants page, select a tenant and go to the _Settings_ tab. Then you can add the setting to customize the timeout. The timeout is configured in seconds.\
![](<../../.gitbook/assets/image (2) (1) (3).png>)

If you are increasing the session timeout beyond the AWS default of 1 hour, you will also need to update the maximum session duration value for the IAM role assigned to your DuploCloud tenant. You can get access to AWS Console as an admin using the instructions above. Then you can goto IAM->Roles and modify the value for that tenant.&#x20;

For example: If your tenant is named "dev01", and you need to set the timeout to 2 hours. Find the IAM role called "duploservices-dev01" and modify the value for "Maximum session duration" to 2 hours.

