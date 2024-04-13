# Cloud Account

Cloud provider account is the heaviest hammer of isolation.&#x20;

* **Azure Subscription**: One DuploCloud portal can manage multiple Azure subscriptions. To add a subscription go to Administrator -> CloudCredentials as shown in the figure below. One can use a managed identity or a service principle with keys

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

*   **AWS Account**: In case of AWS you need one DuploCloud VM per AWS account. This is because in AWS the account is the fundamental IAM construct. The AWS organizations and SCP are very light weight and were infact more recently added in the products lifespan unlike Azure where Active Directory is the fundamental IAM construct. Originally DuploCloud used to manage multiple AWS accounts but this support was removed after consistent feedback from customers and security experts and it was deemed that one VM agent per account federated in a single pane with an account switcher drop down is the best security practice. See figure below:\


    <figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>


*   **Google Project**: Multiple GCP projects can be added and managed by same DuploCloud installation. To add a project go to Administrator -> CloudCredentials as shown in the figure below\
    \


    <figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
