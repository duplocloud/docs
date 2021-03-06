# JIT Access

DuploCloud allows Just-In-Time (JIT) to AWS for a user. This access is restricted to the resources in scope of access to the user in the DuploCloud portal. For admin users, JIT access at an Admin level is also available. This access is generated real time and revoked in 1 hour.

## Access through UI

AWS JIT access is possible directly from the DuploCloud UI. Simply goto your user profile and click to generate the JIT access keys.  This page also links directly to the AWS Console

![](<../../.gitbook/assets/Screen Shot 2022-06-29 at 11.58.46 PM.png>)

## Access through command line

Download the latest ZIP from [https://github.com/duplocloud/duplo-aws-jit/releases](https://github.com/duplocloud/duplo-aws-jit/releases) based on your Operating System. Extract the ZIP, and add **duplo-aws-credential-process** to your $PATH environment variable.

duplo-aws-credential-process needs to obtain an AWS JIT session using a DuploCloud [API token](https://docs.duplocloud.com/docs/administrators/access-control/api-tokens). This token can either be specified by you as part of your local AWS config or could obtained interactively using your DuploCloud portal session. Both options are specified below

### Obtain credentials interactively

Edit AWS Config file **\~/.aws/config** and add the below content

```
[profile ENV_NAME]
region=us-west-2
credential_process=duplo-aws-credential-process --admin --host https://ENV_NAME.duplocloud.net --interactive
```

Replace the ENV\_NAME with your account name. You can make AWS API calls using this profile:

\
**`AWS_PROFILE=ENV_NAME aws ec2 describe-instances`**

_<mark style="color:blue;"></mark>_\
_<mark style="color:blue;"></mark>_When you first make the AWS call, you will be prompted to authorize through your DuploCloud portal as below. Upon successful authorization, A just-in-time token is given which is valid for 1 hour. When ever the token expires, you will be prompted to re-authorize the request.

![](<../../.gitbook/assets/image (18) (1) (1).png>)

### Obtain credentials using an API Key

Edit AWS Config file **\~/.aws/config** and add the below content

```
[profile ENV_NAME]
region=us-west-2
credential_process=duplo-aws-credential-process --admin --host https://ENV_NAME.duplocloud.net --token <DUPLO_TOKEN>
```

Obtain the DUPLO\_TOKEN using [this](https://docs.duplocloud.com/docs/administrators/access-control/api-tokens) process.&#x20;
