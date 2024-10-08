---
status: proposed
date: 2024-09-23T17:21
decision-makers:
  - Andor Kesselman
consulted:
  - Darrell O'Donnell
informed: []
created: 2024-09-18T13:43
updated: 2024-09-25T10:50
---

# Use LDP-VC and DIDComm v1 for the first message-centric Verifiable Credential Exchange Technical Interop Profile

## Context and Problem Statement

- We need to select an initial technical interop profile to establish conformance testing.
- The selected profile must have a reference implementation or system that can be used or instructed to test other systems against it.
- The profile must ensure that all necessary components are included to facilitate the successful exchange of verifiable data between systems.
- An existing example is the Aries Agent Test Harness, which supports interoperability testing for systems like Aries Cloud Agent Python (ACA-Py).
- ACA-Py currently supports AnonCreds v1 and DIDComm v1, using various Aries RFCs from the Aries Interop Profile (e.g., version 1.0 and version 2.0).
- This decision focuses on message-centric protocols (e.g., DIDComm v1) and credential formats (e.g., AnonCreds v1), with a view toward expanding support for other formats and protocols as needed.
- Some of the challenges include ensuring compatibility with existing systems and protocols, and balancing simplicity with feature completeness in the selected profile.
- This decision will lay the groundwork for future upgrades to DIDComm v2 and support for newer credential formats like SD-JWT-VC or LDP-VC as the ecosystem evolves.
- This decision impacts technical teams responsible for interoperability, product management, and system implementers who need to ensure their systems conform to the chosen profile.

### Background and Terminology Alignment

The objective of this section is to establish a common framework for discussing the dimensions and properties of interoperability—defining the key elements that must be aligned to ensure systems can work together seamlessly.

### Glossary

- Abstract Data Model
	- A high-level conceptual framework that defines the structure and relationships of the core components in a system, such as issuer, subject, claims, and proofs in Verifiable Credentials. It describes what data must be present but does not specify how it is formatted or transmitted.
- Credential Format
	- The specific way that credential data from the abstract model is structured and serialized for storage, transmission, or communication between systems. Different formats (e.g., AnonCreds, LDP-VC, JWT-VC) offer varying levels of security, privacy, and compatibility depending on the use case and underlying cryptographic methods.
- Data Representation or Encoding
	- Refers to how the credential’s data is serialized or represented for transmission. Common encoding formats include JSON, JWT, SD-JWT, CBOR, and JSON-LD. These formats dictate how the data is structured, whether as a compact binary format like CBOR or a more human-readable format like JSON.
- Credential Exchange and Lifecycle Standards
	- These standards define how verifiable credentials are requested, issued, presented, and verified across different systems and protocols. They establish common frameworks to ensure interoperability and security between credential issuers, holders, and verifiers. Unlike specific transport protocols (such as DIDComm or OIDC), these standards are often agnostic to the underlying transport mechanism and can be implemented in various environments.
- Transport and Credential Exchange Protocols
	- The mechanisms or protocols that allow Verifiable Credentials and Presentations to be securely transmitted between entities (such as issuers, holders, and verifiers). Examples include OIDC (OpenID Connect), DIDComm v1 and v2, which handle the secure exchange of credentials over the web or peer-to-peer networks.
- Data Integrity and Cryptographic Assurance (Proof and Signing)
	- This encompasses the cryptographic mechanisms used to ensure that data within a credential is valid, tamper-proof, and can be trusted. This includes proof mechanisms like Linked Data Proofs (LD-PROOF), CL Signatures, BBS+ Signatures, and standards like Verifiable Credential Data Integrity 1.0.
- Revocation Mechanism or Status List
	- Mechanisms used to determine whether a credential has been revoked or remains valid. This could involve revocation registries, status lists, or privacy-preserving revocation techniques to ensure that only valid credentials are used.
- Key Management and Identifiers
	- Involves the management of cryptographic keys and identifiers, such as DIDs (Decentralized Identifiers), which are associated with credentials. This ensures secure storage, key rotation, and cryptographic operations tied to the identity of the issuer, holder, or verifier.
- Command Interfaces
	- These are standardized interfaces that allow for issuing, verifying, and interacting with Verifiable Credentials programmatically. For example, VC-API defines HTTP-based interfaces to manage credential issuance and verification across platforms.
- Misc
	- Other properties or dimensions of interoperability that don't fit in the other categories defined above

### Examples

- Abstract Data Model
	- Verifiable Credential Data Model 1.0
		- The original W3C standard for defining the components of a Verifiable Credential, such as issuer, subject, claims, and proof.
	- Verifiable Credential Data Model 1.1
		- An updated version of the VCDM 1.0, with improvements for interoperability and the inclusion of new features such as more robust proof mechanisms and privacy enhancements.
	- Verifiable Credential Data Model 2.0
		- The next generation of the VCDM, focusing on more advanced privacy features, such as selective disclosure, and integration with decentralized identity ecosystems like DID.
- Credential Format
	- AnonCreds
		- A privacy-preserving credential format used in Hyperledger Indy ecosystems, focused on selective disclosure and zero-knowledge proofs. It supports CL Signatures for privacy features.
	- LDP-VC (using VCDM and JSON-LD)
		- A Verifiable Credential format that uses Linked Data Proofs (LD-PROOF) for cryptographic assurance. It is typically encoded in JSON-LD and is aligned with the W3C Verifiable Credential Data Model.
	- MDOC
		- A mobile driver's license (mDL) standard based on ISO/IEC 18013-5, used for digital identification on mobile devices. It supports offline and online verification with cryptographic proofs.
	- JWT-VC
		- A Verifiable Credential format using JSON Web Tokens (JWT). Commonly used in web environments, it relies on JWS (JSON Web Signatures) for cryptographic proofs.
	- SD-JWT-VC
		- A combination of SD-JWT with the Verifiable Credential Data Model, allowing selective disclosure within the structure of a W3C Verifiable Credential.
	- x509
		- A widely used certificate format, typically for public key infrastructure (PKI) systems. It is used for digital certificates, such as SSL/TLS certificates, and can be adapted for use with Verifiable Credentials.
- Data Representation or Encoding
	- CBOR
		- A binary format (Concise Binary Object Representation) that provides efficient encoding of data. It is useful for environments with limited resources, such as IoT devices.
	- JSON
		- A lightweight text-based data interchange format, commonly used in web applications. It is the basis for formats like JWT.
	- JSON-LD
		- A JSON-based format for representing Linked Data. It allows data to be linked across different contexts, making it useful for decentralized identity and Verifiable Credentials.
		- Can be secured using JWS
	- JWT
		- An encoding format used to securely transmit information between parties (not just credentials but widely used as a compact token format efficient for web transactions)
	- SD-JWT
		- A selective disclosure version of JWT, allowing holders to reveal only certain parts of the JWT, while maintaining venerability through cryptographic proofs but in itself is not a credential (can reveal claims within the JWT token)
- Credential Exchange and Lifecycle Standards
	- These standards are designed to be independent of Transport and Credential Exchange protocols (listed below) however, many are targeted towards newer protocols and may not be easily implemented
	- Dencentralized Identity Foundation (DIF) Presentation Exchange
		- A specification from the DIF that standardizes how verifiable credentials are requested and presented. It defines the data model for a presentation request and how a holder can provide a presentation response using credentials they possess.
		- This standard is transport-agnostic and can be used with protocols such as OIDC, DIDComm, and **CHAPI**, enabling flexibility in its implementation.
	- Hyperledger Indy Proof Request
		- A mechanism within the Hyperledger Indy ecosystem used to request and verify AnonCreds. The proof request specifies which attributes or claims should be revealed from the holder’s credential, supporting selective disclosure and privacy-preserving proofs.
	- Hyperledger AnonCreds Proof Request
		- Focused on AnonCreds in self-sovereign identity (SSI) systems. It allows verifiers to request a proof of specific claims from the holder’s credentials, while allowing the holder to reveal only the necessary information without exposing the full credential.
	- WACI-DIDCcomm (Wallet and Credential Interaction)
		- An interaction model that standardizes how wallets and credential issuers/verifiers interact over DIDComm. It defines flows for credential issuance and presentation, focusing on interoperability between digital wallets and identity systems.
	- CHAPI (Credential Handler API)
		- A browser-based API that facilitates credential issuance and presentation in a user-friendly way. It allows users to select a digital wallet to securely present credentials when requested by a website or service. CHAPI is designed to work with verifiable credentials following the W3C Verifiable Credential Data Model, making it part of the decentralized identity stack.
		- It interacts with protocols like DIDComm to enable secure exchanges of credentials, focusing on user experience during credential presentation.
- Transport and Credential Exchange Protocols
	- OIDC
		- OpenID Connect (OIDC) is an identity layer built on top of the OAuth 2.0 protocol, enabling the verification of an end-user’s identity based on authentication performed by an authorization server. It also allows for secure, structured information (claims) about the user to be shared between parties. OIDC is widely used for Single Sign-On (SSO)
		- Credential Exchange Protocols
			- 4VC
				- OpenID Connect for Verifiable Credentials (4VC) is an extension of OIDC, enabling the secure issuance and exchange of Verifiable Credentials.
			- 4VP
				- OpenID Connect for Verifiable Presentations (4VP) is another OIDC extension that allows holders to present Verifiable Credentials to verifiers securely.
	- DIDComm
		- v1
			- The first version of the Decentralized Identifier Communication protocol, allowing secure and privacy-respecting peer-to-peer messaging between parties.
			- Credential Exchange Protocols
				- Issue Credential v1:
					- The initial Aries protocol for issuing verifiable credentials. It allows issuers to securely issue credentials to holders through a series of predefined steps, including offering, requesting, and receiving credentials.
					- This protocol follows a relatively simple flow, but it lacks advanced features such as the ability for selective disclosure or more sophisticated credential lifecycle management.
				- Present Proof v1:
					- The first version of the Present Proof protocol allows verifiers to request proofs of credentials from holders. Holders can present verifiable proofs, such as identity claims or other credential-based information.
					- While it supports basic proof requests, it does not handle more complex proof scenarios, such as combining multiple credentials or handling more detailed restrictions on proofs.
		- v2
			- The updated version of the protocol with enhanced support for Verifiable Credentials and Presentations. It introduces better handling of credential exchanges, allowing for more secure, flexible, and complex presentation requests.
			- DIDComm V2.x supports multiple compatibility profiles, each specifying additional mechanisms that must align in order to communicate. This includes:
				- Type of service endpoint
				- Key types use for encryption and/or signing
				- Format of encryption and/or signing envelopes
				- Encoding of plain text messages
				- Protocol used for forward and route
				- The protocol embodied in the plain text message
			- Credential Exchange Protocols (these protocols are backward-compatible with v1 but may be subject to some limitations):
				- Issue Credential v2:
					- The updated protocol for issuing verifiable credentials, improving security and adding more sophisticated features. It supports credential lifecycle management (e.g., revocation) and allows for selective disclosure, where credential holders can choose which attributes to share.
					- It also supports a wider variety of credential formats and provides better compatibility with new and emerging standards for verifiable credentials.
				- Present Proof v2:
					- The upgraded Present Proof protocol allows for more complex proof requests, including combining multiple credentials in a single proof and adding more flexibility in how proofs are generated and verified.
					- This version offers better support for privacy-preserving features like selective disclosure and improves security and trust by allowing verifiers to specify stricter proof requirements.
- Data Integrity and Cryptographic Assurance (Proof and Signing)
	- Proof Standards
		- Linked Data Proofs (LD-PROOF)
			- A cryptographic proof mechanism primarily used with JSON-LD data. It ensures the integrity and authenticity of data through cryptographic signatures, commonly applied in LDP-VC credentials. LD-Proofs support various cryptographic algorithms, such as Ed25519 for fast and secure signatures, and BBS+ for selective disclosure.
		- Verifiable Credential Data Integrity 1.0
			- A W3C standard for applying cryptographic data integrity proofs to Verifiable Credentials, regardless of their format (e.g., JSON, JSON-LD). It supports multiple cryptographic suites, including Ed25519 and BBS+, enabling secure and tamper-evident credentials.
	- Cryptographic Algorithms
		- CL Signatures
			- A signature scheme used in AnonCreds to provide privacy-preserving credentials. It supports selective disclosure and zero-knowledge proofs, allowing the holder to reveal only specific parts of their credential while proving its authenticity.
		- BBS+ Signatures
			- A cryptographic scheme that allows for selective disclosure in Verifiable Credentials. With BBS+, a credential holder can reveal specific claims without exposing the entire credential, preserving privacy.
		- EdDSA
			- The Edwards-curve Digital Signature Algorithm, used with cryptographic curves like Ed25519. This signature scheme is known for being fast, secure, and space-efficient, making it popular in environments that use Linked Data Proofs and other cryptographic protocols for Verifiable Credentials.
	- Envelope or Encoding Signatures
		- JSON Web Signature (JWS)
			- Signature technology used to sign JWT and SD-JWT tokens. It ensures the integrity and authenticity of the data contained within these tokens.
			- JWS does not interact with the credentials themselves but rather applies to the envelope that wraps the credentials, ensuring they are securely transmitted without tampering.
- Revocation Mechanism or Status List
	- Status List 2021
    	- A revocation mechanism defined by the W3C for Verifiable Credentials. It allows issuers to revoke or suspend credentials by maintaining a list of credential statuses in a verifiable and privacy-preserving manner. Each credential is associated with a status entry, which is published in a machine-readable format that verifiers can query without disclosing which credential is being checked.
	  	- Indy Revocation
    	- The revocation mechanism used in Hyperledger Indy and AnonCreds. It provides a way for credential issuers to revoke credentials using a cryptographic accumulator, which allows for efficient revocation checks without revealing private information. Verifiers can check the revocation status of a credential by querying the accumulator, ensuring that only valid, non-revoked credentials are accepted.
- Key Management and Identifiers
	- did:web
		- Uses Domain Name System (DNS) to perform DID operations
	- did:tdw - Trust-Domain Web
		- Enhancement of the did:web DID method, providing addittional features which enable greater trust and security
	- did:key
		- A self-contained DID method where the entire identifier is derived from a cryptographic key pair.
- Command Interfaces
	- VC-API
		- The Verifiable Credentials API (VC-API) defines standardized HTTP interfaces that allow for the issuing, verifying, and presenting of Verifiable Credentials across various systems. It abstracts the complexities of credential management, enabling the easy integration of Verifiable Credentials into existing web services. VC-API enables smooth credential exchanges between issuers, holders, and verifiers while maintaining security and interoperability.
- Misc
	- Overlay Capture Architecture (OCA)
		-  A framework which can be used to standardize the visual presentation of verifiable credentials as well as define other meta data (such as categoriation or classification system). OCA enables data to be displayed in a customizable, human-readable format without altering its core structure or cryptographic integrity. This ensures that credentials can be presented in various formats across systems while maintaining consistent data representation for interoperability and user-friendly experiences.

## Decision Drivers

- Availability - Ability to find a reference system to use for testing for the given profile
- Adoption - picking something that enables many systems to work together now
- Simplicity - picking something that's easy to implement now where we can focus our energy on the extensibility into future components
- Feature complete - picking something that can do everything the industry expects as table stakes features

## Considered Options

The following options are supported in the available reference systems of `ACA-Py` and `credo-ts`

- Credo supports
	- LDP-VC and JWT-VC (both using VCDM 1.1)
		- LDP-VC uses JSON-LD with LD-Proof
		- JWT-VC uses JWT and JWS
	- SD-JWT-VC
	- AnonCreds
	- Only supports verification only (not issuance) over DIDComm for JWT-VC and and SD-JWT-VC
	- Support for OIDC is experimental but this works with JWT-VC and SD-JWT-VC
- ACA-Py Supports
	- AnonCreds (in AnonCreds original as well as in VCDM 1.1 and VCDI)
	- LDP-VC with VCDM 1.1 and the DIF Presentation Exchange Standard

The following are therefore two possible Technical Interoperability Profiles:

- Linked-Data-Proof Verifiable Credentials (LDP-VC)
	- Abstract Data Model
		- Verfiable Credential Data Model 1.1
	- Credential Format
		- LDP-VC
	- Data Representation or Encoding
		- JSON-LD
	- Credential Exchange and Lifecycle Standards
		- DIF Presentation Exchange
	- Transport and Credential Exchange Protocols
		- DIDComm v1 with
			- Aries RFC 0023 DIDExchange
			- Aries RFC 0453 Issue Credential v2
			- Aries RFC 0454 Present Proof v2
	- Data Integrity and Cryptographic Assurance (Proof and Signing)
		- Proof Standard
			- LD-Proofs
		- Cryptographic Signature
			- Ed25519 Signature 2018
	- Revocation Mechanism or Status List
	- Key Management and Identifiers
		- DID Method
			- did:key
	- Command Interfaces
- AnonCreds v1
	- Abstract Data Model
		- AnonCreds
	- Credential Format
		- AnonCreds
	- Data Representation or Encoding
		- Binary encoding (ZKP-based cryptographic structure)
	- Credential Exchange and Lifecycle Standards
		- AnonCreds 1.0 Specification
	- Transport and Credential Exchange Protocols
		- DIDComm v1 with
			- Aries RFC 0023 DIDExchange
			- Aries RFC 0453 Issue Credential v2
			- Aries RFC 0454 Present Proof v2
	- Data Integrity and Cryptographic Assurance (Proof and Signing)
		- Proof Standard
			- Zero-Knowledge Proof (ZKP)
		- Cryptographic Signature
			- CL Signatures (Camenisch-Lysyanskaya)
	- Revocation Mechanism or Status List
		- Indy Revocation - Revocation using cryptographic accumulators
	- Key Management and Identifiers
		- DID Method
			- did:sovrin
			- did:indy
			- did:peer
	- Command Interfaces
		- Aries protocols through ACA-Py (Aries Cloud Agent Python)

## Decision Outcome

Chosen option: LDP-VC, as it is widely adopted and does not depend on the Indy blockchain. While the AnonCreds option may provide additional privacy features, its reliance on Indy is considered unnecessary overhead at this initial stage of conformance testing.

### Consequences

- Good, because you don't have to run an Indy network node in order to be technically interoperable (as a specific verifiable data registry).
- Good, because the profile allows for more possible combinations/ways to implement, for example, being ledger-agnostic and hosting Status List 2021 at different locations.
- Bad, because the profile we have selected does not support selective disclosure.

### Confirmation

This ADR can be confirmed through the implementation of the conformance test suite and use of the Aries Agent Test Harness (AATH)

The tests that need to pass for this to be confirmed can be listed using the AATH `dry-run` command and specifying the tags which constrain the test run to the interop profile criteria.

To run, change the `dry-run` command to `run`.

#### AnonCreds

Example `dry-run` command

```bash
./manage dry-run -d acapy -t @RFC0023,@RFC0453,@RFC0454,@Anoncreds -t ~@CredFormat_JSON-LD -t @critical -t ~@RFC0793 -t ~@RFC0434
```

The output should look as follows:

```bash
Tags:  --tags=@RFC0023,@RFC0453,@RFC0454,@Anoncreds --tags=~@CredFormat_JSON-LD --tags=@critical --tags=~@RFC0793 --tags=~@RFC0434

@RFC0023 @AIP20
Feature: RFC 0023 Establishing Connections with DID Exchange
  @T001-RFC0023 @critical @AcceptanceTest
  @T005-RFC0023 @critical @AcceptanceTest
@RFC0453 @AIP20
Feature: RFC 0453 Aries Agent Issue Credential v2
  @T001-RFC0453 @RFC0592 @critical @AcceptanceTest @CredFormat_Indy @Schema_DriversLicense_v2 @Anoncreds @RFC0160
  Scenario Outline: Issue a Indy credential with the Holder beginning with a proposal -- @1.1
  @T001-RFC0453 @RFC0592 @critical @AcceptanceTest @CredFormat_Indy @Schema_DriversLicense_v2 @Anoncreds @DIDExchangeConnection
  Scenario Outline: Issue a Indy credential with the Holder beginning with a proposal -- @2.1
@RFC0454 @AIP20
Feature: RFC 0454 Aries agent present proof v2
  @T001-RFC0454 @critical @AcceptanceTest @DIDExchangeConnection @CredFormat_Indy @RFC0592 @Schema_DriversLicense_v2 @CredProposalStart @Anoncreds
  Scenario Outline: Present Proof of specific types and proof is acknowledged with a Drivers License credential type with a DID Exchange Connection -- @1.1
  @T001-RFC0454 @critical @AcceptanceTest @DIDExchangeConnection @CredFormat_Indy @RFC0592 @Schema_DriversLicense_v2 @CredProposalStart @Anoncreds
  Scenario Outline: Present Proof of specific types and proof is acknowledged with a Drivers License credential type with a DID Exchange Connection -- @1.2
```

#### LDP-VC

Example `dry-run` command

```bash
./manage dry-run -d acapy -t @RFC0023,@RFC0453,@RFC0454,@CredFormat_JSON-LD,@DidMethod_key,@ProofType_Ed25519Signature2018 -t ~@Anoncreds -t @critical -t ~@RFC0793 -t ~@RFC0434 -t ~@DidMethod_orb -t ~@DidMethod_sov -t ~@ProofType_BbsBls12381G2PubKey
```

The output should look as follows:

```bash
Tags:  --tags=@RFC0023,@RFC0453,@RFC0454,@CredFormat_JSON-LD,@DidMethod_key,@ProofType_Ed25519Signature2018 --tags=~@Anoncreds --tags=@critical --tags=~@RFC0793 --tags=~@RFC0434 --tags=~@DidMethod_orb --tags=~@DidMethod_sov --tags=~@ProofType_BbsBls12381G2PubKey

@RFC0023 @AIP20
Feature: RFC 0023 Establishing Connections with DID Exchange
  @T001-RFC0023 @critical @AcceptanceTest
  @T005-RFC0023 @critical @AcceptanceTest
@RFC0453 @AIP20
Feature: RFC 0453 Aries Agent Issue Credential v2
  @T001.1-RFC0453 @RFC0593 @critical @AcceptanceTest @DIDExchangeConnection @CredFormat_JSON-LD @Schema_DriversLicense_v2 @ProofType_Ed25519Signature2018 @DidMethod_key
  Scenario Outline: Issue a JSON-LD credential with the Holder beginning with a proposal -- @2.1
  @T001.1-RFC0453 @RFC0593 @critical @AcceptanceTest @DIDExchangeConnection @CredFormat_JSON-LD @Schema_DriversLicense_v2 @ProofType_BbsBlsSignature2020 @DidMethod_key
  Scenario Outline: Issue a JSON-LD credential with the Holder beginning with a proposal -- @3.1
@RFC0454 @AIP20
Feature: RFC 0454 Aries agent present proof v2
  @T001-RFC0454 @critical @AcceptanceTest @DIDExchangeConnection @CredFormat_JSON-LD @RFC0510 @Schema_DriversLicense_v2 @CredProposalStart @ProofType_Ed25519Signature2018 @DidMethod_key
  Scenario Outline: Present Proof of specific types and proof is acknowledged with a Drivers License credential type with a DID Exchange Connection -- @2.1
  @T001-RFC0454 @critical @AcceptanceTest @DIDExchangeConnection @CredFormat_JSON-LD @RFC0510 @RFC0646 @Schema_DriversLicense_v2 @CredProposalStart @ProofType_BbsBlsSignature2020 @DidMethod_key
  Scenario Outline: Present Proof of specific types and proof is acknowledged with a Drivers License credential type with a DID Exchange Connection -- @3.1
  @T002-RFC0454 @RFC0510 @critical @AcceptanceTest @DIDExchangeConnection @CredFormat_JSON-LD @Schema_Citizenship_Context @CredProposalStart @ProofType_Ed25519Signature2018 @DidMethod_key
  Scenario Outline: Present Proof of specific types and proof is acknowledged with a Citizenship credential type with a DID Exchange Connection -- @1.1
  @T002-RFC0454 @RFC0510 @critical @AcceptanceTest @DIDExchangeConnection @CredFormat_JSON-LD @Schema_Citizenship_Context @CredProposalStart @RFC0646 @ProofType_BbsBlsSignature2020 @DidMethod_key
  Scenario Outline: Present Proof of specific types and proof is acknowledged with a Citizenship credential type with a DID Exchange Connection -- @2.1
```

## Pros and Cons of the Options

### Linked-Data-Proof Verifiable Credentials (LDP-VC)

- Good, because it is simple
- Good, because a lot of ecosystems use it
- Good, because it provides semantic disambiguation
- Neutral, because it is used by some very large ecosystems
- Bad, because it uses JSON-LD which adds overhead
- Bad, because it is not privacy preserving
- Bad, because no selective disclosure
- Bad, because it reveals a persistent identifier

### AnonCreds v1

- Good, because it is privacy preserving
- Good, because it provides [limited selective disclosure](https://hyperledger.github.io/anoncreds-spec/#restrictions)
- Good, because it supports ZKP (Zero-Knowledge Proofs)
- Good, because it doesn’t need a persistent identifier
- Bad, because it is complicated
- Bad, because it’s slow
- Bad, because it doesn’t provide semantic disambiguation
- Bad, because it is not widely adopted outside DIDComm
- Bad, because relies on interaction with the Indy Ledger as VDR for Revocation and Key Management/identification (establishing trust of issuer / verifiers)

Note: As we are using AnonCreds v1 with Issue Credential v2 and Present Proof v2, we should be able to take advantage of Aries RFC 0771, which provides an attachment format for AnonCreds. This allows AnonCreds to function in a ledger-agnostic way. However, this introduces additional work for the implementer, specifically around key management and revocation. Additionally, the AATH does not currently test AnonCreds with the RFC-0771 extension.


## More Information

- We originally considered a wide range of options, including:
    - Verifiable Credential Data Model 2.0:
        - Not widely adopted and therefore does not align with decision drivers.
    - Verifiable Credential Data Model 1.1 with JWT-VC or SD-JWT-VC:
        - Not widely used in message-centric environments, but suitable for API-centric (OIDC) use cases.
	        - ACA-Py does not support JWT-VC, only SD-JWT-VC and only over OIDC
	        - Credo-ts does support JWT-VC and SD-JWT-BC but only verification is supported over DIDComm (not issuance)
    - Verifiable Credential Data Model 1.1 with JSON-LD and ZKP using BBS+ signatures:
        - Not widely used and more complex to start with.
- This ADR does not address the requirements for an API-centric approach.
