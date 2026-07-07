# Changelog

All notable changes to **The Agent-Native Enterprise** specification are recorded here.
The version in the document header is the authoritative one; every bump gets an entry.

## [2.0.2] — 2026-07-07

Editorial (patch). The Contents block is now clickable — every entry links to its section's
GitHub anchor (all 23 hrefs generated from the actual heading text and verified). No content changes.

## [2.0.1] — 2026-07-07

Editorial (patch, per the versioning policy). Adds [SUMMARY.md](SUMMARY.md) — an informative
narrative companion to the spec (a two-page overview plus a twenty-line at-a-glance version;
the spec governs on divergence) — linked from the README front matter. No normative changes.

## [2.0.0] — 2026-07-07

Review pass — the spec examined against its own text, the reference implementation, and the
July-2026 state of the art (multi-agent failure research, LLM-judge reliability, agent
identity/interop standards, regulation, adoption data). **Major bump** under the new versioning
policy: two invariants gained meaning (INV-2 now carries the bounded-takeover qualification;
INV-9's two-channel rule now defines gate-powers), and §6's idempotency requirement was
corrected. Section numbering is unchanged.

**Contradictions fixed (verifiable against the prior text):**
- **§6 vs INV-4** — the handbrake hard requirement no longer demands universal idempotency;
  HB-2 restates it as *as safe to retry as the effect allows* (exactly-once for owned/reversible,
  at-most-once attempt + recorded outcome for irreversible).
- **§11** — the Auditor-suspends/Steward-reinstates loophole closed: lifting a danger-grade
  suspension is a *human decision*; the Steward may only execute it. Missed-SLA fallback gains a
  defined terminal state (suspension holds; declared safe mode) instead of a circular break-glass path.
- **§11/§10** — suspension now has runtime semantics (compiles to a Governance-plane predicate;
  blocks new dispatch and pre-effect checks), explicit breaker precedence (suspension outranks
  Steward restart), and routing eligibility is registry *status*, not lagging ratings.
- **§9 vs §17** — the Steward's "swap an implementation" is now *provisional failover* to an
  already-authorized implementer; permanent replacement stays Board-only.
- **INV-9/§8/§17** — L1 approval, L0 execution, and break-glass defined as **gate-powers** of the
  constitution channel, resolving the impersonation-binding paradox that made L0 unexecutable.
- **INV-2 vs §7** — the invariant itself now carries the qualification (§7 no longer weakens it);
  contracts declare a human-takeover mode (*run* or *suspend-and-inspect*).
- **§5/§12** — a human takeover always opens a tracked variant (scorecards measure the release,
  not human rescues); Auditor suspension of human-held variants is defined.

**Evidence-contested claims hedged, with §19 citations:**
- Correlated model failure / monoculture named as a trust boundary; implementer heterogeneity
  for checking seats (§4, §4.4, §10, §14).
- Verifier reliability caveat, verdict semantics (pass/return/block), bounded revise loop,
  deterministic programs as a third (and for Verification, preferred) implementer class;
  Verifier false-pass and gaming rows in §14.
- Prompt injection restated as contained-not-prevented (trust boundary); memory-plane provenance
  labels stop stored second-order injection (§5, §14).
- Observability capture is mediated, not self-reported (§5).
- §4.1's coordination-bottleneck claim restated as a named design bet; Direction gains
  contestation (premise-bounce, bounded Board spot-review interval, divergent-framing check).
- Ironies of automation acknowledged; takeover drills + time-to-competent-intervention (§7);
  Board succession duty (§3).
- Statistical floor for autonomy raises (rule of three); complementary evidence for rare-severe
  classes; version identity pins the upstream model snapshot (§5, §8).
- §18's "cost nothing" corrected to "cost no human time"; assurance floor/ceiling and measured
  overhead (§17).
- Board review requires at least one evidence channel the system cannot shape; all
  machine-surfaced proposals carry provenance (§3, §17).
- Adoption base rates engaged: falsifiable pilot kill criteria (§15); adoption-failure table (§14).

**New coverage:** intra-cell human-channel identity (HB-3 + trust boundary); data governance
across the planes (§5); probationary versions + governed deployment (§5, §8, §11); the legal
interface — binding acts are L0, the trail as regulator-facing evidence, named liability (§17);
plane-outage postures + fork-resistant state plane (§14); escalation roster/SLA/compensation and
gate-health monitoring (§12, §7); federation hardening — inbound treaty content untrusted, supra-
constitution through the §17 pipeline at maximal blast radius, cell lifecycle, attested cross-cell
scorecards (§16); compilation hardening — translator ≠ attester, diff-scoped attestation,
integrity-protected compiled artifact, three compile targets (§17).

**Apparatus:** conformance language (required/recommended/optional) + INV/HB requirement ids +
normative/informative marking + maturity note; one-page summary and contents up front; a third
worked example — the failure path, including a wrongful suspension (§18); §13 redrawn so the four
planes span the roles (memory plane first-class); `<br/>` in all diagram labels for renderer
portability; **Appendix A** (all seven role contracts in the §2 shape), **Appendix B** (minimal
handoff vocabulary: Ticket→Goal→WorkItem→Output→Verdict + ActorRef), **Appendix C** (conformance
profiles — Minimal Viable Cell / Full Cell / Federated — and a 27-point evidence checklist),
**Appendix D** (glossary); §19 refreshed (MAST, correlated errors, LLM-judge self-preference,
METR, OWASP/Greshake/CaMeL, Bainbridge, Gartner; MCP, A2A, Entra Agent ID, AP2; EU AI Act,
NIST AI RMF, ISO/IEC 42001, IMDA agentic framework; durable execution; MetaGPT/ChatDev;
Anthropic/OpenAI agent guides); ISO-8601 dates and an explicit semantic versioning policy.

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
