# Security

Apeiro integrates security from the start using open-source solutions.

## Sub-Topics

- [[Security-Compliance-Automation]] - ISMS automation with SCF and OCM
- [[Key-Management]] - OpenKCM for encryption key hierarchy and HSM integration
- [[Secrets-Management]] - OpenBao for secrets and PKI
- [[Platform-Mesh-Security]] - AuthN/AuthZ architecture for the Platform Mesh

## CNOE Perspective

CNOE selects **Keycloak** as the identity provider for Identity & Access, supporting OAuth 2.0/OIDC, SAML, and identity brokering/federation (e.g. Active Directory). For machine-to-machine identity, CNOE aligns with mTLS and SPIFFE-based workload identity patterns. Keycloak serves as the SSO gateway for developer portal (Backstage) and CD tools (Argo CD). This directly mirrors Apeiro's Platform Mesh security model, which also centers on Keycloak + OIDC for AuthN/AuthZ across the platform.
