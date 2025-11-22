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
```

It MUST allow the auditor to find the corresponding Evidence Bundle.

3.3 Evidence Bundle Requirement

Every Proof Rail–protected payment MUST point to a Novara Evidence Bundle v0.1+,
containing at minimum:
	•	meta.json – system, model, policy, time window
	•	aal.ndjson – AI Action Ledger entries
	•	anchors.json – external anchors (blockchain / TEE / TSA / CTK-2 mini, etc.)

The bundle MUST verify using standard Novara tools.

⸻

4. Protocol flow (happy path)

Minimal flow for a conformant implementation:
	1.	AI decision
	•	AI system produces a decision (e.g. APPROVE_LOAN, PAY_CLAIM).
	•	System writes to AAL and seals a CTK-2 mini record.
	2.	Proof request
	•	Payment system calls the Proof Rail with:
	•	proposed payment details (payer, payee, amount, currency)
	•	AI decision_id
	•	CTK-2 mini reference (or bundle_id)
	3.	Verification
Proof Rail MUST verify:
	•	A valid Evidence Bundle exists
	•	AAL hash chain is intact up to the decision
	•	Anchors in anchors.json match the bundle hash
	•	Decision type is authorised to trigger this kind of payment
	•	Amount is within allowed bounds for this decision type
	4.	Decision
	•	If all checks pass → ALLOW with a proof_token
	•	If any check fails → DENY with a clear reason_code
	5.	Payment
The payment processor MUST:
	•	record the proof_token in its own ledger
	•	refuse to execute if no valid ALLOW is present
	6.	Audit
Later, auditors can take:
	•	payment record → proof_token → Evidence Bundle
	•	re-run verification offline using Pocket Judge / Atlas

⸻

5. Minimum data fields

A conformant Proof Rail implementation MUST store at least:

{
  "proof_token": "nvrp:2025-11-19:rail-01:abcd1234",
  "decision_id": "dec-2025-11-19-00123",
  "bundle_id": "nvr-eb-2025-11-19-000045",
  "amount": {
    "value": 50000,
    "currency": "JPY"
  },
  "payer": "insurer:xyz",
  "payee": "customer:12345",
  "decision_type": "INSURANCE_PAYOUT",
  "rail_decision": "ALLOW",
  "reason_code": "OK",
  "timestamp_rail": "2025-11-19T12:34:56Z"
}

Implementations MAY add more fields,
but MUST NOT remove or repurpose these.

⸻

6. Failure modes and handling

6.1 Missing or invalid bundle

If the Evidence Bundle is missing or fails verification:
	•	Proof Rail MUST return DENY with reason_code one of:
	•	NO_BUNDLE
	•	ANCHOR_MISMATCH
	•	AAL_BROKEN_CHAIN
	•	Payment processor MUST NOT execute the payment.

Optional: the system MAY route the case to manual review.

⸻

6.2 Amount mismatch

If the requested payment amount does not match the amount in the AI decision context:
	•	Proof Rail MUST return DENY with reason AMOUNT_MISMATCH.
	•	Operator MUST log and investigate for possible fraud or mis-implementation.

⸻

6.3 Policy violation

If the decision violates active policy (e.g. wrong product, excluded risk):
	•	Proof Rail MUST return DENY with reason POLICY_VIOLATION.
	•	System SHOULD generate a candidate Novara Incident for review.

⸻

7. Security and privacy
	•	Proof Rail SHOULD be deployed in a hardened environment
(e.g. TEE, HSM-protected keys).
	•	Personally identifiable data SHOULD NOT be stored in the Proof Rail database;
only pseudonymous IDs.
	•	All Proof Rail decisions SHOULD be appended to an AAL stream for later audit.
	•	Access to Proof Rail APIs SHOULD be authenticated and rate-limited.

⸻

8. Conformance levels

To keep the bar progressive, we define three levels:
	•	Level 0 – Non-conformant
	•	AI decisions move money with no proof requirement.
	•	Level 1 – Basic Proof Rail
	•	Each payment requires a valid proof_token.
	•	Evidence Bundles are stored but not yet public.
	•	Level 2 – Public Proof Rail (recommended)
	•	Same as Level 1, plus:
	•	aggregated stats are published
(number of payments, total amount, failure reasons)
	•	regulators and auditors get direct read-only access
	•	Level 3 – Full Novara Integration (target)
	•	Proof Rail integrated with:
	•	Novara Incident Protocol (automatic remedy)
	•	SLO-Bond accounting
	•	CTK-2 global evidence mesh

⸻

9. Revision history
	•	v0.1.0 — initial draft (2025-11-19)

⸻

This document is dedicated to the public domain via CC0 1.0.
It may be copied, modified, and integrated into other systems
without permission or attribution.
 