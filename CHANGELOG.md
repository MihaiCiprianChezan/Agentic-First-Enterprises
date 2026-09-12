# Changelog

All notable changes to **The Agent-Native Enterprise** specification are recorded here.
The version in the document header is the authoritative one; every bump gets an entry.

## [3.0.0] — 2026-09-12

Fact-check pass, evidence refresh to the September 2026 state of the art, and a complete
re-authoring of the text in controlled English.

**Major bump.** No invariant changed meaning. Every sentence changed form, and one normative
claim was corrected, so a reader of 2.0.2 must re-read rather than diff. The versioning policy
calls a change to the meaning of a normative requirement major. §6's replay claim was a
normative assumption that implementations were entitled to rely on, and it was wrong.

**Corrections found by the fact-check:**
- **§19 citation error.** arXiv 2506.07962 was labeled *Great Models Think Alike*. That paper is
  arXiv 2502.04313. 2506.07962 is *Correlated Errors in Large Language Models*, and it is the
  correct support for §14's correlated-model-failure boundary. Both are now cited, with the
  distinction stated.
- **§6 replay, corrected.** The prior text asserted that an LLM step is not reproducible in
  general. That is now too strong. Temperature-zero nondeterminism traces to batch-size-dependent
  reduction kernels, and batch-invariant kernels give bit-identical output at roughly a third of
  throughput. Bit-exact re-execution is now an engineering choice with a measured price where you
  control the serving stack. It stays unavailable on a hosted endpoint you do not control. The
  model-snapshot pin and the decision trail remain required, and the section says why.
- **§19 EU AI Act timeline, superseded.** The Digital Omnibus on AI (Regulation (EU) 2026/1744)
  entered into force on 27 July 2026. Annex III high-risk obligations moved from 2 August 2026 to
  2 December 2027. Embedded high-risk moved to 2 August 2028. Article 50 was not deferred. The
  text now states plainly that the deadline moved and Article 14's substance did not.
- **§15 base rates, dated and attributed.** Vague appeals to pilot-failure rates are replaced with
  sourced, dated figures, including the one that matters most for this model: roughly one
  organization in five reports a mature agentic governance model.

**Verified unchanged.** Every 2026 arXiv citation in §19 was checked against the paper and is
correct as cited. The Gartner forecast, the CMR article, the MAST taxonomy, and the
interruptibility lineage all verified.

**New normative content (minor, additive):**
- **§5** — a learned memory policy may operate over working context. It must never write to the
  audit trail, the event history, or the effects ledger. Learned forgetting is a governance
  hazard, because a policy optimized for task success has an incentive to discard the records
  that make an act attributable. New checklist row C27.
- **§6, HB-1** — implementations should checkpoint at effect boundaries rather than at fixed
  intervals, on published evidence that over 75% of agent turns produce no recovery-relevant
  state. The checkpointer-against-durable-execution distinction is now stated.
- **§6** — the replay posture must be declared per implementer class. New checklist row C28.
- **§14** — a new failure row, *allowlist inversion*, with the two 2026 CVEs behind it.
  Authorization binds to the effect and the identity at the tool-call boundary. It never binds to
  the surface form of a command.
- **§14** — a new subsection on the July 2026 agent containment failure, read against this model.
  The lesson is that the failure was organizational, not architectural.
- **§17 — reverse-direction traceability.** The prior text checked traceability in one direction
  only: every compiled rule traces to a clause. It acknowledged that purposive clauses do not
  compile, but never required that partition to be attested, so a ratified clause could be sorted
  silently into the non-compiling bucket and leave a boundary unenforced. Nothing in the forward
  direction could detect it, and the compiled artifact still looked clean. Every clause must now
  leave the translation stage with a recorded disposition — a compiled rule, or an attested
  purposive classification — and no clause may be undisposed. Completeness of the register is a
  deterministic check. Correctness of a purposive classification is a human attestation, and a
  move from compiled to purposive carries the blast radius of a governance change. New §14 failure
  row *silent non-compilation*, fourth adversarial residue in §17, and new checklist row C29. The
  Federated-only row moves to C30.
- **§17 — a rule never outlives its clause.** Every rule carries the content hash of its source
  clause. The runtime refuses to load a rule whose hash no longer matches the ratified text, so an
  amended clause cannot leave an old rule enforcing superseded wording. A stale rule fails closed
  and waits for re-attestation. Folded into checklist row C10 rather than a new row.
- **§17 — break-glass expiry has an enforcement site.** The grant carries its own expiry and the
  pre-effect check evaluates it, on the §11 precedent that a breaker is enforced by the plane
  rather than by a reactive process. A scheduled revoker fails open, which is the one outcome the
  subsection exists to prevent, so it may warn but may never be load-bearing. The clock must be one
  the grant-holder cannot influence. Checklist row C22 rewritten.
- **§14 — the fork-resistance backstop is named.** "Structural backstop" was vague enough to be
  read as endorsing a distributed lock. A lock is advisory, and a writer stalled past its lease
  continues believing it holds the lock, which is exactly the resumed-after-death case. The losing
  writer must be refused at the append. New checklist row C30. The Federated-only row moves to C31.
- **§4.2 and §4.3 — the compensation split is stated.** It was derivable from the authority scopes
  and written nowhere. Orchestration decides whether to unwind, because the decision spans work
  items. Execution performs the compensating call as a within-task effect. A compensating action
  is itself side-effecting, so it carries its own action class, autonomy level, idempotency key,
  and ledger entry. Checklist row C7 extended.
- **§16 — treaties declare vocabulary, not only limits.** New subsection. Two cells can exchange a
  message inside every limit and still mean different things by it, and no limit check can see
  that. The model does not solve semantic divergence and says so. It requires four things: the
  treaty defines every exchanged term, an undefined term is out of envelope and escalates
  Board-to-Board, the boundary mapping passes through the §17 pipeline with its residues, and
  semantic drift is a watched signal. Checklist row C31 extended.
- **§2 and Appendix A — a *run* takeover mode declares its bound.** Fan-out grows over the life of
  a cell, so a role that was human-runnable at its original load may saturate its buffers later,
  and nobody finds out until a takeover is under way. The contract now states the condition under
  which *run* holds, and the Steward monitors it. The mode itself stays static: a role that
  re-declared its own takeover mode from telemetry would author its own governance (INV-10).
  Checklist row C2 extended.
- **How to read, maturity** — the reference cell does not yet implement the clause-disposition
  register. It traces rules forward to clauses and checks the reverse direction by inspection,
  which is adequate at twelve rules and is not an auditable artifact. Stated in the document
  rather than left for an auditor to find.

**Evidence refreshed:** the NVIDIA AVO harness result as the central empirical case for the whole
document, the Five Eyes joint guidance of 1 May 2026, the OWASP 2026 agentic top ten, the
Singapore IMDA agentic framework, the NIST agent-standards initiative, the honest gap in NIST AI
RMF and ISO/IEC 42001 for agentic risk, A2A and MCP under one foundation, agent-identity
mechanisms that reached general availability, OpenTelemetry GenAI conventions as a candidate for
mediated capture, Policy Cards and layered-translation prior art for §17, and the 2026 memory and
continual-learning direction. Every §19 entry now carries a date.

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
