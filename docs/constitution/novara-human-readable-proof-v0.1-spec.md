# Novara Human-Readable Proof v0.1

**Status:** Draft  
**Version:** 0.1.0  
**Date:** 2025-11-19  
**License:** CC0 1.0 (Public Domain)

---

## 1. Purpose

This spec defines how to turn technical evidence  
(Evidence Bundles, Proof Rail records, policies)  
into a **human-readable narrative**.

The audience:

- people harmed by AI-driven decisions (subjects)  
- regulators, judges, ombuds, journalists  
- the general public

Goal:

> After reading one Human-Readable Proof,  
> a non-technical person should understand  
> **what happened, who pays, and what will change.**

---

## 2. Scope

This document applies when:

- a Novara-compatible system has produced one or more **Evidence Bundles**, and  
- an incident, dispute, or large payout has occurred, and  
- a subject or regulator requests **an explanation in plain language**.

It does **not** define:

- the full legal judgement text,  
- PR statements, or  
- deep forensic reports for engineers.

It defines the **minimum standard** for a public-facing explanation.

---

## 3. Core principles

Human-Readable Proofs MUST follow these principles:

1. **Truthful to the evidence**  
   - Every claim in the story MUST be traceable  
     to a cryptographically verifiable artefact  
     (bundle, policy, Proof Rail record, etc.).

2. **Plain language first**  
   - Use short sentences and common terms.  
   - Avoid jargon unless it is explained in-place.

3. **No “mystical AI” language**  
   - Do not say “the AI decided on its own”  
     without specifying the operator, model, and policy context.

4. **Respect for subjects**  
   - Do not blame or shame individuals in the narrative.  
   - Be precise about system and organisational errors.

5. **Actionable outcome**  
   - Clearly state what compensation and changes are triggered,  
     according to the Incident Protocol and SLO-Bonds.

---

## 4. Document structure (v0.1)

A Human-Readable Proof SHOULD follow this structure:

1. **Header / summary block**  
2. **Timeline of events**  
3. **What went wrong (root cause, simplified)**  
4. **Who is responsible for what**  
5. **What compensation is owed**  
6. **What will change to reduce future harm**  
7. **Technical appendix (short)**

### 4.1 Header / summary block

At the top, a short summary in 5–10 lines:

- Incident ID  
- Date range  
- System / product name  
- Type of harm (e.g. *wrongly denied claim*, *overcharge*, *privacy leak*)  
- Short summary (2–3 sentences)  
- One-line outcome (e.g. *“Your claim is now approved and we will pay ¥40,000.”*)

Example:

> On 2025-10-12, our claims AI wrongly rejected your insurance claim.  
> This was caused by an outdated risk policy that we failed to update.  
> We have now approved your claim. You will receive ¥40,000 within 7 days.

### 4.2 Timeline of events

Chronological list of key events,  
with human-readable times and references to evidence:

- When the subject submitted data / request  
- When the AI system processed it  
- When a decision was made and by which model/policy  
- When payments were blocked or executed  
- When the issue was detected and by whom

Each event SHOULD be linked (by ID)  
to AAL entries or specific bundles.

### 4.3 What went wrong

A short explanation of:

- wrong model / threshold / policy / data, and  
- why the system behaved in that way at the time.

This section MUST:

- avoid purely abstract blame like “the algorithm failed”, and  
- name at least one concrete factor (e.g. outdated policy version,  
  misconfigured threshold, missing data validation).

### 4.4 Who is responsible for what

Clear attribution across roles:

- Operator responsibilities (e.g. monitoring, policy updates)  
- Vendor responsibilities (e.g. model release notes, safety limits)  
- Any third parties (e.g. data providers, integrators)

If SLO-Bonds are in place,  
this section SHOULD mention which bond(s) are triggered.

### 4.5 What compensation is owed

A concrete statement of:

- what is being paid (amount, currency, timing),  
- under which contract / SLO / policy,  
- any additional non-monetary remedies  
  (e.g. record correction, apology, service change).

Where relevant, link to **Proof Rail** decisions that authorised the payment.

### 4.6 What will change

Practical changes the operator commits to:

- model updates or rollbacks  
- policy changes  
- new monitoring or limits  
- timelines for these changes

This SHOULD be written so that future audits  
can check whether the promised changes actually happened.

### 4.7 Technical appendix (short)

A short, optional section for more technical readers:

- Incident bundle IDs (one or more Evidence Bundles)  
- Relevant decision IDs  
- Proof Rail proof_tokens  
- Policy IDs / versions  
- Anchors (e.g. CTK-2 references)

This appendix SHOULD be enough for an independent auditor  
to go from the narrative back to raw evidence.

---

## 5. Input and output

### 5.1 Inputs

To generate a Human-Readable Proof, a system will typically consume:

- One or more **Novara Evidence Bundles**  
- Proof Rail records (payments allowed / denied)  
- Incident records (from Novara Incident Protocol)  
- Policy definitions and SLO-Bond contracts

### 5.2 Output

The output is a **renderable document**:

- text/markdown, HTML, or PDF,  
- ideally in multiple languages when needed,  
- with stable identifiers so it can be cited in cases.

The document SHOULD be:

- stored alongside the technical evidence, and  
- referenced in any public or regulatory communications about the incident.

---

## 6. Language and accessibility

### 6.1 Reading level

Human-Readable Proofs SHOULD target  
a reading level roughly equivalent to B1–B2 in CEFR:

- short paragraphs  
- minimal nested clauses  
- common words where possible

### 6.2 Multi-lingual

Where subjects are multi-lingual,  
operators SHOULD provide the narrative:

- in the subject’s primary language where feasible, and  
- in at least one widely used lingua franca (e.g. English).

If translations exist,  
their relationship SHOULD be logged (e.g. translation of HRP-2025-0001-en).

---

## 7. Conformance

An implementation MAY claim:

- **“Human-Readable Proof compatible (v0.1)”**  
  if it generates documents that:

  - follow the structure in §4,  
  - obey principles in §3, and  
  - link all factual claims to Novara evidence.

If parts are omitted (e.g. no compensation section),  
the reason SHOULD be explicitly stated in the document.

---

## 8. Revision history

- v0.1.0 — initial draft (2025-11-19)

---

This spec is dedicated to the public domain under **CC0 1.0**.  
You may copy, modify, or integrate it into other systems  
without permission or attribution.