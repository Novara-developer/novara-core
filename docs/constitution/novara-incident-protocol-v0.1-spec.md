# Novara Incident Protocol v0.1

**Status:** Specification Draft  
**Version:** 0.1.0  
**Date:** 2025-11-19  
**License:** CC0 1.0 (Public Domain)

---

## Overview

When an AI system causes damage, this protocol defines:

1. When the incident qualifies for **automatic remedy**  
2. How responsibility (**attribution**) is calculated  
3. How payment is executed from **SLO-Bonds**

This document is implementation-neutral and must be read together with:

- Novara Constitution v0.1 (evidence-first governance)
- Novara Evidence Bundle v0.1 (technical format)

---

## Damage threshold

- **Minimum:** ¥10,000 (or local currency equivalent)  
- **Below threshold:**
  - Vendor / operator MAY remediate voluntarily
  - No automatic SLO-Bond payment is triggered
- **At or above threshold:**
  - This protocol MUST be applied
  - The case becomes a **Novara incident** and SHOULD appear in public stats

---

## Attribution

Responsibility is split between:

- **AI Vendor** — model, training data, updates  
- **Operator** — deployment, configuration, monitoring  
- **User** — misuse, bad faith, clear policy violation  

They MUST sum to 1.0:

```text
Attribution_AI + Attribution_Operator + Attribution_User = 1.0

Example (medical triage, unnecessary test ¥10,000)

Attribution_AI        = 0.8
Attribution_Operator  = 0.2
Attribution_User      = 0.0

Interpretation:
	•	Model clearly over-weighted age → AI Vendor 80%
	•	Operator failed to cap high-cost tests for low-risk cases → 20%
	•	User followed instructions reasonably → 0%

⸻

Evidence requirements

Automatic payment MUST NOT trigger unless all conditions hold:
	1.	A valid Novara Evidence Bundle v0.1+ exists
	•	Includes: meta.json, aal.ndjson, anchors.json
	2.	Technical verification passes
	•	AAL hash chain is intact
	•	Anchors match the AAL digest
	•	No tampering detected
	3.	Damage is documented
	•	Receipts, bank records, insurer statement, or equivalent
	•	Amount is ≥ threshold
	4.	Causality is clear
	•	There is a plausible link between AI decision and damage
	•	Human reviewer (or encoded rule) confirms the link is not speculative

If any of these fail, the protocol MAY be used as guidance,
but automatic SLO-Bond payment is NOT mandatory.

⸻

Payment execution

Tier 1 — Automatic (¥10,000–¥1,000,000)

For damage between ¥10,000 and ¥1,000,000:
	•	Payment SHOULD be executed automatically by smart contract or equivalent
	•	Target execution time: within 24 hours after:
	•	Evidence verification = OK
	•	Attribution vector = agreed or computed

The amounts are:

Payment_AI        = Damage * Attribution_AI
Payment_Operator  = Damage * Attribution_Operator
Payment_User      = Damage * Attribution_User  (usually 0)

Payments for User share are only allowed when:
	•	Misuse or bad faith is clearly documented, and
	•	This condition is compatible with local law and consumer protection.

Tier 2 — Manual review (≥¥1,000,000)

For damage ≥ ¥1,000,000:
	•	Future Novara Foundation (or equivalent neutral body) MUST review
	•	Recommended timeline: 7–30 days
	•	Parties MAY submit extra evidence or arguments
	•	Partial payments MAY be executed earlier if undisputed portion is clear

⸻

SLO-Bond requirements

Each conformant AI deployment SHOULD maintain:
	•	Minimum SLO-Bond: ¥10,000,000 per deployment
	•	Bonds MUST be:
	•	Segregated from operating funds
	•	Dedicated to incident remedy only
	•	Transparent (public or regulator-visible balance)

When bond balance < 50%:
	•	Operator MUST replenish within a defined grace period (e.g. 30 days)
	•	New high-risk features SHOULD NOT be rolled out until replenished

⸻

Escalation

If any party disputes the result:
	1.	Mediation (optional)
	•	Non-binding, facilitated by neutral third party
	2.	Arbitration (binding, if agreed)
	•	Fast-track, with limited scope:
	•	Evidence validity
	•	Attribution vector
	•	Damage amount
	3.	Court system (jurisdiction-dependent)
	•	Always available as a last resort
	•	This protocol is intended to reduce, not remove, legal rights

⸻

Public reporting

For each incident that triggers this protocol, operators SHOULD publish:
	•	Incident ID (pseudonymous if needed)
	•	Date and domain (medical, finance, etc.)
	•	Damage amount (rounded)
	•	Attribution vector (AI / Operator / User)
	•	Status: resolved / pending / disputed

This enables:
	•	Pattern detection (e.g. repeated failure modes)
	•	Risk pricing
	•	Public and journalistic oversight

⸻

Revision history
	•	v0.1.0 — initial draft (2025-11-19)

⸻

This document is dedicated to the public domain via CC0 1.0.
It may be copied, modified, and integrated into other governance systems
without permission or attribution.