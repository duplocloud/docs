# Architecture

Advanced Observability Suite (AOS) is based on open telemetry and involves dozens of components. The following picture shows the various components. The ovals are daemon sets that run on each node. The rest are either deployment sets or stateful sets.



{% hint style="info" %}
The OTEL stack comprised to 50+ components and 100s of configurations, we advise that if you need any change to control plane configuration then work with your DuploCloud support team that is readily available on the support channel. &#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/image (446).png" alt=""><figcaption></figcaption></figure>

To view the complete deployment of the Open telemetry stack please see the setup under the tenant where OTEL is deployed under the Kubernetes menu. Data is stored in S3 buckets that you can find under cloud services --> Storage --> S3. The setup is deployed and managed via Flux Helm release

&#x20;

<figure><img src="../../.gitbook/assets/image (447).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (448).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (449).png" alt=""><figcaption></figcaption></figure>
