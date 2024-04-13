# Encryption in Transit

Except for AWS, users need to generate SSL certificates out of band either from cloud provider ACM or issue them outside and upload to the cloud provider ACM. Then a reference to these certificates should be added under administrator-> plan -> Certificates. Then during the creation of cloud resources like LB, ingress, Cloudfront, API gateway one of these certificates can be selected and the platform will apply them to the resources.\
In case of AWS, DuploCloud automatically generates a wildchar certificate in the ACM for each DNS domain that the platform is managing and add its to the Plan itself. Users can at anytime add more certificates.

