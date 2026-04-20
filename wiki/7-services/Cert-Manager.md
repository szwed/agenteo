# Cert-Manager

**cert-manager** is a CNCF Graduated project for automated TLS certificate management on Kubernetes.

## Overview

Adds certificates and certificate issuers as first-class resource types in Kubernetes. Automates issuance and renewal from multiple sources.

## CRDs

| CRD | Purpose |
|---|---|
| `Certificate` | Desired certificate specification (DNS names, duration, renewal) |
| `Issuer` | Namespaced certificate issuer configuration |
| `ClusterIssuer` | Cluster-wide certificate issuer |
| `CertificateRequest` | Individual certificate signing request |
| `Order` | ACME order tracking |
| `Challenge` | ACME challenge tracking (HTTP-01, DNS-01) |

## Supported Issuers

- **Let's Encrypt** (ACME) — HTTP-01 and DNS-01 challenges
- **HashiCorp Vault** — PKI secrets engine
- **Venafi** — enterprise certificate management
- **Self-signed** — development and internal use
- **CA** — custom Certificate Authority
- **External** — webhook-based custom issuers

## Key Features

- Automatic certificate renewal before expiry
- Integration with Ingress controllers (annotations-based)
- Integration with service mesh (Istio, Linkerd)
- Certificate lifecycle events and metrics

Related: [[Secrets-Management]] (PKI/ACME), [[Key-Management]].

## Links

- [cert-manager.io](https://cert-manager.io/)
- [GitHub — cert-manager/cert-manager](https://github.com/cert-manager/cert-manager)
