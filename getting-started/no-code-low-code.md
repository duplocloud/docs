# No-Code / Low-Code

It must be obvious by now how DuploCloud provides a no-code UI based approach to build and operate the cloud infrastructure. [Here](http://www.duplocloud.com/intro-demo) is an elaborate demo of the approach.

\
For an audience that desires to use Infrastructure-as-Code (IaC) we have a [Terraform Provider](https://registry.terraform.io/providers/duplocloud/duplocloud/latest) that enables low-code IaC. This provider exposes all the DuploCloud abstractions and constructs to be programmed via Terraform. Using the DuploCloud Terraform provider, one can build the same infrastructure using 10x less code with all compliance controls built-in. The user is not required to have subject matter expertise in DevSecOps. This [white-paper](https://duplocloud.com/white-papers/devops/) describes the process in detail.

{% hint style="info" %}
A common misconception is that DuploCloud is generating Terraform behind the scenes to provision the cloud infrastructure. The DuploCloud UI and Terraform (with the DuploCloud Provider) are layers on top of DuploCloud. Behind the scenes, DuploCloud uses the cloud provider APIs as shown in picture below
{% endhint %}

![](<../.gitbook/assets/image (4) (1) (1).png>)

The reason DuploCloud uses APIs behind the scenes is that this is not just about taking user requests and generating configurations synchronously and calling the cloud provider. Such a system requires many operations to be done asynchronously, requiring a state machine with retries and the ability to detect and fix configuration drift continuously. Further, faults and compliance controls must be monitored continuously.\
Terraform or for that matter any scripting approach are meant to be run with human supervision. There is no synchronicity and retries. A script start and ends.
