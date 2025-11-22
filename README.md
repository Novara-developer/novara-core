# novara-core

Text-only constitutional specs for the Novara ecosystem.  
Code lives in the implementation repo; this repo defines **what must be obeyed**.

---

## Core documents (v0.1)

- [Novara Constitution v0.1](docs/constitution/novara-constitution-v0.1-spec.md)
- [Novara Human-Readable Proof v0.1](docs/constitution/novara-human-readable-proof-v0.1-spec.md)
- [Novara Incident Protocol v0.1](docs/constitution/novara-incident-protocol-v0.1-spec.md)
- [Novara Proof Rail v0.1](docs/protocols/novara-proof-rail-v0.1-spec.md)

---

## Conceptual layers (v0.1)

Novara Core is organised into layers:

- **Constitution layer**  
  - *Novara Constitution v0.1* – evidence-first principles, civic time horizon (2040–2060).

- **Protocol layer**  
  - *Novara Incident Protocol v0.1* – how harms are recorded, attributed, and remedied (SLO-Bonds).  
  - *Novara Proof Rail v0.1* – “no valid proof, no money flow” for AI-driven payments.

- **Story layer**  
  - *Novara Human-Readable Proof v0.1* – plain-language narratives for victims, regulators, and the public.

Planned (not yet specified in this repo):

- **Time Court** – counterfactual re-trial of past AI decisions, based on evidence bundles.  
- **Gen-Z Pact** – a civic right to demand verifiable evidence from AI systems (“show your receipts”).

Implementation details, libraries, and CLIs live in the separate [`Novara`](https://github.com/Novara-developer/Novara) repository.  
`novara-core` stays text-only, spec-first, and vendor-neutral.

---

## How to use these specs

- **Read & critique** – these docs are meant to be argued with.  
- **Fork & adapt** – regulators, insurers, and researchers are encouraged to adapt the texts to their own contexts.  
- **Implement** – any system that claims “Novara-compatible” behaviour SHOULD point to the exact spec version it implements (e.g. `novara-proof-rail-v0.1`).

---

## License

All texts in this repository are dedicated to the public domain under **CC0 1.0**.  
They may be copied, modified, and integrated into other systems without permission or attribution.