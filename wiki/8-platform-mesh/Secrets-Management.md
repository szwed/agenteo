# Secrets Management

**OpenBao** - identity-based secrets and encryption management system extended with enterprise-grade features.

## Bootstrapping

Stores credentials (e.g. database passwords) for automated provisioning procedures.

Requirements:
- **Auto-unseal** with unseal key stored in HSM
- **PKCS#11** support for HSM access
- **Namespace** support for multi-tenancy
- Disaster recovery for enterprise readiness

## PKI

Central component: Certification Authority (CA) issuing certificates for authentication.

- CA private key stored in HSM (or encrypted with HSM-stored key)
- **ACME protocol** support for automated TLS certificate provisioning
- PKCS#11 extended for digital signatures when private key is in HSM

## CNOE Perspective

CNOE uses **External Secrets Operator** (ESO) as the Kubernetes-native bridge to secret repositories (Vault, AWS Secrets Manager, cloud KMS). This shifts secret lifecycle responsibility to the platform -- secrets are synced from external stores into K8s secrets automatically. The lifecycle covers promotion across environments, distribution to clusters, rotation, and revocation. CNOE's secret repos integrate with HSM-backed stores and PKI (e.g. cert-manager for TLS certificates synced via ESO). This complements Apeiro's OpenBao approach: OpenBao provides the identity-based secrets engine and HSM/PKI backend, while ESO handles the Kubernetes integration layer that CNOE standardizes.

See also: [[Security]], [[Key-Management]]
