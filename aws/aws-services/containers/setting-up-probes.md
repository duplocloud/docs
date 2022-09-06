# Setting up Probes

Liveness, Readiness and Startup probes are well-known methods to detect Pod health in Kubernetes. They are used in regular uptime monitoring as well as enable initial startup health that allows rolling deploys of new service updates.

In the example below, we are going to define **Liveness, Readiness** and **Startup probes** to one service deployment.

While creating a deployment, provide the below configuration to set up probes for your service.

{% code title="Other Container Config" %}
```yaml
# setup http livenessProbe
# To perform a probe, the kubelet sends an HTTPGET request
# Service is considered healthy when /healthz retuns success code
livenessProbe:
  httpGet:
    path: /healthz #endpoint path
    port: 8080
  initialDelaySeconds: 3  #first Liveness check to be performed after 3 seconds.
  periodSeconds: 3       #verify the liveness of the application every 3 seconds

# setup http readinessProbe
readinessProbe:
  httpGet:
    path: /healthz
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 5

# setup startupProbe
# The application will have a maximum of 300s(30 * 10) to finish its startup
startupProbe:
  httpGet:
    path: /healthz
    port: 8080
  failureThreshold: 30
  periodSeconds: 10
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/image (75).png" alt=""><figcaption><p>Other Container Config</p></figcaption></figure>

We have seen httpGet example earlier, TCP Probes can also be configured from **Other Container Config** field, here is one  example for reference.

```yaml
readinessProbe:
  tcpSocket:
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10
livenessProbe:
  tcpSocket:
    port: 8080
  initialDelaySeconds: 15
  periodSeconds: 20
startupProbe:
  tcpSocket:
    port: 8080
  failureThreshold: 30
  periodSeconds: 10
```

Full details of this K8 feature can be referenced [here](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

