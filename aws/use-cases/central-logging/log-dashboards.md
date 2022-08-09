# Log Dashboards

Logging dashboards per tenants are available under Diagnostics --> Loggings. Note that the logs are in the context of the Tenant (That can be switched using tenant switcher). In addition the logs are segregated per services that also can switched using the "Select Service" option as shown in the picture below

![](<../../../.gitbook/assets/image (20) (1).png>)

Note that these dashboards are native Kibana dashboards with preset-filters. One can easly add their own filter or change existing ones.

{% hint style="info" %}
The separation of logs across tenants is only a filter. All logs are in a single index. Today one tenant user can see other tenant logs by changing filters. The central logging control plane is shared with no per tenant access control.&#x20;
{% endhint %}
