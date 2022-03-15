# Creating advanced functions

## Allocation Tags <a href="#0-toc-title" id="0-toc-title"></a>

By default, DuploCloud spreads the container replicas across the hosts. By virtue of allocation tag the user can pin a container to a set of hosts that have a specific tag. Click on the edit icon next to allocation tag under host.

`AllocationTags` as key is already pre-populated, configure the value of your choice for example `"highmemory;highcpu"` or `"serviceA"` and click on save on the left. Then, when creating a service, set the allocation tag value to be a substring of the above tag, for example `highmemory` or serviceA. The allocation algorithm tries to pick a host where `AllocationTag` specified in the service is a substring of the `AllocationTags` of the host.&#x20;

![](https://duplocloud.com/wp-content/uploads/2021/11/edit-allocationtag.png)

![](https://duplocloud.com/wp-content/uploads/2021/11/configure-allocationtag.png)
