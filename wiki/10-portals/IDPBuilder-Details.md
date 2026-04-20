# IDPBuilder Details

Technical details for IDPBuilder -- installation, security, networking, OCI registry, Gitea integration, and customization. For the high-level overview and reference stack, see [[IDP-Reference-Implementation]].

## Installation

Requires a container engine: Docker Desktop is supported. Podman requires rootful mode and setting `DOCKER_HOST` (e.g., `export DOCKER_HOST="unix:///var/run/docker.sock"`).

**Bash script:**
```bash
curl -fsSL https://raw.githubusercontent.com/cnoe-io/idpbuilder/main/hack/install.sh | bash
```

**Manual installation:**
```bash
version=$(curl -Ls -o /dev/null -w %{url_effective} https://github.com/cnoe-io/idpbuilder/releases/latest)
version=${version##*/}
curl -L -o ./idpbuilder.tar.gz "https://github.com/cnoe-io/idpbuilder/releases/download/${version}/idpbuilder-$(uname | awk '{print tolower($0)}')-$(uname -m | sed 's/x86_64/amd64/').tar.gz"
tar xzf idpbuilder.tar.gz
```

**Release page:** Download binaries directly from [cnoe-io/idpbuilder releases](https://github.com/cnoe-io/idpbuilder/releases).

**Codespaces:** Supported with `--use-path-routing` and `--protocol http` flags since Codespaces provides a single routable hostname.

## Security

### Self-Signed Certificates

IDPBuilder creates a wildcard TLS certificate for the configured domain (default: `cnoe.localtest.me` and `*.cnoe.localtest.me`). This certificate is:
- Set as the default TLS certificate for ingress-nginx
- Imported into ArgoCD as a trusted CA (so ArgoCD can talk to Gitea over TLS)
- Stored as a Kubernetes secret: `kubectl get secret -n default idpbuilder-cert`

You can override the TLS certificate at the Ingress level by specifying a `tls.secretName` on individual Ingress objects.

### Retrieving Secrets

```bash
idpbuilder get secrets          # all relevant secrets
idpbuilder get secrets -p gitea # secrets for a specific package
```

This retrieves ArgoCD admin password, Gitea admin credentials, and any secrets labeled `cnoe.io/cli-secret=true`. To make a custom secret discoverable, label it:

```bash
kubectl label secret my-secret "cnoe.io/package-name=foo" "cnoe.io/cli-secret=true"
```

## Networking

### DNS Configuration

**External:** The default domain `cnoe.localtest.me` (and subdomains) resolves to `127.0.0.1` via [localtest.me](https://readme.localtest.me/).

**In-cluster (CoreDNS):** IDPBuilder configures CoreDNS rewrite rules so that in-cluster pods resolve `*.cnoe.localtest.me` to the ingress-nginx service instead of the pod's own loopback:

```
rewrite name regex (.*).cnoe.localtest.me ingress-nginx-controller.ingress-nginx.svc.cluster.local
rewrite name exact cnoe.localtest.me ingress-nginx-controller.ingress-nginx.svc.cluster.local
```

Two ConfigMaps are created: `coredns-conf-default` (managed by IDPBuilder) and `coredns-conf-custom` (empty, for user extensions).

### Traffic Flow

1. Domain resolves to loopback (`127.0.0.1`)
2. Request hits host port 8443, forwarded to Kind container port 443
3. Ingress-nginx (NodePort on 443) routes by SNI/host header to the target service

### Routing Modes

- **Domain-based** (default): Services at `argocd.cnoe.localtest.me`, `gitea.cnoe.localtest.me`, etc.
- **Path-based** (`--use-path-routing`): All services under one domain -- `cnoe.localtest.me/argocd`, `cnoe.localtest.me/gitea`. Required for GitHub Codespaces and similar single-hostname environments.

## Local OCI Registry

The Gitea instance includes a built-in OCI-compliant container registry.

**Push images:**
```bash
docker login gitea.cnoe.localtest.me:8443
docker tag myimage:latest gitea.cnoe.localtest.me:8443/giteaadmin/myimage:latest
docker push gitea.cnoe.localtest.me:8443/giteaadmin/myimage:latest
```

**Tagging convention:** `{registry}/{owner}/{image}` -- enforced by Gitea (e.g., `gitea.cnoe.localtest.me:8443/giteaadmin/ubuntu:24.04`).

**Pull images:** Anonymous read access is enabled. No pull secret needed.

**In-cluster access:** containerd is configured to rewrite image names so that pods can reference images at the external URL (`gitea.cnoe.localtest.me:8443/...`) even though the ingress is not directly reachable from inside the cluster. See the [Kind config template](https://github.com/cnoe-io/idpbuilder/blob/main/pkg/kind/resources/kind.yaml.tmpl).

**Transferring images:** Tools like [ORAS](https://oras.land) or [regclient](https://github.com/regclient/regclient) can copy images between remote registries and the local registry. Useful for pre-loading images before going offline.

## Gitea Integration

IDPBuilder creates an internal Gitea server with an administrator-scoped token stored as a Kubernetes secret.

```bash
# Retrieve the token
idpbuilder get secrets -p gitea -o json | jq -r '.[0].data.token'
```

The token can be used to create organizations, users, and repositories via the Gitea API. The `cnoe://` prefix in ArgoCD Application specs triggers IDPBuilder to create Gitea repos and push local manifests automatically.

## Custom Packages

The `-p` flag adds custom ArgoCD Application packages. The `cnoe://` prefix in `spec.source.repoURL` signals local directory sync:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
spec:
  source:
    repoURL: cnoe://manifests  # relative path from this file
```

IDPBuilder creates a Gitea repo, pushes the contents, and updates the Application to point at it.

## ArgoCD ConfigMap Customization

Override core package manifests with the `-c` flag:

```bash
idpbuilder create -c argocd:/tmp/argocd-cm.yaml
```

This replaces only the specified resource (e.g., `argocd-cm` ConfigMap) while keeping all other built-in manifests. The `-c` flag accepts `argocd`, `nginx`, or `gitea` as package names. The `--package-custom-file` flag provides the same capability.

## See Also

- [[IDP-Reference-Implementation]] -- Reference stack overview
- [[IDPBuilder-Stacks]] -- Available community stacks
- [[CNOE]] -- Framework overview
