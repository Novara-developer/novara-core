# novara-core

Text-only constitutional specs for the Novara ecosystem.  
Code lives in the implementation repo; this repo defines **what must be obeyed**.

---

## Core documents (v0.1)

- [Novara Constitution v0.1](docs/constitution/novara-constitution-v0.1-spec.md)
- [Novara Human-Readable Proof v0.1](docs/story/novara-human-readable-proof-v0.1-spec.md)
- [Novara Incident Protocol v0.1](docs/protocols/novara-incident-protocol-v0.1-spec.md)
- [Novara Proof Rail v0.1](docs/protocols/novara-proof-rail-v0.1-spec.md)

---

## Conceptual layers (v0.1)

Novara Core is organised into layers:

- **Constitution layer**  
  - Novara Constitution v0.1 – evidence-first principles, civic time horizon (2040–2060).
- **Protocol layer**  
  - Novara Incident Protocol v0.1 – how harms are recorded, attributed, and remedied (SLO-Bonds).  
  - Novara Proof Rail v0.1 – “no valid proof, no money flow” for AI-driven payments.
- **Story layer**  
  - Novara Human-Readable Proof v0.1 – plain-language narratives for victims, regulators, and the public.

Planned (not yet specified in this repo):

- **Time Court** – counterfactual re-trial of past AI decisions, based on evidence bundles.  
- **Gen-Z Pact** – a civic right to demand verifiable evidence from AI systems (“show your receipts”).

Implementation details, libraries, and CLIs live in the separate `Novara` repository.  
`novara-core` stays text-only, spec-first, and vendor-neutral.

---

## License

All texts in this repository are dedicated to the public domain under **CC0 1.0**.  
They may be copied, modified, and integrated into other systems without permission or attribution.


⸻







2. docs/protocols/novara-proof-rail-v0.1-spec.md（Proof Rail v0.1）

# Novara Proof Rail v0.1

**Status:** Specification Draft  
**Version:** 0.1.0  
**Date:** 2025-11-19  
**License:** CC0 1.0 (Public Domain)

---

## 1. Overview

The **Novara Proof Rail** is a payment gate.

Any money flow that is **caused by an AI decision**  
MUST pass through a Proof Rail checkpoint **before** funds are released.

Goal:

- If an AI decision moves money,  
  there MUST be a **verifiable evidence trail** behind it.

This document is implementation-neutral and is designed to work together with:

- **Novara Evidence Bundle v0.1** (technical evidence format)  
- **Novara Incident Protocol v0.1** (remedy & SLO-Bond execution)  
- **CTK-2 mini** (commitment & anchoring profile)

---

## 2. Scope

Proof Rail applies to payments where all are true:

1. An AI system produced a decision or recommendation, and  
2. That decision directly triggers or authorises a payment, transfer, or pricing change, and  
3. The amount is **≥ ¥10,000** (or local equivalent).

Examples:

- Insurance payout approved by AI  
- Loan approval / rejection decision  
- Government subsidy or grant decided by AI  
- High-value ad bidding / settlement driven by AI  
- Automated compensation under the Novara Incident Protocol

---

## 3. Core concepts

### 3.1 Proof Rail Checkpoint

A service that sits **between**:

- The AI decision system, and  
- The payment / settlement system.

It enforces this rule:

> **No valid proof → No money flow.**

### 3.2 Proof Token

A short identifier that links a payment to its evidence.

Format example:

```text
nvrp:2025-11-19:rail-01:abcd1234

It MUST allow the auditor to find the corresponding Evidence Bundle.

3.3 Evidence Bundle Requirement

Every Proof Rail–protected payment MUST point to a Novara Evidence Bundle v0.1+, containing at minimum:
	•	meta.json – system, model, policy, time window
	•	aal.ndjson – AI Action Ledger entries
	•	anchors.json – external anchors (blockchain / TEE / TSA)

The bundle MUST verify using standard Novara tools.
