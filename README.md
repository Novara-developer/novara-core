novara-core

Novara core specifications and reference designs for an evidence first Reality OS.

日本語でも簡単に書くと
「AIと人間の判断を、後から検算できるようにする中核仕様集」です。

⸻

0. Status
	•	Early experimental draft
	•	Specs will break between tags v0.x
	•	Not production ready, but stable enough to read, review, and start prototyping

If you are looking for running code, start from the minimal bundle repo and come back here for the rules of the game.

⸻

1. What lives in novara core

This repository is the place where Novara decides
「そもそも何を記録しろ」
「どの粒度まで証拠として要求するか」
「それを誰がどう検算できるか」
を固定する。

Scope
	•	Core concepts and threat model
	•	Normative specs for trace and bundle formats
	•	Canonical schemas and example payloads
	•	Design notes for CTK 2 and AAL
	•	Change control and versioning rules for all of the above

Out of scope
	•	Full production implementations
	•	Vendor specific glue code
	•	Private deployment details

Those live in separate repos and products.

⸻

2. Relationship to other Novara repositories

This repo is the spine. Others hang off it.
	•	novara evidence bundle minimal
Minimal reference implementation and sample bundles that follow the specs in novara core
	•	novara owner spec
Guides for organisations that want to be Novara compatible owners
what to log, how to publish, how to expose evidence to auditors
	•	novara civilization os v0001
Long horizon design notes about 2040 plus governance, economics, courts, and social use cases

Rough mental model
	•	novara core
What is a valid trace and bundle, in exact terms
	•	evidence bundle minimal
Here is one concrete way to emit and verify that trace
	•	owner spec
Here is how an organisation wires this into policy and process

⸻

3. Core ideas in under 5 minutes

These names appear across the docs. novara core is where their exact meaning is pinned down.

CTK 2
Canonical Trace Kit version 2
A minimal but strong checklist of what must be attached to any serious AI decision
inputs, model context, environment, anchors, and a way to replay

AAL
Audit Aligned Ledger
An append only log where every step of a decision is linked, signed, and time anchored in a way that third parties can replay without trusting the operator

Evidence bundle
A portable zip like package that contains
data, configs, logs, anchors, proofs, and a manifest
so that an auditor can say
this decision really came from that system, in that state, under those limits

Proof to Pay
A pattern where payments, approvals, or risk limits are only unlocked if the attached bundle passes verification

Independence
A set of metrics that answer
how many different parties and infrastructures agree that this trace is real
The exact definition and formula live in this repo

Everything else in novara is built on top of these primitives.

⸻

4. Repository layout

Target layout for this repo
	•	docs
High level docs and design notes
	•	docs spec
Normative specifications
CTK 2
AAL
Evidence bundle
Web visit and related sub specs
	•	docs schema
Machine readable schemas
JSON Schema for manifests and entries
Canonical field names and types
	•	docs rfc
Numbered change proposals
rfc 0001 ctk2 minimal fields
rfc 0002 aal entry invariants
rfc 0003 evidence bundle compatibility rules
	•	docs guide
Human readable guides
Implementer guide for infra teams
Auditor guide
Policy writer guide

Some of these directories may be missing right now. The README describes the intended structure so that early contributors and future you have a clear target.

⸻

5. Who this repo is for

The text here is not marketing. It is for people who have to sign off on something that can go catastrophically wrong.

Primary audiences
	•	Infra and platform engineers who will implement logging and bundles
	•	Security and reliability teams who will have to defend incidents in public
	•	Risk, compliance, and insurance people who care about calculable guarantees
	•	Researchers working on AI governance, reproducibility, and secure logging
	•	Regulators and courts that need a concrete technical reference, not buzzwords

If you are writing production code, you probably want to
	•	read specs here
	•	clone novara evidence bundle minimal
	•	emit a small test bundle
	•	run verify on it
	•	only then propose larger integration work

⸻

6. Design principles

At a high level novara core is trying to be
	•	Evidence first
If something is not reconstructable from public or bundled data, it does not count as proof
	•	Tool and vendor neutral
The spec describes what must be visible on the wire and in the bundle, not which specific cloud or model
	•	Auditor centric
A careful third party with no access to internal systems should be able to say
this is consistent or this is broken
in a bounded amount of time
	•	Good enough for 2040
Strong crypto, hybrid attestation, and independent timing are treated as default, not luxury add ons
	•	Strict at the edge, flexible inside
The required external surface is locked down
Inside your organisation you can have many internal logs, but only one canonical projection outwards

These principles show up in the acceptance criteria and invariants for every spec.

⸻

7. Getting started

Short path to make this repo useful for you

Step 1
Read the overview documents in docs
Names and concepts first, maths and edge cases later

Step 2
Pick one spec
For most people that will be ctk2 or evidence bundle manifest
Try to map it onto one real system or process you own today

Step 3
Write down what is missing
Fields you cannot fill yet
Anchors you do not have
Independence dimensions you cannot satisfy

Step 4
File an issue or keep your own notes
This repo will only get better if concrete friction from real systems flows back into the text

⸻

8. Versioning and compatibility

The intention is
	•	v0.x
Fast iteration, breaking changes allowed, explicit changelog
	•	v1.x
Stabilised core
Backwards compatible within the major version
Extensions via optional fields and new profiles, not breaking existing fields

Specs will carry explicit
	•	status draft, experimental, stable
	•	last reviewed date
	•	version and change history

Any implementer is strongly encouraged to record which spec versions and profiles they target inside their bundles, so that future auditors can reason about them.

⸻

9. Contributing

Even at this early stage, outside eyes are useful.

Good contributions include
	•	Threat model corrections
	•	Simpler definitions for the same invariants
	•	Example incidents that should or should not be representable
	•	Cross references to existing standards we should align with, not reinvent

For now, open an issue or a discussion on GitHub. A formal governance and RFC process will move into this repo once the first few specs harden.

⸻

10. License and governance sketch

Code and schemas will be under a permissive open source license.
Textual specifications will be open and usable in both open and commercial contexts, but the Novara name and compatibility marks will be guarded by a future foundation so that they cannot be quietly weakened.

Exact legal text is still in progress and will be documented here once ready.

⸻

11. Contact

For now
	•	GitHub issues on this repository
	•	Direct messages or email listed on the Novara developer profile
	•	In the future, a more formal spec mailing list and public call schedule

If you are a regulator, insurer, or large infra provider and want a private conversation about the direction of these specs, reach out and mention your institution in the subject line so it gets prioritised.