---
description: Use just-in-time (JIT) to access the console in Azure
---

# JIT Access

DuploCloud users can obtain Just-In-Time (JIT) access to the Azure Console using `duplo-jit`. This access is restricted to resources that the user has access to in the DuploCloud portal. With JIT access, DuploCloud administrators have admin-level access within the Azure Console and the access is generated in real-time and revoked, by default, in one hour.

## Access the Azure Console using the CLI and `duplo-jit`

Obtain access through the command line interface (CLI) with `duplo-jit`. `duplo-jit` must obtain an Azure JIT session using a [DuploCloud API Token](https://docs.duplocloud.com/docs/administrator-tools/access-control/api-tokens). This token can be specified either as part of your local Azure configuration or can be obtained interactively, using your DuploCloud portal session.

### Install with Homebrew

Run the following command:&#x20;

```
brew install duplocloud/tap/duplo-jit
```

### Install from GitHub Releases

1. Download the latest **.zip** archive from [https://github.com/duplocloud/duplo-jit/releases](https://github.com/duplocloud/duplo-jit/releases) for your operating system.
2. Extract the archive listed in the table below based on the operating system and processor you are running.&#x20;
3. Add the path to `duplo-jit` to your `$PATH` environment variable.&#x20;

| Processor/Operating System  | Archive                |
| --------------------------- | ---------------------- |
| Intel macOS                 | **darwin\_amd64.zip**  |
| M1 macOS                    | **darwin\_arm64.zip**  |
| Windows                     | **windows\_amd64.zip** |

### Obtaining credentials&#x20;

Obtain credentials using a DuploCloud API Token or interactively.

#### Using an API Token

1. [Obtain a DuploCloud API Token](https://docs.duplocloud.com/docs/administrator-tools/access-control/api-tokens).
2. Edit the Azure Config file (**\~/.azure/config**) and add the following profile, as shown in the code snippet below:

```
[profile <ENV_NAME>]
region=us-west-2
credential_process=duplo-jit az --admin --host https://<ENV_NAME>.duplocloud.net --token <DUPLO_TOKEN>
```

#### Obtain credentials interactively

To obtain credentials interactively, rather than with a token, replace `--token <DUPLO_TOKEN>` in the argument above with `--interactive`.

When you make the first AWS call, you are prompted to grant authorization through the DuploCloud portal, as shown below. Click **Authorize** if you consent.

<figure><img src="../../.gitbook/assets/image (18) (1).png" alt="A prompt reads &#x22;The duplo-aws-credential-process application on your computer wants to access your Duplo credentials.&#x22; The options are a green button on the right for Authorize and a Red button on the left for Cancel."><figcaption><p><strong>Local Access Requested</strong> prompt</p></figcaption></figure>

Upon successful authorization, A Just-In-Time token is provided, which is valid for one hour. When the token expires, you are prompted to re-authorize the request.

## Accessing the Azure Console using the CLI

Obtain access to the Azure console using the Command Line Interface (CLI).

### **Accessing the Azure Console**

As long as you use one `AZURE_PROFILE` that matches the profile name you set [in the section above](jit-access.md#obtaining-credentials), the Azure CLI obtains the required access credentials.

For example:

`AZURE_PROFILE=<ENV_NAME> az vm list`

### **Obtaining a link to the Azure Console URL**

To obtain a link to the Azure Console, run one of the following commands, which copies the Console URL to your clipboard that you can use in any browser.

All of these examples assume Administrator role access, passing the `--admin` flag. If you are obtaining JIT access for a User role (not Administrator), ensure that you replace the `--admin` argument in the following code snippets with `--tenant <YOUR_TENANT>`, for example `--tenant dev01`.  Tenants are lower-case at the CLI.

{% hint style="info" %}
If you are receiving errors when attempting to retrieve credentials, try running the command with the `--no-cache` argument.
{% endhint %}

#### Using an API Token

```
duplo-jit az --admin --host "https://<ENV_NAME>.duplocloud.net" --token <DUPLO_TOKEN> | jq -r .ConsoleUrl | pbcopy
```

#### Obtain a link interactively

```
duplo-jit az --admin --host "https://<ENV_NAME>.duplocloud.net" --interactive | jq -r .ConsoleUrl | pbcopy
```

#### Obtain a link interactively in PowerShell

```
duplo-jit az --admin --host "https://<ENV_NAME>.duplocloud.net" --interactive | ConvertFrom-Json | Select-Object -ExpandProperty ConsoleUrl | Set-Clipboard
```

#### Obtain a link by configuring your `zsh` shell

Add the following to your `.zshrc` file:

```
function jitnow() {
  duplo-jit az --admin --no-cache --host "https://$1.duplocloud.net" --interactive | jq -r .ConsoleUrl | pbcopy
}
```

{% hint style="info" %}
usage is `jitnow <ENV_NAME>`
{% endhint %}
