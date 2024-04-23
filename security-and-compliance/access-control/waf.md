---
description: Web Application Firewall (WAF) in DuploCloud
---

# WAF

WAF provides an HTTP-level firewall with advanced mechanisms for bot protection, geofencing, rate limiting, and so forth. The WAF should be created and curated directly in the cloud provider interface and a reference to the WAF added to the platform using the **Administrator** -> **Plans** menu.&#x20;

Subsequently, when creating the load balancer endpoints, this [WAF ](../../aws-user-guide/aws-services/web-application-firewall-waf.md)is attached.&#x20;
