---
description: Common problems with DAST and how to fix them.
---

# Troubleshooting and FAQ

## Error messages

| What you see | What it means | What to do |
| --- | --- | --- |
| **"Target URL must be an absolute http(s) URL."** | The Application URL has no scheme, or isn't `http` or `https`. | Enter the full URL, for example `https://app.example.com`. |
| **"An API definition (OpenAPI) URL is required for the 'api' scan type."** | You chose API without an API definition URL. In **Run scan**, the API option is unavailable for the same reason. | Add the OpenAPI or Swagger URL to the target. |
| **"Max duration must be between 1 and 240 minutes."** | The value is out of range. | Enter 1 to 240. |
| **"Repository must be 'organization/repository'"** or **"Select a GitHub scope to access the listed repositories."** | A repository isn't in `org/repo` form, or repositories are listed without a GitHub scope. | Fix the entry, or choose a GitHub scope. |
| **"The authentication scope must belong to an 'other' provider holding the app login."** or **"The source-control scope must be a GitHub scope."** | The wrong kind of scope was chosen. | Choose an **Other** scope for the login and a GitHub scope for the code. Other source-control providers aren't supported. |
| Scan fails: **"Docker daemon not reachable from the agent"** | The agent can't run the ZAP container. | Ask your administrator to check Docker for the agent. |
| Scan fails: **"cannot pull ghcr.io/zaproxy/zaproxy:stable and it is not present locally"** | The agent can't download the ZAP image. | Allow the agent to reach `ghcr.io`, or ask your administrator to pre-load the image. |
| Scan fails: **"auth scope … has no usable login"** or **"is set to authType=form but lacks username/password"** | The login is missing keys. The message lists the key names it found. | Add the missing keys (see [Set Up](set-up.md#add-an-application-login-optional)), or clear **Scan as a signed-in user** on the target. |
| Scan fails: **"auth scope … is not materialized"** | The login scope isn't attached to this workspace. | Attach the scope to the workspace and run the scan again. |
| **"ZAP did not finish within N min … raise it or narrow includePaths"** | The scan hit its time limit. | Raise **Max duration**, or narrow **Include paths**. |
| **"ZAP exited N without a report"** or **"ZAP finished but produced no report"** | ZAP failed. | Open the **Artifacts** tab and read the end of `zap.log`. Full and API scans aren't retried automatically. |
| **"The target has no GitHub scope/repositories — add them to the target and re-scan."** | Fixing needs a GitHub scope and repositories on the target. | Edit the target, add them, and run a new scan. |
| **"This scan has no provisioning ticket yet — wait for it to complete, then Fix."** | The scan's chat hasn't started yet. | Wait a moment and try again. |

## Other problems

| What you see | What it means | What to do |
| --- | --- | --- |
| A scan stays at **Ticket created**, or shows **Running…** in the history, and never moves on | The agent couldn't start work, usually because it can't reach its AI model (for example an expired key or a used-up usage limit). | Ask your administrator to check the agent's AI model settings, then run a new scan. |
| The scan can't reach the application, or finds almost nothing, when the URL uses `localhost` | ZAP runs in its own container next to the agent, where `localhost` isn't your computer. | Use an address the agent can reach, such as the machine's network IP address or a real host name. |
| Your login or GitHub scope isn't in the target's drop-down | The scope isn't attached to the current workspace. | Attach the scope to the workspace, then reopen the form. |
| The **Repositories** list is empty, or doesn't show your repository | The GitHub token can't list it. | Check the token's access, then click **Refresh**. You can also type `org/repo`. |
| Zero or very few findings | A single-page application may expose few URLs, or the scan is anonymous. This isn't a failure. | Add a login, an API definition, or include paths. Zero findings is a valid result. |
| Findings show ZAP's ratings and **Needs review** | ZAP has finished and the agent is still triaging. | Wait. The list updates by itself. |
| No **Fix** buttons | Fixing needs a GitHub scope and repositories on the target, the **Fix DAST findings via pull request** permission, and findings that aren't false positives. | Add what's missing, then run a new scan if you changed the target. |
| A banner of notes above the scan's tabs | The agent's notes about this scan, such as settings it couldn't apply or limits of a passive scan. | Read them. Fix the target's settings if needed, and run again. |
| An action is refused | You don't have the permission. | Ask an administrator. See [Permissions and Safety](permissions-and-safety.md). |

## FAQ

**Is a scan safe to run in production?** Only a Baseline scan, and even then exclude destructive paths. Don't run Full or API scans against production. See [Permissions and Safety](permissions-and-safety.md).

**Do I have to prove I own the application?** No. DAST doesn't check ownership, so it's up to you to scan only applications you own or have written permission to test.

**Which scan type should I start with?** Baseline. It only observes traffic.

**Do I need to link my code?** No. Without it you still get triaged findings, just no code locations or fix pull requests.

**Can I scan behind a login?** Yes, with an **Other** scope that holds a test account. Use a dedicated test account, never a real user's.

**Does the agent merge its fixes?** No. It opens a pull request for you to review.

**Can I get the raw ZAP report?** Yes, on the **Artifacts** tab: the HTML report, the JSON report and the log, as soon as ZAP writes them.

**Why does a finding have a different severity than in ZAP?** The agent rates severity for your application, taking into account exposure, whether authentication is needed, and compensating controls. Its reason is on the finding, and ZAP's original rating is shown under the new one.

**Does it work with GitLab or Bitbucket?** No, only GitHub.
