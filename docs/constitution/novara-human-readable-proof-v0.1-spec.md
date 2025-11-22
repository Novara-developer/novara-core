# Novara Human-Readable Proof v0.1

**Status:** Specification Draft  
**Version:** 0.1.0  
**Date:** 2025-11-19  
**License:** CC0 1.0 (Public Domain)

---

## Goal and Context

Technical evidence bundles are for machines and auditors. **Victims and the public need plain-language explanations.**

This document defines three human-facing views of an incident, ensuring accountability is understood by all stakeholders:

1. **Victim View** – for the person who was harmed
2. **Public View** – for community and regulators
3. **Journalist View** – for investigative reporting

It is implementation-neutral and must be read together with the Novara Core documents.

---

## 1. Victim View: Remedy for the Harmed

**Goal:** Help the victim understand, in simple language: what happened, how it harmed them, and what will be done to fix it.

A minimum victim-facing report **MUST** contain:

### 1.1. What Happened

* One or two short paragraphs.
* **No technical jargon.**
* Clear description of the AI decision and the context of the harm.

### 1.2. Impact on You

* Financial impact (amount, currency).
* Time lost (hours, days).
* Other quantifiable harm (e.g., stress, loss of access to critical services).

### 1.3. What We Found (Attribution)

* AI system name and version.
* The specific decision or recommendation the AI made.
* The primary reason that decision was found to be wrong or harmful.
* Attribution split (Was this mainly AI fault, Operator fault, or both?).

### 1.4. Your Remedy

* Payment amount and currency.
* How and when the payment will be executed (Tier 1 vs. Tier 2 protocol).
* Any non-financial remedy (e.g., apology, data correction, systemic fix).

Operators **SHOULD** provide this in the victim’s preferred language where possible.

---

## 2. Public View: Risk Monitoring

**Goal:** Allow the public to monitor patterns and systemic risk **without** exposing personal data.

For each incident that triggers the Novara Incident Protocol, a public record **SHOULD** include at least:

* Incident ID (pseudonymous if needed).
* Date of incident and the Domain (e.g., medical, finance, hiring).
* AI system name and version (or family).
* Damage amount (rounded).
* **Attribution vector (AI / Operator / User percentages).**
* Status (resolved / pending / disputed).

This public view **SHOULD** be publishable as an open dashboard and a machine-readable feed (JSON, CSV).

---

## 3. Journalist View: Accountability Access

**Goal:** Support investigative journalism and accountability reporting, without compromising victim privacy.

With proper justification, accredited journalists **MAY** request:

* **Redacted evidence bundle** (with personal data removed or masked).
* Model and policy version that were active at the time of the incident.
* Statistics on similar incidents in the last N months.
* Explanation of systemic changes made since the incident (model, policy, process).

Requests **SHOULD** include the journalist's identity, affiliation, purpose of the investigation, and the Incident ID(s) of interest.

---

## 4. The Seven Green Checks (Proof of Verification)

For any case that claims to be **“Novara-verified”**, the following seven checks **MUST** all be true:

1.  **Evidence bundle exists:** A verifiable Novara Evidence Bundle (v0.1+) is stored and accessible.
2.  **Hash chain intact:** AAL hash chain verifies end-to-end.
3.  **Timestamps consistent:** No impossible jumps, gaps, or rewrites in the timeline.
4.  **Policy and model specified:** Model version and policy hash are clearly recorded within the bundle.
5.  **Attribution sums to 1.0:** AI / Operator / User fractions (Attribution vector) add up precisely to 1.0.
6.  **Damage documented:** Financial or other harm is backed by external records (Receipts, insurer statement, etc.).
7.  **Payment executed or scheduled:** SLO-Bond payment is confirmed, or a clear schedule exists according to the Incident Protocol.

If any of these checks fail, the case **MUST NOT** be advertised as **“Novara-verified”** without an explicit disclaimer.

---

## 5. Relationship to Core Documents

This specification is a mandatory companion to technical evidence and must be read with:

* **Novara Incident Protocol v0.1:** Defines damage thresholds, attribution calculation, and payment execution logic.
* **Novara Constitution v0.1:** Defines the core principles (Evidence Sovereignty, Independence, etc.).
* **Novara Evidence Bundle v0.1:** Defines the technical log format (`aal.ndjson`, `anchors.json`).

---

## Revision History

* v0.1.0 — initial draft (2025-11-19)

---

This document is dedicated to the public domain via **CC0 1.0**.