# novara-core

Constitutional documents for **evidence-first AI governance**.

This repo is **text-only**: it defines what Novara-compatible systems  
MUST obey at the _constitutional / protocol_ level.  
All executable code lives in the separate [`Novara`](https://github.com/Novara-developer/Novara) implementation repo.

---

## Core documents (v0.1)

These are the “v0.1 canon” for Novara:

- **[Novara Constitution v0.1](docs/constitution/novara-constitution-v0.1-spec.md)**  
  Evidence-first principles, civic time horizon (2040–2060).

- **[Novara Human-Readable Proof v0.1](docs/constitution/novara-human-readable-proof-v0.1-spec.md)**  
  Plain-language narratives for victims, regulators, and the public.

- **[Novara Incident Protocol v0.1](docs/protocols/novara-incident-protocol-v0.1-spec.md)**  
  How harms are recorded, attributed, and remedied via SLO-Bonds.

- **[Novara Proof Rail v0.1](docs/protocols/novara-proof-rail-v0.1-spec.md)**  
  “No valid proof, no money flow” for AI-driven payments.

Each document is versioned as `*-v0.x-spec.md`.  
Implementations are expected to **pin** the exact version they follow.

---

## Conceptual layers (v0.1)

Novara Core is organised into three main layers:

### 1. Constitution layer

Long-horizon principles and guard-rails:

- What counts as acceptable evidence
- How attribution and responsibility are handled
- Why Novara targets the **2040–2060** civic time window, not just the next product cycle

> If a future implementation disagrees with this layer,  
> it is **not** “Novara-compatible”, even if it reuses the code.

### 2. Protocol layer

Operational rules for systems that move money or cause harm:

- **Incident Protocol** – what happens when things go wrong  
  (incident declaration, evidence requirements, SLO-Bond based remedies).
- **Proof Rail** – payment gate for AI decisions  
  (no valid evidence bundle → payment MUST be refused).

These protocols are **implementation-neutral** and can be adopted by:

- insurers / banks / payment processors  
- regulators and auditors  
- AI system operators who want verifiable rails

### 3. Story layer

How all of this appears to normal humans:

- Human-readable proofs / narratives
- What a victim, journalist, or regulator actually sees
- How “hashes and JSON” turn into “who did what / who pays / what changed”

---

## Planned extensions (not yet in this repo)

The v0.1 set is intentionally small. Future documents are expected to add:

- **Time Court** – counterfactual re-trial of past AI decisions  
  using preserved evidence bundles and policy snapshots.
- **Gen-Z Pact** – a civic right to demand verifiable evidence from AI systems  
  (“show your receipts” as a default expectation).

These will be added under `docs/` as separate specs once they are stable enough.

---

## Relationship to the `Novara` implementation repo

- This repo (`novara-core`) is **text-only** and **vendor-neutral**.
- The [`Novara`](https://github.com/Novara-developer/Novara) repo is the **implementation side**:
  - Evidence Bundle format and reference library
  - CLI tools and tests
  - Example integrations and demo bundles

A system MAY implement the Novara specs without using the reference code,  
but then it MUST still:

1. Point to the exact spec versions it follows (e.g. `novara-proof-rail-v0.1`), and  
2. Provide enough public evidence for third parties to verify conformance.

---

## How to use these specs

You can think of `novara-core` as a **reference constitution** for AI systems that move money.

Typical uses:

- **Read & critique**  
  - The texts are meant to be argued with.  
  - Open issues or forks are welcome when something is unclear, unrealistic, or missing.

- **Fork & adapt**  
  - Regulators, insurers, and researchers are encouraged to copy and adapt the specs  
    to their own legal / cultural context.  
  - Please keep version markers and major changes visible.

- **Implement**  
  - If you claim a system is “Novara-compatible”, you SHOULD:
    - reference the exact spec documents and versions, and  
    - expose evidence (e.g. Novara Evidence Bundles) that third parties can verify.

---

## Versioning

- v0.x documents are **experimental but serious**:  
  they are intended for pilots, research, and early regulatory sandboxes.
- Breaking changes will bump the minor version (e.g. `v0.2`),  
  and, when stable, major versions (`v1.0+`) will be reserved for production use.

Old versions will remain in the repo so that **past cases**  
can always be mapped to the exact rules that were in force.

---

## Contributing

Text contributions are welcome:

- Fix unclear language, typos, or contradictions
- Propose new sections (with clear motivation and examples)
- Link real-world pilots, incidents, and research that stress-test the specs

Please keep changes **minimal and well-scoped**, and open an issue for any  
proposal that changes semantics in a non-trivial way.

---

## License

All texts in this repository are dedicated to the public domain under **CC0 1.0**.  

You may copy, modify, translate, and integrate them into other systems  
without permission or attribution, including for commercial and governmental use.