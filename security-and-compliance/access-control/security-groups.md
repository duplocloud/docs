# Security Groups

Each tenant is its own security group and within the tenant the security group allows full access between resources. Various cloud managed services like AWS RDS, Opensearch, MSK, Azure SQL etc are created and placed in their respective tenant's security groups so that any compute in that tenant can reach them.

An administrator can allow inter-tenant traffic by explictly opening them under Administrator -> Tenants->Security menu. \


<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

In Azure network security is implemented at the virtual network level and all traffic within the VNET is allowed. This behavior can be overridden by placing a low priority deny rule for all VNET traffic. Azure ASGs allow intra-tenant traffic. So if the user desires they can treat tenant as a security boundry with the above suggested approach. The menu to manage security group rules is under administrator --> Infrastructure -> Security.&#x20;

&#x20;

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>
