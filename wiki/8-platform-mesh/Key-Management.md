# Key Management

**OpenKCM** - open-source Key Management solution for encryption of data at rest across the Apeiro Reference Architecture.

## Concepts

HSM (Hardware Security Module) stores root keys securely. Keys form a hierarchy (keychain) where each key is wrapped by a higher-level key up to the HSM-protected root.

### Key Levels

- **Level 1 (Root keys)** - customer-managed, BYOK/HYOK capabilities, HSM-protected
- **Level 2-4** - Key Encryption Keys (KEKs) managed by OpenKCM's Krypton layer

OpenKCM extends the keychain concept across multiple clusters and heterogeneous infrastructure providers.

## Architecture

- **HSM integration** - connects HSMs from different providers (on-premise and cloud); plugin mechanism for additional providers
- **CMK (Level 1)** - manages root keys protected by HSM; BYOK and HYOK support
- **Krypton** - manages L2-L4 key hierarchy; key assignment, rotation, and disabling
- **Infrastructure integration** - connects to providers like IronCore and CobaltCore (block/object storage); plugin mechanism for extensions

See also: [Security](Security.md), [Platform Mesh Account Model](Platform-Mesh-Account-Model.md)
