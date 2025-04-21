# Ayra Trust Network RFC: DID Traits

## DID Traits RFC

| Field         | Value                |
|---------------|----------------------|
| **Document Title** | DID Requirements For Ecosystem and Trust Registry DIDs         |
| **Version**         | 1.0                    |
| **Status**          | Draft                  |
| **Author**          | andor.kesselman@ayra.forum       |
| **Last Updated**    | 2025-04-21             |
| **Description**     | Defines required traits for DIDs used as Trust Registry or Ecosystem DIDs. |

---

## 1. Description

This RFC outlines the required and recommended traits for Decentralized Identifiers (DIDs) eligible to be used as **Trust Registry DIDs** or **Ecosystem DIDs** in the Ayra Trust Network. These identifiers anchor core governance functions, schema registries, and verifiable delegation chains within the network. The traits were adapted from the [DID Traits Registry by DIF](https://identity.foundation/did-traits/) and provide a baseline for assessing DID method compatibility at the infrastructure level.

> These traits **do not** apply to entity-level identifiers (e.g., participant DIDs or service-specific DIDs), which may use lighter-weight methods based on local context.

---

## 2. Trait Evaluation Table

| **Trait Name** | **Description** | **Valid?** |
|----------------|-----------------|------------|
| Update supported | Ability to update the DID Document. | [x] |
| Service Endpoints can be updated | Ability to update service endpoints in the DID Document. | [x] |
| Deactivate supported | Ability to deactivate the DID. | [x] |
| Delete supported | Ability to permanently delete the DID and its document. | [x] |
| Transactional Fees | Indicates if operations incur fees (e.g., on blockchains). | [ ] |
| Self-Certifying | DID embeds cryptographic material, enabling self-verification. | [x] |
| Verification Methods can be updated | Ability to update cryptographic keys in the DID Document. | [x] |
| Pre-rotation of Keys | Supports committing to future key rotations securely. | [x] |
| Multi-Signature Verification Method | Supports requiring multiple signatures for operations. | [ ] |
| Human-readable | DIDs are designed to be easily read and remembered by humans. | [ ] |
| Enumerable | All DIDs can be listed or discovered publicly. | [ ] |
| Locally Resolvable | DIDs can be resolved within a local context only. | [ ] |
| Globally Resolvable | DIDs can be resolved from any network location. | [x] |
| DID Document History | Maintains a history of changes to the DID Document. | [x] |
| Cryptographically signed DID Document History | History is maintained in a cryptographically verifiable manner. | [x] |
| Hosting not required | DID Document doesn’t require persistent external hosting. | [x] |
| Centrally Hosted | DID Document is stored on a centralized infrastructure. | [x] |
| Decentrally Hosted | DID Document is stored on a decentralized infrastructure. | [x] |
| Privacy Preserving Crypto – BBS+ | Supports BBS+ signatures for selective disclosure. | [x] |
| Privacy Preserving Crypto – niZKPs | Supports non-interactive zero-knowledge proofs (e.g., zk-SNARKs). | [x] |
| RSA, 2048 bit key size | Supports RSA with 2048-bit keys. | [x] |
| RSA, 3072 bit key size | Supports RSA with 3072-bit keys. | [x] |
| RSA, 4096 bit key size | Supports RSA with 4096-bit keys. | [x] |
| ECDSA, curve secp256k1 | Supports ECDSA using the secp256k1 curve. | [x] |
| ECDSA, curve secp384r1 | Supports ECDSA using the secp384r1 curve. | [x] |
| ECDSA, curve secp512r1 | Supports ECDSA using the secp512r1 curve. | [x] |
| EdDSA, curve ed25519 | Supports EdDSA using the ed25519 curve. | [x] |
| EdDSA, curve ed448 | Supports EdDSA using the ed448 curve. | [x] |
| Brainpool, curve BrainpoolP256r1 | Supports BrainpoolP256r1 curve. | [x] |
| Brainpool, curve BrainpoolP384r1 | Supports BrainpoolP384r1 curve. | [x] |
| Brainpool, curve BrainpoolP512r1 | Supports BrainpoolP512r1 curve. | [x] |
| GOST, curve GOST-256 | Supports GOST-256 curve. | [x] |
| GOST, curve GOST-512 | Supports GOST-512 curve. | [x] |
| SM, curve SM2 | Supports SM2 curve. | [x] |

---

## 3. Scope Clarification

- **Applies To:**
  - Trust Registry DIDs  
  - Ecosystem Authority DIDs  

- **Does Not Apply To:**
  - Organization, Person, or Service-specific DIDs within the ecosystem  
  - Interaction or exchange-layer identifiers that are ephemeral or local-only  

These infrastructure-level DIDs are essential to decentralized policy propagation, schema publication, and credential framework governance.

---

## 4. Current Compatible DID Methods

The following DID methods are considered compatible as of this writing (pending deeper conformance testing):

- `did:webvh`

---
