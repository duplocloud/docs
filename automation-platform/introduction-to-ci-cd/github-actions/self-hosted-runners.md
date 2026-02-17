---
description: Run GitHub Actions with self-hosted runners in DuploCloud
---

# Self-Hosted Runners

Self-hosted runners let repository users run code inside your environment, which can pose security risks. Before continuing, read at least GitHub's [self-hosted runner security doc](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners#self-hosted-runner-security) and the [runner security hardening doc](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions#hardening-for-self-hosted-runners).

The setup outlined here simplifies security by supporting runners for a single repository only. Supporting multiple repos or organizations requires additional controls like restricting runner use or managing access with groups.

DuploCloud recommends using the [Actions Runner Controller (ARC)](https://github.com/actions/actions-runner-controller) and isolating workloads by running the controller in one tenant and the runners in another ( `gharc01` and `ghrun01` in the example below). If runners need access to other tenants, grant cross-tenant permissions only to the runner tenant.

The Helm charts for the controller and scale sets are pinned to specific versions for stability, while runners run the latest image to stay updated. Keeping runners patched is critical despite possible compatibility risks.

Example code below is adapted from Terraform and can also be used with Helm CLI. Both charts were tested at version 0.9.3, with variable references replaced by explicit values for clarity.

## **Deploying Self-Hosted Runners**

### Deploy the Actions Runner Controller (ARC)

1. Deploy the controller Helm chart in the `gharc01` tenant using this Terraform resource as an example:

```hcl
resource "helm_release" "runner_scale_set_controller" {
  name      = "runner-scale-set-controller"
  namespace = "duploservices-gharc01"

  repository = "oci://ghcr.io/actions/actions-runner-controller-charts"
  chart      = "gha-runner-scale-set-controller"
  version    = "0.9.3"

  atomic  = true
  timeout = 600

  values = [
    yamlencode({
      nodeSelector = {
        # Only place the controller pods on hosts for this tenant.
        tenantname = "duploservices-gharc01"
      }
    })
  ]
}
```

### Setup Access by Creating a GitHub App

1. [Create a new GitHub App](https://docs.github.com/en/actions/tutorials/use-actions-runner-controller/authenticate-to-the-api#authenticating-arc-with-a-github-app) in your GitHub organization or user account:
   * Uncheck the option to configure a webhook URL.
   * Choose **Only allow this app to be installed on this account** during installation.
   * Limit the app’s access to the specific repository you will use (matching the `githubConfigUrl`).
2. In the Kubernetes tenant where runners will run (e.g., `ghrun01`), create a secret named as your `githubConfigSecret` (e.g., `github-auth`) with these keys:

```yaml
github_app_id: '<your-app-id>'
github_app_installation_id: '<your-installation-id>'
github_app_private_key: |
  -----BEGIN RSA PRIVATE KEY-----
  YOUR_PRIVATE_KEY
  -----END RSA PRIVATE KEY-----
```

See the upstream [values.yaml](https://github.com/actions/actions-runner-controller/blob/8b36ea90ebe81710fcdcb4f96424b43203d24f1e/charts/gha-runner-scale-set/values.yaml#L7-L12) for docs of the key names.

### Deploy the Runners

1. Deploy the runner and controller Helm charts as configured. This will create:
   * A runner pod in the tenant where runners are deployed (e.g., `ghrun01`).
   * A listener pod in the tenant where the controller is deployed (e.g., `gharc01`).
2. In the DuploCloud Portal, go to **Kubernetes** → **Containers** (not **Services**) in each tenant and confirm the pods are running.

```
resource "helm_release" "runner_scale_set" {
  # This is the value you enter in the `runs-on` key of GitHub Actions workflows to make them use these runners.
  name = "duplo-ghrun01-myorg-myrepo"

  namespace = "duploservices-ghrun01"

  repository = "oci://ghcr.io/actions/actions-runner-controller-charts"
  chart      = "gha-runner-scale-set"
  version    = "0.9.3"

  atomic  = true
  timeout = 600

  values = [
    yamlencode({
      # Name of a Duplo k8s secret containing your preferred auth values:
      # https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/authenticating-to-the-github-api
      githubConfigSecret = "github-auth"
      githubConfigUrl    = "https://github.com/myorg/myrepo"
      listenerTemplate = {
        spec = {
          # Required when setting spec. Set to empty to clear validation error. Setting to empty didn't change defaults.
          containers = []

          nodeSelector = {
            # Only place the listener pods on hosts for the tenant that runs ARC.
            # The listener is run in the ARC controller namespace, not the namespace of the runners.
            tenantname = "duploservices-gharc01"
          }
        }
      }
      minRunners = 1 # With the default min of 0, jobs never triggered scaling.
      template = {
        spec = {
          containers = [
            {
              name = "runner"

              # Set memory to guaranteed QoS mode so hungry jobs get killed before they take down the host (which may
              # have other runners on it).
              resources = {
                limits = {
                  memory = "1Gi"
                }
                requests = {
                  memory = "1Gi"
                }
              }

              # Setting resources removes these. This sets them back to the default.
              command = ["/home/runner/run.sh"]
              image   = "ghcr.io/actions/actions-runner:latest"
            }
          ]
          nodeSelector = {
            # Only place the runner pods on hosts for this tenant.
            tenantname = "duploservices-ghrun01"
          }
        }
      }
    })
  ]
}
```

## Test the Runners

1. Run a test GitHub Actions workflow in the repository using the configured `runs-on` label, for example:

```yaml
runs-on: duplo-ghrun01-myorg-myrepo
```

Replace `duplo-ghrun01-myorg-myrepo` with the actual label from your runner configuration.

If you need help creating a test workflow, [see this example](https://github.com/myorg/myrepo/blob/main/.github/workflows/example.yml).

## Additional Resources

* [Actions Runner Controller GitHub repository](https://github.com/actions/actions-runner-controller)
* [GitHub Actions Self-Hosted Runner documentation](https://docs.github.com/en/actions/concepts/runners/self-hosted-runners)
* [Managing Self-Hosted Runners with ARC](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/authenticating-to-the-github-api)
