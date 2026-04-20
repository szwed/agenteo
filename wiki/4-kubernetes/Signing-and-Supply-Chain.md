# Signing and Supply Chain Security

Cryptographic signing ensures the integrity and provenance of software artifacts throughout the delivery pipeline. CNOE identifies signing as a core capability for building trust in the software supply chain. ApeiroRA addresses this through [Software Bill of Delivery](../5-software-delivery/Software-Bill-of-Delivery.md) (OCM) and [Security Compliance Automation](../8-platform-mesh/Security-Compliance-Automation.md).

## Why Signing Matters

Without signing, there is no verifiable proof that:
- A container image was built by a trusted CI pipeline
- Source code was not tampered with between commit and deployment
- Dependencies are genuine and unmodified

Supply chain attacks (SolarWinds, Codecov, Log4Shell) demonstrate the consequences of unsigned or unverified artifacts.

## Core Concepts

### Signatures
Cryptographic proof that an artifact (image, binary, manifest) was produced by a specific identity. A signature binds an artifact digest to a signing key.

### Attestations
Structured metadata about how an artifact was produced. Examples:
- Build provenance (who built it, from what source, on what system)
- SBOM (Software Bill of Materials) -- list of all components
- Vulnerability scan results
- Policy compliance checks

Attestations go beyond "who signed it" to answer "what happened during production."

### Trust Telemetry
The chain of signatures and attestations from source to deployment creates a "trust signal" that can be verified at each stage. Each step in the supply chain adds its attestation, building cumulative evidence of artifact integrity.

## Tools

| Tool | Purpose |
|------|---------|
| **Sigstore** | Keyless signing for container images and artifacts. Includes cosign (signing), Rekor (transparency log), and Fulcio (certificate authority). Removes key management burden. |
| **PGP** | Traditional key-based signing. Used for Git commits and package signatures. Requires manual key distribution and management. |
| **PKCS#11** | Hardware security module (HSM) interface for signing. Used when keys must reside in hardware (regulatory requirement). |
| **Notation** | OCI artifact signing from the Notary project. Alternative to cosign for container image signing. |

## Secure Software Supply Chain

A complete supply chain security posture combines:

1. **Source** -- Signed commits (PGP/SSH), branch protection, code review
2. **Build** -- Hermetic builds, build provenance attestation (SLSA framework)
3. **Package** -- Signed container images and artifacts (Sigstore/cosign)
4. **Distribute** -- Signed SBOMs, vulnerability attestations
5. **Deploy** -- Admission control verifies signatures before allowing deployment ([Validation and Policy](Validation-and-Policy.md))
6. **Runtime** -- Continuous monitoring for known vulnerabilities

## Integration with Kubernetes Admission

Signing connects directly to [Validation and Policy](Validation-and-Policy.md):
- Kyverno can verify cosign signatures and attestations as part of admission control
- OPA Gatekeeper can enforce image signing policies
- Only images with valid signatures from trusted builders are admitted to the cluster

This is **binary authorization** -- a deploy-time gate that prevents unsigned or untrusted artifacts from running.

## Relation to ApeiroRA

- **[Software Bill of Delivery](../5-software-delivery/Software-Bill-of-Delivery.md)** -- OCM (Open Component Model) provides a framework for describing, signing, and transporting software artifacts with full provenance metadata.
- **[Security Compliance Automation](../8-platform-mesh/Security-Compliance-Automation.md)** -- Automated compliance checks integrate with signing to produce attestations that satisfy regulatory requirements.
- **[Key Management](../8-platform-mesh/Key-Management.md)** -- Signing keys and certificates are managed through the key management infrastructure.

## CNOE Perspective

CNOE endorses signing as essential for enterprise supply chains but does not mandate a specific tool. Sigstore is the most common choice in the CNCF ecosystem due to its keyless model and transparency log. The pluggability principle applies -- organizations can use Sigstore, Notation, or PGP based on their requirements.

## See Also

- [Software Bill of Delivery](../5-software-delivery/Software-Bill-of-Delivery.md) -- OCM for artifact provenance
- [Security Compliance Automation](../8-platform-mesh/Security-Compliance-Automation.md) -- Compliance attestations
- [Validation and Policy](Validation-and-Policy.md) -- Admission control enforcing signatures
- [Key Management](../8-platform-mesh/Key-Management.md) -- Key infrastructure
- [CI CD](CI-CD.md) -- Signing happens in CI pipelines
- [CNOE](../CNOE.md) -- Framework overview
