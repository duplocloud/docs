# Application Environment

SSO to the platform is via Google, Microsoft or Okta. We do not support username/password. The identity of a user in the platform is their email address.&#x20;

The basis of all access management is the Tenant. Users only need to be granted access to the tenant and from there when they login to the DuploCloud platform they are given access to the individual resources within that tenant on a need basis as described in the next section.&#x20;

Beyond tenant level access there 3 more types of users:

* ReadOnly
* Administrator
* Security Auditor who can only view the monitoring aspects of security. &#x20;

Users can also create groups in Microsoft AD or Okta and those can be mapped to Tenants in DuploCloud. Thus all access administrator can be done from AD or Okta.
