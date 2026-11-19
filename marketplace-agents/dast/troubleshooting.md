---
description: Common problems with DAST and how to fix them.
---

# Troubleshooting and FAQ

## Common problems

| What you see | What it means | What to do |
| --- | --- | --- |
| **"Target URL must be an absolute http(s) URL."** | The Application URL is missing the scheme or is not `http` or `https`. | Enter the full URL, for example `https://app.example.com`. |
| **"An API definition (OpenAPI) URL is required for the 'api' scan type."** | You chose API without an API definition URL. In Run scan the API option is disabled for the same reason. | Add the OpenAPI or Swagger URL to the target. |
| **"Max duration must be between 1 and 240 minutes."** | The value is out of range. | Enter 1 to 240. |
| **"Repository must be 'organization/repository'"** or **"Select a GitHub scope to access the listed repositories."** | A repository is not in `org/repo` form, or repositories are listed without a GitHub scope. | Fix the entry, or choose a GitHub scope. |
| **"The authentication scope must belong to an 'other' provider holding the app login."** or **"The source-control scope must be a GitHub scope."** | The wrong kind of scope was selected. | Pick an "other" scope for the login, and a GitHub scope for code. Other source-control providers are not supported. |
| **"No repositories visible to this token"** | The GitHub credential cannot list repositories. | Check the credential, then select **Refresh**. You can still type `org/repo`. |
| **Scan fails: "Docker daemon not reachable from the agent"** | The agent's host cannot run Docker. | Ask your administrator to fix Docker on the agent host. |
| **Scan fails: "cannot pull ghcr.io/zaproxy/zaproxy:stable and it is not present locally"** | The host cannot download the ZAP image. | Allow access to `ghcr.io` from the agent host, or ask your administrator to pre-load the image. |
| **Scan fails: "auth scope ... has no usable login"** or **"is set to authType=form but lacks username/password"** | The login scope is missing keys. The message lists the key names it found. | Add the missing keys (see [Set Up](set-up.md)), or turn off **Scan as a signed-in user** on the target. |
| **Scan fails: "auth scope ... is not materialized"** | The login scope is not attached to this workspace. | Attach the scope to the workspace and run again. |
| **"ZAP did not finish within N min ... raise it or narrow includePaths"** | The scan hit its time limit. | Raise Max duration, or narrow Include paths. |
| **"ZAP exited N without a report"** or **"ZAP finished but produced no report"** | ZAP failed. | Open the **Artifacts** tab and read the end of the ZAP log. Full and API scans are not retried automatically. |
| **Zero or very few findings** | A single-page application may expose few URLs, or the scan is anonymous. The log shows "Job spider ... warning" lines. This is not a failure. | Add a login, an API definition, or include paths. Zero findings is a valid result. |
| **Findings show "Triaging..."** | ZAP finished and the agent is still reviewing. ZAP's own ratings are shown meanwhile. | Wait. The list updates by itself. |
| **No Fix buttons, or "The target has no GitHub scope/repositories — add them to the target and re-scan."** | Fix needs a GitHub scope and repositories on the target, and findings that are not false positives. | Edit the target, add them, and run a new scan. |
| **"This scan has no provisioning ticket yet — wait for it to complete, then Fix."** | The scan has not started its chat yet. | Wait a moment and try again. |
| **A warning banner on the scan** | A setting was not applied, with a one-line reason. | Read it, fix the setting on the target, and run again. |
| **A duplicate scan name error** | Scan names must be unique. | Change the name. |
| **Buttons refused, or "Access denied"** | You lack the permission. | Ask an administrator (see [Permissions and Safety](permissions-and-safety.md)). |

<!-- VERIFY: messages are copied from the backend validation and the scan scripts; confirm the exact wording users see in QA. -->
<!-- VERIFY: the duplicate scan name message text and the "Access denied" wording come from the UI comments and platform behaviour, not from a message in this repo. -->

## FAQ

**Is a scan safe to run in production?** Only Baseline, and even then you should exclude destructive paths. Do not run Full or API scans in production. See [Permissions and Safety](permissions-and-safety.md).

**Do I have to prove I own the application?** Not today in this draft. <!-- VERIFY: the review said active scans require proof of domain ownership; the repo has no such check. Rewrite once confirmed. -->

**Which scan type should I start with?** Baseline. It only observes traffic.

**Do I need to link my code?** No. Without it you still get triaged findings, but no code locations or fix pull requests.

**Can I scan behind a login?** Yes, with an "other" scope that holds a test account. Use a dedicated account, never a real user.

**Does the agent merge its fixes?** No. It opens a pull request for you to review.

**Can I get the raw ZAP report?** Yes, on the **Artifacts** tab: HTML report, JSON report and log. They are available as soon as ZAP writes them.

**Why did a finding get a different severity than in ZAP?** The agent adjusts severity for your application (exposure, authentication needed, compensating controls) and gives its reason on the finding.

**Does it work with GitLab or Bitbucket?** No, GitHub only.

**Is it free?** <!-- VERIFY: pricing is not in the repo. -->

<!-- VERIFY: FAQ list is a first guess. The owner to add the questions customers actually ask. -->
