
# DID Threat Model Specification (DID-TM)

[![Status: Editor's Draft](https://img.shields.io/badge/Status-Editor's%20Draft-orange)](https://github.com/sirraya-labs/did-tm)
[![Version](https://img.shields.io/badge/Version-1.0.0-blue)](https://github.com/sirraya-labs/did-tm)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Specification](https://img.shields.io/badge/Specification-HTML%20Preview-red)](https://sirraya-labs.github.io/did-tm/)

A comprehensive, normative threat model and security framework for Decentralized Identifiers (DIDs), Verifiable Credentials (VCs), and Self-Sovereign Identity (SSI) systems.

---

## 📖 Overview

Decentralized identity systems invert the classical security model. There is no trusted third party, no central authority to override compromises, and no administrative recovery path. The key *is* the identity. This architectural shift renders classical threat frameworks—STRIDE, LINDDUN, PASTA, MITRE ATT&CK—structurally incomplete.

**DID-TM** fills this gap by providing:

- A formal threat taxonomy purpose-built for decentralized identity
- A novel **K-Class** (Key Lifecycle Failure) with no equivalent in any existing framework
- A structured attack catalog of 50+ named attacks with CVSS-DID scoring
- Normative security and privacy requirements with threat-to-control traceability
- Cryptographic threat analysis covering VSS, ZKP, VDF, and threshold signatures
- Compliance alignment with NIST SP 800-63, ISO 27001, eIDAS 2.0, and SOC 2

---

## 🎯 Target Audience

| Audience | Purpose |
|----------|---------|
| **Protocol Implementers** | Design and build more secure DID methods, wallets, and verifiers |
| **Security Architects & Auditors** | Canonical reference for threat modeling and risk assessment of SSI infrastructure |
| **Standards Bodies** | Inform security and privacy sections of evolving identity standards (W3C, IETF, ISO) |
| **Academic Researchers** | Foundational document for the formal study of decentralized identity security |

---

## 📚 Specification Structure

The specification is organized into six main parts:

| Part | Title | Description |
|------|-------|-------------|
| **I** | Threat Taxonomy | STRIDE-DID, K-Class (Key Lifecycle Failure), LINDDUN-DID, CVSS-DID Scoring |
| **II** | Attack Surface Model | The DID Stack, Adversary Model, Identity Lifecycle Threat Map |
| **III** | Attack Catalog | 50+ named attacks with identifiers, CVSS-DID scores, attack trees, and mitigations |
| **IV** | Cryptographic Threat Analysis | Algebraic assumptions, VSS, ZKP, VDF, threshold signatures, side-channel, post-quantum |
| **V** | Normative Countermeasures | Security requirements, privacy requirements, threat-to-control traceability matrix |
| **VI** | Compliance & Interoperability | Framework alignment, DID method security profiles |

---

## 🔐 Key Contributions

### STRIDE-DID

A re-specification of the classical STRIDE threat classes for the decentralized identity context:

| Class | DID-Specific Definition |
|-------|------------------------|
| **S** — Spoofing | Adversary asserts control of a DID or presents credentials as if issued to a DID they do not control |
| **T** — Tampering | Unauthorized modification of DID Documents, VCs, VPs, or cryptographic infrastructure |
| **R** — Repudiation | Denial of having authorized a DID operation, issued a credential, or participated in a transaction |
| **I** — Information Disclosure | Unintended exposure of identity-related information, social graphs, or behavioral patterns |
| **D** — Denial of Service | Disruption of identity services—resolution, verification, issuance, or recovery |
| **E** — Privilege Escalation | Gaining capabilities beyond what is authorized—key rotation, credential issuance, secret reconstruction |

### K-Class — Key Lifecycle Failure (Novel)

The primary novel contribution of this specification. K-Class threats arise when cryptographic key management fails in ways that are often irreversible:

| Sub-class | Description |
|-----------|-------------|
| **K1** — Key Ceremony Failure | Insecure key generation, unwitnessed ceremonies, improper escrow |
| **K2** — Share Lifecycle Failure | Distribution, custody, refreshment, or reconstruction failures in threshold schemes |
| **K3** — Time-Lock Integrity Failure | VDF difficulty miscalibration, ASIC advantage, false proof acceptance |
| **K4** — Rotation and Revocation Failure | Revoked keys remain accepted; windows of dual validity |
| **K5** — Post-Quantum Migration Failure | Failure to migrate before cryptographically relevant quantum computers arrive |
| **K6** — Inheritance and Recovery Chain Failure | Broken succession paths, dead-man's switch failures, inheritance chain breaks |

### CVSS-DID Scoring

Extends CVSS 3.1 with four metrics specific to decentralized identity:

- **DF** — Decentralization Factor (High / Medium / Low)
- **RA** — Recovery Availability (Available / Degraded / None)
- **TC** — Threshold Collusion Required (None / Partial / Full)
- **QA** — Quantum Advantage (Applicable / Not Applicable)

---

## 🗂️ Attack Catalog

The catalog assigns each attack a permanent identifier of the form `DID-TM-ATK-NNN`. Attacks are never renumbered across versions.

### Registry Layer Attacks (50x)
- `DID-TM-ATK-050` — Smart Contract Registry Reentrancy (CVSS-DID 9.1 Critical)
- `DID-TM-ATK-051` — did:web DNS Hijacking (CVSS-DID 8.6 High)
- `DID-TM-ATK-052` — Ledger Consensus Eclipse Attack (CVSS-DID 8.2 High)

### Resolution Layer Attacks (100x)
- `DID-TM-ATK-100` — Universal Resolver Cache Poisoning (CVSS-DID 9.3 Critical)
- `DID-TM-ATK-101` — DID Resolution SSRF (CVSS-DID 7.9 High)
- `DID-TM-ATK-102` — Resolver Amplification DoS (CVSS-DID 6.5 Medium)

### Wallet Attacks (200x)
- `DID-TM-ATK-200` — Cold Boot Seed Phrase Extraction (CVSS-DID 9.6 Critical)
- `DID-TM-ATK-201` — Wallet Malware Keylogging (CVSS-DID 9.0 Critical)
- `DID-TM-ATK-202` — Biometric Bypass via Spoofed Artifact (CVSS-DID 7.5 High)

### VC/VP Attacks (300x)
- `DID-TM-ATK-300` — Credential Replay Attack (CVSS-DID 8.0 High)
- `DID-TM-ATK-301` — Holder Binding Absence Exploit (CVSS-DID 8.4 High)
- `DID-TM-ATK-302` — ZKP Nonce Reuse Linkability (CVSS-DID 5.9 Medium)

### Recovery Attacks (400x)
- `DID-TM-ATK-400` — Guardian Collusion at Threshold (CVSS-DID 9.8 Critical)
- `DID-TM-ATK-401` — MPC Epoch Share Drift (CVSS-DID 7.8 High)
- `DID-TM-ATK-402` — VDF Difficulty Miscalibration (CVSS-DID 8.1 High)
- `DID-TM-ATK-403` — VSS Share Pollution (CVSS-DID 9.5 Critical)
- `DID-TM-ATK-404` — Recovery Loop Deadlock (CVSS-DID 7.2 High)

### Cross-Cutting Attacks (500x)
- `DID-TM-ATK-500` — Sybil Attack on Guardian Network (CVSS-DID 8.7 High)
- `DID-TM-ATK-501` — Cross-DID Correlation via Resolver Logs (CVSS-DID 6.1 Medium)
- `DID-TM-ATK-502` — Governance Attack on DID Method Registry (CVSS-DID 8.3 High)

---

## 📋 Normative Requirements

The specification defines security and privacy requirements with MUST/SHOULD/MAY conformance levels, each traceable to specific threats.

### Security Requirements (Selected)

| ID | Requirement | Mitigates |
|----|-------------|-----------|
| REQ-50 | Registry contracts MUST implement Checks-Effects-Interactions | ATK-050 |
| REQ-100 | Cached DID Documents MUST be cryptographically anchored | ATK-100 |
| REQ-200 | Wallets MUST use OS-provided secure key storage | ATK-200 |
| REQ-300 | VPs MUST include verifier-provided nonce | ATK-300 |
| REQ-400 | Guardian sets MUST be distributed across independent jurisdictions | ATK-400 |
| REQ-412 | Every VSS share MUST be verified against commitments | ATK-403 |
| REQ-450 | fROST MUST use deterministic nonce generation | ATK-440 |

### Privacy Requirements (Selected)

| ID | Requirement |
|----|-------------|
| PRI-100 | Credential issuers MUST support selective disclosure schemes |
| PRI-200 | Holders MUST use pairwise DIDs for unlinkability |
| PRI-300 | DID Documents MUST NOT contain personal data |
| PRI-301 | Recovery methods MUST use hashed or pseudonymous guardian identifiers |

---

## 🔗 Compliance Alignment

| Framework | Alignment |
|-----------|-----------|
| **NIST SP 800-63** | IAL2/AAL2/AAL3/FAL2 mappings provided |
| **ISO/IEC 27001** | Annex A controls mapped to DID-TM requirements |
| **SOC 2** | Trust Services Criteria (CC6.1, etc.) mapped |
| **eIDAS 2.0** | Aligns with EUDI Wallet security requirements |
| **W3C DID Core §10–11** | Operationalizes security/privacy considerations into testable requirements |

---

## 📖 Reading the Specification

The specification is available in two formats:

| Format | Link | Description |
|--------|------|-------------|
| **HTML Preview** | [sirraya-labs.github.io/did-tm/](https://sirraya-labs.github.io/did-tm/) | Fully formatted specification with diagrams, tables, and attack catalog |
| **Source** | `/index.html` | Single HTML document with embedded CSS, JavaScript, and Mermaid diagrams |

---

## 🧪 Test Assertions

Appendix A provides machine-readable test assertions for validating conformance:

```json
{
  "id": "DID-TM-TA-001",
  "scope": ["W"],
  "requirement": "REQ-200",
  "description": "Wallet MUST store private keys in OS secure storage",
  "attack": "DID-TM-ATK-200"
}
```

---

## 🤝 Contributing

Contributions are welcome! This specification is under active development as an Editor's Draft.

### Areas for Contribution
- Additional attack entries with CVSS-DID scoring
- Test assertions for new requirements
- DID method security profiles
- Post-quantum migration strategies
- Implementation experience reports

### How to Contribute
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-contribution`)
3. Commit your changes (`git commit -m 'Add amazing contribution'`)
4. Push to the branch (`git push origin feature/amazing-contribution`)
5. Open a Pull Request

---

## 📄 License

This specification is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## 📬 Contact

| Role | Name | Contact |
|------|------|---------|
| **Editor** | Amir Hameed Mir | [amir@sirraya.org](mailto:amir@sirraya.org) |
| **Organization** | Sirraya Labs | [sirraya.org](https://sirraya.org) |
| **Issues** | | [GitHub Issues](https://github.com/sirraya-labs/did-tm/issues) |

---

## 📚 References

### Normative
- [W3C DID Core v1.0](https://www.w3.org/TR/did-core/)
- [W3C VC Data Model 2.0](https://www.w3.org/TR/vc-data-model-2.0/)
- [CVSS v3.1 Specification](https://www.first.org/cvss/v3.1/specification-document)
- [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) — Key words for use in RFCs
- [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174) — Ambiguity of Uppercase vs Lowercase

### Informative
- [STRIDE-ORIGINAL] Kohnfelder, L. & Garg, P. "The threats to our products." Microsoft, 1999.
- [FELDMAN-1987] Feldman, P. "A Practical Scheme for Non-interactive Verifiable Secret Sharing." FOCS 1987.
- [SHAMIR-1979] Shamir, A. "How to Share a Secret." CACM 1979.
- [HERZBERG-1995] Herzberg, A. et al. "Proactive Secret Sharing." CRYPTO 1995.
- [BONEH-2018] Boneh, D. et al. "Verifiable Delay Functions." CRYPTO 2018.

---

**Sirraya Labs** · Editor's Draft v1.0.0 · March 2026
```

---

