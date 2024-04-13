# WAF

WAF provides HTTP level firewall along with advanced mechanisms for bot protection, geofencing, rate limiting and so forth. The WAF itself should be created and curated directly in the cloud providers interface and a reference to that added in the platform under administrator -> Plans. Subsequently when creating the loadbalancer endpoints this WAF is attached. This is described in the earlier sections for [AWS](../../aws-user-guide/aws-services/web-application-firewall-waf.md), Azure and GCP.&#x20;
