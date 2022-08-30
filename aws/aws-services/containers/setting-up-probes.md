# Setting up Probes

Liveness, Readiness and Startup probes are a well known method to detect Pod health in Kubernetes. They are used in regular uptime monitoring as well as enable initial startup health that allow rolling deploys of new service updates.

Below is an example of Readiness and Liveness probes in DuploCloud K8 service configuration:

<figure><img src="../../../.gitbook/assets/Screen Shot 2022-08-29 at 9.53.42 PM.png" alt=""><figcaption></figcaption></figure>

Full details of this K8 feature can be referenced [here](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

