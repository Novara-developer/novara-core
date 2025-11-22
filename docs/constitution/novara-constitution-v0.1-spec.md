# Novara Constitution v0.1

**Status:** Draft  
**Version:** 0.1.0  
**Date:** 2025-11-19  
**License:** CC0 1.0 (Public Domain)

---

## 0. Purpose

Novara Core exists to answer three questions for the AI era:

1. When an AI system causes harm, **what actually happened?**  
2. **Who is responsible**, under which policy and economic contract?  
3. How can anyone **verify this without trusting the vendor**?

This document sets the **constitutional principles** that all
Novara-compatible systems MUST obey.

---

## 1. Scope

This constitution applies to systems that:

- use AI to make or recommend decisions, and  
- move money or materially affect people’s lives, and  
- claim to implement any Novara Core spec (Evidence Bundle, Proof Rail, etc.).

It does **not** try to govern:

- all logging everywhere,  
- general social media activity, or  
- purely local, non-economic experiments.

The focus is **“when AI + money + harm meet”**.

---

## 2. Core principles

### 2.1 Evidence First

Logs before UX, proof before branding, verification before trust.

- No major AI decision that moves money should exist **without a trace**.
- If something must be dropped (due to cost, time, etc.),  
  **fancy UX goes first, evidence goes last**.

### 2.2 Evidence Sovereignty

“Ground truth” is whatever can be shown by open, tamper-evident evidence bundles,  
not by press releases or PR.

- Marketing claims do not override verifiable logs.
- If public statements contradict the evidence,  
  the evidence wins – and the contradiction itself must be logged.

### 2.3 Zero-Trust Verification

Anyone should be able to verify what happened **without trusting**:

- the AI vendor,  
- a specific cloud environment, or  
- hidden private keys.

Verification SHOULD be possible:

- offline,  
- on modest hardware,  
- using open tools and documented algorithms.

### 2.4 Determinism

Same inputs → same outputs → same evidence bundle, byte-for-byte.

- If two runs produce different evidence bundles,  
  the difference itself MUST be explainable and logged.
- “We changed it but forgot to record why” is unconstitutional.

### 2.5 Tamper-Evidence

Any change to logs, models, policies, or configs must be either:

- **impossible**, or  
- **visible as a cryptographic scar** (hash-chain break, anchor mismatch, etc.).

Soft edits (e.g. correcting a typo) are allowed,  
but previous states MUST remain reconstructable.

### 2.6 Attribution-Ready

Every important decision MUST be traceable to:

- actors (AI / operator / user),  
- policy version,  
- model + version,  
- time window.

Blame MUST NOT be pushed to an anonymous “the AI” without these links.

### 2.7 SLO-Bound Remedy

Once harm crosses a public threshold (e.g. ¥10,000 equivalent):

- compensation SHOULD be driven by **pre-funded SLO-Bonds** and  
  an open attribution formula,  
- not by ad-hoc negotiation, dark settlements, or “oops, our bad” PR.

Economic responsibility MUST be **predictable and pre-committed**.

### 2.8 Human-Readable Proof

Victims, regulators, and the public SHOULD receive a plain-language narrative:

- what happened,  
- who pays what, and  
- what will change to reduce future harm,

not just hashes, JSON, or cryptographic jargon.

The **Human-Readable Proof** spec defines minimum expectations.

### 2.9 Multi-Anchor Neutrality

Evidence anchors MUST be spread across **multiple independent infrastructures**:

- different chains,  
- different operators,  
- different political blocs.

No single cloud, vendor, or jurisdiction  
should be able to silently erase the trail.

### 2.10 Civic Time Horizon

Novara Core is designed as public infrastructure for **2040–2060**,  
not as a short-term feature of any particular startup or product cycle.

Roadmaps SHOULD be assessed on **decades**,  
not on quarterly feature releases.

---

## 3. Actors and roles

This constitution assumes four main roles:

- **Subject** – the person or group affected by the AI decision.  
- **Operator** – the organisation deploying the AI system.  
- **Vendor** – providers of AI models, tools, or platforms.  
- **Auditor / Regulator** – entities that verify and enforce behaviour.

In some systems, one legal entity may play multiple roles.  
Responsibilities below still apply to the **role**, not the marketing label.

---

## 4. Constitutional obligations

### 4.1 Evidence Bundles

Operators that claim Novara compatibility MUST:

- generate **Novara Evidence Bundles** for covered decisions, and  
- keep them verifiable for an agreed retention period.

At minimum, each bundle MUST include:

- `meta.json` – system / model / policy / time window,  
- `aal.ndjson` – AI Action Ledger entries (hash-chained),  
- `anchors.json` – digests and external anchors.

### 4.2 Proof Rail

For payments above the threshold (default: ¥10,000 equivalent):

- funds MUST NOT move unless a **Proof Rail** instance returns ALLOW, and  
- the payment record MUST link to a valid `proof_token`.

By claiming Novara Proof Rail compliance,  
operators accept “**no valid proof → no money flow**” as a rule.

### 4.3 CTK-2 Style Commitments

Where practical, important decisions SHOULD be:

- pre-committed (input + environment + model hash), and  
- anchored to at least one independent time / state reference.

This makes later re-runs and counterfactuals possible.

### 4.4 Right to Evidence

Subjects affected by AI decisions SHOULD have:

- the right to request a Human-Readable Proof, and  
- the right to have an independent auditor verify the underlying bundle.

Operators MAY redact or aggregate personal data,  
but MUST NOT destroy the ability to verify the **structure** and **logic** of events.

### 4.5 Refusal and Opt-Out Boundaries

Novara MUST NOT be used as a justification for:

- total surveillance of all human activity, or  
- forcing individuals to log every detail of private life.

Deployments that begin to look like general surveillance  
are **outside the intended scope** of this constitution.

---

## 5. Governance and versioning

### 5.1 Version tags

Every implementation that claims Novara compatibility MUST:

- state which spec versions it implements  
  (e.g. `novara-constitution-v0.1`, `novara-proof-rail-v0.1`), and  
- record this in its own evidence bundles.

### 5.2 Amendments

This constitution is **v0.1**:

- It is expected to evolve as real pilots, regulators, and communities  
  find edge cases and new risks.
- Future versions SHOULD keep an **upgrade path** from older bundles,
  not erase previous semantics.

### 5.3 Foundation and stewardship

Long term, Novara Core SHOULD be governed by a neutral foundation
(or similar public-interest structure) that:

- maintains the specs,  
- coordinates reference implementations, and  
- keeps multi-jurisdictional neutrality.

Until then, this repo acts as the **public draft log**.

---

## 6. Non-goals

Novara Core **does not** try to:

- replace all existing audit standards (ISO, SOC2, etc.),  
- define every detail of ML training or data pipelines,  
- decide which AI models are “good” or “bad” in general.

It focuses on **evidence and accountability**  
for decisions that move money and harm.

---

## 7. License

This constitution is dedicated to the public domain under **CC0 1.0**.

It may be copied, modified, and integrated into other systems  
without permission or attribution.

If you improve it,  
publishing your changes helps everyone living in the same AI century.