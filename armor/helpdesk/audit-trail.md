# Audit Trail

HelpDesk activity is captured in a pluggable audit log. This is a backend, ops-configured pipeline — there's no in-app screen for browsing audit records; instead, they land in whichever sink you configure and get reviewed there (e.g. an S3 bucket queried through Athena, CloudWatch, or wherever your log sink already ships to).

**What's captured** — every write request (POST/PUT/PATCH/DELETE) and every SignalR hub call, recording the method, path, status code, elapsed time, query string, action name, and a masked copy of the request payload, along with who made the call (effective email, authenticated email, workspace, admin flag, and any "on behalf of" identity for bot/Slack-driven actions). Auth failures and routing errors (401, 403, 404, 405) are captured too, even when they never reach an action — and if an action throws partway through, the event for it is still logged.

**Sensitive fields are masked automatically.** Any field whose name contains a keyword like `secret`, `key`, `password`, `token`, `credentials`, or similar is replaced with `***` in the logged payload — no manual annotation needed for the common cases.

**Configuring sinks** — a logger-based sink is always on and flows through the platform's existing logging configuration. Shipping audit records to cloud storage instead (or as well) is opt-in, configured under an `Audit` section in the service's configuration:

* `Audit:S3:Enabled`, `Audit:S3:BucketName`, `Audit:S3:Prefix`, `Audit:S3:Region`
* `Audit:AzureBlob:Enabled`, `Audit:AzureBlob:ConnectionString`, `Audit:AzureBlob:ContainerName`, `Audit:AzureBlob:Prefix`
* `Audit:Gcs:Enabled`, `Audit:Gcs:BucketName`, `Audit:Gcs:Prefix`

All three cloud sinks are disabled by default. For S3, records are written as newline-delimited JSON, batched and partitioned by date (`.../year=YYYY/month=MM/day=DD/...`) so they can be queried directly with Athena without any repair step. Enabling the S3 sink requires the service's AWS credentials to have `s3:PutObject` on the target bucket/prefix.

{% hint style="info" %}
This audit pipeline covers the AI Studio/HelpDesk API surface. It's a separate mechanism from the general DuploCloud infrastructure audit trail available elsewhere in the platform.
{% endhint %}
