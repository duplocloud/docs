# Supporting Components

### Cartography

Duplo Cartography is a Dockerized build of Cartography extended with custom Duplo intelligence and Neo4j models that unifies DuploCloud, Kubernetes, AWS, GitHub, and external systems into a single, queryable graph. It injects a Duplo ingestion stage at runtime (via sitecustomize) to ingest tenants, plans, infra, hosts, pods, agents, and container versions, standardizing on IN\_TENANT relationships for clean scoping and authorization. The project supports an optional dependencies manifest (local file or Kubernetes ConfigMap) to link workloads to Kubernetes objects, AWS resources (e.g., S3, RDS), and external services, while helper scripts and JIT credential support make it straightforward to run against Neo4j for local development or production.

This guide explains how to describe a service/workload's dependencies in YAML, how the file is discovered at runtime, and how each dependency type is matched in Neo4j. It is written for junior engineers; examples are included throughout.

***

#### Where the file comes from

You can supply the manifest as a plain file inside the container, or by mounting a Kubernetes ConfigMap to a file path.

* Set `DEPENDENCIES_SOURCE=local` to force reading `/dependencies.yaml`.
* Otherwise set `DEPENDENCIES_CONFIG_MAP=/path/to/file.yaml` to use a specific file path (e.g., a ConfigMap mounted at `/config/config`).
* If `DEPENDENCIES_CONFIG_MAP` is not set, the dependencies step is skipped (we do not crash; we log an error and continue).
* If the file cannot be opened, is empty, or has malformed YAML, we log a warning and skip the step (no crash).

Important: The mounted file must contain only the YAML shown below – do NOT wrap it in a `config: |` key. The file content should start with `namespaces:`.

***

#### YAML schema (high level)

```yaml
namespaces:
  - <namespace>:
      <workload-name>:
        dependencies:
          kubernetes: []  # list of K8s dependency items
          aws: []         # list of AWS dependency items
          external: []    # list of external dependency items
```

* `namespaces` is a list. Each list item maps one namespace to one or more workloads under it.
* `<workload-name>` is a logical workload key. We derive this from pod names by trimming hashes/ordinals, so all pod instances of the same workload share one definition.

Examples of derived workload names:

* Deployment pod: `api-7c9d88f9d9-abc12` → `api`
* StatefulSet pod: `db-0` → `db`

***

#### Kubernetes dependencies

These link your pod(s) to existing typed Kubernetes nodes in Neo4j. Supported kinds in v1:

* `Service`, `Secret`, `ConfigMap`

Item shape:

```yaml
- type: Service         # Kubernetes Kind (PascalCase)
  name: <k8s-name>
  namespace: <optional; defaults to this namespace>
  protocol: <optional>
  port: <optional int>
  url: <optional>       # for documentation; stored on the relationship
  critical: <optional bool>
  description: <optional string>
```

Example:

```yaml
kubernetes:
  - type: Service
    name: neo4j
    namespace: duploservices-andy
    protocol: bolt
    port: 7687
    url: bolt://neo4j.example.net:7687
    critical: true
    description: Graph database used by architecture-diagram
```

Matching behavior:

* We link to existing typed nodes: `(:KubernetesService)`, `(:KubernetesSecret)`, or `(:KubernetesConfigMap)` by `name` + `namespace`.
* If the target doesn’t exist in the graph, we skip and log a warning. We do not create generic K8s nodes in v1.

***

#### AWS dependencies

AWS dependencies link your pod(s) to existing typed AWS nodes in Neo4j. In v1 we support at least:

* `s3` → `(:S3Bucket)` by bucket name
* `rds` → `(:RDSInstance)` by DB instance identifier

We intentionally do not model non-resource AWS offerings here (e.g., Bedrock, SES). Treat those under `external` instead.

Item shapes:

```yaml
# S3 bucket
- type: s3
  bucket_name: <bucket>       # REQUIRED; maps to S3Bucket.name
  region: <optional>
  critical: <optional bool>
  description: <optional string>

# RDS instance
- type: rds
  db_instance_identifier: <id>  # REQUIRED; maps to RDSInstance.db_instance_identifier
  region: <optional>
  critical: <optional bool>
  description: <optional string>
```

Example:

```yaml
aws:
  - type: s3
    bucket_name: my-diagrams
    region: us-east-1
    critical: true
    description: Stores rendered diagrams

  - type: rds
    db_instance_identifier: orders-db-prod
    region: us-east-1
    critical: true
    description: Primary orders database
```

Matching behavior:

* S3: `MATCH (s3:S3Bucket {name: bucket_name})`
* RDS: `MATCH (rds:RDSInstance {db_instance_identifier: db_instance_identifier})`
* If the target doesn’t exist, no edge is created (and we can log a debug line for troubleshooting).

***

#### External dependencies

External dependencies represent systems outside your cluster/AWS account (or AWS offerings that don’t create resources, like Bedrock/SES).

Item shape:

```yaml
- type: <freeform slug>     # e.g., api, database, cache, queue
  name: <display name>
  url: <url>
  region: <optional>
  inference_profile_arn: <optional>
  critical: <optional bool>
  description: <optional string>
```

Example:

```yaml
external:
  - type: api
    name: azure-communication-server
    url: https://example.communication.azure.com
    critical: false
    description: Customer notifications via Azure Communication Server

  - type: api
    name: anthropic-claude-sonnet-3.5
    url: https://bedrock.aws.amazon.com
    critical: true
    description: Anthropic Claude Sonnet 3.5 via Application Inference Profile
    region: us-east-1
    inference_profile_arn: arn:aws:bedrock:us-east-1:123456789012:application-inference-profile/abcd
```

Graph behavior:

* We `MERGE` `(:ExternalService {name})` and `MERGE` a `DEPENDS_ON` relationship from the pod.
* If the pod has `IN_TENANT`, we also `MERGE (ExternalService)-[:IN_TENANT]->(DuploTenant)` so the external system inherits tenant scoping.
* On the relationship, we store helpful fields like `critical`, `description`, `url`, `region`, `inference_profile_arn`, and `service_name`.

***

#### Full working example

```yaml
namespaces:
  - duploservices-andy:
      architecture-diagram:
        dependencies:
          kubernetes:
            - type: Service
              name: neo4j
              namespace: duploservices-andy
              protocol: bolt
              port: 7687
              url: bolt://neo4j.example.net:7687
              critical: true
              description: Graph database used by architecture-diagram

            - type: ConfigMap
              name: architecture-diagram-dependencies
              namespace: duploservices-andy
              description: Dependencies for the service

            - type: Secret
              name: gpg-passphrase
              namespace: duploservices-andy
              description: GPG material for signing

          aws:
            - type: s3
              bucket_name: my-diagrams
              region: us-east-1
              critical: true
              description: Stores rendered diagrams

            - type: rds
              db_instance_identifier: orders-db-prod
              region: us-east-1
              critical: true
              description: Primary orders database

          external:
            - type: api
              name: azure-communication-server
              url: https://example.communication.azure.com
              critical: false
              description: Customer notifications via Azure Communication Server
```

#### Full Example in Duplo

```yaml
config: |
  namespaces:
    - duploservices-andy:
        k8s:
          dependencies:
            kubernetes:
              - type: Service
                name: neo4j
                namespace: duploservices-andy
                protocol: bolt
                port: 7687
                url: bolt://neo4j.test10-apps.duplocloud.net:7687
                critical: true
                description: "Graph database used by architecture-diagram"

              - type: ConfigMap
                name: duplo-cartography
                namespace: duploservices-andy
                description: "Dependencies for architecture-diagram"

              - type: Secret
                name: my-k8s-secret
                namespace: duploservices-andy
                description: "GPG passphrase for architecture-diagram"

            aws:
              - type: s3
                bucket_name: duplo-nonprod-awslogs-938690564755
                region: us-east-1
                critical: true
                description: "Stores exported diagrams"

              - type: rds
                db_instance_identifier: duploandy-forcost
                region: us-east-1
                critical: true
                description: "Primary application database"

            external:
              - type: api
                name: azure-communication-server
                url: https://example.communication.azure.com
                critical: false
                description: "Customer notifications via Azure Communication Server"

              - type: bedrock
                region: us-east-1
                name: anthropic-claude-sonnet-3.5
                critical: true
                description: "Anthropic Claude Sonnet 3.5 via Application Inference Profile"
                inference_profile_arn: arn:aws:bedrock:us-east-1:938690564755:application-inference-profile/5hli7gcftss9
```

***

#### Troubleshooting checklist

* YAML wrapper: The file must start with `namespaces:` – do not wrap with `config: |`.
* Indentation: Keys under list items must be indented two spaces more than the `-` line.
* Workload key: The workload name must match the derived workload from pod names (e.g., `api`, `architecture-diagram`). If in doubt, check logs for `No manifest for pod=` messages.
* K8s targets missing: Ensure the target `Service`/`Secret`/`ConfigMap` exists in Neo4j. Missing targets are logged and skipped.
* AWS linking:
  * S3 uses `bucket_name` → `S3Bucket.name`
  * RDS uses `db_instance_identifier` → `RDSInstance.db_instance_identifier`
* External scoping: ExternalService nodes inherit `IN_TENANT` from the pod when present.
* Logging: Enable debug logs to see each mapping decision. Look for lines like `K8s map`, `AWS map`, and `External map` in the logs.

***

#### Operational notes

* The ingestion runs even when the manifest is missing or malformed; we log and continue.
* You can switch modes at runtime by changing `DEPENDENCIES_SOURCE` or `DEPENDENCIES_CONFIG_MAP` and re-running.
* We de-duplicate relationships by stable keys and set `lastupdated` on each run.

If you have questions or see skipped targets, copy the relevant log lines and open an issue with the exact pod name, namespace, and the YAML snippet.



### GenAI-ToolBox

### Presidio

