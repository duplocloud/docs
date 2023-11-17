---
description: Configuration and Secret management in GCP
---

# Passing Config and Secrets

There are many ways to pass configuration to the containers at run time.

## **Using Environmental Variables (EVs)**

Using EVs is the simplest method but can be cumbersome if there are too many configurations, especially files and certificates. In Kubernetes, you have the option to populate environment variables from [Config Maps or Secrets](setting-environment-variables-from-config.md).

## Mounting Configs and Secrets as files

You can mount data from Kubernetes [ConfigMap and secrets as files](mounting-config-as-files.md).
