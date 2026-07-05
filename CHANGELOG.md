# Changelog

All notable changes to **The Agent-Native Enterprise** specification are recorded here.
The version in the document header is the authoritative one; every bump gets an entry.

## [1.6.0] — 2026-07-05

Definition and precision pass — closes the gaps surfaced by building the reference
implementation ([Agentic-Enterprises-A](https://github.com/MihaiCiprianChezan/Agentic-Enterprises-A)).
No structural changes; sections and invariant numbering are unchanged.

- **§8** — blast radius formally defined: two axes (reach × reversibility), a default
  level-mapping table (tighten-only), worse-axis-wins, round-up-in-doubt.
- **§2** — acceptance-criteria authorship and negotiation: Direction authors, Executor and
  Verifier are barred from authoring, criteria must be checkable, untestable criteria return
  to Direction as an escalation.
- **§5** — the version registry sketched as fields and guarantees: identity, lineage
  (incl. tracked handbrake variants), status lifecycle, attribution; the per-version
  scorecard is derivable from the event history.
- **§17** — a worked example of one clause traversing the full compilation pipeline
  (constitution → structured policy → machine rule → runtime enforcement → validation).
- **§10** — the Optimizer/floor feedback loop named and closed: telemetry informs a floor
  proposal with visible provenance; only a human moves a floor.
- **§1** — invariant #9 sharpened: pithy "Office ≠ Role" headline with the two-channel rule
  as its explicit corollary (numbering unchanged).

## [1.5.0] — 2026-06-15

- First public release of the specification (the document reached v1.5.0 through
  pre-publication drafts; earlier versions predate this repository).
- 19 sections: the 11 design invariants, role-as-interface, the Representation &
  Accountability layer, operating and system roles (Director / Orchestrator / Executor /
  Verifier · Steward / Optimizer / Auditor), the four planes, the Handbrake, the authority
  and autonomy model, escalation and takeover, reference topology, failure modes, adoption
  sequence, cell sovereignty and federation, constitutional mechanics, worked examples,
  and related work.

### Post-release notes (unversioned)

- 2026-06-27 — "Note on intent" refined; added the reference back-link to the practical
  implementation repo ([Agentic-Enterprises-A](https://github.com/MihaiCiprianChezan/Agentic-Enterprises-A)).
- 2026-07-05 — Repository licensed under CC BY 4.0; this changelog added. No specification
  content changes (still v1.5.0).
