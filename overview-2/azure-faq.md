# Azure FAQ

## One or more of my containers are showing in a pending state, how can I debug? <a href="#id-7-toc-title" id="id-7-toc-title"></a>

[Click here for the details](../overview/aws-faq.md#7-toc-title)

## How to create a VM host with public IP? <a href="#id-9-toc-title" id="id-9-toc-title"></a>

While creating a VM Host, under Advanced Option, you can enable Public IP.

For the already created VM Host, View the Host from DuploCloud, under Features Tab, select the option **Enable Public IP**

## I'm trying to create a Kubernetes cluster and failing to establish server endpoints and a token. What can be causing this?

If your Kubernetes cluster displays empty values for the **Server Endpoint** and **Token**, you may need to [set your default AKS Cluster](prerequisites/set-the-aks-cluster-version.md) in the DuploCloud Portal **System Config** tab in **System Settings**.
