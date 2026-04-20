# Backstage Plugins (CNOE)

CNOE has developed and contributed several open-source Backstage plugins that integrate the [[Developer-Portal]] with cloud-native technologies and workflows.

## Available Plugins

| Plugin | Repository | Description |
|--------|-----------|-------------|
| **Terraform Plugin** | [cnoe-io/plugin-terraform](https://github.com/cnoe-io/plugin-terraform) | Displays Terraform outputs and resources from TFState files associated with Backstage components. Connects the developer portal to [[Infrastructure-as-Code]] visibility. |
| **Argo Workflows Plugin** | [cnoe-io/plugin-argo-workflows](https://github.com/cnoe-io/plugin-argo-workflows) | Displays Argo Workflows execution status and details within Backstage. Integrates [[CI-CD]] workflow visibility into the portal. |
| **Scaffolder Actions Plugin** | [cnoe-io/plugin-scaffolder-actions](https://github.com/cnoe-io/plugin-scaffolder-actions) | Extended actions for the Backstage Scaffolder, including `cnoe:kubernetes:apply` (deploy manifests to clusters) and `cnoe:utils:sanitize` (sanitize YAML documents). Enables custom scaffolding workflows. |
| **Scaffolder Frontend Plugin** | [cnoe-io/plugin-scaffolder-actions-frontend](https://github.com/cnoe-io/plugin-scaffolder-actions-frontend) | Provides the `KubernetesClusterPicker` UI field for displaying and selecting Kubernetes clusters configured in Backstage. |
| **Apache Spark Plugin** | [cnoe-io/plugin-apache-spark](https://github.com/cnoe-io/plugin-apache-spark) | Displays information about Apache Spark Applications running on Kubernetes, integrated into Backstage entity pages. |

## How They Extend the Developer Portal

These plugins follow the Backstage plugin architecture:

- **Backend plugins** (Scaffolder Actions) add new capabilities to the template engine -- deploying Kubernetes manifests, running verifications, sanitizing YAML
- **Frontend plugins** (Cluster Picker, Spark, Terraform, Argo Workflows) add UI components to entity pages and template forms, giving developers visibility into infrastructure state without leaving the portal
- **Verification integration** -- The Scaffolder Backend can invoke [[CNOE-CLI]] verification checks as a step in template workflows, halting execution if prerequisites are not met

## See Also

- [[Developer-Portal]] -- Backstage developer portal overview
- [[CNOE]] -- Framework overview
- [[CNOE-CLI]] -- Template generation and verification tools
