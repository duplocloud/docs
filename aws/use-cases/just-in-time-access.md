# Just-In-Time Access

## Access through UI

AWS JIT access is possible directly from the DuploCloud UI. Simply goto your user profile and click to generate the JIT access keys.  This page also links directly to the AWS Console

![](<../../.gitbook/assets/Screen Shot 2022-06-29 at 11.58.46 PM.png>)

## Access through command line

Download the latest ZIP from [https://github.com/duplocloud/duplo-aws-jit/releases](https://github.com/duplocloud/duplo-aws-jit/releases) based on your Operating System.\
\
Extract the ZIP, and add **duplo-aws-credential-process** to your $PATH environment variable.\
\
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

![](<../../.gitbook/assets/image (18).png>)
