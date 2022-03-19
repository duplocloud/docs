# Container Orchestration

There are several container orchestration technologies in the state of art. DuploCloud abstracts the complexity of these allowing you to purely focus on you being able to achieve the deployment, update and debugging of the your containerized application. User can choose which technology to use. DuploCloud supports all of them and makes it easy for the user to consume

* **Natively Built-in a.k.a "I don't care"**: DuploCloud platform has a built in container management capability which at a high level has the exact same input interface as Docker Run command except that it can be scaled to hundreds of containers across many hosts along with capabilities like associating LB, DNS etc.
* **Kubernetes (AWS EKS)**: DuploCloud platform uses AWS EKS underneath and provides a simple easy to use interface hiding the complexities of Kubernetes. This abstraction also allows you to input more complex K8S configurations around POD, Container, Secrets etc. The key advantage of Kubernetes based deployments is that beyond deploying containers it provides a couple other cloud-agnostic functions like config store, secrets store etc. It should be noted that each of these functionalities can be achieved by AWS native services like Secrets Manager, SSM Parameter store.&#x20;

{% hint style="info" %}
The main advantage of a K8S based deployment is that it allows a cloud agnostic interface and has an open source community that actively provides templates for various cloud products.

But the biggest disadvantages are one that K8S cluster in AWS gets deprecated every 6 months and one has to upgrade them and all the nodes. DuploCloud automates this but nevertheless, the disruption and planning for the same may or may not be worth it especially in small environments. &#x20;
{% endhint %}

* **AWS ECS Fargate**: This is a cloud Native proprietary service from AWS. The key advantage of this is that one does not have to manage any servers especially in terms of patching and capacity management. Patching is less of an issue is because DuploCloud takes care of this. The disadvantage of ECS is that it is a very proprietary interface to AWS and being serverless one cannot easily debug issues unlike in a server based environment where the user can have full control for things like Docker restart, Docker exec, Docker logs etc. &#x20;
