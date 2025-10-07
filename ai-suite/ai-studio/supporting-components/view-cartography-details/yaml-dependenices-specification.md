# YAML Dependenices Specification

## Dependencies Manifest Specification - Version 2

**Document Version:** 2.0\
**Last Updated:** October 3, 2025\
**Status:** Current

***

### Overview

This document specifies the schema, validation rules, and matching behavior for the dependencies manifest YAML format used by duplo-cartography. This manifest allows workloads to declare their runtime dependencies on Kubernetes resources, AWS services, external systems, and source control repositories.

**⚠️ Important:** As of duplo-cartography version 0.5.0 and higher, **Version 1 manifests are no longer supported**. Manifests without `version: 2` will not cause import failures, but dependency items that don't match the Version 2 format will be silently skipped.

***

### Document Structure

#### Top-Level Schema

```yaml
version: <integer>        # OPTIONAL: defaults to 1 if omitted
namespaces:               # REQUIRED: list of namespace entries
  - <namespace-name>:     # namespace identifier
      <workload-name>:    # logical workload/service name
        dependencies:     # dependency declarations
          kubernetes: []
          aws: []
          external: []
          source_control: []
```

#### Field Definitions

| Field        | Type    | Required      | Default | Description                                                                                                      |
| ------------ | ------- | ------------- | ------- | ---------------------------------------------------------------------------------------------------------------- |
| `version`    | integer | Yes (v0.5.0+) | -       | Manifest version number. Must be `2` for v0.5.0+. Omitting or using `version: 1` will cause items to be skipped. |
| `namespaces` | list    | Yes           | -       | List of namespace entries. Each entry is a mapping of namespace name to workloads.                               |

***

### Version Field

#### Specification

* **Type:** Integer
* **Required:** Yes (as of v0.5.0)
* **Required Value:** `2`
* **Legacy Default:** `1` (v1 format, no longer supported)
* **Current Version:** `2`

#### Behavior

* **Version 1 (deprecated as of v0.5.0):**
  * ⚠️ **No longer supported** in duplo-cartography 0.5.0+
  * Items will be silently skipped during import
  * Manifests will not cause errors, but dependencies will not be created
  * Legacy behavior maintained for reference only
* **Version 2 (required):**
  * Kubernetes `type` must match exact Neo4j label (e.g., `KubernetesService`)
  * Dynamic label matching for any K8s resource type
  * Support for `identifier_name` field in kubernetes section
  * Namespace defaulting behavior
  * **Required for all manifests in v0.5.0+**

#### Versioning Strategy

* **v0.5.0+:** `version: 2` is required; omitting `version` or using `version: 1` results in items being skipped
* **v0.4.x and earlier:** Version 1 was the default when `version` field was omitted
* Future versions may introduce additional breaking changes
* Always specify `version: 2` explicitly to ensure compatibility

***

### Namespace & Workload Mapping

#### Workload Name Derivation

Pod names are transformed to logical workload names using these rules:

1. **StatefulSet Pattern:** `name-N` → `name`
   * Example: `worker-0` → `worker`
   * Example: `db-2` → `db`
2. **Deployment Pattern:** Remove last two dash-separated segments
   * Example: `api-7c9d88f9d9-abc12` → `api`
   * Example: `frontend-deployment-xyz` → `frontend`
   * If result ends with `-<digits>`, strip that suffix
3. **Simple Names:** Names with ≤2 segments remain unchanged
   * Example: `simple` → `simple`
   * Example: `a-b` → `a-b`

#### Matching Behavior

* All pods with same derived workload name share one manifest entry
* Workload name is case-sensitive
* Namespace must match exactly

***

### Kubernetes Dependencies

#### Schema

```yaml
kubernetes:
  - type: <string>              # REQUIRED: Neo4j label name
    name: <string>              # REQUIRED: resource identifier value
    namespace: <string>         # OPTIONAL: target namespace
    identifier_name: <string>   # OPTIONAL: property name to match on
    protocol: <string>          # OPTIONAL: protocol (stored on relationship)
    port: <integer>             # OPTIONAL: port number (stored on relationship)
    url: <string>               # OPTIONAL: connection URL (stored on relationship)
    description: <string>       # OPTIONAL: human-readable description
```

#### Required Fields

| Field                             | Validation Rule                        | Error Behavior             |
| --------------------------------- | -------------------------------------- | -------------------------- |
| `type`                            | Non-empty string                       | ERROR logged, item skipped |
| `name` OR `identifier_name` field | At least one must have non-empty value | ERROR logged, item skipped |

#### Optional Fields

| Field             | Type    | Default         | Description                        |
| ----------------- | ------- | --------------- | ---------------------------------- |
| `namespace`       | string  | Pod's namespace | Target resource namespace          |
| `identifier_name` | string  | `"name"`        | Property name to match on in Neo4j |
| `protocol`        | string  | -               | Protocol used for connection       |
| `port`            | integer | -               | Port number for connection         |
| `url`             | string  | -               | Full connection URL                |
| `description`     | string  | -               | Human-readable description         |

#### Matching Logic

1. **Label Matching:**
   * `type` value must exactly match Neo4j label
   * Example: `KubernetesService`, `KubernetesSecret`, `KubernetesConfigMap`
   * Case-sensitive
2. **Property Matching:**
   * Default: Match on `{name: <value>}`
   * With `identifier_name`: Match on `{<identifier_name>: <value>}`
   * Example: `{name: "redis"}` or `{uid: "abc-123"}`
3. **Namespace Matching:**
   * Always matches on `namespace` property
   * Defaults to pod's namespace if not specified
   * Explicit namespace overrides default
4.  **Complete Match Pattern:**

    ```cypher
    MATCH (target:<type> {<identifier_name>: <value>, namespace: <namespace>})
    ```

#### Target Validation

* Targets are validated before relationship creation
* Missing targets logged as WARNING and skipped
* No nodes are created; K8s resources must exist in graph

#### Relationship Properties

Properties stored on `DEPENDS_ON` relationship:

| Property       | Source                | Type               |
| -------------- | --------------------- | ------------------ |
| `kind`         | Fixed                 | `"k8s"`            |
| `type`         | `type` field          | string             |
| `name`         | identifier value      | string             |
| `protocol`     | `protocol` field      | string (nullable)  |
| `port`         | `port` field          | integer (nullable) |
| `url`          | `url` field           | string (nullable)  |
| `description`  | `description` field   | string (nullable)  |
| `service_name` | Derived workload name | string             |
| `firstseen`    | Auto                  | timestamp          |
| `lastupdated`  | Auto                  | timestamp          |

***

### AWS Dependencies

#### Schema

```yaml
aws:
  - type: <string>              # REQUIRED: Neo4j label (e.g., S3Bucket)
    name: <string>              # REQUIRED: resource identifier
    identifier_name: <string>   # OPTIONAL: property to match on
    region: <string>            # OPTIONAL: AWS region
    engine: <string>            # OPTIONAL: database engine (RDS)
    description: <string>       # OPTIONAL: human-readable description
    # ... additional AWS-specific fields ...
```

#### Required Fields

| Field  | Validation Rule                |
| ------ | ------------------------------ |
| `type` | Non-empty string (Neo4j label) |
| `name` | Non-empty string               |

#### Optional Fields

| Field               | Default              | Description               |
| ------------------- | -------------------- | ------------------------- |
| `identifier_name`   | `"name"`             | Property name to match on |
| `region`            | -                    | AWS region code           |
| `engine`            | -                    | Database engine (for RDS) |
| `<identifier_name>` | Falls back to `name` | Explicit identifier value |

#### Matching Logic

1. Match on `{<identifier_name>: <value>}`
2. If `identifier_name` field present in item, use that value
3. Otherwise, fall back to `name` value
4. Example: RDS uses `db_instance_identifier`, S3 uses `name`

#### Relationship Properties

| Property       | Source                |
| -------------- | --------------------- |
| `kind`         | `"aws"`               |
| `type`         | `type` field          |
| `name`         | Unified name          |
| `description`  | `description` field   |
| `service_name` | Derived workload name |
| `firstseen`    | Auto                  |
| `lastupdated`  | Auto                  |

***

### External Dependencies

#### Schema

```yaml
external:
  - type: <string>              # REQUIRED: service type slug
    name: <string>              # REQUIRED: unique service name
    url: <string>               # OPTIONAL: service URL
    region: <string>            # OPTIONAL: region/location
    inference_profile_arn: <string>  # OPTIONAL: AWS Bedrock ARN
    description: <string>       # OPTIONAL: description
    <custom-field>: <any>       # Additional fields allowed
```

#### Required Fields

| Field  | Validation Rule                      |
| ------ | ------------------------------------ |
| `type` | Non-empty string (not `"git"`)       |
| `name` | Non-empty string (unique identifier) |

#### Node Creation

* Creates `(:ExternalService {name: <name>})` node
* All item properties (except internal fields) stored on node
* Properties sanitized: `[^A-Za-z0-9_]` → `_`

#### Property Normalization

| Input Type               | Storage Format |
| ------------------------ | -------------- |
| string, int, float, bool | Direct storage |
| List of primitives       | Array storage  |
| Object, complex types    | JSON string    |

#### Stale Property Cleanup

* Properties present in previous run but not current run are removed
* Protected properties: `name`, `firstseen`, `lastupdated`
* Cleanup uses explicit `SET prop = NULL` (no APOC required)

#### Tenant Scoping

* `ExternalService` inherits `IN_TENANT` relationship from pod
* Backfill: All external services linked to pod's tenant
* Orphaned services: Deleted when no pods reference them

***

### Source Control Dependencies

#### Schema

```yaml
source_control:
  - type: <string>              # REQUIRED: "github" or "scm"
    name: <string>              # OPTIONAL: display name
    url: <string>               # REQUIRED: repository URL
    description: <string>       # OPTIONAL: description
```

#### Required Fields

| Field  | Validation Rule       |
| ------ | --------------------- |
| `type` | `"github"` or `"scm"` |
| `url`  | Non-empty string      |

#### URL Canonicalization

All URLs canonicalized to `https://host/path` format:

| Input Format                  | Canonical Output        |
| ----------------------------- | ----------------------- |
| `git@host:org/repo.git`       | `https://host/org/repo` |
| `ssh://git@host/org/repo.git` | `https://host/org/repo` |
| `git://host/org/repo.git`     | `https://host/org/repo` |
| `https://host/org/repo.git`   | `https://host/org/repo` |

Rules:

* Remove `.git` suffix
* Remove trailing `/`
* Lowercase scheme and host
* Preserve path case
* Preserve provider-specific segments (e.g., `_git` in Azure DevOps)

#### GitHub Matching

* Type `"github"` or host `github.com`: Link to `(:GitHubRepository)`
* Match on `url` (HTTP) or `giturl` (git/ssh)
* No node creation; repositories must exist in graph

#### Generic SCM

* Other providers: Creates `(:SCMRepository {canonical_url: <url>})`
* Properties: `host`, `provider`, `url`, `giturl`, `lastupdated`

***

### Validation Rules

#### Field-Level Validation

| Field                    | Rule                   | Action on Failure            |
| ------------------------ | ---------------------- | ---------------------------- |
| K8s `type`               | Non-empty string       | Log ERROR, skip item         |
| K8s `name` or identifier | At least one non-empty | Log ERROR, skip item         |
| K8s `namespace`          | String or omitted      | Use pod namespace if omitted |
| AWS `type`               | Non-empty string       | Skip item silently           |
| AWS `name`               | Non-empty string       | Skip item silently           |
| External `type`          | Non-empty, not `"git"` | Skip item silently           |
| External `name`          | Non-empty string       | Skip item silently           |
| Source Control `url`     | Non-empty string       | Skip item silently           |

#### Logging Levels

| Event                  | Level   | Format                                                                                                             |
| ---------------------- | ------- | ------------------------------------------------------------------------------------------------------------------ |
| Missing required field | ERROR   | `[DepsIntel] K8s dependency missing required '<field>' field for pod=<name> ns=<ns> workload=<workload>; skipping` |
| Target not found       | WARNING | `[DepsIntel] Skipping N K8s dependencies; targets not found: <type>/<prop>=<value>@<ns>`                           |
| Successful mapping     | DEBUG   | `[DepsIntel] K8s map pod=<name> ns=<ns> workload=<workload> -> type=<type> identifier=<prop>=<value> tgt_ns=<ns>`  |
| File issues            | WARNING | `[DepsIntel] DEPENDENCIES_MAPPING_FILE not set; skipping dependencies mapping.`                                    |

#### Continuation Behavior

* Single item validation failure: Skip item, continue processing
* Multiple failures: Log each, continue processing
* File-level failure: Log warning, skip entire sync
* No pods found: Log info, skip gracefully
* No manifest data: Log info, skip gracefully

***

### Examples

#### Minimal Example (v2)

```yaml
version: 2
namespaces:
  - production:
      api:
        dependencies:
          kubernetes:
            - type: KubernetesService
              name: database
```

#### Complete Example (v2)

```yaml
version: 2
namespaces:
  - staging:
      frontend:
        dependencies:
          kubernetes:
            - type: KubernetesService
              name: backend-api
              port: 8080
              protocol: http
              description: "Backend API service"
            
            - type: KubernetesSecret
              name: oauth-credentials
              namespace: platform  # cross-namespace
              description: "Shared OAuth credentials"
          
          aws:
            - type: S3Bucket
              name: user-uploads-staging
              region: us-east-1
              description: "User uploaded files"
            
            - type: RDSInstance
              name: staging-db
              identifier_name: db_instance_identifier
              db_instance_identifier: staging-db
              region: us-east-1
          
          external:
            - type: api
              name: stripe-payments
              url: https://api.stripe.com
              tier: production
              description: "Payment processing"
          
          source_control:
            - type: github
              name: myorg/frontend
              url: https://github.com/myorg/frontend
```

#### ⚠️ Deprecated Example (v1 - No Longer Supported)

```yaml
# ❌ This format NO LONGER WORKS in v0.5.0+
# Items will be silently skipped during import
namespaces:
  - default:
      worker:
        dependencies:
          kubernetes:
            - type: Service      # v1 format - will be skipped
              name: redis
```

**Must be migrated to:**

```yaml
version: 2  # ✅ Required
namespaces:
  - default:
      worker:
        dependencies:
          kubernetes:
            - type: KubernetesService  # ✅ Exact Neo4j label
              name: redis
```

***

### Implementation Notes

#### Cypher Generation

* **Kubernetes:** Dynamic blocks generated per `(type, identifier_name)` combination
* **AWS:** Dynamic blocks generated per `(type, identifier_name)` combination
* **External:** Single static block with property merging
* **Source Control:** Static blocks for GitHub, generic SCM

#### Neo4j Compatibility

* Target: Neo4j 4.4 (Community)
* No APOC required for core functionality
* Stale property cleanup uses explicit `SET prop = NULL`
* Bulk operations use `UNWIND` for efficiency

#### Performance Considerations

* Pre-validation of targets reduces failed relationship attempts
* Batch processing via `UNWIND`
* Single query execution for all dependency types
* Stale cleanup in separate transaction

***

### Migration from v1 to v2

#### Breaking Changes

**⚠️ As of v0.5.0:** Version 1 manifests are no longer supported. Items in v1 format will be **silently skipped** during import.

#### Required Updates

**All manifests must be migrated to Version 2 format to function in v0.5.0+:**

1. **Add `version: 2` to manifest** (required at top level)
2. **Update K8s `type` values to exact Neo4j labels:**
   * `Service` → `KubernetesService`
   * `Secret` → `KubernetesSecret`
   * `ConfigMap` → `KubernetesConfigMap`
3. **Explicitly set `namespace` for clarity** (or omit to use default)
4. **Use `identifier_name` for custom matching** if needed

#### Example Migration

**Before (v1):**

```yaml
namespaces:
  - prod:
      api:
        dependencies:
          kubernetes:
            - type: Service
              name: db
              namespace: prod
```

**After (v2):**

```yaml
version: 2
namespaces:
  - prod:
      api:
        dependencies:
          kubernetes:
            - type: KubernetesService
              name: db
              # namespace omitted - defaults to pod namespace (prod)
```

***

### Error Handling Reference

#### Common Errors

| Error Message                       | Cause                                           | Resolution                     |
| ----------------------------------- | ----------------------------------------------- | ------------------------------ |
| `missing required 'type' field`     | `type` field missing or empty                   | Add valid `type` field         |
| `missing required identifier`       | Both `name` and `identifier_name` field missing | Add `name` field               |
| `targets not found`                 | K8s resource doesn't exist in graph             | Ensure resource ingested first |
| `DEPENDENCIES_MAPPING_FILE not set` | Environment variable not configured             | Set env var to file path       |
| `is empty; skipping`                | File exists but has no content                  | Add valid YAML content         |
| `Malformed YAML`                    | YAML syntax error                               | Fix YAML syntax                |

#### Debugging

1. Enable DEBUG logging: Set log level to DEBUG
2. Check manifest loading: Look for `Loaded manifest for N namespace/pod entries`
3. Verify workload matching: Check `No manifest for pod=` messages
4. Review mapping logs: Look for `K8s map`, `AWS map`, etc.
5. Check target validation: Look for `targets not found` warnings

***

### Changelog

#### duplo-cartography v0.5.0+ (October 2025)

**Breaking Change:**

* Version 1 manifests no longer supported
* Manifests without `version: 2` will have items silently skipped
* Migration to Version 2 format is now required

#### Version 2.0 (October 2025)

* Added `version` field support
* Kubernetes dependencies now use exact Neo4j labels
* Added `identifier_name` support for Kubernetes (like AWS)
* Namespace defaulting behavior for Kubernetes
* Dynamic Cypher generation for any K8s resource type
* Enhanced validation with ERROR-level logging
* Improved debugging with detailed log messages

#### Version 1.0 (Initial - deprecated)

* Basic manifest support
* Hardcoded K8s types (Service, Secret, ConfigMap)
* AWS dependencies with custom identifiers
* External service tracking
* Source control linking
* **No longer supported as of v0.5.0**

***

**Document Status:** This specification is current and actively maintained. For implementation details, see `src/intel/duplo/dependencies.py`.
