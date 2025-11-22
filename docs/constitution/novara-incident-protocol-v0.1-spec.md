# Novara Incident Protocol v0.1

**Status:** Specification Draft  
**Version:** 0.1.0  
**Date:** 2025-11-19  
**License:** CC0 1.0 (Public Domain)

---

## 1. Overview

The **Novara Incident Protocol** defines how AI-related harms are:

- detected and recorded  
- attributed to systems, policies, and actors  
- remedied using **SLO-Bonds** and other mechanisms

It connects three things:

- **Evidence Bundles** (what actually happened)  
- **Proof Rail** (what payments are allowed)  
- **Human-Readable Proof** (what is explained to people)

Goal:

> When an AI system harms someone,  
> there is a predictable, verifiable way  
> to answer: *what happened, who pays, and what changes*.

---

## 2. Scope

This protocol applies when all are true:

1. An AI-involved system made or heavily influenced a decision, and  
2. The decision caused or plausibly caused harm (financial, access, rights, etc.), and  
3. The harm crosses a **public threshold** (e.g. ≥ ¥10,000 or equivalent non-monetary impact).

Examples:

- A claims AI wrongly denies an insurance payout  
- A credit scoring model blocks access to a loan  
- An automated subsidy system under-pays a group  
- An AI moderation system wrongly deletes important content

This spec does **not** cover:

- purely internal near-misses without impact  
- general model evaluations without specific harm

---

## 3. Core concepts

### 3.1 Incident

A **Novara Incident** is a structured record that:

- points to one or more **Evidence Bundles**  
- describes the harm and affected subjects  
- triggers SLO-Bond logic and potential payments  
- anchors the Human-Readable Proof

Each incident has a stable ID, e.g.:

```text
nvr-inc-2025-000123

3.2 Harm Threshold

A deployment MUST define:
	•	a monetary threshold (e.g. ¥10,000) and/or
	•	a qualitative threshold (e.g. denial of essential service)

Above that, the Incident Protocol MUST be invoked.

3.3 SLO-Bond

A SLO-Bond is a pre-funded commitment:
	•	tied to a system, policy, or SLO (Service Level Objective)
	•	with a formula for compensation once harm is confirmed

The Incident Protocol specifies when and how SLO-Bonds are triggered.

3.4 Roles

Key roles in an incident:
	•	Subject – person(s) harmed by the AI-involved system
	•	Operator – organisation that runs the system
	•	Vendor – model / tool provider(s)
	•	Insurer / Guarantor – entity backing SLO-Bonds
	•	Regulator / Auditor – oversight bodies

This spec is neutral about who combines which roles in practice.

⸻

4. Lifecycle (v0.1)

Minimal incident lifecycle:
	1.	Detection – something may be wrong
	2.	Triage – is this in scope? does it cross the threshold?
	3.	Evidence freeze – pin relevant Evidence Bundles
	4.	Attribution – which systems / policies / actors are responsible?
	5.	Remedy calculation – how much compensation / what actions?
	6.	Execution – payments via Proof Rail, system changes
	7.	Human-Readable Proof – narrative for subjects / public
	8.	Closure – mark as resolved, with follow-up checks

4.1 Detection

Incidents MAY be detected by:
	•	subjects (complaints, appeals)
	•	operators (monitoring, internal review)
	•	regulators / auditors (inspections)
	•	automated anomaly detection

Each detection creates a preliminary record with:
	•	timestamp_detected
	•	reporter type (subject / operator / regulator / other)
	•	short description

4.2 Triage

The operator (or designated handler) MUST decide:
	•	Is AI involvement plausible?
	•	Does it cross the harm threshold?
	•	Is it obviously out-of-scope (e.g. mis-typed account number)?

Outcomes:
	•	NO_INCIDENT – logged but not escalated
	•	INCIDENT_OPENED – full Incident created

4.3 Evidence freeze

For INCIDENT_OPENED, the handler MUST:
	•	identify relevant Evidence Bundles (dates, subjects, systems)
	•	pin them by ID in the incident record
	•	ensure bundles are preserved (no deletion, retention ok)

Where possible, additional logs may be snapshotted
but the canonical reference SHOULD be Evidence Bundles.

4.4 Attribution

Attribution answers:
	•	Which system(s) and policy version(s) contributed?
	•	Was the primary failure in:
	•	model behaviour,
	•	policy design,
	•	implementation / integration,
	•	monitoring / operations, or
	•	external constraints?

Attribution SHOULD be:
	•	explicit (e.g. percentage weight or primary/secondary tags)
	•	backed by references to bundles, configs, and policies

4.5 Remedy calculation

Based on:
	•	contract terms (insurance, credit, subsidy, etc.)
	•	active SLO-Bond definitions
	•	regulatory requirements

The handler computes:
	•	baseline compensation (what should have happened)
	•	additional compensation (harm, delay, etc.)
	•	which SLO-Bond(s) are charged

The calculation SHOULD be expressible as:

amount_due = f(harm, delay, policy, SLO-Bond)

and logged in the incident.

4.6 Execution (via Proof Rail)

Payments triggered by an incident MUST:
	•	be executed through Novara Proof Rail where available
	•	reference both:
	•	incident_id and
	•	proof_token from the rail

Non-monetary remedies (e.g. record correction)
SHOULD still be logged with references to Evidence Bundles.

4.7 Human-Readable Proof

For confirmed incidents, the operator SHOULD:
	•	generate a Human-Readable Proof document (v0.1)
	•	link it to the incident by ID
	•	provide it to subjects and regulators

The incident record MUST store:
	•	hrp_id (e.g. nvr-hrp-2025-000045)
	•	language(s) available
	•	publication / delivery date

4.8 Closure

An incident MAY be closed when:
	•	remedy has been executed, and
	•	Human-Readable Proof has been generated (if required), and
	•	follow-up checks (if any) have been performed.

The closure record MUST include:
	•	status (CLOSED / PARTIALLY_CLOSED / ESCALATED)
	•	final timestamps
	•	who authorised closure

⸻

5. Minimum incident record

A conformant implementation MUST be able to represent at least:

{
  "incident_id": "nvr-inc-2025-000123",
  "status": "OPEN",
  "subject_ids": ["customer:12345"],
  "detected_at": "2025-11-19T10:15:00Z",
  "detected_by": "SUBJECT",
  "system_id": "claims-ai-v3",
  "policy_id": "claims-policy-v7",
  "harm_summary": "Claim for accident on 2025-10-25 was wrongly denied.",
  "estimated_harm_amount": {
    "value": 40000,
    "currency": "JPY"
  },
  "evidence_bundles": [
    "nvr-eb-2025-10-25-000045",
    "nvr-eb-2025-10-26-000012"
  ],
  "attribution": {
    "primary_cause": "OUTDATED_POLICY",
    "secondary_causes": ["MISSING_MONITORING"]
  },
  "remedy": {
    "amount_due": {
      "value": 40000,
      "currency": "JPY"
    },
    "slo_bond_ids": ["slo-bond-claims-delay-v1"],
    "non_monetary": ["Correct claim status", "Update policy threshold"]
  },
  "payments": [
    {
      "proof_token": "nvrp:2025-11-19:rail-01:abcd1234",
      "rail_decision": "ALLOW"
    }
  ],
  "hrp_id": "nvr-hrp-2025-000045",
  "closed_at": null
}

Implementations MAY add fields,
but MUST NOT repurpose these for different meanings.

⸻

6. Security and privacy
	•	Incident records SHOULD avoid storing raw sensitive content
when equivalent pseudonymous references are possible.
	•	Links to Evidence Bundles SHOULD respect data protection laws
(e.g. retention limits, access controls).
	•	Access to incident records SHOULD be role-based and auditable.

⸻

7. Conformance levels

We define indicative levels:
	•	Level 0 – No Incident Protocol
	•	Incidents are handled ad-hoc, no structured link to evidence.
	•	Level 1 – Internal Novara Incidents
	•	Incidents are logged with IDs and bundle references.
	•	Remedy is executed but not yet transparently reported.
	•	Level 2 – Public Novara Incidents
	•	Same as Level 1, plus:
	•	aggregated stats are published (counts, categories, amounts),
	•	Human-Readable Proof is produced for major incidents.
	•	Level 3 – Full Novara Integration (target)
	•	Integrated with:
	•	Novara Proof Rail for payouts
	•	SLO-Bond accounting
	•	public dashboards for regulators and auditors

⸻

8. Revision history
	•	v0.1.0 — initial draft (2025-11-19)

⸻

This document is dedicated to the public domain via CC0 1.0.
It may be copied, modified, and integrated into other systems
without permission or attribution.