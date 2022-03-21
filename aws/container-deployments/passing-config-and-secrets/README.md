# Passing Config and Secrets

There are many ways to pass configuration to the containers at run time.

## **Environmental variables**

* This is the simplest way but can be cumbersome if there are too many configurations, especially files and certificates.
* In Kubernetes you also have the option to populate environment variables from [Config Maps](setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-configmap) or [Secrets](setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-secret).

## **Via AWS Services**

### S3

One can use S3 Bucket to store and pass configuration to the containers with the following steps:

* Create an S3 bucket in the same tenant and then add the needed configurations in an S3 as files.
* Set the S3 Bucket name as an environmental variable
* Have the Entrypoint / Command of the container to be a startup script that would download the files from S3 bucket (by referencing the environmental variable) into the container and set it in the appropriate location within the container. This could be simply a [S3 cp](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/cp.html) and copy the config file in S3 into a location in the container or it could first do an S3 cp then parsing the file and setting the contents as ENV variables. It also could be that the config in S3 is already a bash file that when run sets the Environmental variables.

Here is a simple example of getting config from S3.&#x20;

```
aws s3 cp s3://$S3_BUCKET_NAME/myconfig.json /app/config/config.json
```

### SSM parameter Store

Similar to S3, one can create the values on a SSM parameter store **Devops -> AppIntegration -> SSM Parameters** then set the Name of the parameter in the Environmental variables and then in the startup script use AWS CLI to pull values from SSM and set it for the application in the container, either as an Environmental variable or files.

### **AWS Secrets Manager**

Similar to SSM one can use AWS secrets manager to create the necessary configs and secrets and then set the secret name in the Environmental variables and then in the container startup script use AWS CLI to pull the secrets and set it in the appropriate format in the container.

```
aws secretsmanager get-secret-value --region us-west-2 
--secret-id "${ENVIRONMENT}/${PROJECT}/env" 
--query SecretString --output text | base64 -d > ${ENVIRONMENT_FILE_NAME}
```

## Via Kubernetes

### Config Maps

You can mount data from a Kubernetes Config Map [as files](mounting-config-as-files.md#mount-a-kubernetes-configmap), or you can import it [as environment variables](setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-configmap).

### Secrets

You can mount data from a Kubernetes Secret [as files](mounting-config-as-files.md#mount-a-kubernetes-secret), or you can import it [as environment variables](setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-secret).
