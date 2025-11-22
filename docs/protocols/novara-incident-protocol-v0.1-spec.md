# Novara Incident Protocol v0.1

**Status:** Specification Draft  
**Version:** 0.1.0  
**Date:** 2025-11-19  
**License:** CC0 1.0 (Public Domain)

---

## 1. Overview

The **Novara Incident Protocol** defines how harms caused by AI-assisted systems are:

1. detected and recorded,  
2. attributed to actors, models, and policies, and  
3. remedied via **SLO-Bonds** and other pre-agreed mechanisms.

Goal:

- When something goes wrong in an AI-driven system,  
  the path from *harm* → *evidence* → *attribution* → *payment*  
  SHOULD be predictable, auditable, and explainable to the public.

This document is implementation-neutral and is designed to work together with:

- **Novara Evidence Bundle v0.1** – technical evidence format  
- **Novara Proof Rail v0.1** – “no valid proof, no money flow” payment gate  
- **Novara Human-Readable Proof v0.1** – narrative output for humans  
- **Novara Constitution v0.1** – core principles and thresholds

---

## 2. Scope

The Incident Protocol applies when **all** of the following are true:

1. An AI-assisted system **contributed** to a decision or action, and  
2. A person, organisation, or the public experienced **harm** (financial or non-financial), and  
3. The harm crosses a **materiality threshold** defined in policy (e.g. ≥ ¥10,000 or equivalent), and  
4. There exists (or SHOULD exist) a Novara Evidence Bundle covering the relevant time window.

Examples:

- An AI claims handler underpays an insurance claim.  
- A loan scoring model wrongly rejects a credit application.  
- An AI-powered subsidy allocation system unfairly excludes a group.  
- A content moderation model wrongfully blocks a creator’s revenue for a significant period.

Non-examples (outside Protocol scope, but MAY be logged for analytics):

- Pure UX annoyances with no measurable harm.  
- Incidents purely internal to a company with no external impact and below thresholds.  
- Events unrelated to AI assistance (purely human decisions).

---

## 3. Core concepts

### 3.1 Incident

An **Incident** is a structured record that connects:

- one or more **harms**,  
- the relevant **evidence bundles**, and  
- the resulting **remedies** (payments, reversals, policy changes).

An Incident is **not** the same as a single log entry.  
It is a higher-level object that can be revisited, re-opened, and referenced in public reports.

### 3.2 Harm

A **harm** is any negative outcome that crosses the configured materiality threshold, including:

- direct financial loss (e.g. underpaid claim, wrongly denied payout),  
- opportunity loss (e.g. unfair rejection of a loan),  
- systematic bias or discrimination (e.g. protected group consistently disadvantaged),  
- reputational or civic harm (e.g. wrongful labelling or exclusion).

Each harm MUST have a clear **harm_type** and **harm_amount** (if applicable).

### 3.3 SLO-Bond

An **SLO-Bond** is a pre-funded pool or contractual mechanism that:

- is tied to specific Service Level Objectives (SLOs), and  
- pays out automatically (or semi-automatically) when those SLOs are breached.

The Incident Protocol uses SLO-Bonds as the **default remedy mechanism** once attribution is clear.

### 3.4 Evidence Bundle link

Every Incident MUST reference at least one **Novara Evidence Bundle** for the relevant time window.  
The Incident record SHOULD store:

- `bundle_id` (or multiple), and  
- `chain_hash` / `last_hash` from the bundle verification.

---

## 4. Incident lifecycle

### 4.1 States

An Incident MUST move through a small, explicit set of states:

- `OPEN` – harm detected, investigation not complete  
- `UNDER_REVIEW` – evidence and attribution being examined  
- `RESOLVED` – remedy applied (payment, reversal, fix)  
- `ESCALATED` – handed to external authority (regulator, court, ombudsman)  
- `VOID` – opened in error, no actual Incident (with explanation)

Implementations MAY add more granular sub-states,  
but MUST be able to map them to these canonical states for reporting.

### 4.2 Minimal flow (happy path)

1. **Detection**  
   - A potential harm is detected (by monitoring, user complaint, or external signal).  
   - System creates an Incident with state `OPEN`.

2. **Evidence attachment**  
   - Relevant Evidence Bundle(s) are identified.  
   - The Incident is linked to `bundle_id` and key hashes.

3. **Attribution**  
   - Actors, models, and policies involved are identified.  
   - Responsibility shares (e.g. AI vs. operator vs. policy) MAY be estimated.

4. **Remedy proposal**  
   - A remedy is proposed (e.g. payout from SLO-Bond, policy change, apology, reversal).  
   - Proof Rail MAY be used to guard any outgoing payments.

5. **Decision and execution**  
   - Remedy is approved (or rejected) under defined governance rules.  
   - Payments go through Proof Rail with a `proof_token`.  
   - Incident state moves to `RESOLVED`.

6. **Human-readable proof**  
   - A narrative is generated for the affected party and, if required, the public.  
   - This may be published or delivered privately depending on policy.

---

## 5. Incident data model (minimal fields)

A conformant implementation MUST store at least the following fields for each Incident:

```jsonc
{
  "incident_id": "inc-2025-11-19-0001",
  "status": "RESOLVED",
  "opened_at": "2025-11-19T10:23:00Z",
  "closed_at": "2025-11-19T13:45:00Z",

  "harm": {
    "harm_type": "UNDERPAID_CLAIM",
    "description": "Auto claim was underpaid due to misclassified damage.",
    "amount": {
      "value": 30000,
      "currency": "JPY"
    },
    "affected_party": "customer:12345"
  },

  "evidence": {
    "bundle_ids": ["nvr-eb-2025-11-19-000045"],
    "chain_hash": "3d487a71050ad38c25740c7a93ee6212c57be0dd8dab0eec5f878ebca3fbb761"
  },

  "attribution": {
    "ai_system_id": "claims-llm-v3",
    "model_version": "llm-2025-10-01",
    "policy_version": "claims-policy-v12",
    "operators": ["operator:567"],
    "responsibility_notes": "Primary responsibility: policy mis-specification."
  },

  "remedy": {
    "type": "SLO_BOND_PAYOUT",
    "amount": {
      "value": 30000,
      "currency": "JPY"
    },
    "bond_id": "slo-bond-claims-2025",
    "payment_proof_token": "nvrp:2025-11-19:rail-01:abcd1234"
  }
}

Implementations MAY extend this with additional fields,
but MUST NOT remove or repurpose the above without clear migration paths.

⸻

6. Thresholds and materiality

Each deployment MUST define:
	•	harm_threshold – minimum value for an Incident to be required (e.g. ¥10,000),
	•	aggregate thresholds – for systematic harms (e.g. many small harms to a group),
	•	time windows – e.g. “incidents per day / week / month” for reporting.

These thresholds MUST be:
	•	documented in policy,
	•	consistent with Novara Constitution v0.1 principles, and
	•	available for audit by regulators and independent reviewers.

⸻

7. Relation to Proof Rail

When an Incident involves a payment (compensation, refund, adjustment):
	1.	The payment SHOULD be executed via Novara Proof Rail v0.1 or later.
	2.	The resulting proof_token SHOULD be stored in the Incident remedy section.
	3.	If a payment is made outside Proof Rail, the Incident MUST record:
	•	why Proof Rail was bypassed, and
	•	which authority approved the bypass.

⸻

8. Security, privacy, and ethics
	•	Incident records MAY contain sensitive information about individuals.
	•	Systems implementing this protocol SHOULD:
	•	pseudonymise identifiers where possible,
	•	separate identity store from Incident store,
	•	implement strict access controls and audit trails for Incident access,
	•	avoid using Incidents as a general-purpose surveillance mechanism.

If a deployment starts to resemble general mass surveillance,
it is likely outside the intended scope of Novara Core and SHOULD be questioned.

⸻

9. Reporting and transparency

Conformant operators SHOULD maintain at least:
	•	internal dashboards with:
	•	number of Incidents opened / resolved / escalated,
	•	total harm amounts,
	•	breakdown by harm_type,
	•	SLO-Bond activity (payouts, remaining capacity);
	•	periodic public or regulator-facing reports with aggregated statistics,
ensuring no individual can be re-identified from published data.

Over time, operators MAY adopt common reporting schemas
so that different organisations’ Incident data can be compared.

⸻

10. Conformance levels

To support gradual adoption, we define three levels:
	•	Level 1 – Basic Incident Logging
	•	Incidents recorded with minimal fields and linked to Evidence Bundles.
	•	No SLO-Bond automation required.
	•	Level 2 – SLO-Bond Integrated
	•	Incidents used to trigger SLO-Bond payouts in a structured way.
	•	Payments largely executed through Proof Rail.
	•	Aggregated Incident statistics available to regulators.
	•	Level 3 – Civic-grade
	•	Human-readable proofs routinely generated and delivered.
	•	Public reporting of Incident statistics and remedies.
	•	Incidents, Evidence Bundles, and Time Court tooling used in courts and policy debates.

⸻

11. Revision history
	•	v0.1.0 — initial draft (2025-11-19)

⸻

This document is dedicated to the public domain via CC0 1.0.
It may be copied, modified, and integrated into other systems
without permission or attribution.