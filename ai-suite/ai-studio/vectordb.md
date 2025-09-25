# VectorDB

In the DuploCloud AI Suite, the Vector Database (VectorDB) enables you to upload documents, such as architecture diagrams, runbooks, internal wikis, or API references, that you want the AI Agent to use for context during conversations. These documents are transformed into high-dimensional vector representations, which allow the system to retrieve the most relevant content when the Agent processes your queries. This enhanced context allows the Agent to better understand your cloud environment, use your terminology, and align with your organization’s best practices.

DuploCloud supports two types of VectorDBs:

### **Managed VectorDBs**

DuploCloud deploys and manages VectorDBs directly within your Kubernetes environment, handling setup, environment variables, and connectivity for seamless integration. Supported engines include:

* **Chroma:** Lightweight, fast, ideal for local AI workloads.
* **MilvusDB:** Scalable for high-performance vector search at large scale.

Use managed VectorDBs if you want to keep all components within your cloud account, prefer zero setup, or don’t have an external VectorDB provider.

### **Third-Party VectorDBs**

These are externally hosted vector databases like Pinecone or PostgreSQL that DuploCloud connects to but does not manage or deploy.

Choose third-party VectorDBs if you already use an external provider or need to integrate with specialized vector DB services outside your Kubernetes cluster.

## Integrating VectorDBs with DuploCloud&#x20;

The first step for working with VectorDBs in DuploCloud is to integrate a VectorDB with the DuploCloud AI Suite. This allows the platform to store and retrieve vectorized content.

### Prerequisites

* You must have access to the AI Suite feature in the DuploCloud Portal.
* For third-party VectorDBs (e.g., Pinecone), make sure you have your API endpoint and any necessary authentication information.
* For managed VectorDBs (e.g., Chroma, MilvusDB), ensure your Kubernetes environment is ready to deploy services.

### Integrating Third-Party VectorDBs

To integrate a third-party vector database, such as Pinecone:

1. In the DuploCloud Platform, navigate to **AI Suite** → **Studio** → **Vector DBs**.
2. Click **Add**. The **Add Vector Database** pane displays.

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (474).png" alt=""><figcaption><p>The <strong>Add Vector Database</strong> pane</p></figcaption></figure></div>

3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="165.11114501953125"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a friendly name for the VectorDB.</td></tr><tr><td><strong>Vector DB Type</strong></td><td>Select <strong>pinecone</strong> for a third-party VectorDB.</td></tr><tr><td><strong>API Endpoint</strong></td><td>Enter the endpoint URL for your Pinecone instance.</td></tr><tr><td><strong>Metadata</strong></td><td>Optionally, enter key-value pairs to organize or filter this VectorDB later.</td></tr></tbody></table>

4. Click **Submit** to save the VectorDB. Your third-party VectorDB is ready to use immediately.

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (475).png" alt=""><figcaption><p><strong>Vector DBs</strong> page in the DuploCloud <strong>AI Suite Studio</strong></p></figcaption></figure></div>

### Integrating Managed VectorDBs

To integrate a DuploCloud-managed VectorDB (Chroma or MilvusDB), add and then deploy the database in the DuploCloud Platform.

#### Adding a Managed VectorDB&#x20;

1. In the DuploCloud Platform, navigate to **AI Suite** → **Studio** → **VectorDBs**.
2.  Click **Add**. The **Add Vector Database** pane displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (476).png" alt=""><figcaption><p>The <strong>Add Vector Database</strong> pane in the DuploCloud Portal</p></figcaption></figure></div>
3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="189.1112060546875"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a friendly name for the Vector DB.</td></tr><tr><td><strong>Vector DB Type</strong></td><td>Select your Vector DB type, (e.g., <strong>chroma</strong> or <strong>milvusdb)</strong>.</td></tr><tr><td><strong>Deployment Environment Variables</strong></td><td>Optionally, add custom environment variables (e.g., API keys, flags).</td></tr><tr><td><strong>Metadata</strong></td><td>Optionally, enter key-value pairs for organizing or tagging the VectorDB.</td></tr></tbody></table>

4. Click **Submit** to save the VectorDB.

{% hint style="info" %}
**Note**: Adding a Managed Vector DB within DuploCloud saves the configuration, but does not deploy the database. Deployment is required before you can upload or ingest files.
{% endhint %}

#### Deploying a Managed VectorDB

After adding a managed VectorDB, deploy it to make it active and usable.

1. Navigate to **AI Suite** → **Studio** → **Vector DBs**.
2. Select the VectorDB from the **NAME** column.
3. Select the **Deployment** tab, and click **Deploy**. The **Deploy** pane displays.

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (478).png" alt="" width="424"><figcaption><p>The <strong>Deploy</strong> pane for the <strong>duplo-managed-db</strong> Vector DB</p></figcaption></figure></div>

4. Review or complete the deployment fields:

<table data-header-hidden><thead><tr><th width="226.4444580078125"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Auto-filled with the VectorDB name; can be customized if desired.</td></tr><tr><td><strong>Docker Image</strong></td><td>Auto-filled for managed VectorDBs. For third-party VectorDBs, confirm or provide the correct image if applicable.</td></tr><tr><td><strong>Deployment Environment Variables</strong></td><td>Define any environment variables required for your VectorDB.</td></tr><tr><td><strong>Advanced Options</strong></td><td>Optional settings such as replicas, service name, network, volumes, and load balancer listeners.</td></tr></tbody></table>

5. Choose either:
   * **Quick Deploy** to deploy with default settings immediately.
   * **Advanced** to customize deployment options before deploying.
6. If using **Advanced Deploy**, click **Next** to navigate through additional configuration screens, then click **Create** to start deployment. For **Quick Deploy**, click **Quick Deploy**.
7. Monitor the deployment status; it usually takes 4 to 5 minutes. Once complete, the status on the **Deployment** tab will show **Running**.

<figure><img src="../../.gitbook/assets/Screenshot (479).png" alt=""><figcaption><p><strong>Deployment</strong> tab for the VectorDB with status <strong>Running</strong></p></figcaption></figure>

## Uploading Files

Upload your source documents or data files to your AWS S3 storage to make your files available for processing and ingestion into the VectorDB.

1. In the DuploCloud portal, go to **AI Suite** → **Studio** → **Vector DBs**.
2. Select the VectorDB you want to upload files to from the **NAME** column.
3. Select the **Uploaded Files** tab.
4.  Click **Browse**. This will open your AWS S3 console where you can select the files you want to upload.\


    <figure><img src="../../.gitbook/assets/Screenshot (482) (1).png" alt=""><figcaption><p>The AWS S3 Console </p></figcaption></figure>
5. Select the files to upload (**Click Upload Files** → **Add File**, select your file(s), and click **Open**).
6. Return to the DuploCloud **Uploaded Files** tab, and click **Sync** to update the VectorDB’s **Uploaded Files** list. The uploaded files are displayed on the **Uploaded Files** tab.

<figure><img src="../../.gitbook/assets/Screenshot (483).png" alt=""><figcaption><p>The <strong>Uploaded Files</strong> tab in the DuploCloud Platform</p></figcaption></figure>

## Ingesting Files

Ingesting transforms your uploaded files into vector representations.&#x20;

1. In the DuploCloud portal, go to **AI Suite** → **Studio** → **Vector DBs**.
2. Select the **Uploaded Files** tab.
3. Click the checkbox(s) to select one or more files you want to ingest.
4.  Click **Ingest**. The **Trigger Build** pane displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (485).png" alt="" width="420"><figcaption><p>The <strong>Trigger Build</strong> pane</p></figcaption></figure></div>
5. Configure the fields as needed:
   * **Review the Docker Image:** This field is prepopulated with the container used for ingestion. You usually do not need to change it unless you're using a custom image.
   * **Timeout:** Enter the maximum duration (in minutes) for the ingestion job.&#x20;
   * **Custom Meta Data (Optional):** Use key-value pairs to customize how the ingestion job processes your data. Common options include:
     * `chunk_size`: Size of each text chunk in characters (e.g., `1000`).
     * `chunk-overlap`: Number of overlapping characters between chunks (e.g., `100`).
6.  Click **Submit** to trigger the ingestion job. Monitor the ingestion status on the **Ingested Jobs** tab.\


    <figure><img src="../../.gitbook/assets/Screenshot (489).png" alt=""><figcaption><p><strong>Ingested Jobs</strong> tab in the DuploCloud Platform</p></figcaption></figure>

## Viewing Ingestion Jobs

After uploading and ingesting documents into a VectorDB, you can monitor the status and output of each job in the **Ingestion Jobs** tab. This tab provides access to ingestion history, logs, and detailed configuration metadata to help validate behavior and troubleshoot issues.

* In the DuploCloud portal, go to **AI Suite** → **Studio** → **Vector DBs**.
* Select the **Ingestion Jobs** tab.
*   Click the **menu icon** (<img src="../../.gitbook/assets/menu icon (2) (1).avif" alt="" data-size="line">) next to the job you want to inspect.\


    <figure><img src="../../.gitbook/assets/ingestion jobs1.png" alt=""><figcaption><p>The <strong>Ingestion Jobs</strong> tab with the <strong>Logs</strong> and <strong>Details</strong> menu options highlighted</p></figcaption></figure>
* Choose one of the following options:
  *   **Logs:** View output that includes source file paths, chunking progress, chunk IDs, and any success or error messages.\


      <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (491).png" alt="" width="563"><figcaption><p>The <strong>Logs</strong> for an ingested job</p></figcaption></figure></div>
  *   **Details:** Open a structured JSON summary showing VectorDB type and provider, API endpoint, file paths ingested, output directory, chunking configuration, embedding model, and other technical metadata.\


      <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (492).png" alt="" width="563"><figcaption><p>The <strong>Details</strong> for an ingested job</p></figcaption></figure></div>

## Using VectorDBs with DuploCloud AI Agents

To learn how to integrate the files uploaded to your VectorDBs with the DuploCloud AI Agent, see the DuploCloud documentation for [creating AI Agents](agents.md).&#x20;
