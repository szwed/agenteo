# CNOE CLI

The CNOE CLI streamlines Internal Developer Platform workflows by converting Kubernetes CRDs, Crossplane XRDs, and Terraform modules into [[Developer-Portal|Backstage]] templates. It also provides verification tooling to check cluster readiness before deploying resources.

Install from [cnoe-io/cnoe-cli](https://github.com/cnoe-io/cnoe-cli).

## Template Generation from CRDs/XRDs

`cnoe template crd` converts CRD and XRD definitions into Backstage scaffolder templates.

```bash
cnoe template crd \
  --inputDir examples/ack-crds \
  --outputDir /tmp/templates-ack-deploy \
  --templatePath config/templates/k8s-apply-template.yaml \
  --templateName deploy-ack-resource \
  --templateTitle "Deploy ACK Resource" \
  --templateDescription "Deploy ACK Resource to Kubernetes" \
  -c
```

Key flags:
- `-i, --inputDir` -- directory containing CRD/XRD YAML files
- `-o, --outputDir` -- where generated templates are written
- `-t, --templatePath` -- base Backstage scaffolder template to augment
- `-c, --collapse` -- render all items as a dropdown in a single template
- `--depth` -- search depth for CRDs (default 2)
- `-v, --verifier` -- list of verifiers to test the resource against
- `-p, --insertAt` -- jq path for insertion (default `.spec.parameters[0]`)

**Example: ACK CRDs** -- The [cnoe-cli examples](https://github.com/cnoe-io/cnoe-cli/tree/main/examples/ack-crds) contain ~120 Amazon Controllers for Kubernetes CRDs. Running the command above generates a template with all ACK resources available as a selectable dropdown in Backstage. Each resource exposes its full set of configurable properties with validation.

## Template Generation from Terraform

`cnoe template tf` generates Backstage input fields from Terraform module variables.

```bash
cnoe template tf \
  -i /tmp/data-on-eks/analytics/terraform/spark-k8s-operator \
  -t /tmp/ref-impl/examples/template-generation/data-on-eks.yaml \
  -p '.spec.parameters[0].properties.tfVars' \
  -o .
```

Key flags: same global flags as `crd` subcommand (`-i`, `-o`, `-t`, `-p`, `-c`, `--depth`).

**Example: Data on EKS** -- Converts Terraform variables from the [Data on EKS](https://github.com/awslabs/data-on-eks) repository into Backstage form fields. The tool reads `variables.tf`, extracts variable names/types/defaults/descriptions, and populates the specified insertion point in the template.

## Kubernetes Verification

`cnoe k8s verify` checks that required CRDs and operators exist and are running on a target cluster before deploying resources.

```bash
cnoe k8s verify --config config/prereq/ack-s3-prerequisites.yaml
```

Flags:
- `-c, --config` -- prerequisite configuration files (can specify multiple)
- `-k, --kubeconfig` -- path to kubeconfig (default `~/.kube/config`)

**Prerequisite spec example:**

```yaml
apiVersion: cnoe.io/v1alpha1
kind: Prerequisite
metadata:
  name: ack-s3
spec:
  pods:
  - name: ack-release-s3
    namespace: ack-system
    state: Running
  crds:
  - group: s3.services.k8s.aws
    version: v1alpha1
    kind: Buckets
```

Verifications can also run inside Backstage via the Scaffolder Backend Plugin, halting the workflow on failure. Full prerequisite specs are in the [cnoe-cli config/templates](https://github.com/cnoe-io/cnoe-cli/tree/main/config/templates) directory.

## See Also

- [[Developer-Portal]] -- Backstage developer portal
- [[IDP-Reference-Implementation]] -- CNOE reference stack
- [[Backstage-Plugins]] -- CNOE-developed Backstage plugins
