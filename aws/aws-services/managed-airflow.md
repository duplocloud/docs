# Managed Airflow

Configure Apache Airflow by following the listed steps.

### Step1: Create S3 Bucket

Create a S3 bucket by following the steps [here](s3-bucket.md).

### Step2:  Upload DAGs in S3 **Bucket**

Package and upload your DAG (Directed Acyclic Graph) code to Amazon S3. Amazon MWAA loads this code into Airflow.

<div align="left">

<figure><img src="../../.gitbook/assets/image (57) (1).png" alt=""><figcaption><p>S3 Objects for Aitflow configuration</p></figcaption></figure>

</div>

{% hint style="info" %}
Make sure Versioning is enabled for the custom plugins in a `plugins.zip`, and Python dependencies in a `requirements.txt` on your Amazon S3 bucket.&#x20;
{% endhint %}

Refer to[ Amazon documentation ](https://docs.aws.amazon.com/mwaa/latest/userguide/working-dags.html)on DAGs for more details.

### Step3:  Configure Airflow Environment

Navigate to **DevOps** > **Analytics** > **Airflow**

Provide the required information like airflow version, name, S3 bucket, DAGs folder location.

If Plugins.zip and requirements.txt is specified while adding airflow, you would need to provide the S3 Version of these files.&#x20;

User can also enable logs while creating airflow.

<figure><img src="../../.gitbook/assets/image (5) (3).png" alt=""><figcaption></figcaption></figure>

### **View Airflow Environment**

User can view Airflow Environment details from DuploCloud Portal. You can  view AIrflow Envrionment in AWS Console by click Webserver URL.

<figure><img src="../../.gitbook/assets/image (38) (1).png" alt=""><figcaption></figcaption></figure>
