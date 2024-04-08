# GCP FAQ

### My Kubernetes service was “pending” for several minutes waiting to start a new pod. After that, it was able to start and stop pods quickly. What happened?

DuploCloud typically runs Kubernetes services in GCP on GKE in Autopilot mode. Autopilot dynamically provisions nodes as needed to run your pods. This can add a couple of minutes to pod start time. You may see warnings from Kubernetes about being unable to place pods while autopilot hosts are starting, but they’ll clear once the hosts are available.

### One or more of my containers are showing in a pending state, how can I debug? <a href="#id-7-toc-title" id="id-7-toc-title"></a>

[Click here for the details](../aws-user-guide/aws-faq.md#7-toc-title)

### How do I grant a user access to only one Tenant in my GCP project?

To give a user access to a specific Tenant, navigate the Users page. For a new user, click Add and enter the user's information. From the Role list box, select User. When the user role is selected, the Tenant list box displays. In the Tenant list box, select the Tenant(s) you would like to give the user access to. Click Submit. For an established user, navigate to the Users page and select the name of the user whose access you would like to update. From the Actions menu, click Update. From the Role list, select User, and from the Tenant list box, select the Tenant(s) to which you want to give them access. Click Submit.&#x20;

### How do I create a Google Managed certificate for use with DuploCloud?&#x20;

To create a Google Managed certificate for use with DuploCloud, complete the steps in the table using the listed commands or the Google Cloud Console.&#x20;

<table><thead><tr><th width="83">Step</th><th width="303">Task</th><th>Command or Actions</th></tr></thead><tbody><tr><td>1</td><td><strong>Ensure that Google Cloud is installed</strong></td><td><code>gcloud</code></td></tr><tr><td>2</td><td><strong>Open Google Cloud Console</strong></td><td><a href="https://console.cloud.google.com/">https://console.cloud.google.com/</a></td></tr><tr><td>3</td><td><strong>Select the correct project</strong></td><td><code>gcloud config set project </code><em><strong><code>YOUR_PROJECT_ID</code></strong></em></td></tr><tr><td>4</td><td><strong>Check to see if an DNS authorization exists for your domain</strong></td><td><code>gcloud certificate-manager dns-authorizations list</code></td></tr><tr><td>5</td><td><strong>Create a new DNS authorization</strong> <strong>(if needed)</strong></td><td><code>gcloud beta certificate-manager dns-authorizations create </code><em><strong><code>AUTHORIZATION_NAME</code></strong></em><code>--domain=</code><em><strong><code>YOUR_DOMAIN_NAME</code></strong></em></td></tr><tr><td>6</td><td><strong>Verify that the authorization was created</strong></td><td><code>gcloud certificate-manager dns-authorizations describe </code><em><strong><code>AUTHORIZATION_NAME</code></strong></em></td></tr><tr><td>7</td><td><strong>Create  DNS record</strong></td><td><p></p><ul><li>Navigate to: <a href="https://console.cloud.google.com/net-services/dns/zones">https://console.cloud.google.com/net-services/dns/zones</a></li><li>Select your managed zone</li><li>Click <strong>Add record set</strong></li><li>Enter the details for the DNS record, including <strong>name</strong>, <strong>type</strong>, and <strong>data</strong></li><li>Click <strong>Create</strong></li></ul></td></tr><tr><td>8</td><td><strong>Create a new cert</strong></td><td><code>gcloud certificate-manager certificates create </code><em><strong><code>CERTIFICATE_NAME</code></strong></em><code> --domains=*</code><em><strong><code>YOUR_DOMAIN_NAME</code></strong></em><code> --dns-authorizations=</code><em><strong><code>AUTHORIZATION_NAME</code></strong></em></td></tr><tr><td>9</td><td><strong>Check the cert status</strong></td><td>gcloud certificate-manager certificates describe <em><strong><code>CERTIFICATE_NAME</code></strong></em></td></tr></tbody></table>

