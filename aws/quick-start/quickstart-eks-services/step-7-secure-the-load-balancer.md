# Step 7: Secure the Load Balancer

If the user created an Application load balancer, there are a way to secure the load balancer by:

* Attaching a WAF to the load balancer
* Setting up HTTP to HTTPs redirect&#x20;
* Enabling access logging to monitor request details
* Protecting from requests that contain invalid headers

This security settings can be accessed by navigating to _Services->Load Balancers->Other Settings-> Edit :_

![](<../../../.gitbook/assets/Screen Shot 2022-05-25 at 12.20.28 PM.png>)



To create and attach a WAF to the load balancer, please go over the corresponding [section](https://docs.duplocloud.com/docs/aws/aws-services/web-application-firewall-waf?q=waf).
