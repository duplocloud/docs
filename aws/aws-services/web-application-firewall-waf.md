# Web App Firewall (WAF)

Creation of a Web Application Firewall (WAF) is a one time process. Create a WAF in the AWS Console, fetch the ID/ARN and update the plan in DuploCloud. Once the plan has the WAF it can be used attached to the LB.

![](https://duplocloud.com/wp-content/uploads/2021/11/plan-waf.png)

![](https://duplocloud.com/wp-content/uploads/2021/11/attach-waf.png)

## Analyzing inbound traffic with WAF dashboard <a href="#1-toc-title" id="1-toc-title"></a>

DuploCloud also provides a WAF Dashboard through which you can analyze the traffic that is coming in and the requests that are blocked. The Dashboard can be accessed from left navigation panel: **Security > WAF**.

![WAF Dashboard](../../.gitbook/assets/waf.png)
