---
description: Test the application to ensure you get the results you expect
---

# Step 7: Test the Application

You can test your application directly from the **Services** page using the **DNS** status card.

_Estimated time to complete Step 7 and finish tutorial: 5 minutes._

## Prerequisites

Before testing your application, verify that you accomplished the tasks in the previous tutorial steps.   Using the DuploCloud Portal, confirm that:

* An [Infrastructure and Plan](../step-1-infrastructure.md) exist, both with the name **NONPROD**.
* A Tenant with the name [**dev01** has been created](../step-2-tenant.md).
* An EC2 Host with the name [host01 has been created](step-4-create-ec2-host.md).
* A Service with the name [**demo-service-d01** has been created](step-5-create-app-via-docker-native.md).&#x20;
* A Load Balancer [configured to listen on port xxxx has been created](step-6-create-loadbalancer.md).

### Select the Tenant you created

In the **Tenant** list box, on the upper-left side of the DuploCloud Portal, select the **dev01** Tenant that you created.

<figure><img src="../../../.gitbook/assets/tenant_dev01 (3).png" alt=""><figcaption><p>DuploCloud <strong>Tenant</strong> list box with Tenant <strong>dev01</strong> selected</p></figcaption></figure>

## Testing the Application

1. In the DuploCloud Portal, navigate to **Docker** -> **Services**. The **Services** page displays.
2. From the **Name** column, select **demo-service-d01**.
3. Click the **Load Balancers** tab. The Application Load Balancer configuration is displayed.
4.  In the **DNS** status card on the right side of the Portal, click the Copy Icon ( <img src="../../../.gitbook/assets/copy_icon (1).png" alt="" data-size="line"> ) to copy the DNS address displayed to your clipboard.\


    <figure><img src="../../../.gitbook/assets/services new.png" alt=""><figcaption><p>Service page with <strong>Load Balancers</strong> tab selected<br></p></figcaption></figure>
5. Open a browser instance and **Paste** the DNS in the URL field of your browser.
6. Press **ENTER**. A web page with the text **Hello World!** is displayed, from the JavaScript program residing in your Docker Container that is running in **demo-service-d01**, which is exposed to the web by your Load Balancer.

<figure><img src="../../../.gitbook/assets/dockern.png" alt=""><figcaption><p>Browser instance displaying <strong>Hello World!</strong></p></figcaption></figure>

{% hint style="info" %}
It can take from five to fifteen (5-15) minutes for the DNS Name to become active once you launch your browser instance to test your application.
{% endhint %}

Congratulations! You have just launched your first web service on DuploCloud!

## Reviewing what you learned

In this tutorial, your objective was to create a cloud environment to deploy an application for testing purposes, and to understand how the various components of DuploCloud work together.&#x20;

The application rendered a simple web page with text, coded in JavaScript, from software application code residing in a Docker container. You can use this same procedure to deploy much more complex cloud applications.&#x20;

In the previous steps, you:

* [Created a DuploCloud Infrastructure](../step-1-infrastructure.md) named **NONPROD**, a Virtual Private Cloud instance, backed by an AKS-enabled Kubernetes cluster.&#x20;
* [Created a Tenant](../step-2-tenant.md) named **dev01** in Infrastructure **NONPROD**. While generating the Infrastructure, DuploCloud created a set of templates ([Plan](../step-1-infrastructure.md)) to configure multiple Azure and Kubernetes components needed for your environment.
* [Created an EC2 host](step-4-create-ec2-host.md) named **host01**, so that your application has storage resources with which to run.
* [Created a Service](step-5-create-app-via-docker-native.md) named **demo-service-d01** to connect the Docker containers and associated images, in which your application code resides, to the DuploCloud Tenant environment.
* [Created an ALB Load Balancer Listener](step-6-create-loadbalancer.md) to expose your application via ports and backend network configurations.&#x20;
* [Verified that your web page rendered](step-7-test-the-application.md#testing-the-application) as expected by testing the DNS Name exposed by the  Load Balancer Listener.

## Cleaning up your tutorial environment

In this tutorial, you created many artifacts for testing purposes. When you are ready, clean them up so that another person can run this tutorial from the start, using the same names for Infrastructure and Tenant.

1. To delete the **dev01** tenant [follow these instructions](../../../user-administration-1/access-control/tenant-access/deleting-a-tenant.md) and then return to this page. As you learned, the Tenant segregates all work in one isolated environment, so deleting the Tenant that you created cleans up most of your artifacts.
2. Finish by deleting the **NONPROD** Infrastructure. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**. Click the **Action** menu icon (<img src="../../../.gitbook/assets/image (4) (3).png" alt="" data-size="line">) for the **NONPROD** row and select **Delete**.&#x20;

The **NONPROD** Infrastructure is deleted and you have completed the clean-up of your test environment.

Thanks for completing this tutorial and proceed to the next section to learn more about [using DuploCloud with AWS](../../use-cases/).
