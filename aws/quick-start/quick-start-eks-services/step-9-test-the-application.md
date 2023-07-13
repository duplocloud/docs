---
description: Test the application to ensure you get the results you expect
---

# Step 9: Test the Application

You can test your application directly from the **Services** page using the **DNS** status card.

_Estimated time to complete Step 9 and finish tutorial: 10 minutes._

## Prerequisites

Before securing a Load Balancer, verify that you accomplished the tasks in the previous tutorial steps.   Using the DuploCloud Portal, confirm that:

* An [Infrastructure and Plan](../step-1-infrastructure.md) exist, both with the name **NONPROD**.
* The **NONPROD** infrastructure has [Kubernetes (EKS or ECS) **Enabled**](../step-1-infrastructure.md#check-your-work).&#x20;
* A Tenant with the name [**dev01** has been created](../step-2-tenant.md).
* A Host with the name [**host01** has been created](step-3-create-host.md).
* A Service with the name [**demo-service** has been created](step-5-create-app-via-k8s.md).
* An [HTTPS ALB Load Balancer](../quick-start-duplocloud-docker-services/step-6-create-loadbalancer.md) has been created.&#x20;

### Select the Tenant you created

In the **Tenant** list box, on the upper-left side of the DuploCloud Portal, select the **dev01** Tenant that you created.

## Testing the Application

{% hint style="info" %}
Note that if you skipped [Step 7](step-7-secure-the-load-balancer.md) and/or [Step 8](step-8-create-dns-name.md), the configuration in the **Other Settings** and **DNS** cards appears slightly different from the configuration depicted in the screenshot below. These changes do not impact you in testing your application, as these steps are optional. You can proceed to test your app with no visible change in the output of the deployable application.
{% endhint %}

1. In the DuploCloud Portal, navigate to **DevOps** -> **Containers** -> **EKS/Native**. The **Services** page displays.
2. From the **Name** column, select **demo-service**.
3. Click the **Load Balancers** tab. The ALB Load Balancer configuration is displayed.
4.  In the **DNS** status card on the right side of the Portal, click the Copy Icon ( <img src="../../../.gitbook/assets/copy_icon (1).png" alt="" data-size="line"> ) to copy the DNS address displayed to your clipboard.\


    <figure><img src="../../../.gitbook/assets/AWS_QS_28.png" alt=""><figcaption><p><strong>Load Balancers</strong> tab on the <strong>Services</strong> page with <strong>DNS</strong> status card highlighted</p></figcaption></figure>


5. Open a browser instance and **Paste** the DNS in the URL field of your browser.
6. Press **ENTER**. A web page with the text **Hello World!** is displayed, from the JavaScript program residing in your Docker Container that is running in **demo-service**, which is exposed to the web by your Load Balancer.

<figure><img src="../../../.gitbook/assets/AWS_QS_29.png" alt=""><figcaption><p>Web page with <strong>Hello World!</strong> displayed</p></figcaption></figure>

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
* [Created an EC2 host](step-3-create-host.md) named **host01**, so that your application has storage resources with which to run.
* [Created a Service](step-5-create-app-via-k8s.md) named **demo-service** to connect the Docker containers and associated images, in which your application code resides, to the DuploCloud Tenant environment.
* [Created an ALB Load Balancer Listener](step-6-create-a-load-balancer.md) to expose your application via ports and backend network configurations.&#x20;
* [Verified that your web page rendered](step-9-test-the-application.md) as expected by testing the IP address exposed by the  Load Balancer Listener.

## Cleaning up your tutorial environment

In this tutorial, you created many artifacts for testing purposes. When you are ready, clean them up so that another person can run this tutorial from the start, using the same names for Infrastructure and Tenant.

1. To delete the **dev01** tenant [follow these instructions](../../../administrator-tools/access-control/tenant-access/deleting-a-tenant.md) and then return to this page. As you learned, the Tenant segregates all work in one isolated environment, so deleting the Tenant that you created cleans up most of your artifacts.
2. Finish by deleting the **NONPROD** Infrastructure. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**. Click the **Action** menu icon (<img src="../../../.gitbook/assets/image (4) (3).png" alt="" data-size="line">) for the **NONPROD** row and select **Delete**.&#x20;

The **NONPROD** Infrastructure is deleted and you have completed the clean-up of your test environment.

Thanks for completing this tutorial and proceed to the next section to learn more about [using DuploCloud with AWS](../../use-cases/).
