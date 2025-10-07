# View Cartography Details

The Cartography feature visualizes the relationships and dependencies within your infrastructure. By providing a Dependencies Manifest (YAML), DuploCloud maps services, workloads, and external resources into a Neo4j graph. This allows you to explore, analyze, and manage dependencies across Kubernetes, cloud services, and external systems, giving you a clear picture of how your applications interact and rely on each other.

This guide explains how to describe a service/workload's dependencies in YAML, how the file is discovered at runtime, and how each dependency type is matched in Neo4j. It is written for junior engineers; examples are included throughout.

***

### Where the file comes from

You can supply the manifest as a plain file inside the container, or by mounting a Kubernetes ConfigMap to a file path.

* Set `DEPENDENCIES_MAPPING_FILE=/path/to/file.yaml` to use a specific file path (e.g., a ConfigMap mounted at `/config/config`).
* If `DEPENDENCIES_MAPPING_FILE` is not set, we log a warning and skip the dependencies step (no crash).
* If the file cannot be opened, is empty, or has malformed YAML, we log a warning and skip the step (no crash).

Important: The mounted file must contain only the YAML shown below – do NOT wrap it in a `config: |` key. The file content should start with `namespaces:`.

***

### YAML schema (high level)

The detailed specification can be found [here](yaml-dependenices-specification.md).

```yaml
namespaces:
  - <namespace>:
      <workload-name>:
        dependencies:
          kubernetes: []  # list of K8s dependency items
          aws: []         # list of AWS dependency items
          external: []    # list of external dependency items
          source_control: [] # list of source control dependency items
```

* `namespaces` is a list. Each list item maps one namespace to one or more workloads under it.
* `<workload-name>` is a logical workload key. We derive this from pod names by trimming hashes/ordinals, so all pod instances of the same workload share one definition.

Examples of derived workload names:

* Deployment pod: `api-7c9d88f9d9-abc12` → `api`
* StatefulSet pod: `db-0` → `db`

***

### Kubernetes dependencies

These link your pod(s) to existing typed Kubernetes nodes in Neo4j. Supported kinds in v1:

* `KubernetesService`, `KubernetesSecret`, `KubernetesConfigMap`

Item shape:

```yaml
- type: KubernetesService         # Kubernetes Kind (PascalCase)
  name: <k8s-name>
  namespace: <optional; defaults to this namespace>
  protocol: <optional>
  port: <optional int>
  url: <optional>       # for documentation; stored on the relationship
  description: <optional string>
```

Example:

```yaml
kubernetes:
  - type: KubernetesService
    name: neo4j
    namespace: duploservices-andy
    protocol: bolt
    port: 7687
    url: bolt://neo4j.example.net:7687
    description: Graph database used by architecture-diagram
```

Matching behavior:

* We link to existing typed nodes: `(:KubernetesService)`, `(:KubernetesSecret)`, or `(:KubernetesConfigMap)` by `name` + `namespace`.
* If the target doesn’t exist in the graph, we skip and log a warning. We do not create generic K8s nodes in v1.

***

### AWS dependencies

AWS dependencies link your pod(s) to existing typed AWS nodes in Neo4j.

* Use the actual Neo4j label in `type` (e.g., `S3Bucket`, `RDSInstance`).
* Optional `identifier_name` selects the node property to match. Default: `name` for all types.
* Identifier value: by default we use the item’s `name`. If you set `identifier_name`, you can also supply a property with that exact key; when present, it takes precedence over `name`.

Item shapes:

```yaml
# S3 bucket
- type: S3Bucket
  name: <bucket>               # maps to S3Bucket.name (default property)
  identifier_name: name        # optional; explicit for clarity
  region: <optional>
  description: <optional string>

# RDS instance
  - type: RDSInstance
  name: <db_identifier>        # used if db_instance_identifier not provided
  identifier_name: db_instance_identifier
  db_instance_identifier: <db_identifier>
  # optional; when set, used over name
  region: <optional>
  description: <optional string>
```

Example:

```yaml
aws:
  - type: S3Bucket
    name: my-diagrams
    region: us-east-1
    description: Stores rendered diagrams

  - type: RDSInstance
    name: orders-db-prod
    identifier_name: db_instance_identifier
    # db_instance_identifier: orders-db-prod
    # optional; if set, used over name
    region: us-east-1
    description: Primary orders database
```

Matching behavior:

* Generic: `MATCH (n:<type> { <identifier_name or default>: <value> })`
* Examples:
  * S3: `MATCH (b:S3Bucket {name: name})`
* RDS: `MATCH (r:RDSInstance {db_instance_identifier: db_instance_identifier OR name})`
* If the target doesn’t exist, no edge is created (we log for troubleshooting).

Neo4j property mapping rules:

* If `identifier_name` is not set, we match on the default property (`name`) using the item’s `name` value.
* If `identifier_name` is set and a property with that exact key is provided on the item, we use that property’s value; otherwise we fall back to `name`.

***

### External dependencies

External dependencies represent systems outside your cluster/AWS account (or AWS offerings that don’t create resources, like Bedrock/SES).

Item shape:

```yaml
- type: <freeform slug>     # e.g., api, database, cache, queue
  name: <display name>
  url: <url>
  region: <optional>
  inference_profile_arn: <optional>
  description: <optional string>
```

Example:

```yaml
external:
  - type: api
    name: azure-communication-server
    url: https://example.communication.azure.com
    description: Customer notifications via Azure Communication Server

  - type: api
    name: anthropic-claude-sonnet-3.5
    url: https://bedrock.aws.amazon.com
    description: Anthropic Claude Sonnet 3.5 via Application Inference Profile
    region: us-east-1
    inference_profile_arn: arn:aws:bedrock:us-east-1:123456789012:application-inference-profile/abcd

  # (git repositories are modeled under source_control → see section below)
```

Graph behavior:

* We `MERGE` `(:ExternalService {name})` and `MERGE` a `DEPENDS_ON` relationship from the pod. If the pod has `IN_TENANT`, we also `MERGE (ExternalService)-[:IN_TENANT]->(DuploTenant)` so the external system inherits tenant scoping.
* On external relationships, we store helpful fields like `critical`, `description`, `url`, `region`, `inference_profile_arn`, and `service_name`.

Dynamic ExternalService properties:

* In addition to the fields listed above, any extra keys you place on an `external` item are also written to the `ExternalService` node as properties.
* Keys are sanitized to Neo4j-safe names: only letters, numbers, and underscore are kept; everything else becomes `_`.
* Values are normalized:
  * Primitives (string, number, boolean) are stored directly.
  * Lists of primitives are stored as arrays.
  * Complex values (objects, mixed lists) are JSON-serialized into a string for stability.
* Properties are added/updated when present in the YAML. Keys not present in the current YAML are removed on each run (protected keys `name`, `firstseen`, `lastupdated` are preserved).

Example with custom fields:

```yaml
external:
- type: api
  name: partner-billing
  url: https://billing.partner.example
  owner: finance-platform           # custom string → ex.owner
  tier: 1                           # custom number → ex.tier
  tags: [pci, external]             # list of strings → ex.tags
  metadata:                         # object → JSON string → ex.metadata
    contact: ops@partner.example
    sla: gold
```

***

### Source control dependencies

These link your pod(s) to source code repositories.

Item shape (generic SCM):

```yaml
- type: scm
  url: <https-or-ssh-or-git-url>   # REQUIRED
  provider: <optional: github|gitlab|azure_devops|bitbucket|other>
  name: <optional display name>
  description: <optional string>
```

Examples:

```yaml
source_control:
  - type: scm
    url: https://github.com/myorg/myrepo
    provider: github
    name: myorg/myrepo
    description: Main application repository

  - type: scm
    url: git@mygit.example.com:team/service-repo.git
    provider: other
    name: team/service-repo
    description: Self-hosted Git

  - type: scm
    url: https://dev.azure.com/myorg/myproject/_git/myrepo
    provider: azure_devops
    name: myproject/myrepo
```

Example (GitHub):

```yaml
source_control:
  - type: github
    url: https://github.com/myorg/myrepo
    name: myorg/myrepo   # optional
    description: Main application repository
```

Matching behavior:

* We compute a canonical\_url from the provided url (strip `.git`, strip trailing `/`, normalize host to lowercase, convert SSH/SCP forms to `https://host/path`).
* If provider is `github` or the host is `github.com`, we attempt to link to an existing `(:GitHubRepository)` by `url` (http/https) or `giturl` (git/ssh). If none exists, we skip linking (GitHub repositories are created by a separate ingestion).
* Otherwise, we `MERGE` a generic `(:SCMRepository {canonical_url})` node, setting helpful properties like `host`, `provider`, `url`/`giturl` (originals), and `lastupdated`.
* The relationship created is `(:KubernetesPod)-[:DEPENDS_ON {kind:'source_control', type:'scm', provider?, name?, description?, service_name}]->(<repo node>)`. `name` is optional and stored on the relationship when provided.

Notes on canonicalization:

* `git@host:org/repo(.git)?` → `https://host/org/repo`
* `ssh://git@host/org/repo(.git)?` → `https://host/org/repo`
* `git://host/org/repo(.git)?` → `https://host/org/repo`
* Keep path case; lowercase only scheme and host; preserve Azure DevOps `_git` path segment.

***

```yaml
config: |
  namespaces:
    - duploservices-andy:
        k8s:
          dependencies:
            kubernetes:
              - type: KubernetesService
                name: neo4j
                namespace: duploservices-andy
                protocol: bolt
                port: 7687
                url: bolt://neo4j.test10-apps.duplocloud.net:7687
                description: "Graph database used by architecture-diagram"

              - type: KubernetesConfigMap
                name: duplo-cartography
                namespace: duploservices-andy
                description: "Dependencies for architecture-diagram"

              - type: KubernetesSecret
                name: my-k8s-secret
                namespace: duploservices-andy
                description: "GPG passphrase for architecture-diagram"

            aws:
              - type: S3Bucket
                name: duplo-nonprod-awslogs-938690564755
                region: us-east-1
                description: "Stores exported diagrams"

              - type: RDSInstance
                name: duploandy-forcost
                identifier_name: db_instance_identifier
                # db_instance_identifier: duploandy-forcost
                # optional; if set, used over name
                region: us-east-1
                description: "Primary application database"

            external:
              - type: api
                name: azure-communication-server
                url: https://example.communication.azure.com
                description: "Customer notifications via Azure Communication Server"

              - type: bedrock
                region: us-east-1
                name: anthropic-claude-sonnet-3.5
                description: |
                  Anthropic Claude Sonnet 3.5 via Application Inference Profile
                inference_profile_arn: arn:aws:bedrock:us-east-1:938690564755:application-inference-profile/5hli7gcftss9
```

***

When you use our [Architecture Diagram Agent](../../../ai-helpdesk/out-of-the-box-agents.md#architecture-diagram-agent), here is example of what the above example looks like:

<figure><img src="../../../../.gitbook/assets/architecture-diagram-agent (1).png" alt=""><figcaption></figcaption></figure>

### Troubleshooting checklist

* YAML wrapper: The file must start with `namespaces:` – do not wrap with `config: |`.
* Indentation: Keys under list items must be indented two spaces more than the `-` line.
* Workload key: The workload name must match the derived workload from pod names (e.g., `api`, `architecture-diagram`). If in doubt, check logs for `No manifest for pod=` messages.
* K8s targets missing: Ensure the target `Service`/`Secret`/`ConfigMap` exists in Neo4j. Missing targets are logged and skipped.
* AWS linking:
  * S3 uses `name` → `S3Bucket.name`
  * RDS: default is `name` unless you set `identifier_name: db_instance_identifier` (recommended) and optionally provide `db_instance_identifier`.
* External scoping: ExternalService nodes inherit `IN_TENANT` from the pod when present.
* Logging: Enable debug logs to see each mapping decision. Look for lines like `K8s map`, `AWS map`, `External map`, and `SourceControl map` in the logs.

***

### Operational notes

* The ingestion runs even when the manifest is missing or malformed; we log and continue.
* You can change the file path at runtime by setting `DEPENDENCIES_MAPPING_FILE` and re-running.
* We de-duplicate relationships by stable keys and set `lastupdated` on each run.

If you have questions or see skipped targets, copy the relevant log lines and open an issue with the exact pod name, namespace, and the YAML snippet.
