# Ingress Loadbalancer

Ingress controllers abstract the complexity of routed Kubernetes application traffic, providing a bridge between Kubernetes services and external services. They play a crucial role in managing access to the services within a Kubernetes cluster, ensuring that traffic is efficiently directed to the appropriate backend services.

### Creating Tenants, Hosts, and Services

See the DuploCloud documentation on creating [Tenants](../../welcome-to-duplocloud/application-focussed-interface/duplocloud-common-components/tenant.md), [Hosts](../../overview/use-cases/hosts-vms/), and [Services](../../welcome-to-duplocloud/application-focussed-interface/duplocloud-common-components/app-service-and-cloud-services.md) for your cloud provider. These foundational steps are essential for deploying and managing your applications and services within a Kubernetes environment.

Once your Service is deployed, you can add and configure Kubernetes Ingress. The steps to create Ingress for each cloud provider are slightly different. Ingress setup is a critical step in defining how external traffic is routed to your services, providing a scalable and secure entry point for your applications.

### Monitoring and Troubleshooting

To ensure the smooth operation of services within a cluster, it's important to have access to and understand how to view container logs. For troubleshooting or monitoring purposes, you can easily view the logs of containers within a cluster directly from the containers' user interface. This is achieved by utilizing the context menu in the UI, offering a straightforward method to access the necessary log information. This capability is crucial for diagnosing issues, understanding service behavior, and ensuring the reliability and performance of your applications.

In summary, setting up Ingress controllers and understanding how to access container logs are fundamental aspects of managing and troubleshooting Kubernetes applications. By following the documented steps for creating tenants, hosts, and services, and by utilizing the UI for log access, you can effectively manage traffic flow and monitor the health and performance of your services.
