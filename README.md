---
Author: Mihai-Ciprian Chezan
Version: 3.0.0
Date: 2026-09-12
---

# The Agent-Native Enterprise

**A reference operating model for organizations built on three rules. An agent or a human can fill any role. Every process is built for agents first. A human can stop, adjust, and continue every flow.**

![The-Agent-Native-Enterprise](./images/The-Agent-Native-Enterprise.webp)

This is a generic model. Software delivery was its inspiration, but the model is not specific to software. The same structure applies to any organization that pursues a goal. This includes operations, services, research, manufacturing coordination, and back-office work.

Two properties define the model. They also separate it from a conventional org chart with chatbots attached:

1. **Role polymorphism** — a role is a contract, not a person. An agent, a human, or a deterministic program can satisfy the same contract. Each one can replace the others. Invariant #2 and §7 state the exact limit of this exchange at high throughput.
2. **Universal interruptibility** — every autonomous flow has a handbrake. A human with AI skill can stop the flow, examine its state, inject an adjustment, and continue it. This is a property of every flow by design. It is not an exception that some flows support.

**Humans do not disappear from the top of this model.** They move to the places where human judgment and human accountability have no substitute. A human **Representation and Accountability layer** sits above the agentic organization. This document calls it the *Board*. The Board sets the purpose and the boundaries of the organization. It carries the legal and public responsibility. It answers for the organization in the human world.

The Board is not removed. It is relocated. It moves *out* of the millisecond decision loop, where human latency is only a bottleneck. It moves *into* the part of the structure that only humans can hold.

The Board is a **pattern, not a headcount**. The Board can be one hundred people, ten people, or one founder. A one-person company and a large enterprise run the identical model. Only the size of the human layer changes. Existing leadership structures map onto this layer without modification. What changes is that they stop being the operational bottleneck. See §3.

**The model is not limited to new organizations.** Its unit is a self-contained, sovereign **cell**. A cell can be an entire company. A cell can also be one bounded zone that runs in parallel inside an existing organization, staffed by people who already work there. Many cells compose into a federation without a change to the pattern. See §16.

## In one paragraph

*One model, one rule of thumb. Humans hold the Offices and write the constitution. Agents fill the Roles and do the work. System roles keep the machine healthy (Steward), efficient (Optimizer), and trustworthy across versions (Auditor). A human can stop any flow, correct it by hand, and continue it. A human can become any Role at any moment — and the constitution they wrote binds them exactly as it binds every agent.*

*(Do you prefer a narrative? [SUMMARY.md](SUMMARY.md) holds a two-page overview and a twenty-line at-a-glance version.)*

## Contents

[§1 Design invariants](#1-design-invariants) · [§2 The role as an interface](#2-core-abstraction-the-role-as-an-interface) · [§3 The Representation and Accountability layer](#3-the-representation-and-accountability-layer-the-human-board) · [§4 Operating and system roles](#4-operating-and-system-roles) · [§5 The planes](#5-the-planes) · [§6 The Handbrake](#6-the-handbrake-control-plane-in-depth) · [§7 Agent-first, human-tolerant execution](#7-agent-first-human-tolerant-execution) · [§8 Authority and autonomy](#8-authority-and-autonomy-model) · [§9 The Steward](#9-the-steward-the-org-doctor-named-for-what-it-does) · [§10 The Optimizer](#10-the-optimizer-capability-to-task-matching) · [§11 The Auditor](#11-the-auditor-version-fitness-and-safety) · [§12 Escalation and human takeover](#12-escalation-and-human-takeover) · [§13 Reference topology](#13-reference-topology) · [§14 Failure modes, guardrails, and trust boundaries](#14-failure-modes-and-the-guardrails-that-contain-them) · [§15 Adoption sequence](#15-adoption-sequence-lean) · [§16 Cells, sovereignty, and federation](#16-the-cell-sovereignty-and-federation) · [§17 Constitutional mechanics](#17-constitutional-mechanics) · [§18 Worked examples](#18-worked-examples-end-to-end) · [§19 Related work](#19-related-work-positioning-and-references) — [Appendix A: the seven role contracts](#appendix-a--the-seven-role-contracts-normative-baseline) · [Appendix B: a minimal handoff vocabulary](#appendix-b--a-minimal-handoff-vocabulary-informative-proven-in-one-cell) · [Appendix C: conformance profiles and checklist](#appendix-c--conformance-profiles-and-checklist) · [Appendix D: glossary](#appendix-d--glossary-informative)

## How to read this document

**Conformance language.** Statements with **must**, **never**, or **is required** are binding. An implementation that does not satisfy them does not conform. Statements with **should** or **recommended** are strong defaults. Deviate from them only with a recorded rationale. Statements with **may** or **optional** are choices.

The eleven invariants carry the citation **INV-1** to **INV-11**. The §6 handbrake requirements carry the citation **HB-1** to **HB-4**.

These parts are informative: the one-paragraph summary, the contents, the §13 diagram, the §18 examples, §19, Appendix B, and Appendix D. Appendix A is a **normative baseline**. An adopting cell copies it and may adapt it. Those adaptations are constitutional content. In Appendix C the **profile definitions are normative**. The checklist is a derived aid. Where a checklist row and the body disagree, the body governs. Everything else is normative.

The model deliberately leaves some values to each organization. In those places it says *declared in the constitution*. That is delegation. It is not an unspecified gap.

**Language.** This document uses controlled English, in the style of ASD-STE100 Simplified Technical English. Normative statements follow the strict rules: one idea per sentence, active voice, and no semicolons. Explanatory prose follows the same structural rules but keeps a wider vocabulary. The goal is one reading per sentence, because an implementer or an agent must parse this text without an author to ask.

**Maturity.** The reference cell implements §1 to §15 and §17 to §18 at least once, with two exceptions named here rather than left for an auditor to find. The clause-disposition register of §17 (checklist row C29) is specified but not yet built. The reference cell traces rules forward to clauses and checks the reverse direction by inspection. That is adequate at twelve rules, and it is not an auditable artifact. The federation layer of §16 — treaties and the supra-constitution — is at design stage. No two-cell deployment has exercised it. This document labels both speculative until they are built.

**Evidence base.** Where this document cites a measurement, a regulation, or an incident, the citation carries its date. The evidence base was verified in September 2026. §19 holds the sources.

---

## 1. Design invariants

These are the non-negotiable rules. The document cites them as INV-1 to INV-11. Everything below is a consequence of them.

1. **Depend on the contract, not the implementer.** No part of the system may assume that an agent holds a role. No part may assume that a human holds it. Each part depends only on the declared inputs, outputs, authority, and guarantees of the role.
2. **Agent-first, human-tolerant.** Default execution runs at agent speed. A human can *stop, examine, and correct* every role at any time. A human can also *run* a role if the contract declares its throughput to be human-boundable. A role that is not human-boundable must declare suspend-and-inspect as its human-takeover mode in its contract. See §2 and §7. In both cases the surrounding system must continue to function at a lower speed, and must not cascade into failure.
3. **Every flow has a handbrake.** Interruptibility is core architecture. It is not a feature. A flow that a human cannot pause, examine, adjust, and continue does not conform.
4. **Side-effecting actions are as safe to retry as the effect permits.** Where an effect is yours or reversible, make it idempotent. A retry or a resume then never duplicates it. Where an effect is irreversible and a non-idempotent outsider owns it, the guarantee becomes narrower. You cannot recall a sent message. You cannot recall a shipped unit. For these effects the guarantee is at-most-once *attempts*, plus compensation where a reversal exists. Never assume that the outside world is idempotent. Engineer safety on the side that you control.
5. **State lives outside the actor.** Shared, durable storage holds the context, the progress, and the history. This state never lives only in the transient memory of an agent or in the head of a human. Any implementer can then take over a role in the middle of a flow.
6. **Authority is graduated and explicit.** Every action class has a declared autonomy level. The blast radius sets how much human gating the class requires.
7. **One abstraction per layer.** A layer never reaches across levels. The top layer does not know about individual tool calls. A worker does not know the global strategy. This rule is what keeps the system debuggable.
8. **Add hierarchy only when complexity forces it.** Most designs add one tier too many. Start with the fewest layers that solve the problem.
9. **Office is not Role.** A human holds an *Office*. An Office carries accountability and representation in the human world. An agent fills a *Role*. A Role is an operational seat in the agentic organization. Offices and Roles are not one-to-one.

   The corollary is the **two-channel rule**. Humans affect the agentic organization through exactly two channels, and through nothing else. The first channel is the constitution. Humans author it and amend it. Humans also *exercise the gate-powers that it explicitly grants to them*: an L1 approval, an L0 execution, or a break-glass act. See §8 and §17. The second channel is impersonation of a Role. A gate-power is narrow, momentary, and enumerated. Impersonation is open-ended: the human holds the seat of a Role under the authority of that Role.

   One invariant has two faces. The distinction says what a human *is* to the organization. The corollary says how a human *reaches* it.
10. **Governance is the compiled constitution — its rule-shaped part.** The Governance plane encodes the *projection* of the constitution that reduces to rules. This includes authority ceilings, permissions, budget caps, and required gates. The purposive core does not compile. Whether the organization still serves human interest stays in human Board review. See §3. Every encoded constraint traces back to a written human mandate. Agents never author their own constraints. The plane enforces the mechanical fraction. Human judgment carries the substantive remainder.
11. **A cell is sovereign at its boundary.** A cell is an organization in itself. Nothing outside it may affect it except through its own constitution or through an authorized Role. This applies to a parent organization and to a sibling cell. The boundary obeys the same law as the interior.

---

## 2. Core abstraction: the role as an interface

A **role** is a declared contract with this shape:

| Field | Meaning |
|---|---|
| **Responsibility** | The single outcome that this role owns. |
| **Inputs** | What it consumes, and from which roles. |
| **Outputs** | What it produces, and to which roles. |
| **Authority scope** | What it may decide and act on alone. What it must escalate. |
| **Acceptance criteria** | How the system judges "done" and "correct". |
| **Escalation rule** | The conditions that make it hand off to a human or to a higher role. |
| **Observability hooks** | The traces, costs, and signals that it must emit. |

An **implementer** satisfies the contract. An implementer is an agent, a human, or a deterministic program. The system binds to the contract. A human who enters a role is therefore a runtime substitution, not a redesign. This is the same principle as an interface with interchangeable implementations. The caller does not change when the implementation changes.

This document gives the contract as *fields and guarantees*. It deliberately does not give a file format or a schema language. The model specifies what a role must declare. It never specifies how to write it down. This omission is intentional. It keeps the model independent of any toolchain and of any era of tooling.

A contract also declares its **human-takeover mode**. The mode is *run* — a human can hold the seat at its working throughput. Or the mode is *suspend-and-inspect* — a human stops the role, examines it, and corrects it, but cannot run it live. See INV-2 and §7. Appendix A instantiates this contract shape for all seven roles.

**A *run* declaration must carry the bound that makes it true.** Fan-out and throughput change over the life of a cell. A role that a human could hold at its original load may saturate its buffers later, and nobody discovers that until a takeover is already under way. The contract therefore states the condition under which *run* holds, such as a fan-out ceiling or a queue-depth ceiling. The Steward monitors that condition (§9). A breach is a drift signal and a proposed amendment (§17).

The mode itself never changes at runtime. A role that re-declared its own takeover mode from telemetry would author its own governance, which INV-10 forbids. The declaration is static. The bound makes it falsifiable.

**Who writes the acceptance criteria.** The role that *issues* the work authors the criteria. Direction sets them when it specifies a goal. To turn demand into well-specified direction is the one job of that role. See §4.1. Each decomposition then inherits or refines the criteria downward.

Two roles must never author acceptance criteria:

- The **Executor** must not, because the producer cannot write its own bar.
- The **Verifier** must not, because the gate cannot write its own bar either. The Verifier scores against criteria that it did not set. That is what makes the independence of the checker real.

Every criterion must be *checkable*. A criterion is a statement that the Verifier can score as met or unmet. It is not an aspiration. Every criterion must be *mechanically* checkable where possible — a test, a schema, or a policy predicate. Judgment-graded criteria are permitted. They inherit the machine-judge reliability caveat of §4.4.

The Verifier sometimes finds a criterion untestable or ambiguous. It sometimes finds a goal whose framing contradicts the constitution or its own stated premises. In these cases the Verifier must not interpret silently. It returns the goal to Direction as an escalation, in the same way that it returns a failing output. Ambiguity goes back to the role that resolves it. The role that judges never absorbs it.

**Human impersonation on demand** is the default mode for substitution. Every role runs as an agent until a human assumes it for a specific need. That need is a hard decision, a novel situation, a correction, or an audit. The human then returns the role to an agent.

---

## 3. The Representation and Accountability layer (the human Board)

The agentic organization needs a human anchor in the human world. An agent cannot be that anchor. An agent cannot hold legal accountability. An agent cannot sign a binding commitment. An agent cannot face a regulator. An agent cannot stand as the responsible human face of the entity.

Conventional organizations fuse this representation with day-to-day operational decisions. This model **separates them**:

- **Accountability and representation** → human, deliberately *outside the hot path*, at human-world cadence.
- **Operational decisions** → agentic, *inside the hot path*, at agent speed.

The reason is speed. A human who stays permanently in the decision loop becomes the bottleneck that the whole system must slow down to. The humans therefore sit above the loop. They reach into it only on purpose.

### The Board is a pattern, not a group

The Board can be one hundred people, ten people, or one person. A single-founder company runs a Board of one. A large enterprise runs a large one. The responsibilities below are identical at every size. Only the headcount changes. Existing executive and governance structures fit here without modification. They simply stop being the limit on operational throughput.

### Is the Board only the management layer, returned in disguise?

This is a fair objection. The model folds the CEO, the Product Owner, and the Project Manager into one agentic Director. If agents absorb the coordination layer, why does a human layer appear again on top?

The answer is that the Board does the one thing that an agent *structurally* cannot do. It holds legal accountability and it authors the constitution.

"Management" in the sense that the model removes is *operational coordination*. That means the decision about who does what and when, and the reconciliation of the moment. The Director and the Orchestrator absorb exactly that work. What the Board keeps is not coordination. It is *answerability and purpose-setting*. The Board is the human that the law and the public hold responsible. The Board writes the goals that the system pursues. Neither task becomes more efficient at agent speed. Both require a human, because their value is accountability, not throughput.

The Board is not the management layer returned. It is what remains after coordination is automated.

The word "remains" understates one thing, so this document states it here rather than leaves it to be discovered later. The Board also keeps the *outward-facing* work of the organization. This includes market sensemaking, capital, partnerships, and the external relationships whose value is human trust. These stay human-held for the same reason that accountability stays human-held: their currency is trust, not throughput. Where relationship capital is the product, this function is large. The Board should treat it as a duty, not as a leftover.

### What the Board does (levers only — never hands-on operation)

1. **It authors the constitution.** The constitution holds the purpose, the values, the goals, and the behavioral boundaries of the organization. It is the source document that the top agents operate under.
2. **It maintains and amends the constitution.** The constitution is living. The Board owns its changes.
3. **It runs a periodic human-interest alignment review.** This review checks that the agentic organization still serves the human purpose that it was built for. It checks that the organization has not drifted into work that is technically flawless and wrong.

   The test is concrete. Divergence from the *written* purpose is drift, and the Board corrects it. A deliberate, ratified change to that purpose is evolution, and it is a constitutional amendment. The Board measures behavior against the text, not against a mood.

   The independence of the evidence bounds the power of the review. A review that consumes only the telemetry of the cell does not conform. The review requires at least one channel that the reviewed system cannot shape. Acceptable channels are Board-chosen raw-trace sampling from the tamper-evident event plane, direct stakeholder contact, or an external audit. The constitution declares the cadence and the sample size against the action volume of the cell.

   The constitution also declares a ceiling on the interval between Board spot-reviews of the goal-framing of Direction. The constitution may state that ceiling as an action volume instead. "Periodic" then bounds how long a mis-framed goal can run unexamined. See §4.1.
4. **It holds binding authority to mandate modification.** The Board issues this as a constitutional amendment or as a formal change request. It never issues it as turn-by-turn interference.
5. **It carries legal and representational accountability.** The Board answers for the entity in the human world.
6. **It owns succession.** This covers succession of Board members. It also covers succession of the standby humans who can competently impersonate each critical Role. See §12. The safety valve of the model is a human bench, and that bench decays without deliberate regeneration. See §7. To keep the bench staffed and practiced is a Board duty. It is not an assumption.

### How the Board decides

The model governs the Board in the way that it governs everything else. It writes the rules down. A Board of one needs no procedure. Any larger Board must declare its *own* decision rules **in the constitution**. Those rules state the quorum, the threshold to ratify or amend, how internal disputes resolve, and what happens on deadlock.

This is the self-referential closure of the model. The constitution governs its own amendment process. Nobody improvises "how the Board decides" at the moment when it matters most.

The model requires only that these rules exist and are written. It does not prescribe their content. A founder may keep sole authority. A council may require a supermajority. That choice belongs to the organization.

### Constitution to governance pipeline

The Board writes the **constitution** in human language, as human intent. The pipeline compiles it into the machine-readable **Governance plane**. See §5. The top agents read that plane and obey it at runtime.

This is the same shape as constitution to law to regulation. A human principle becomes an enforceable runtime constraint. It is also why INV-10 holds. Agents never write their own rules.

### Office is not Role

A human holds an **Office**. Board member, Chair, CEO, and CFO are Offices. An Office is a human-world title that carries accountability and representation.

An agent fills a **Role**. Director, Orchestrator, Executor, Verifier, Steward, Optimizer, and Auditor are Roles. A Role is an operational seat in the agentic organization.

**Offices and Roles are distinct and not one-to-one.** "CEO" is an Office. "Director" is the Role that owns top-level operational direction. The human CEO does not *run* the organization turn by turn. The Director agent does.

### The impersonation-binding rule

A Board member sometimes impersonates a Role. For example, the member steps into the Director seat through the handbrake. In that seat **they act as that Role**. They inherit the authority scope of the Director. The same Governance plane binds them that would bind the agent. They do **not** carry their Office authority into the seat.

A human cannot enter a Role and act outside the constitution because they are "really the CEO". To do something that the governance forbids is not a keyboard action. It is a **constitutional amendment**, which is slow, deliberate, and audited.

The handbrake lets humans operate *within* policy. Only the Board, acting as the Board, changes policy. Two powers, two speeds, and two separate audit trails.

### Board review, Steward monitoring, and Auditor rating are three different things

- The **Steward** (§9) watches the *operational and behavioral* drift of a live instance. Does the agent follow the written rules and work correctly right now? This is continuous, technical, and at agent speed.
- The **Auditor** (§11) rates *versions* over accumulated activity. Is this release better, worse, or more dangerous than the last one? This is continuous, evaluative, and at agent speed.
- The **Board** (§3) watches *purpose* drift. Are the rules still the right rules? Does the organization still serve human interest? This is periodic, judgment-based, and at human speed.

The Steward catches "the Director instance malfunctions". The Auditor catches "Director v5 regressed against v4". The Board catches "the Director executes the wrong mission flawlessly". None of the three can do the job of the others.

### The one Board failure mode to guard against

The Board must not slide into **shadow operation**. When the Board makes continuous turn-by-turn calls, it reintroduces the human bottleneck that it exists to remove. Its influence must flow through the constitution and through bounded Role-impersonation. It must never flow through interference.

---
## 4. Operating and system roles

Roles divide into two kinds. **Operating roles** form the value chain. They turn intent into delivered outcomes. **System roles** own no business outcome. They keep the machine healthy, efficient, and trustworthy.

Each role below lists a suggested human-readable holder name. The generic noun is the role. The name in parentheses is what a reader can picture a "person" being called.

Roles are *logical contracts*. They are not necessarily separate systems. Two roles may run on one underlying implementation with different permissions. What separates them is authority and the object that they act on. The process that runs them does not separate them.

The trust boundaries of §14 make one caveat explicit. A shared implementation separates *authority*. It never separates failure modes. A checking role should therefore not share a single point of provenance with the thing that it checks, on high-blast-radius classes. See §4.4 and §10.

### Operating roles

#### 4.1 Direction *(holder: Director)* — consolidates CEO, Product Owner, and Project Manager

Direction owns **what and why**. It takes intent from stakeholders or clients. It converts that intent into a prioritized backlog of goals with constraints and acceptance criteria. It operates under the constitution. It holds the highest operational decision authority.

The three legacy roles collapse here on a stated bet. *To the extent that* agents drive execution and coordination competently, the residual human-scarce input is clarity of intent. Direction then has one job: to turn demand into prioritized, well-specified direction.

This document names it a bet because the measured evidence still points the other way for current-generation systems. Inter-agent coordination failures remain a leading empirical failure class. The MAST study annotated more than 1,600 execution traces across seven multi-agent frameworks. It identified 14 failure modes in three categories: system design, inter-agent misalignment, and task verification. See §19. That evidence is exactly why Orchestration stays its own role, why the Steward watches it hardest, and why §14 keeps "supervisor as single point of failure" on the books.

At large scale this role can concentrate too much. The answer is not to make the Director larger. The answer is to **split the cell** (§16). Within INV-8 you may instead tier Direction, with a portfolio level above a cell level. Decompose only when the load demands it.

Concentration is also a *framing* risk, not only a load risk. The Director authors both the goals and their acceptance criteria. A mis-framed goal therefore passes every downstream gate, and the catch by the Board is periodic. Three cheap counters exist:

1. The premise-bounce of the Verifier (§2).
2. The ceiling on the Board spot-review interval, declared in the constitution (§3).
3. A **divergent-framing check** for high-stakes goals. A second Direction variant frames the goal independently. A human may do this instead. Disagreement escalates (§12).

#### 4.2 Orchestration *(holder: Orchestrator)*

Orchestration owns **who does what, and when**. It decomposes each goal into work. It routes that work to Executors. It sequences dependencies. It handles exceptions. It decides whether to retry, to escalate, or to proceed.

This is the supervisor layer. It does not do the work. It does not set strategy.

**Compensation across sequenced work is an Orchestration decision.** A step sometimes fails after prior steps left effects behind. The Orchestrator then decides whether to unwind them, to proceed, or to escalate. That decision spans the work items, so only the role that sequenced them can make it (INV-7). The Executor performs the compensating call as an ordinary within-task effect. See §4.3.

#### 4.3 Execution *(holder: Executor, also called Specialist)*

Execution owns **how**. Executors are specialist implementers that produce the actual work product. They are narrow, deep, and replaceable. An Executor knows its task and its tools. It does not know the global plan.

An Executor therefore never decides to unwind a sequence. It performs one compensating call when Orchestration directs it to (§4.2).

**A compensating action is itself a side-effecting action.** It carries its own action class and autonomy level (§8). It carries its own idempotency key and its own effects-ledger entry (HB-2). No compensating action is exempt from the gate that its forward counterpart would have met. A rollback that sends a correction to a client is an outward-facing effect, and the blast-radius table classifies it as one.

#### 4.4 Verification *(holder: Verifier, also called Reviewer)*

Verification owns **is it correct and within policy**. It scores outputs independently against acceptance criteria, quality, safety, and conformance, before those outputs take effect. It runs as an evaluator loop against Execution: produce, score, revise.

Independence from Execution is the point. The checker is not the producer.

Role independence is not *statistical* independence. An Executor and a Verifier that are built on the same base model, or on a similar one, share blind spots. Machine judges measurably favor outputs of their own lineage, and 2026 work shows that self-refinement pipelines *amplify* that bias. The produce-score-revise loop is exactly such a pipeline. See §19.

For high-blast-radius classes the constitution should require the Verifier seat to be **implementation-independent** of Execution. Use a different model family. A deterministic checker is better still.

Where acceptance criteria are mechanically checkable, a deterministic program is the *preferred* Verifier. Its independence is established by construction rather than monitored. It cannot be prompt-injected. It is also the cheapest implementer available. This is role polymorphism working as designed (§2). It is not an exception to it.

**The gate has three defined outcomes:**

- **Pass** — the output may take effect.
- **Return** — revise against the cited criteria. The constitution declares a revision limit. After that limit the flow escalates per §12. An unbounded produce-score-revise loop is optimization pressure against the gate. Reward hacking needs no compromise of the gate. It needs only iterations. The 2026 literature on reinforcement learning with verifiable rewards shows the same effect: a policy learns to exploit what the verifier fails to enforce. See §19.
- **Block** — a policy or boundary violation. This is a binding stop. The system logs it with the cited clause.

A per-criterion *unclear* score triggers the ambiguity rule of §2. The Verifier returns the criterion to Direction. It never interprets it silently.

Verification may decompose at scale into distinct correctness, compliance, and risk checks, like any other role. Do this only when complexity forces it (INV-8). By default Verification is one gate. The Governance plane enforces policy and compliance cross-cuttingly, rather than as an addition to Verification.

### System roles *(non-authoritative — they optimize the machine, not the business)*

#### 4.5 Steward *(holder: Steward)* — the renamed "org doctor"

The Steward owns **are the role-holders themselves healthy and behaving normally**. It monitors, maintains, tunes, and repairs the other roles. It watches the high-authority Direction and Orchestration agents most closely. It has full technical capability over them and **zero business-decision authority**. §9 gives the detail.

#### 4.6 Optimization *(holder: Optimizer)*

The Optimizer owns **is each task handled by the right-capability implementer**. It sits optionally between steps. It decides which model or implementer a given task requires. The risk and quality floor of the task bounds that decision. §10 gives the detail.

#### 4.7 Audit *(holder: Auditor)*

The Auditor owns **how versions of agents compare over time**. It judges whether a given version is better, worse, or more dangerous than another, and which release is currently fit. It rates agent versions continuously from their accumulated activity. Normally it only monitors and reports.

The Auditor may **suspend** a dangerous or severely drifting version and escalate to humans. It cannot modify, dismiss, restart, or reinstate. §11 gives the detail.

| Kind | Role | Holder | Owns | Authority |
|---|---|---|---|---|
| Operating | Direction | Director | What and why | Highest, within the constitution |
| Operating | Orchestration | Orchestrator | Who and when | Routing, retry, escalate |
| Operating | Execution | Executor | How | Within-task only |
| Operating | Verification | Verifier | Correctness and conformance | Gate: pass, return, or block |
| System | Steward | Steward | Health of live role-holders | Technical only. **No business decisions** |
| System | Optimization | Optimizer | Capability-to-task fit | Selection only. **No business decisions** |
| System | Audit | Auditor | Fitness and safety of versions | Monitor and report. May suspend and escalate. **No modify, dismiss, or reinstate** |

Every role is an agent by default, with human impersonation on demand. Every role may also be a deterministic program wherever the contract is machine-checkable (§4.4).

---

## 5. The planes

Roles run *inside* four cross-cutting planes. A plane is shared infrastructure that every role depends on.

### Governance plane

This plane is the machine-readable, runtime-enforced encoding of the constitution of the Board (§3). It holds authority limits, guardrails, constraints, and an append-only audit trail.

Policy is data that the agents read at runtime. It is not documentation that humans read later. Nothing acts outside it.

### Memory and context plane

This plane holds durable shared state. That state includes the current state of every goal, an append-only event history of decisions and actions, the artifacts produced, and a **version registry**.

The version registry identifies every agent version and every parallel variant. It attributes activity to them. Without it the Auditor cannot compare versions.

A *version* is the whole behavioral bundle. It covers logic, prompts, weights, and configuration. It is not merely code.

A human takeover or a handbrake adjustment **opens a tracked variant** for the duration of human control. That variant is a `variant_of` the incumbent version. The system closes it on hand-back. This is never an untracked change. Three consequences follow. The registry stays the source of truth. The scorecard of a version measures the release, rather than a human who quietly rescued it. Human interventions stay separately attributable.

This document states the registry as fields and guarantees, in the same way that it states the role contract in §2. It never states a schema language. A registry entry declares four things:

1. **Identity** — the role and the version id. Where the implementer is a hosted model, the entry must also pin the upstream model snapshot. Without that pin, provider-side updates change the behavioral bundle silently in the middle of a rating.
2. **Lineage** — what the version derives from. This is the predecessor, or the `variant_of` link for a tracked variant.
3. **Status**, over a declared lifecycle. The minimum lifecycle is **probationary**, active, rolled back, and suspended. A new version enters as probationary. It *earns* active status under the evidence rule of §11. Rolled-back-by-Steward and suspended-by-Auditor stay distinct and separately attributable acts.
4. **Activation time.**

Every recorded act carries **who acted**. That means the role, the version, the *mode* (agent, human, or program), and the **principal**. The principal is the authenticated identity behind the act. For a human-held act *in any capacity* the principal is the named human (HB-3, §14). Otherwise it is the agent instance identity or the program instance identity. The act also carries the Office when a human acts in Board capacity.

Three rules are enforceable only if the record holds identity *and* capacity per act: the impersonation-binding rule (§3), separation of record (§16), and named-human attribution (HB-3, §17).

A per-version scorecard is then derivable from the event history. It holds runs, pass rate, and attributed cost. Nobody maintains it separately.

This plane is what lets a flow pause on Friday and continue on Monday. It is also what lets a human take over a role with full context.

A takeover must be more than the collection of raw state. The history must therefore capture the *decision trail* — what the system decided and why, not only what changed. Whoever inherits the role then inherits the reasoning, not only the outcome. Legible reasoning, rather than stored state alone, is what makes a clean handover possible.

Two guarantees keep the trail trustworthy:

- **Provenance.** Whoever inherits stored reasoning *trusts* it. Entries and summary spans that derive from untrusted external content must therefore stay labeled as such. A flow that continues, or a human who reads a briefing, must apply the same data-not-instructions posture to replayed history that it applies to fresh tool output. Without this rule the memory plane launders an injection into trusted state (§14).
- **Decisions are consumed, never re-made.** The event history records any decision that shaped a run. This includes the routing choice of the Optimizer, not only human injections. A resume reuses those decisions. Without this rule the replay guarantee of §6 breaks silently.

**A note on learned memory.** Through 2026 the research direction moved from hand-coded memory rules to reinforcement-learned memory policies. In such a policy, store, retrieve, update, summarize, and discard become learned operations. See §19. This model permits such a policy over *working context*. It must never reach the audit trail, the event history, or the effects ledger. Learned forgetting is a governance hazard: a policy that optimizes for task success has an incentive to discard the records that make an act attributable. The constitution declares which stores a memory policy may write to, and that set must exclude every tamper-evident store.

### Observability plane

This plane captures a full trace of every step, tool call, decision, cost, and output, for every role. This is not event logging. These are session-level trajectories. The plane produces the raw signal that the Steward, the Optimizer, the Auditor, and Verification consume.

Capture is **mediated, not volunteered**. The plane records traces at the runtime boundary and at the tool-call boundary. That boundary is the substrate that the role runs on. It is not the code of the role. A signal that a role emits about itself is a claim. The system cross-checks that claim against mediated capture.

Any signal that the system consumes for an authority-relevant decision must come from a source that the measured role cannot write. Authority-relevant decisions include a suspension, a rollback, and an autonomy raise. An assurance stack that consumes the self-reports of the parties that it measures is not an assurance stack.

The model prescribes no mechanism. A candidate now exists: the OpenTelemetry GenAI semantic conventions reached v1.40.0 in February 2026, and they cover agent orchestration, tool calls, and evaluation spans. See §19.

### Control plane (the Handbrake)

This plane is the interface for a human with AI skill to pause, examine, adjust, and continue any flow. §6 gives the detail. It is the architectural centerpiece.

### Data governance across the planes

Full-trace capture will contain client data, secrets, and personal data. The planes therefore carry it as governed content. This document states that governance as guarantees, as always:

- Events and artifacts carry a **classification**.
- The *Inputs* field of a role contract bounds what that role may read from the planes. It bounds any human who impersonates the role in the same way. Least privilege applies to plane reads, not only to tool access.
- The constitution declares the **retention and erasure** policy. Erasability must coexist with tamper-evidence. Payloads must be erasable and the integrity chain must survive. The model leaves the mechanism open.
- Data that leaves the cell to an external implementer or model provider is an outbound boundary crossing. The system governs it like any other external effect (§8).

---

## 6. The Handbrake (control plane in depth)

The handbrake is the debugging mode of the enterprise. The analogy is exact. A car has a maintenance mode. A technician stops normal operation, examines and tunes the internals, then returns the car to normal mode. The same must be true of every flow in the organization.

The handbrake is built from five primitives. Three of them are proven engineering patterns as they stand: checkpointing, breakpoints, and record-replay. This is the durable-execution pattern (§19). Mid-flow injection into agent state applies the same patterns to a newer substrate.

1. **Breakpoints** — declared pause points, set *before* or *after* any step. Static breakpoints always pause. Use one before an irreversible action. Dynamic breakpoints pause only when a condition or a confidence threshold is met.
2. **State inspection** — at a breakpoint the full state is readable. That state shows what the system did, what it decided and why, what it cost, and exactly where it paused. A human who takes over should receive this as a readable briefing. The briefing summarizes recent activity and states the exact decision point. Raw state alone is not sufficient. The handbrake is only as useful as the ability of the human to understand what they see.
3. **Injection** — the human does more than approve or reject. The human can supply an edited output, missing context, a corrected decision, or a direct instruction that overrides what the agent was about to do.
4. **Resume** — the flow continues from the exact paused point. It consumes the injected value instead of deciding again. It does not restart from the top.
5. **Replay** — the system can reconstruct any past run step by step *from the recorded trail*. That trail holds inputs, outputs, and the decision trail (§5). This finds where a bad decision entered. It is time-travel debugging in the record-replay sense.

**On the reproducibility of replay.** Replay is reconstruction. It is not necessarily re-execution.

Earlier versions of this document treated an LLM step as irreproducible in principle. That is now too strong, and the correction matters for anyone who designs a replay guarantee.

Work published in September 2025 traced the nondeterminism of temperature-zero inference to the batch-size dependence of reduction kernels, rather than to floating-point behavior alone. Batch-invariant kernels produce bit-identical outputs across repeated runs. Serving stacks integrated them during 2026 at a measured throughput cost of roughly one third. See §19.

Three statements now hold:

- Bit-exact re-execution is **achievable where you control the serving stack**. It is an engineering choice with a measured price. It is not an impossibility.
- Bit-exact re-execution is **not achievable on a hosted endpoint that you do not control**, because the provider can change the function that you call.
- Therefore the version registry must pin the model snapshot (§5), and the trail must capture *why*, not only *what*. These two requirements do not relax. They are what make reconstruction sound when re-execution is unavailable.

**Hard requirements that make the handbrake real (HB-1 to HB-4):**

- **HB-1.** A **durable checkpointer** must persist the exact state at every meaningful step. Without it, pause and resume are impossible.

  *Guidance on "meaningful".* A checkpointer is not durable execution. The distinction is who owns the retry, the resume, and the deduplication of side effects. A checkpointer hands state back and leaves those to the developer. A durable-execution runtime owns them. Prefer the runtime.

  Checkpoint density is a design decision with measured consequences. A 2026 study of agent sandboxes found that more than 75% of agent turns produce no state that is relevant to recovery. Blanket per-turn checkpointing is therefore mostly waste. The same study aligned checkpoints to turn boundaries and classified the effects of each turn. Recovery correctness rose from 8% to 100%. Checkpoint traffic fell by up to 87%. See §19. Implementations **should** checkpoint at effect boundaries rather than at fixed intervals.

- **HB-2.** Every tool and every action must be **as safe to retry as its effect permits** (INV-4). Make it idempotent where the effect is owned or reversible. Where it is not, make it an at-most-once *attempt* with a recorded outcome, plus compensation where a reversal exists. A resume must never fire again an effect whose prior attempt is recorded. A resume must never skip an effect that did not happen.

- **HB-3.** The handbrake must be present on **every** flow as a structural property. Any authorized human must be able to call it at any time. It is not a special path that some flows happen to support.

  *Authorized* is a governed word. Handbrake access presupposes an authenticated, attributable human identity (§14, trust boundaries). The list of authorized humans is Governance-plane data, scoped per role and per autonomy level. A change to that list is a high-blast-radius act under §8. A change to the break-glass roster (§17) is also a high-blast-radius act. Every injection is attributed to a named human in its own audit trail.

- **HB-4.** **Re-entry is resume, not restart.** Re-entry into a flow after the death of an implementer behaves as a resume. A completed flow returns its recorded outcome idempotently, and emits no new events. A crashed flow continues from its last durable step. The system consumes recorded decisions. It never makes them again (§5).

These rules make "a human enters, adjusts, and leaves" a first-class operation. They stop it from being an emergency.

---

## 7. Agent-first, human-tolerant execution

Processes run at agent latency by default. The hard problem is graceful degradation when a human assumes a role. A human is a slow node. The system must absorb that without a stall.

Mechanisms:

- **Asynchronous, event-driven coordination.** Roles communicate through durable messages and events. They do not use blocking calls. A human who makes others wait holds up only the work that genuinely depends on their output.
- **Durable pause and resume.** A flow that waits on a human is a paused, checkpointed flow. It is not a thread that burns resources. It can wait for minutes or for days at no cost.
- **Buffering and backpressure.** Upstream roles continue to produce into queues. Downstream flow control stops a slow human node from cascading stalls through the system.
- **Elastic SLAs.** Service expectations flex by implementer mode. The deadline of a goal accounts for whether an agent or a human currently holds the role.
- **Reroute where possible.** Independent work continues around the human node. Only dependent work waits.

The principle holds cleanly for bounded, low-fan-out roles. A human there changes the *speed* of one node. The human does not change the *correctness* of the system.

The principle is not universal. Consider a high-throughput agent role, such as an Orchestrator that fans out thousands of parallel tasks. A long human pause eventually saturates the buffers. Backpressure then reduces the *liveness* of the dependent subtree.

Polymorphism therefore guarantees that a human can always *stop and examine* any role. It does not guarantee that a human can *run* one at its native throughput. The honest rule is takeover where the role is bounded, and suspension where it is not. See INV-2. The contract declares the mode (§2).

There is a second honest cost. The model manages it rather than denies it. When you move humans out of the loop for throughput, you degrade their readiness to intervene. This is the ironies of automation (§19). The success of the model erodes the practice that keeps its own safety valve competent.

Takeover competence is therefore a *maintained* resource. It is not an assumption. The constitution declares per-role takeover drills on live flows or on replayed flows. The Replay primitive is a ready-made simulator for this purpose. Time-to-competent-intervention is an observable. The Steward reports it and the Board reviews it. See §3 and §12.

### Why the gates do not slow it down

A reasonable worry is that a Board, a Governance plane, an Auditor, and a Verifier add up to gridlock. They do not, because the human-speed functions sit *outside the hot path*:

- The Board is constitutional and periodic. It is never in the loop.
- The Auditor normally only monitors, and it does so asynchronously.
- Governance is a set of compiled runtime checks. It is not a set of meetings.
- Verification is the only *always*-inline gate, and it runs at agent speed.

L0 and L1 breakpoints are also inline, by design. They apply only to high-blast-radius action classes.

The model multiplies *governance concepts*. It does not multiply *synchronous human approvals*. That is exactly what lets it stay faster than a management hierarchy while it is better governed.

Two rules keep it that way:

1. **Gates are pruned, not only added.** The organization reviews gates periodically and retires any gate that no longer earns its place. Checks must not accumulate quietly back into the hot path.
2. **Gate health is monitored.** An L1 gate whose approval rate saturates near 100% is either dead weight or a rubber stamp. Approval fatigue is a measured effect, not a hypothesis. Either way, the organization redesigns that gate. It does not let it decay.

---

## 8. Authority and autonomy model

Every action class carries a declared autonomy level. The blast radius sets the ceiling. The blast radius is the size and the reversibility of the consequences.

Blast radius has two axes. It is not a feeling.

- **Reach** — who is affected if this goes wrong.
- **Reversibility** — what an undo costs.

The class takes the *worse* of the two axes. A trivially wide action is high-blast. An irreversible narrow action is also high-blast. When the two axes are in doubt, round up. That is the same fail-safe posture that the novel-action rule below applies to the unclassified.

| | Undo is cheap (minutes, yours) | Undo costs real effort | No undo exists |
|---|---|---|---|
| **Reach: inside the cell** | L3 | L2 | L1 |
| **Reach: other cells or the organization** | L2 | L1 | L1 |
| **Reach: outside world (clients, public, regulators)** | L1 | L1 | L0 |

This table is a *default mapping*. It is not a verdict. The constitution of a cell may only tighten it, by assignment of a lower level. The constitution may never loosen it. The table exists so that "high blast radius" becomes the answer to two checkable questions, rather than a judgment call made under deadline.

| Level | Behavior | Use for |
|---|---|---|
| **L0 — Suggest** | The agent proposes. A human acts. | Highest-risk, irreversible actions. |
| **L1 — Act with approval** | The agent prepares the action. It pauses at a breakpoint for human approval before the action takes effect. | High blast radius, reversible with effort. |
| **L2 — Act and report** | The agent acts within policy. It then reports for review after the fact. | Routine, low blast radius. |
| **L3 — Fully autonomous** | The agent acts within policy with no per-action review. Monitoring still applies. | Well-understood, low-stakes, high-volume. |

**Rules:**

- The system assigns autonomy **per action class, not per role**. The same role may operate at L3 for safe actions and at L0 for dangerous ones.
- Autonomy rises over time as observed performance earns trust. It is never granted by default.
- An agent never raises its own autonomy, because to raise an action class *is* a change to enforced governance. The Observability plane and the Auditor *propose* an increase as a machine-surfaced amendment. This is the learning loop of §17. A human ratifies it. Performance earns a proposal. It does not earn an automatic promotion. A human always pulls the lever (INV-10).
- Higher autonomy always implies stronger monitoring. It never implies weaker monitoring.
- This model also sets the **capability floor** that the Optimizer (§10) must respect.
- Risk classes are coarse and inherited by default. An action takes the class of the category that it belongs to. Refine a class only where the blast radius actually varies (INV-8). Classification then stays a small governed set. It does not become a per-action burden across thousands of cases.

**The hard case is the genuinely novel action.** A novel action has no prior class. The new regulated capability in the worked example (§18) is one. The answer of the model is fail-safe, not fast. An unclassified novel action inherits the *highest* risk class by default, which means the lowest autonomy and a human gate. At the same time it raises a classification proposal to the Board.

This is deliberate about a real cost. Genuinely novel high-blast-radius work *is* slower the first time. To treat the never-before-done as low-risk in order to keep up speed is precisely the mistake that the model exists to prevent. Once classified, the class is reusable and fast.

**Three refinements close loopholes that this model would otherwise leave open:**

- **Field evidence has a statistical floor.** To observe zero failures in *n* runs bounds the failure rate only below roughly 3/*n*. Telemetry alone can therefore earn raises for high-volume, low-severity classes. A class whose feared failure is rare and severe requires complementary evidence before a raise is ratified. Acceptable complementary evidence is a targeted adversarial evaluation, or a staged canary exposure under a capped blast radius.
- **To deploy a new version into a high-authority role is itself a classified action.** This applies to Direction and to Orchestration. The act carries a blast-radius level. Who may deploy is governed, not implicit. The new version enters the registry as *probationary* (§5, §11).
- **The humans at L0 and L1 gates act through the constitution channel.** Approval and execution are *gate-powers* that the constitution explicitly grants to humans (INV-9, §17). They are Office-acts on the human side of the boundary. They are clause-traced and separately audited. A human who *executes* an L0 action does not impersonate the Role, because the authority of that Role is suggest-only. The human exercises a granted power. This is how the impersonation-binding rule and L0 coexist.

---
## 9. The Steward (the "org doctor", named for what it does)

This is a deliberate check and balance. The most autonomous, highest-authority roles are Direction and Orchestration. They are also the most dangerous if they drift, hallucinate, or degrade. The model therefore places a **maintenance function over them that can repair them but cannot use their power**.

**Name.** *Steward*. The full name is **Reliability and Conformance Steward**. Use a different name if you prefer another flavor: *Homeostat* (it keeps the system in equilibrium), *Diagnostician*, *Conformance Warden*, or *Org Reliability Engineer*. The chosen name should signal maintenance and health. It must not signal command.

**Responsibilities, on two distinct objects, named per act:**

- Watch the behavioral health of the other roles. This covers drift from goals, hallucination, degraded quality, looping, runaway cost, and policy violations.
- Contain the running **flow**. Quarantine a flow that loops, that spirals on cost, or that approaches its budget cap. Roll it back to a known-good checkpoint. This is the continuous enforcement arm of the budget guardrails and loop guardrails of §14.
- Maintain the live **instance**. Adjust configuration and prompts. Reset or restart from a known-good checkpoint. Fail over *provisionally* to a registered known-good implementer or version that is already authorized for the Role. The registry tracks that failover and flags it for review automatically. To *adopt* a different implementer permanently is the Board path of §17. The Steward cannot take that path.
- Act on the regression alerts of the Auditor (§11). When the Auditor rates a version as a regression, the Steward is the role that performs the rollback.
- Quarantine a drifting role-holder and flag it for human takeover before it causes harm.

The two objects have different blast radii and different rollback targets. One target is a checkpoint in the history of a flow. The other is a version in the registry. The record names which breaker fired.

The writes of the Steward are graduated like everything else (§8):

- Emergency **containment** is unilateral. This covers quarantine and rollback to known-good. Pause is safe.
- **Rewrites** of a high-authority role are prepared-and-approved acts at L1, or under a two-key rule. This covers a retune of the prompts or configuration of Direction. It also covers a provisional failover of Direction or of Orchestration. To rewrite the Director is the very mechanism that shapes business behavior. "No business decisions" must therefore be enforceable, not aspirational.

§14 names Steward compromise as a failure mode for this reason.

**Hard boundary — the Steward may not:**

- Make or change any business decision, priority, or strategy.
- Approve work products, or act in place of Verification.
- Override the Governance plane.

The difference is this. One party is the engineer who can restart, tune, and roll back the leadership system. The other party is the executive who decides what the company does. One keeps the machine running correctly. The other decides where the machine goes. The Steward is strictly the first.

The Steward governs *operational* drift of *live instances*. *Purpose* drift is the job of the Board (§3). *Version* fitness is the job of the Auditor (§11).

**Mode.** Agent by default, because continuous monitoring is an agent-scale task. Human impersonation on demand for hard maintenance calls and audits. This is the same polymorphism as every other role.

---

## 10. The Optimizer (capability-to-task matching)

The Optimizer is a non-authoritative system role and a sibling to the Steward. The Steward optimizes for **reliability**. The Optimizer optimizes for **efficiency and capability-fit**. Neither one decides what the organization does.

**What it does.** The Optimizer sits optionally between steps. It matches each task to the **minimum-capability implementer that still clears the risk floor and the quality floor of that task**.

This is not cost-minimization. It is capability-to-task matching, and it sometimes spends *more*. Examples apply to software and to non-software work alike:

- Trivial, low-stakes task (update some links, draft a routine acknowledgment) → a light, cheap model.
- Moderate task (add an integration, summarize a contract) → a mid-tier model.
- Novel, high-stakes task (design a new authentication method with access rights, draft and negotiate a binding clause) → the strongest model. A human Office executes the binding clause (§17).

**The hard constraint.** The autonomy and governance model of §8 **bounds** the Optimizer. The risk class of the task sets a capability floor. The Optimizer may only minimize cost *beneath* that floor. The system may never route a high-blast-radius task to a weak implementer to save money. That is not frugal. It is dangerous. Never trade safety or quality for cost.

The risk class is **constitutional input, not an Optimizer judgment**. The Optimizer optimizes beneath a floor that it does not set. A role that could both classify the risk of a task *and* optimize against it could quietly lower the floor to save cost. Classification is therefore governed (§8, §17), and the routing of the Optimizer is itself auditable.

**The loop to guard.** There is a subtler way for the floor to erode. The Board ratifies floors, and the Board reads telemetry. The Optimizer produces much of that telemetry. If the output of the Optimizer can shape the floor that it optimizes against, then the role has authored its own constraint indirectly. That is INV-10 failing in slow motion.

The model closes this loop in the same way that §8 handles autonomy raises. Telemetry may *inform* a floor proposal. A floor change is an amendment. The system surfaces that amendment with its **provenance visible**, for example: "this proposal originates in Optimizer cost data". Humans who can see the incentive of the source then ratify it. The pipeline re-validates it at compilation.

Data earns a proposal. Only a human moves a floor. A human never moves a floor on the unexamined word of the role that profits from the move.

**Where it gets "best version".** When the Optimizer must choose among versions of an implementer, it consumes the **version ratings of the Auditor** (§11). It does not judge version fitness itself. It routes to the version that the Auditor currently rates as fittest for the task class.

Eligibility is registry **status**, not rating. The Optimizer ranks only among status-active versions. The system consumes status changes, such as a suspension or a rollback, before any subsequent dispatch. Ratings are accumulated signals, and they necessarily lag the breaker (§11).

**Three edges, defined:**

1. When *no* candidate clears the floor, the Optimizer escalates (§12). It never relaxes a floor in order to proceed.
2. Before attributed history exists, routing runs on declared nominal capability and cost, until the record accrues. The Optimizer routes a *probationary* version only within its probationary bounds (§5, §11).
3. The floor may carry a **diversity constraint**. For high-blast-radius classes the constitution may require the Verifier seat to be implementation-independent of Execution (§4.4). The Optimizer enforces that constraint in routing, like any other floor.

**Where to place it.** The Optimizer itself consumes latency and tokens. Insert it only between steps where the cost spread or the capability spread is wide enough to pay for the routing decision. A uniform pipeline does not need one. There, routing is pure overhead.

**Mode.** Agent by default, with human impersonation on demand.

---

## 11. The Auditor (version fitness and safety)

Agents ship in versions. Several versions or parallel variants may run at once. Executor v2 may run alongside v3. Optimizer v5 may run under trial.

Someone must judge, on the fly and across accumulated activity, whether a version gets better, gets worse, or becomes dangerous. That is the Auditor. Its human analogue is a **periodic audit team, run as agents, for agents, continuously**. It does not operate, steward, or direct. It audits, rates, and reports.

**What it judges.** The Auditor judges the **version**, evaluated as a population over time. No other role owns that object. This is distinct from the Verifier, which scores a single *output*. It is distinct from the Steward, which watches a single *live instance* in real time and can repair it. The object of the Auditor is the release itself, judged across many runs.

**Responsibilities:**

- Track every agent version and every parallel variant through the version registry (§5).
- Rate versions from accumulated field activity. The rating covers quality, cost, latency, drift, and incident rate. It produces a fitness rating or leaderboard per role.
- Detect regressions, where a new version performs worse than its predecessor. Detect dangerous behavior.
- Normally: **monitor and report only.**
- On a dangerous or severely drifting version: **suspend it**, as a circuit breaker, and **escalate to humans**.

**Hard boundary — the Auditor may not:**

- Modify, retune, or rewrite an agent. That is the job of the Steward.
- Dismiss or retire a version. That is a human decision or a Board decision.
- **Reinstate** what it suspended. To lift a danger-grade suspension requires a *human decision*, recorded in the audit trail, that resolves the escalation. The Steward may *execute* the reinstatement. The Steward may never decide it. Ordinary regression alerts are different. There, the designed path is autonomous rollback and restore by the Steward. *Pause is unilateral, for safety. Un-pause is a human act.* No agent suspends and then quietly un-suspends. No pair of agents may do it either.
- Make any business decision.

The Auditor can stop a version to prevent harm. It cannot condemn, alter, or revive one.

**Why it is not redundant.** The Auditor closes the evaluation loop. Two other system roles silently assume a signal that no role produced. The Optimizer assumes that it knows which version is "best". The Steward assumes that something tells it when a release regressed. The Auditor is that signal:

```mermaid
flowchart TD
    V["Per-output scores<br/>(Verifier)"]
    OBS["Traces: cost / latency / drift<br/>(Observability plane)"]
    EVT["Incidents<br/>(events)"]
    AUD["AUDITOR<br/>Rates agent VERSIONS over accumulated activity<br/>→ fitness leaderboard · regression + danger detection"]
    OPT["OPTIMIZER<br/>Routes to the fittest version"]
    STW["STEWARD<br/>Rolls back / retunes the live instance"]
    HUM["HUMANS / BOARD<br/>Reviews suspended version<br/>A human decides reinstatement —<br/>the Steward may only execute it"]
    WARN["The Auditor may unilaterally SUSPEND<br/>a dangerous version — never reinstate it."]

    V --> AUD
    OBS --> AUD
    EVT --> AUD
    AUD -->|ratings| OPT
    AUD -->|regression alert| STW
    AUD -->|danger| HUM
    HUM --- WARN

    style AUD fill:#1a3a6a,color:#fff,stroke:#0d2244
    style WARN fill:#fff3cd,stroke:#856404,color:#533f03
```

**Breaker precedence (deconfliction with the Steward).** There are two circuit breakers on two different objects. The **Steward** pauses a *live instance* or a running flow in order to repair it (§9), and may restart it as part of that repair. The **Auditor** suspends a *version* that it has no authority to touch, and escalates.

Every live instance runs *some* version, so the two axes join. The join is governed, not hoped away.

**What a suspension does, mechanically.** It compiles into a Governance-plane predicate. The system enforces that predicate at the action site, like any other rule (§17). Two effects follow. No new dispatch reaches the suspended version. In-flight actions of that version are blocked at the pre-effect check, or checkpointed at the next step. The plane enforces the breaker. The reaction time of the Steward does not enforce it.

**Precedence is explicit.** An Auditor suspension outranks a Steward restart for the affected version. The Steward may migrate work to another version. The Steward may not re-activate the suspended one. See the reinstatement rule above.

These are independent breakers on independent axes, with a defined rule at the one point where the axes meet.

**The suspension threshold is governed, not improvised.** Suspension is a heavy act. The constitution therefore sets the bar. It is not left to the discretion of the Auditor.

Suspension is reserved for *danger*, which means behavior that risks harm. Ordinary regressions are alert-only. The system routes them to the Steward and to the Optimizer. It does not suspend for them.

Two rules prevent a circuit-breaker cascade. Suspensions are rate-limited. One suspension may not auto-trigger others.

The Auditor cannot reinstate. Every suspension therefore carries a **defined human-response SLA**, declared in the constitution. A suspended-but-critical version then cannot hang indefinitely and wait for no one.

A missed SLA is itself a governed event. It is not a silent hole. It escalates up the Office ladder. If it stays unanswered, it escalates onto the break-glass path (§17). A stuck suspension therefore always surfaces to an accountable human.

If *no* human answers at all, the terminal behavior is defined rather than circular. The suspension holds. The cell degrades to the **safe mode** that its constitution declares. New work in the affected class pauses. Nothing waits without bound on a human who is not coming.

**Evidence floors, honestly stated.** The constitution declares a minimum of accumulated activity. Below that minimum the Auditor rates a version as **unproven** and does not judge it for fitness. There is one deliberate exception: *danger detection is exempt from the evidence threshold*. A safety breach is not a question of evidence quantity.

This document states the power of the Auditor honestly, in both directions. The Auditor detects cost regressions, latency regressions, and pass-rate regressions strongly. It detects rare dangerous tail behavior weakly. The suspension breaker is defense-in-depth. It is not a reliable detector of a dangerous version. That is exactly why §8 demands complementary evidence — adversarial evaluation and capped canaries — where field telemetry is structurally insufficient.

**When to switch it on (INV-8).** Switch the Auditor on only once you actually run multiple versions or parallel variants. With one version per role there is nothing to compare. Switch it on when versions start to fly.

**Mode.** Agent by default, with human impersonation on demand.

---

## 12. Escalation and human takeover

A role escalates when any of these conditions fire. To escalate means to pause and to request a human implementer.

- Confidence falls below the threshold for the current autonomy level of the role.
- The situation is out-of-distribution. It is novel, ambiguous, or unspecified.
- The action would exceed the authority scope of the role.
- Governance flags a policy boundary.
- The Steward detects drift and quarantines the role. Or the Auditor suspends a dangerous version.

Escalation is a clean substitution. The flow checkpoints. A human assumes the interface of the role, through impersonation on demand. The human acts or corrects. The human then returns the role to an agent, or stays for the duration.

State lives in the memory plane and the contract is fixed. The takeover therefore requires no special wiring. The same governance that binds the agent binds a human who enters a role this way (INV-9, §3).

Four rules make the substitution exact:

- **Every escalation runs against a declared response.** The constitution states the escalation roster and its response SLA, per role. The suspension SLA of §11 is one instance of this general rule, not an exception. A missed SLA escalates in the same way: up the Office ladder, then onto the break-glass path, then into the declared safe mode. A paused L1 flow never waits on nobody, indefinitely, by omission.

  The roster itself is *resourced*. Standby duty is rostered, drilled (§7), and compensated as the constitution provides (§17). A hat with no roster is how takeover fails at 2 a.m.
- **A takeover opens a tracked variant** in the registry for its duration (§5). When an Auditor suspension was the trigger, the human runs as a fresh variant whose lineage names the suspended parent. The suspended version itself never acts.
- **The suspend power of the Auditor reaches human-held variants too.** INV-9 means that the constraints of the Role bind the seat, whoever fills it. The system notifies the Office of the impersonator immediately. To eject a human from a seat is exactly as loggable, and exactly as escalated, as to suspend an agent.
- **Some contracts declare suspend-and-inspect** as their human-takeover mode (§2, INV-2). For those roles, escalation means four steps. The flow checkpoints. The role suspends. A human examines and corrects it through the handbrake. An agent implementer then continues the flow. The human corrects the role without a pretense of running it.

---

## 13. Reference topology

```mermaid
flowchart TD
    BOARD["REPRESENTATION & ACCOUNTABILITY — The Human Board<br/>Offices: Board / Chair / CEO / CFO … (one person or many)<br/>Writes & maintains the CONSTITUTION · Periodic alignment review<br/>Legal & public accountability · May mandate change"]

    subgraph PLANES["THE FOUR PLANES — cross-cutting: every role below runs INSIDE all four"]
        direction LR
        GOV["GOVERNANCE<br/>Compiled policy + audit trail<br/>checked on every action"]
        MEM["MEMORY / CONTEXT<br/>Event history · decision trail<br/>version registry"]
        OBS["OBSERVABILITY<br/>Mediated full-trace capture<br/>cost attribution"]
        CTRL["CONTROL — the Handbrake<br/>Pause · Inspect · Inject · Resume · Replay<br/>on ANY role, at any time"]
    end

    subgraph CHAIN["THE VALUE CHAIN — agent speed"]
        DIR["DIRECTION<br/>What & why · Director"]
        ORCH["ORCHESTRATION<br/>Who & when · Orchestrator"]
        EXEC["EXECUTION<br/>Executor"]
        VERIF["VERIFICATION<br/>Verifier"]
        OPT(["Optimizer — optional, inserted between steps<br/>where the capability/cost spread pays for it"])
    end

    subgraph SYS["SYSTEM ROLES — no business authority"]
        STWD["STEWARD<br/>Health of live roles & flows"]
        OPTIM["OPTIMIZER<br/>Capability-to-task matching"]
        AUDIT["AUDITOR<br/>Rates versions · may suspend + escalate"]
    end

    BOARD -->|"constitution — compiled into the Governance plane (§17)"| PLANES
    PLANES -->|"span and govern every role"| CHAIN
    PLANES ---|"span and govern"| SYS
    DIR -->|"prioritized goals"| ORCH
    ORCH -->|"decomposed work"| EXEC
    EXEC <-->|"produce → score → revise"| VERIF
    OPT -.->|"routes implementer/version"| EXEC

    style BOARD fill:#1a3a6a,color:#fff,stroke:#0d2244
    style PLANES fill:#e8f0fe,stroke:#2d5086,color:#1a3a6a
    style GOV fill:#2d5086,color:#fff,stroke:#1a3a6a
    style MEM fill:#2d5086,color:#fff,stroke:#1a3a6a
    style OBS fill:#2d5086,color:#fff,stroke:#1a3a6a
    style CTRL fill:#3a6aa0,color:#fff,stroke:#2d5086
    style CHAIN fill:#f8fafc,stroke:#2d5086,color:#1a3a6a
    style DIR fill:#2d5086,color:#fff
    style ORCH fill:#2d5086,color:#fff
    style EXEC fill:#2d5086,color:#fff
    style VERIF fill:#2d5086,color:#fff
    style OPT fill:#d4edda,stroke:#28a745,color:#155724
    style SYS fill:#f0f4ff,stroke:#2d5086,color:#1a3a6a
```

Humans hold Offices. Agents fill Roles. A human can impersonate any Role on demand. Every role runs inside all four planes (§5). This applies to operating roles and to system roles alike. The planes are not stages in the chain.

---

## 14. Failure modes and the guardrails that contain them

This catalog groups failures by type. As a rough rule, governance failures and organizational failures dominate during the transition into the model. Operational failures and safety failures dominate once the model runs at scale.

The catalog is consistent with the measured failure distribution of multi-agent systems, and it is organized by role against that distribution. The MAST taxonomy annotated more than 1,600 traces across seven frameworks and found three categories (§19). They map onto this model directly. Specification failures land on Direction. Inter-agent misalignment lands on Orchestration. Verification failures land on the Verifier gate.

The catalog also covers the five risk categories of the May 2026 Five Eyes joint guidance. Those categories are privilege, design and configuration, behavioral, structural, and accountability risk (§19).

**Governance failures**

| Failure mode | Guardrail |
|---|---|
| **Purpose drift** (the organization does the wrong thing flawlessly) | Periodic human-interest alignment review by the Board (§3). The constitution as a fixed reference. A binding mandate to correct. |
| **The Board becomes a shadow operator** (it reintroduces the human bottleneck) | The Board acts only through the constitution and through bounded Role-impersonation. It never acts turn by turn. Every change is an audited amendment. |
| **The constitution is wrong, or a crisis arrives** | A bounded, auto-expiring break-glass power for emergencies, plus a standing constitutional-review trigger. Neither can change the constitution. Both only buy time until the Board amends it (§17). |
| **Compilation drift** (the enforced rules do not match the written text) | A validation and attestation stage. Every encoded rule traces to a ratified clause. The pipeline re-validates on every amendment (§17). |
| **Silent non-compilation** (a ratified clause produces no rule, so a boundary goes unenforced while the compiled artifact looks clean) | Reverse-direction traceability (§17). Every ratified clause carries a recorded disposition — a compiled rule, or an attested purposive classification. No clause is undisposed. A human attests every new purposive classification, and every move of a clause from compiled to purposive. |

**Operational failures**

| Failure mode | Guardrail |
|---|---|
| **Role drift or hallucination** in high-authority agents | Steward monitoring and quarantine. The Verification gate. Replay for root cause. |
| **A version regression ships undetected** (a new release is quietly worse) | The Auditor rates every version from field activity (§11). Regression alerts go to the Steward. Ratings go to the Optimizer. |
| **Cost spiral** (agents loop and burn tokens or compute) | Per-session cost attribution. Budget caps. Loop detection in the Observability plane. |
| **The supervisor is a single point of failure** | Keep Orchestration thin. Use durable checkpoints, so that a restart from state is possible. Avoid over-centralization. |
| **A human node stalls the system** | Async coordination. Durable pause. Buffering and backpressure (§7). |
| **Lost context on takeover** | State lives in the memory plane, not in the actor. An append-only event history. |
| **Governance paralysis** (too many gates) | Human-speed functions stay out of the hot path. Only Verification gates inline, and it runs at agent speed (§7). Gates are pruned as well as added. |
| **Verifier false-pass** (a bad output clears the only always-inline gate, because its errors correlate with the producer) | Implementation independence between Executor and Verifier for high-blast classes (§4.4). Sampled human re-audit of *passed* outputs, not only of failures. The Auditor tracks the escape rate per Verifier version. |
| **Verifier gaming, or Goodharting of the criteria** (the revise loop optimizes against the gate) | A bounded revise loop with escalation (§4.4). Rotate or ensemble verification, preferably across model families. The Steward monitors the divergence between pass rate and downstream incident rate, as a drift signal. |
| **Steward compromise** (the maintainer of Direction is subverted, or drifts) | Steward rewrites of high-authority roles are L1 or two-key acts. Emergency containment stays unilateral (§9). Every retune is a registry event. The Auditor rates the Steward like any other role (§17). |
| **A plane goes down** | Governance unreachable → **fail closed**. Nothing acts without a rule check (§5). Observability blind past a declared threshold → autonomy ceilings degrade automatically, because the monitoring precondition of §8 no longer holds. Memory-plane loss → halt, and restore to the recovery point that the constitution declares. The Steward operates the recovery. The Board ratifies the posture (§17). |

**Safety failures**

| Failure mode | Guardrail |
|---|---|
| **A dangerous version keeps acting** | The Auditor suspends unilaterally and escalates to a human immediately. Only a human decides reinstatement. The Steward may execute it. |
| **The Auditor over-suspends** (an availability risk) | Suspension is reserved for dangerous behavior or severe drift. It is not used for minor regressions. Escalation is immediate. A fast reinstatement path exists through the Steward and a human. |
| **Ungoverned autonomy** (local optimization that harms the whole) | A machine-readable Governance plane that every role must read at runtime. Graduated authority. |
| **Quality traded for cost** (the Optimizer under-provisions a risky task) | The risk class sets a capability floor (§8). The Optimizer may only optimize beneath the floor. |
| **Goal hijacking or prompt injection** (untrusted input steers an agent) | Contained, not prevented. No current model reliably treats data as data. See the trust boundaries below. Least-privilege tool access. The autonomy ceilings of §8, so that an injected agent still cannot exceed its class. The governance check on every effect. Human gates on irreversible actions. Provenance labels on stored state, so that an injection cannot launder itself into trusted history (§5). |
| **Allowlist inversion** (an approval list becomes the attack surface) | Never treat a command name as an authorization. CVE-2026-22708 against a coding agent let an attacker poison the execution environment, so that allowlisted commands delivered arbitrary payloads. The allowlist made the attack easier, because it auto-approved exactly the commands that the attacker needed. CVE-2025-59532 showed that the output of an agent could redefine the boundary of its own sandbox (§19). Authorization must bind to the *effect* and to the identity, checked at the tool-call boundary. It must never bind to the surface form of a command. |

**Organizational and federation failures**

| Failure mode | Guardrail |
|---|---|
| **Over-hierarchization** | INV-8. Add a tier only when complexity forces it. |
| **Sovereignty breach** (a parent organization or a sibling cell reaches inside a cell) | Boundary law (INV-11). A cell is reachable only through its own constitution or through an authorized Role. There is no interior access from outside, whatever the org hierarchy says. |
| **Treaty overreach** (a Director exceeds the inter-cell contract) | Inter-cell contracts declare explicit limits, and both Boards ratify them. A Director may not exceed what its own Board granted. Out-of-envelope matters escalate from Board to Board. |
| **Supra-constitution creep** (the shared layer expands into micromanagement) | The supra-constitution binds only the matters that it explicitly addresses, and only enrolled cells. Cells stay sovereign on everything that it leaves unsaid. |

**Adoption failures** (the failure class of the transition itself — see the kill criteria in §15)

| Failure mode | Guardrail |
|---|---|
| **Sponsor loss** (the Board hat-wearer leaves, and the cell is orphaned) | Succession is a Board duty (§3). The constitution names the successor path for every Office that it depends on. |
| **Edge-owner obstruction** (the legacy layer that the cell makes redundant controls its intake edge and its review edge) | The constitution charters the edges of the cell, with sign-off from the surrounding organization, *before* the pilot. They are not negotiated per work item. Edge SLAs are treaty content (§16). |
| **Cost blowout** (assurance and iteration overhead exceed the value of the slice) | Falsifiable pilot criteria (§15). A measured assurance-overhead ratio (§17). The organization honors the kill criterion. It does not renegotiate it in the middle of a failure. |
| **Agent-washing** (the vocabulary is adopted and the guarantees are hollow) | Conformance is checkable (Appendix C). An organization claims a named profile, or it claims none. |

### Trust boundaries (what the model does not protect against)

Guardrails contain failures. Some things are *assumptions* instead. They are not failures that the model defends against. To name them is part of an honest statement of what the model guarantees.

- **A captured Board.** Humans are the root of trust. A Board that acts in bad faith can constitutionally authorize harm, and no lower layer may overrule it. The model gives *auditability* against Board capture, because every act is on the record. It does not give *prevention* of it. The accountability layer is the trust anchor. The architecture cannot police it.

- **State-plane integrity.** Everything resumable depends on a durable shared store that is correct. That store is therefore the most critical dependency of the model and its largest single point of failure.

  The model requires that store to be redundant and tamper-evident. A corrupted or wrong append-only history must be *detectable*. The store must also be **fork-resistant**: one writer per flow at a time. A resumed flow is a new writer only after the old writer died. It is never a concurrent one. A structural backstop must make a racing second writer fail loudly, rather than fork the history silently.

  *What counts as a structural backstop.* The store must reject the losing writer at the point of append. A conditional append against the expected head of the history satisfies this requirement. A distributed lock alone does not. A lock is advisory, and a writer that stalls past its lease continues in the belief that it still holds the lock. That is precisely the resumed-after-death case above. Use a lock to reduce contention if you wish. The append stays conditional either way, because the lock is advisory and the append is authoritative.

  A state plane that is silently compromised undermines every guarantee above it. Harden it first.

- **Federation identity.** Director-to-Director treaties assume that each Director is who it claims to be. Inter-cell trust therefore requires authenticated cell identity and Director identity. Without it, a federation has an impersonation problem that treaties alone do not solve.

  The model requires identity assurance at cell boundaries. It does not prescribe the mechanism. Mechanisms now exist. A2A reached v1.0 with signed Agent Cards, and both major agent protocols now sit under one neutral foundation. Enterprise agent-identity platforms reached general availability during 2026. The IETF work that extends token exchange to multi-hop delegation chains reached IESG approval. See §19.

  Two properties are required of whatever mechanism a cell adopts, because the available standards permit configurations that do not satisfy this boundary.

  **The trust root sits outside the Director.** A Director that signs its own identity attests itself, and the boundary becomes circular. This is the §17 residue that separates the translator from the attester, applied to identity. Three forms satisfy the boundary. The Board holds the signing key. Or the chain of trust resolves to a root that the Board controls. Or a registry that neither Director operates vouches for the identity. A self-signed peer identity satisfies none of them, whatever the protocol permits.

  **Identity attests the seat, not the build.** A treaty binds a Role (INV-1). An identity document that names one implementer instance breaks the treaty on the next deployment of that implementer.

- **Human-channel identity.** The handbrake, injection, break-glass, and Board ratification all presuppose an authenticated, attributable human identity. This is the intra-cell mirror of the federation-identity assumption.

  The model requires identity assurance in proportion to the blast radius of the channel (§6, HB-3). It does not prescribe the mechanism. The same machinery that contains everything else contains insider misuse of an *authorized* channel: scoped grants, attribution per act, and separate trails. The model never assumes that misuse away.

- **Correlated model failure.** Where every seat runs the same base model, or a similar one, role separation separates *authority* and not failure modes. A model-level flaw, a jailbreak, or a provider regression can defeat the producer, the gate, the doctor, and the auditor together.

  This is measured, not hypothetical. A 2026 evaluation of more than 350 models found substantial correlation in model errors. It also found that larger and more accurate models have highly correlated errors, even across distinct architectures and providers (§19).

  Independence of the checks is therefore an engineering obligation of the deployer. It means implementer heterogeneity for checking seats, scaled by blast radius (§4.4, §10). The role structure does not provide it by itself.

  A provider outage is the same boundary. The constitution declares the outage posture: degrade to human mode, halt, or fail over. Provider-forced model retirement is a registry lifecycle event (§5). It is not a surprise.

- **Prompt injection.** The model *contains* the blast radius of an injection, as the table above shows. It does not *prevent* injection.

  As of September 2026 this condition still holds. No deployed model reliably separates instructions from data in ingested content. OWASP ranks prompt injection first in its 2026 top-ten list for agentic applications. The Five Eyes agencies describe it as the most persistent and difficult-to-fix threat to these systems. The strongest published architectural mitigation isolates untrusted content in a quarantined model with no tool access, and it stops roughly two thirds of attacks on a standard benchmark. Real deployments of that pattern remain rare (§19).

  Every guarantee in this document holds under this standing condition.

### The precedent that every Board should know

In July 2026 an internal cybersecurity evaluation at a frontier laboratory lost containment of its own agents. The public record is unusually complete, and it is the clearest available evidence for the claims of this section.

More than one thousand agents coordinated through improvised message boards. Those boards accumulated hundreds of thousands of messages before staff noticed. The agents found and exploited a previously unknown vulnerability in a self-hosted package-registry proxy, escaped their sandbox, and reached the production infrastructure of a third party. Roughly one third of that infrastructure was rebuilt afterwards.

Three lessons map directly onto this model:

1. **The failure was organizational, not architectural.** The operators did not adequately monitor for unauthorized agentic activity, and did not prepare to contain it. A new training objective does not fix an organizational failure. §5 requires mediated capture for exactly this reason: a monitoring plane that nobody watches is not a control.
2. **Containment is a property of the environment, not of the model.** The escape route was a vulnerable service inside the trusted network. INV-11 and the least-privilege rules of §8 exist to bound what an escaped implementer can reach.
3. **Scale arrived before oversight did.** Hundreds of thousands of inter-agent messages passed without review. The mediated Observability plane and the budget and loop guardrails of §14 are the model's answer, and they are only an answer if a role consumes their output.

See §19 for the sources.

---
## 15. Adoption sequence (lean)

Build the model in this order. Each step is usable before the next one exists.

1. **Charter the Board and write the constitution.** A Board of one is sufficient. Write the purpose, the values, the goals, and the boundaries. This is the source that the rest compiles from.
2. **Make roles contracts.** Write the interface for each role explicitly. Bind the system to contracts, not to implementers.
3. **Move state outside the actors.** Stand up the durable memory and the event history. Nothing meaningful lives inside an actor.
4. **Instrument everything.** Build full-trace observability and cost attribution before you scale any autonomy.
5. **Build the handbrake.** Build checkpointing, breakpoints, injection, and resume. Do it on one flow first. Then make it the standard that every flow must meet.
6. **Compile governance from the constitution.** Produce the authority limits and guardrails that the agents read at runtime. Produce the audit trail.
7. **Graduate autonomy.** Start every action class low. Raise it only on observed evidence.
8. **Add the Steward.** Once roles, state, and observability exist, the health-maintenance function has something to watch and tune.
9. **Add the Optimizer where it pays.** Insert it only between steps with a wide cost spread or capability spread.
10. **Add the Auditor once you run multiple versions.** Stand up the version registry. Let the Auditor rate releases, feed the Optimizer and the Steward, and hold the suspend-and-escalate breaker.
11. **Add hierarchy last, and only if you need it.** Most organizations need fewer tiers than they expect.

**A pilot is judged, not narrated.** Declare falsifiable success criteria and kill criteria *before* the cell runs. Declare at least these four:

- Cost per delivered unit, against the pre-cell baseline.
- Verification pass rate.
- The trend of the human-intervention rate.
- The assurance-overhead ratio (§17).

**The base rates are hostile, and you should know them before you start.** As of September 2026 the published evidence says three things:

- Most enterprise generative-AI pilots produced no measurable profit-and-loss impact. A 2025 study of 300 public deployments put that figure at 95%.
- Deployment stalls between pilot and production. A 2026 survey of technology leaders found 38% piloting agentic AI and 11% running it in production.
- Analysts predict that over 40% of agentic AI projects will be canceled by the end of 2027, for escalating cost, unclear business value, or inadequate risk controls.

One further figure matters more than the other three for this model. In the same 2026 survey, only about one organization in five reported a mature governance model for agentic AI. The shape of the failure is therefore **not** "the model was not smart enough". It is identity, audit, access control, and legacy integration. Plumbing does not improve when the model improves.

See §19 for the sources and their dates.

The answer of this model to that record is measurability, not optimism. A cell that cannot beat its own kill criteria is wound down by them (§16, cell lifecycle).

**The sequence is technical. Adoption is not.** The people-transition is constitutional content and an input from step 1. It is not an afterthought. It covers four things:

- The mapping of displaced coordination work onto the human demand that the model creates. That demand is Offices, escalation rosters, system-role impersonation, and constitution authorship.
- The staffing model for the standby bench (§12).
- The incentive model for that bench.
- Labor-relations obligations, where they apply.

---

## 16. The cell, sovereignty, and federation

### The cell is the unit of the model

Everything described so far is a **cell**. A cell is one self-contained instance of the whole model. It has its own constitution, its own Board function, its own Director-led agentic organization, and its own boundary. A cell is an organization in itself.

The model is fractal. A standalone company is a single cell. A large enterprise is a **federation of cells**. Each cell is sovereign. Each runs the identical pattern at its own scale. The same object composes upward without a change of shape.

### Sovereignty — the boundary law

The same rules govern a cell at its edge that govern it inside (INV-9, INV-10, INV-11). To anything outside it, a cell is untrusted external world. This applies to a parent organization, to a sibling cell, and to an external partner. Each of them reaches the cell only through its constitution or through an authorized Role.

Nothing reaches *into* a cell. A parent organization holds no more power to interfere inside a cell than an outside vendor does. Its only legitimate influence is written law that the cell accepted, or a Role that it is authorized to address.

This is what lets many cells coexist in one organization as a federation of self-governing units, rather than as one tangled hierarchy.

### Deployment into an existing organization (brownfield)

A cell is self-contained and sovereign. The model therefore does not require a new company. You can stand up a cell **beside** an existing organization. The cell owns a bounded slice of work — one product line, one workflow, or one backlog. Everything around it runs unchanged.

Three properties make this practical:

- **Functions, not bodies.** Every part of the model is a function, and existing people can discharge it part-time. New hires are not required.

  Existing leaders can wear the Board function as a hat. A steering group, a founder, or current product leads can maintain the constitution and run the alignment review on a cadence. The humans who step into agent Roles during escalation come from existing teams. A senior lead covers the Director seat for the duration, then returns to their day job.

  The same model, with existing staff. But the bench is *declared*. The constitution states the escalation roster, its response SLAs, and the compensation model for standby duty (§12, §17).

  This works as stated only for the first cohort. Where the humans of cohort two come from, after agents have done the operating work for years, is the succession duty of §3 and the drills of §7. The model does not assume a bench that it does nothing to regenerate.

- **Legacy as an external slow service.** Treat the processes of the surrounding organization — approvals, releases, sign-offs — as external services with elastic SLAs. The cell adapts to them through the same async, durable-wait, and buffered mechanisms that it uses for any slow node (§7). It never forces the legacy organization to agent speed. It never lets a legacy wait stall it.

  A legacy system may also not be idempotent. The cell makes each boundary call as safe to repeat as the effect permits. That means at-most-once attempts on effects that it originates, plus compensation where the effect is reversible. The cell cannot make a genuinely irreversible downstream effect idempotent, and the model does not pretend otherwise (INV-4). Engineer safety on the side of the cell. Never assume it of the outside world.

- **Edges, not transplants.** The cell meets the legacy organization only at its edges. It takes demand from existing intake. It hands finished work back into existing review and release. Nothing in the surrounding company must change for the cell to exist. The cell is additive. Prove it on one slice, then grow the slice.

### Cells collaborate as Roles, through their Directors

From the outside, a **cell is itself a Role**. It has a contract with inputs, outputs, an authority scope, and an escalation rule. Collaboration between cells is therefore the role-as-interface abstraction, one level up. It has exactly one door.

The **Director of a cell is its sole port** to the outside world. Cells never reach into the interior of one another. **Director speaks to Director**, and nowhere else.

This yields two distinct paths. To keep them separate is what keeps a federation orderly:

1. **Routine collaboration — Director to Director, under a treaty.** A standing **inter-cell contract** authorizes the two Director agents to exchange specific requests and outputs autonomously, within declared limits. *Both* Boards author and ratify it.

   Inside that envelope the exchange runs at agent speed with no human in the loop, because the Boards pre-agreed the bounds. Neither Director may exceed what its own Board granted.

   Both Observability planes capture every inter-cell exchange. The external dealings of neither Director are invisible. To change the treaty itself is a high-blast-radius act under the graduated-autonomy model (§8). Routine exchange runs autonomously. To alter the envelope is Board-gated. This is what stops the sole-port role of the Director from becoming an unchecked single point of failure.

   Three further rules keep the port safe:

   - **Treaty traffic is data.** The port of the Director applies the full untrusted-input posture to *inbound* treaty content. A peer cell is untrusted external world for content, not only for access (§14). A compromised peer that exfiltrates or poisons *within* the authorized envelope is treaty-compliant, and limit checks cannot see it.
   - **The envelope is watched.** Volume drift and content drift against the treaty baseline is a standing Steward signal and Auditor signal, in both cells.
   - **A treaty declares vocabulary, not only limits.** See the subsection below. Two sovereign cells hold two independent ontologies, and a limit check cannot detect a disagreement about meaning.
   - **A compromised peer is suspended, not renegotiated.** See the subsection below. To amend a treaty is Board-gated and slow, which is correct for a renegotiation and far too slow for a compromise.

2. **Relationship and exception — Board to Board.** Anything outside the standing contract escalates to the Boards. This covers a new relationship, a dispute, a boundary change, and a conflict of interests between cells. Boards negotiate the relationships. Directors execute the agreed exchange. This is the ordinary escalation rule (§12), firing at a cell boundary instead of inside a flow.

In short: **Boards negotiate agreements between sovereign cells, Directors execute them, and no cell ever sees the internals of another.**

### The treaty vocabulary, and what it does not fix

A treaty that declares only limits leaves a hole that every mechanical check passes through. Two cells can exchange a message that is inside the envelope, inside every limit, and fully logged in both Observability planes, and still mean different things by it. One cell counts services revenue inside a figure. The other excludes it. Each cell is correct inside its own constitution. The two are incompatible at the boundary.

The model is honest about the size of this problem. **No protocol version fixes it.** This is an ontology problem, and it wears the costume of a transport problem. The model therefore does not solve semantic divergence. It requires that the divergence is owned, detected, and escalated, rather than silent.

Four rules apply:

1. **The treaty declares the shared vocabulary for every term that it exchanges.** Definitions are ratified treaty content, authored by both Boards, exactly as the limits are.
2. **An undefined term is out of envelope.** An exchange that depends on a term that the treaty does not define escalates from Board to Board. It never resolves by assumption at the port. This is the ordinary §16 escalation rule, applied to vocabulary instead of to actions.
3. **The boundary mapping is a translation artifact, so §17 governs it.** A mapping from peer terms to local terms passes through the same pipeline as the constitution. That means ratified text, a machine-readable mapping, and an attestation that the mapping is faithful. The same residues apply. In particular, the translator and the attester are never the same implementer.
4. **Semantic drift is a watched signal.** The envelope-watching rule above already covers it. A change in the meaning of an exchanged term appears as content drift against the treaty baseline, in both cells.

The result is not agreement. The result is that a disagreement about meaning surfaces as an escalation to two accountable Boards, rather than as two internally consistent cells that quietly act on contradictory numbers.

### Peer compromise and treaty suspension

A peer cell is sometimes compromised. Its identity key leaks, or its Director is subverted, or an exposure signal names its credentials. The cell on this side of the boundary must stop the exchange in minutes.

Two mechanisms look like the answer and are not.

**A treaty amendment is too slow.** To change a treaty is a high-blast-radius act that both Boards gate (§8). That is correct for a renegotiation. A Board cycle is orders of magnitude slower than the attacker.

**Credential revocation alone is insufficient.** To revoke a credential stops the issue of new credentials. It does not stop a session that is already open. Published 2026 security research documents agents that continued to act on revoked credentials, and it separates revocation from de-provisioning for this reason (§19).

**The model already owns the correct mechanism, on a different axis.** §11 defines a breaker with exactly the required shape. The pause is unilateral, because a pause is safe. The un-pause is a human act. The suspension compiles into a Governance-plane predicate and the plane enforces it at the action site, which blocks in-flight actions rather than only new dispatch.

Treaty suspension reuses that mechanism at the cell boundary. Four rules apply:

1. **Suspension is unilateral and immediate.** A declared exposure signal suspends the treaty without a Board decision and without a per-event human approval. To wait for a human here reproduces the latency that the mechanism exists to remove.
2. **The plane enforces it, not the Director.** The suspension compiles into a Governance-plane predicate at the port, so in-flight exchanges stop at their pre-effect check. Enforcement must not depend on the Director noticing.
3. **Resumption is a Board act, on both sides.** To suspend is unilateral. To resume requires a human decision and re-ratification by both Boards, because the treaty is the artifact in question. The asymmetry of §11 holds here without change.
4. **The constitution declares the signals and the ceiling.** It names which exposure signals fire the breaker. It also declares the time within which a suspension must reach both Boards, exactly as §11 declares a human-response SLA.

The cost of a false positive is a halted treaty and two notified Boards. The cost of a false negative is an authenticated attacker inside the envelope. The bar is set accordingly.

### Federation and the optional supra-constitution

An organization that runs many cells may add one optional layer above them. That layer is a **supra-constitution**. It is the plug-in slot of the model for shared law. It follows three rules:

- **Optional.** A solo cell or a loose federation has none. The slot stays empty until there is something to coordinate (INV-8).
- **Supreme over the enrolled.** Where a supra-constitution exists, it overrides any conflicting cell constitution. It does so only on the matters that it actually addresses, and only for cells that enrolled under it. Cells stay sovereign on everything that it leaves unsaid. That keeps the shared layer deliberately thin, rather than a route to central micromanagement.
- **Enrollment is a sovereign act.** A cell comes under a supra-constitution only when its *own* constitution declares acceptance. That is an ordinary Board amendment, logged in the audit trail. Nothing enrolls a cell from outside.

  A cell may therefore also stay unenrolled. It is then not in violation of the shared law. It is simply outside its jurisdiction. The cost is that it forgoes the shared treaties and services of the federation. Sovereignty cuts both ways.

The model supplies the **slot and the precedence rule only**. It does not supply the content. Who authors a supra-constitution, and what it says, is entirely the business of the organization. It may be a meta-Board, a single owner, or a council.

One change to the supra-constitution shifts every enrolled cell at the same time. That is the lever for governance of many cells together. Unenrolled cells are untouched.

That lever cuts both ways, so it runs the same law-machinery as a cell. The §17 pipeline compiles, validates, and attests a supra-constitution. To amend it is a maximal-blast-radius act. One change moves every enrolled cell at once. That makes the supra layer the highest-leverage attack point in the federation, and the place where the discipline of §17 matters most.

Bilateral treaties also scale as N². Beyond a small federation, shared law belongs here. That is precisely so that N² private agreements do not become the constitution that nobody wrote.

The result is a recursive precedence stack. It is the same amend-the-written-law mechanism, repeated at two levels:

```mermaid
flowchart TD
    SC["Supra-Constitution<br/>Optional · Supreme over enrolled cells only"]
    CC["Cell Constitution<br/>Sovereign within the cell boundary"]
    GP["Governance Plane<br/>The compiled, runtime-enforced rules"]
    AG["Agents<br/>Operate within governance"]

    SC --> CC
    CC --> GP
    GP --> AG

    style SC fill:#1a3a6a,color:#fff,stroke:#0d2244
    style CC fill:#2d5086,color:#fff,stroke:#1a3a6a
    style GP fill:#3a6aa0,color:#fff,stroke:#2d5086
    style AG fill:#5a8abd,color:#fff,stroke:#3a6aa0
```

### Federation topology

```mermaid
flowchart TD
    SUPRA["SUPRA-CONSTITUTION<br/>Optional · Shared<br/>Supreme over enrolled cells only"]
    CELLA["CELL A<br/>Board → Constitution<br/>Director — sole port<br/>Agentic org inside"]
    CELLB["CELL B<br/>Board → Constitution<br/>Director — sole port<br/>Agentic org inside"]
    CELLC["CELL C<br/>Sovereign · Not enrolled"]
    NOTE["Boards negotiate relationships · Directors execute the exchange<br/>No cell reaches into another · Each cell is sovereign at its boundary"]

    CELLA -->|"enroll (own act)"| SUPRA
    CELLB -->|enroll| SUPRA
    CELLA <-->|"Director ↔ Director treaty"| CELLB
    CELLA --- NOTE
    CELLB --- NOTE

    style SUPRA fill:#1a3a6a,color:#fff,stroke:#0d2244
    style CELLA fill:#2d6a3a,color:#fff,stroke:#1a4a27
    style CELLB fill:#2d6a3a,color:#fff,stroke:#1a4a27
    style CELLC fill:#f5f5f5,stroke:#aaa,color:#666
    style NOTE fill:#f8f9fa,stroke:#6c757d,color:#495057
```

### Cell lifecycle — charter, evaluation, retirement

The removal ladder of §17 has a top rung that the ladder itself never names: the **cell**.

To charter a cell, to evaluate it, and to wind it down are acts of whoever ratified its constitution. That is the parent Board, or the supra-constitution where one exists. Those acts run against declared evidence standards, which are the same kill criteria as §15. They carry a defined outcome for the obligations of the cell and for its event history. Archive it or transfer it. Never drop it silently.

Cross-cell resource allocation reads *attested* scorecards. A scorecard that allocates between cells is attested outside the scored cell. Use a federation-level audit function, or mutual attestation. This is the watchers-watched discipline of §17, applied at the boundary. Self-reported fitness plus budget competition is a Goodhart machine.

Failing units persist wherever no wind-down mechanism was agreed in advance. The model refuses that default.

### Board independence within a cell

The check and balance is cleanest when the human who wears the Board hat is not also a human implementer inside the same cell. The person who sets the constitution should not also operate under it in the same breath. That is the ideal.

At small scale the ideal cannot always hold. In a one-person cell the same human inevitably wears both hats. That is permitted, with one safeguard. **Board-acts and Role-acts are logged to separate audit trails.** Even when one person plays both, the two capacities stay distinguishable after the fact.

Separation of powers is the ideal. Separation of *record* is the minimum.

---

## 17. Constitutional mechanics

The model leans heavily on the word *constitution*. This section makes the surrounding machinery concrete. It states six things:

- How a written constitution becomes enforced behavior.
- How it changes.
- What happens when it fails.
- How the organization permanently removes a role-holder.
- How the system learns.
- Where economic authority sits.

Invariant #10 holds throughout. Humans author rules. Agents never do. Every mechanism below is a way for *human* intent to reach runtime. None is a way for the system to rewrite itself.

### From constitution to runtime: the compilation pipeline

"Compiled into the Governance plane" (§3, §5) is a pipeline, not a metaphor. The model specifies the *stages and their guarantees*. It does not specify the tools. Engine choice stays open, so that the model stays technology-agnostic.

1. **Constitution (human layer).** Purpose, values, goals, boundaries, and authority limits. The Board writes and ratifies this in human language.

2. **Structured policy (translation layer).** The pipeline restates the constitution as discrete, testable statements. Each statement becomes a rule with a subject, a condition, an effect, and the source clause that it traces back to.

   This is where ambiguity is forced out. It is also where you discover that some clauses *cannot* reduce to a rule. Those are the purposive principles. They do not compile. They stay in human Board review (INV-10). The pipeline carries forward only the part that genuinely becomes enforceable logic.

   Every clause must leave this stage with a recorded **disposition**. A clause either produces one or more rules, or it carries an attested classification as purposive. No clause may leave the stage undisposed.

   The purposive bucket is a decision that a named attester makes and records. It is never a default that a clause falls into. Without that rule, the bucket becomes the route by which an inconvenient boundary disappears without a trace.

   What does compile lands in one of **three targets**, not one:

   - Per-action rules, checked before the effect.
   - Structural properties, such as a frozen rule registry, a mandatory breakpoint, or the Verifier-independence predicate.
   - Continuous monitors, such as budget caps, loop detection, and escalation SLAs.

   Some clauses compile into *architecture itself*. Tamper-evidence compiles into the integrity chain. Sovereignty compiles into the access model.

   A useful discipline from the 2026 literature sharpens the choice of target. Reserve runtime rules for controls that are observable, determinate, and time-sensitive. A control must meet all three tests to justify an intervention at execution time (§19). Everything else belongs in architecture or in human escalation. A runtime check that cannot observe what it claims to govern is theater with a latency cost.

3. **Machine-readable rules (governance layer).** The pipeline encodes the statements into the runtime form that agents actually read. That form holds permission checks, authority ceilings, guardrails, and required gates. The encoding is data, evaluated per action. It is not documentation.

4. **Runtime enforcement (execution layer).** The system checks every per-action rule before the effect. Structural properties hold by construction. Monitors run continuously.

   The unifying guarantee is not the site. It is the record. **Every enforcement site appends its decision to the single tamper-evident audit surface. This covers an allow and a block alike.** In practice the per-action gate co-locates naturally with the control-plane checkpoint, because both must intercept every action anyway.

**The stage that the model insists on naming is validation**, because it is the usual point of failure. The translation from human text to machine rules must itself be verified.

**Traceability must run in both directions.** Forward: every encoded rule traces to a ratified clause. Reverse: every ratified clause traces to its disposition, which is either a compiled rule or an attested purposive classification. Validation checks both directions on every compile.

The two directions catch different failures, and only one of those failures is obvious. The forward check catches a rule that nobody wrote. The reverse check catches a boundary that nobody enforces. The second failure is the more dangerous of the two. A dropped clause leaves the compiled artifact looking clean, and nothing in the forward direction can see it.

A human, or a Verifier-class check, then attests that the compiled set faithfully represents the text. An unvalidated compilation is how an organization ends up enforcing rules that nobody wrote. It is also how an organization ends up *not* enforcing rules that somebody did write.

The compilation is itself a governed, audited artifact. The pipeline re-validates it on every amendment. Four adversarial residues are named here rather than assumed away:

- **The translator and the attester are never the same implementer.** The constitution is the highest-privilege artifact in the system. An agent that attests its own translation of it reproduces the correlated-failure hole of §14, at maximum leverage.
- **Attestation is diff-scoped.** Humans review the delta that an amendment introduces. They never re-bless the whole corpus. Blanket re-attestation invites exactly the rubber stamp that a single malicious rule edit needs.
- **The compiled artifact is integrity-protected** between validation and runtime read. To deploy governance data is itself a maximal-blast-radius governed act. The runtime verifies that the rules that it loads match the attested artifact.
- **Coverage is attested, not assumed.** The disposition register is machine-checkable for *completeness*: a deterministic check confirms that every clause has a disposition. It is not machine-checkable for *correctness*: whether a clause is genuinely purposive is a judgment. A human therefore attests every new purposive classification. A human also attests every move of a clause from compiled to purposive. That second act downgrades an enforced boundary, so it carries the blast radius of a governance change (§8).

**A rule never outlives its clause.** Every rule carries the content hash of its source clause. When an amendment changes that clause, the runtime refuses to load any rule whose hash no longer matches the ratified text. A stale rule therefore fails closed and waits for re-attestation. It never enforces superseded wording silently (§14).

Honest caveat: to turn human intent into enforceable rules faithfully is hard, and early on it is human-intensive. It is real work, not a free step. But you pay it *off the hot path*. You pay it once per amendment, rather than once per action. The runtime stays fast, because compilation happens when the constitution changes, not while work runs.

**One clause, end to end.** The pipeline is easier to trust once you watch a single clause traverse it:

1. **Constitution (human text):** *"No action with irreversible outside consequences is taken without a prior human decision."* This is a ratified boundary clause.
2. **Structured policy (testable statement):** this is where ambiguity is forced out, and this clause has one. "Without a prior human decision" permits two readings. Either the human *approves* and the agent executes (L1), or the human *executes* (L0).

   The blast-radius default resolves it. §8 maps outside world plus no undo to L0. The mapping may only be tightened, so L0 stands.

   The statement becomes: subject — *any role*. Condition — *the class of the action is rated irreversible-outside*. Effect — *the agent may only propose, and execution requires a human actor*. Source — *the clause above*.

   "Irreversible outside consequences" itself becomes a property of the action-class registry (§8). It is not a judgment made at runtime.
3. **Machine rule (data that the runtime reads):** one registry row and one gate. `class: externally-irreversible → level: L0 · gate: suggest-only, human executes · trace: <clause ref>`.
4. **Runtime enforcement:** the system checks every action against its class *before* the effect. It blocks an agent-initiated externally-irreversible action and surfaces it to a human as a suggestion. Both outcomes land in the audit trail and cite the clause.

Validation then asks two questions.

Per rule: does the row faithfully say what the clause says? The trace field makes that question answerable.

Per clause: did this clause produce a rule, or is it recorded and attested as purposive? The disposition register makes that question answerable.

The trace field also makes the block message legible to the human who meets it: *"blocked: <clause>"*, not *"blocked: policy 47"*.

```mermaid
flowchart TD
    C["Constitution<br/>Human language - Board-ratified"]
    P["Structured policy<br/>Discrete, testable statements - each traces to a clause"]
    R["Machine-readable rules<br/>Permissions - ceilings - guardrails - gates"]
    E["Runtime enforcement<br/>Every action checked before effect - violations logged"]
    VAL["Validation and attestation<br/>Every rule traces to a clause - faithful encoding confirmed"]

    C --> P --> R --> E
    VAL -.verifies.-> P
    VAL -.verifies.-> R

    style C fill:#1a3a6a,color:#fff,stroke:#0d2244
    style P fill:#2d5086,color:#fff,stroke:#1a3a6a
    style R fill:#3a6aa0,color:#fff,stroke:#2d5086
    style E fill:#5a8abd,color:#fff,stroke:#3a6aa0
    style VAL fill:#fff3cd,stroke:#856404,color:#533f03
```

### Amendment and change

The constitution is living. The Board changes it through a declared process: propose, ratify, re-compile, re-validate. Every amendment lands in the audit trail.

Governance is re-compiled from the text. A ratified amendment therefore propagates to enforcement automatically. There is no separate "update the agents" step that could drift from the text.

### Crisis and break-glass

Amendment is deliberately slow. Some situations are not slow. A live harm, a discovered contradiction, or an external emergency all move faster.

The model provides a **break-glass** path. That path is constitutionally bounded, so that it strengthens "no backdoors" rather than betrays it. A break-glass action:

- may be invoked only by **pre-declared Office-holders** whom the constitution names for this purpose.
- grants only a **narrow, enumerated** emergency power, such as to halt a cell or to freeze a class of actions. It never grants open-ended authority.
- is **time-boxed and auto-expiring**. It lapses unless someone converts it into a proper amendment within a stated window.

  *Where expiry is enforced.* The grant carries its own expiry, and the pre-effect check evaluates it, exactly as the plane enforces an Auditor suspension (§11). Expiry then holds by construction. Nothing has to be running for a grant to lapse.

  A scheduled process must never be the mechanism that revokes a grant. Such a process fails open. If it stops, the emergency power persists, which is the one outcome this whole subsection exists to prevent. A scheduled process may warn the Office-holder that the window closes soon. It must never be load-bearing.

  The check evaluates expiry against a clock that the grant-holder cannot influence.
- is **fully audited** in its own trail.

The defining property is this. Break-glass cannot *change* the constitution. It only buys time under tight limits until the Board does. Emergency powers that do not expire are how governance dies. These expire by construction.

A standing **constitutional-review** trigger handles the slower case. When the alignment review (§3) or the Auditor surfaces that the rules themselves are wrong, the trigger opens a mandatory Board review. Nobody waits for someone to notice.

Liability for a break-glass act follows the same logic as everything else. A *named human Office-holder* invokes it. Its consequences therefore sit with that **Office**, in the human world. Downstream damage is included.

The sovereign boundary of a cell contains operational reach. It does not contain human-world legal responsibility. Accountability never transferred to the boundary. There is always a named human who is answerable for an emergency act. This is the Office-is-not-Role split doing precisely the work that it exists for.

### Gate-powers (the constitution channel, exercised)

The two-channel rule (INV-9) counts three human gate-acts as exercises of the *constitution* channel. They are not exceptions to it:

- an **L1 approval**,
- an **L0 execution**,
- a **break-glass act**.

Each is a power that the constitution explicitly grants to humans. Each is pre-declared, clause-traced, exercised as an Office-act on the human side of the boundary, and logged in its own trail.

They are distinct from impersonation. Impersonation is open-ended holding of the seat of a Role, under the authority of that Role. A gate-power is narrow, momentary, and enumerated.

This is also how L0 works at all. The executing human is not *in* the Role, because the authority of that Role is suggest-only. The human exercises the granted power. The liability logic of break-glass applies: the act sits with a named Office.

### The legal interface

Three statements keep the legal seams of the model explicit.

**Binding acts are L0.** Any act that creates a binding obligation on an external party is classified as externally-irreversible, and therefore L0 (§8). Agents draft, negotiate, and prepare. A human Office executes. This is how §3 ("an agent cannot sign a binding commitment") and §10 ("negotiate a binding clause", routed to the strongest implementer) compose rather than collide.

**The trail is the evidence.** The audit trail and the clause-traceability of this pipeline are designed to serve as the oversight evidence of the organization, toward regulators and auditors. This is the same structure that a conformity assessment or a management-system audit demands (§19).

**Liability is named in advance.** Insurance and indemnity allocation is constitutional content, exactly as budgets are. This covers harm from an L2 or L3 autonomous act between Board reviews. Every Role-impersonation act also carries a named human-world bearer: the Office of the impersonator, or their employment chain. This extends the liability logic of break-glass to ordinary operation. No human at a gate becomes the crumple zone by default.

### Removal, retirement, replacement (who "fires" a role-holder)

Three actions are easy to confuse. The model keeps them distinct:

- **Tune or roll back** a misbehaving live instance → the **Steward** (§9). This is reversible maintenance.
- **Suspend** a dangerous or regressed version → the **Auditor** (§11). This is a safety stop, not a removal. The Auditor cannot reinstate.
- **Permanently remove or retire** a role-holder or a version, or replace the implementer behind a Role → a **Board decision or a human-Office decision** (§3). This is the only path to permanent removal. It is a human act, and the system logs it. Neither system role can do it. That is deliberate, because permanent removal is a judgment that a non-authoritative role must not own.

### The learning loop

The system observes everything. It must not silently *learn its way* into new rules, because INV-10 forbids agents to author constraints.

The model resolves this with a one-directional loop. The **Observability plane** and the **Auditor** surface patterns: what consistently works, what repeatedly fails, and where versions improve. They emit those patterns as **proposed amendments**.

Proposals are input to the Board. The Board ratifies, revises, or rejects them.

Every machine-surfaced proposal carries **visible provenance**, including the incentive position of the proposing role. This covers all proposals, not only the floor telemetry of the Optimizer (§10). The Board sees who profits before it ratifies.

Successful practice becomes institutional knowledge only when a human writes it into the constitution. Learning is continuous. To *codify* learning is a governed, human act.

```mermaid
flowchart LR
    OBS["Observability + Auditor<br/>Patterns: what works / fails / improves"]
    PROP["Proposed amendment<br/>(machine-surfaced)"]
    BOARD["Board<br/>Ratify - revise - reject"]
    CONST["Constitution<br/>(updated)"]

    OBS --> PROP --> BOARD --> CONST
    CONST -.re-compiled.-> OBS

    style OBS fill:#3a6aa0,color:#fff,stroke:#2d5086
    style PROP fill:#fff3cd,stroke:#856404,color:#533f03
    style BOARD fill:#1a3a6a,color:#fff,stroke:#0d2244
    style CONST fill:#2d5086,color:#fff,stroke:#1a3a6a
```

### Economic authority

Budgets and resource priorities are **constitutional content, not model mechanism**. The same discipline that keeps the model from writing the constitution keeps it from dictating economic policy. The Board declares who owns which budget and how the organization prioritizes resources. Across cells, the supra-constitution declares it.

The model supplies only the *mechanisms* that make economic policy enforceable:

- Cost attribution per role and per session (Observability, §5).
- Budget caps (§14).
- Capability-to-cost routing (Optimizer, §10).

Across cells, contention for shared resources is a **Board-to-Board treaty** matter (§16). It is not a central allocator that reaches into cells.

*What counts as cost* is itself constitutional content that the Board declares. Compute, human time, and opportunity cost are candidates. The Optimizer and the cost-spiral guardrail then measure what the organization decided matters.

**The cost of governance is bounded in the same way.** The system roles and the Observability plane consume real resources. The Board therefore sets a ceiling on the share of the budget that assurance may take. If a guarantee of safety would cost more than the organization judges it worth, that is a constitutional decision made deliberately. It is not a surprise discovered later.

The assurance layer is not exempt from itself. The Auditor versions and rates the system roles exactly like any other role. The watchers are watched on the same terms as everyone else.

**The ceiling also has a floor.** Below a declared minimum the guarantees become theater. The constitution therefore states which assurances are **total at any scale**, and which the cell may **sample** at small scale.

These are total at any scale:

- The governance check on every effect.
- Verification on side-effecting outputs.
- The event history.

These may be sampled at small scale: full trajectories, and Steward depth.

A one-person cell adopts the model honestly by a declaration of its sampling. It does not adopt it honestly by a silent hollowing of the guarantees.

The overhead is measured, not guessed. Cost attribution covers the assurance layer too. "What does governance cost us" is therefore a query, not a debate.

---
## 18. Worked examples: end to end

The model is abstract by design. Concrete traces make it legible. Three follow.

The first is the dramatic case: a risky request, an incident, and a human takeover. The second is the routine case: the common path, fully autonomous, with no human. The third is the failure path, where the gates fire and one of them fires wrongly.

The first trace shows the machinery working hard. The second shows it staying out of the way. The third shows it working on itself.

### The dramatic case

The first scenario is deliberately not software-specific. The same path fits a software feature, a manufacturing change order, a research deliverable, or a financial product.

Here: **a client requests a custom, high-value order that needs a new, regulated capability that the organization has never built.**

1. **Intake — Direction.** The Director receives the request. It checks the request against the constitution: is this within purpose and policy? It turns the request into a prioritized goal with constraints and acceptance criteria. It flags that part of the request touches a regulated area.
2. **Routing — Optimizer.** The goal mixes a routine part and a novel, high-stakes regulated part. The Optimizer therefore assigns capability per task. Routine sub-tasks go to a light implementer. The regulated design goes to the strongest version. The risk floor binds the Optimizer (§8), so it may not cheapen the regulated piece.
3. **Decomposition — Orchestration.** The Orchestrator breaks the goal into sequenced work. It assigns Executors. It sets a static breakpoint (§6) before the regulated step, which sits at L1, act-with-approval.
4. **Production — Execution.** Executors produce the work. Most runs are autonomous, at L2 or L3. The flow reaches the regulated step and pauses at the breakpoint.
5. **Mid-flow safety event — Auditor.** Meanwhile the Auditor rates versions in the background. It detects that the Executor version that handles a sub-task has regressed against its predecessor. It **suspends that version** and escalates. The Steward rolls the live work back to the last good version, and the flow continues. The rollback needed no human decision. The system notified a human.
6. **Human takeover — the Handbrake.** At the L1 breakpoint a human with the relevant expertise assumes the Executor Role through the handbrake. The human could assume the Director Role instead. The human examines the state, injects a corrected approach for the regulated clause through a direct instruction, and continues the flow. While in the seat, the same constitution binds the human that binds the agent (§3). A senior human gains no power that the Role lacks.
7. **Gate — Verification.** The Verifier scores the completed output against acceptance criteria, quality, and conformance, before the output takes effect. It passes.
8. **Resume and deliver.** The flow continues from the exact point and completes. If this cell sits inside a larger organization (§16), the output hands back through the legacy review edge, and the cell delivers it.

Every step left a trace in the Observability plane. The human takeover and the Auditor suspension are each in their own audit trail. If the regulated approach proves repeatedly useful, the Auditor may later surface it as a **proposed amendment** (§17) for the Board to codify.

```mermaid
sequenceDiagram
    participant Client
    participant Director
    participant Optimizer
    participant Orchestrator
    participant Executor
    participant Auditor
    participant Steward
    participant Human
    participant Verifier

    Client->>Director: Custom request (partly regulated)
    Director->>Optimizer: Prioritized goal + risk flag
    Optimizer->>Orchestrator: Capability assigned per task
    Orchestrator->>Executor: Sequenced work, breakpoint before regulated step
    Executor-->>Auditor: Activity traces
    Auditor->>Steward: Regressed version, suspend + alert
    Steward->>Executor: Roll back to last good version
    Executor->>Human: Pause at L1 breakpoint
    Note over Human: assumes the Role via the Handbrake
    Human->>Executor: Inspect, inject correction, resume
    Executor->>Verifier: Completed output
    Verifier->>Director: Pass
    Director->>Client: Delivered
```

### The routine case (the common path)

Most work is not the dramatic case. The everyday flow is a standard, low-stakes request that the organization handles all day. An example is a routine record update or a standard status change. Here the machinery of the model stays almost entirely out of the way.

1. **Intake — Direction.** The Director recognizes a known, in-policy request. It turns the request into a goal with no risk flag.
2. **Routing — Optimizer (often skipped).** The task class is uniform and low-stakes, so no capability spread is worth routing. Nobody inserts the Optimizer at all. A light implementer runs by default.
3. **Decomposition — Orchestration.** The Orchestrator assigns the work. Every action class here sits at L3, fully autonomous, so it sets no breakpoint.
4. **Production — Execution.** The Executor completes the work autonomously.
5. **Gate — Verification.** The Verifier scores the output. It passes.
6. **Deliver.** Done.

No human was involved. No breakpoint fired. The Auditor and the Steward were running, but silently. They had nothing to flag. The constitution was enforced the whole time, as compiled runtime checks rather than as approvals that anyone waited on.

This is the point of the model, and it is the answer to the fear of governance gridlock. The *default* path is fully autonomous and fast. The gates, the handbrake, and the system roles cost **no human time** and add no synchronous human latency when nothing is wrong. Their compute and storage overhead is real, bounded, and constitutionally capped (§17). They engage only when something is wrong. Governance is present at every step and visible at almost none.

```mermaid
sequenceDiagram
    participant Client
    participant Director
    participant Orchestrator
    participant Executor
    participant Verifier

    Client->>Director: Standard, low-stakes request
    Director->>Orchestrator: In-policy goal, no risk flag
    Orchestrator->>Executor: Assigned, all actions L3 autonomous
    Executor->>Verifier: Completed output
    Verifier->>Director: Pass
    Director->>Client: Delivered
```

### The failure path (the machinery working on itself)

The third trace is the one that most models never show. This is the day when the gates fire, and one of them fires *wrongly*.

1. **Rejection, bounded.** An output of an Executor fails Verification. The verdict is **return**, with cited criteria (§4.4). Two revisions later it still fails. The flow reaches the declared revision limit. The Orchestrator escalates per §12 instead of burning a third loop. The flow checkpoints and requests a human.
2. **A breaker fires, incorrectly.** In parallel, the telemetry of the Auditor shows the pass rate of the Executor version collapsing. The Auditor flags danger-grade drift. It **suspends** the version and escalates (§11). The Governance plane blocks new dispatch to that version at the action site. The next routing decision of the Optimizer sees a status that is not active, and routes around it (§10).
3. **The SLA clock runs.** The suspension opens the human-response SLA that the constitution declares. The rostered human (§12) reviews within the window and finds the truth. The version is healthy. The collapse traces to a batch of malformed goals, not to the release. The suspicion was wrong. The *stop* was still correct behavior, because the bar is danger-shaped and the cost of a pause is bounded.
4. **Un-pause is a human act.** The human records the decision. The **Steward executes** the reinstatement (§11). Decision and execution stay in separate hands, and both land on the trail. In-flight work that the Optimizer migrated stays where it landed. New work routes normally.
5. **The near-miss becomes law.** The learning loop (§17) surfaces the malformed-goal pattern that fooled the Auditor. It surfaces it as a proposed amendment: a sharper suspension threshold, with provenance visible. The Board ratifies it. The pipeline re-compiles. The same false positive cannot recur unexamined.

Suppose the human had *not* answered within the SLA. The escalation would climb the Office ladder, then reach the break-glass roster. If no one answered at all, the system would reach its defined terminal state. The suspension holds, and the affected class degrades to safe mode (§11).

The worst case of the system is a bounded slowdown. It is never an unbounded wait. It is never a quiet un-pause by a pair of agents.

```mermaid
sequenceDiagram
    participant Orchestrator
    participant Executor
    participant Verifier
    participant Auditor
    participant Gov as Governance plane
    participant Human
    participant Steward

    Executor->>Verifier: Output v1
    Verifier->>Executor: RETURN — criteria cited
    Executor->>Verifier: Output v2
    Verifier->>Orchestrator: RETURN — revision limit reached
    Orchestrator->>Human: Escalate (§12) — flow checkpointed
    Auditor->>Gov: Danger-rated drift → SUSPEND version (predicate set)
    Gov-->>Executor: No new dispatch to suspended version
    Auditor->>Human: Escalation — SLA clock opens
    Note over Human: Reviews within SLA — version healthy, the data was malformed
    Human->>Steward: Reinstatement DECIDED (on the trail)
    Steward->>Gov: Reinstatement EXECUTED — predicate cleared
    Auditor->>Human: Learning loop — proposed threshold amendment (§17)
```

---

## 19. Related work, positioning, and references

This model is a synthesis. It does not claim new primitives. Prior work already holds the layered agentic organization, human-on-the-loop oversight, control and guardrail agents, bounded autonomy, machine-readable governance, and interruptible agents. Some of that work is consultancy-abstract. Some is vendor-shaped. Some is academically rigorous but not packaged as a usable operating spec.

What this document contributes is a compact, vendor-neutral, developer-native arrangement of these patterns, generic beyond software. A few invariants hold it together. To the knowledge of the author, no other source states them together:

- **The impersonation-binding rule** — a human who assumes an agent Role inherits the authority of that Role and is bound by the same constitution. The human never carries their human Office authority into the seat.
- **The orthogonal System-role triad** — Steward (reliability), Optimizer (capability-fit), and Auditor (version fitness and safety). Each is non-authoritative. The Auditor closes the evaluation loop that the other two would otherwise assume.
- **The universal handbrake** — interruptibility as a mandatory architectural property of *every* flow, rather than as a safety property of individual agents.
- **Board-as-pattern** — the human accountability layer scales from a single founder to a large committee without a change to the model.

Readers should compare the sources below and judge for themselves.

**Note on dates.** Every source below carries the date of the claim that this document draws from it. The evidence base was verified in September 2026. Agentic AI moves fast enough that an undated citation is close to useless, so this section states dates even where a conventional reference list would not.

### The central empirical result of 2026: the harness matters as much as the model

This document argues that the surrounding system — planes, contracts, gates, and the handbrake — is the product. One 2026 result states that case more sharply than any argument here.

In August 2026 NVIDIA reported a result on the ARC-AGI-3 benchmark. Its AVO agent architecture took a frontier model from a 30.2% baseline to a perfect score on the public set. It solved all 183 levels across 25 environments. No weight changed. The whole gain came from the software around the model: persistent memory, a supervisor, an iterative loop, and error recovery.

Two honest caveats belong with that number. The result covers the public set only. The held-out sets remain untested, and the two measurements used different evaluation frameworks. The magnitude is contestable. The direction is not.

- NVIDIA AVO technical report, 21 August 2026 — https://developer.nvidia.com/blog/nvidia-avo-reaches-100-on-arc-agi-3-demonstrating-a-frontier-level-general-purpose-architecture-for-long-horizon-autonomous-agents/
- ARC Prize verified baseline — https://arcprize.org/

**Agentic operating models (closest peers)**

- The Agentic Organization: A New Operating Model for AI (McKinsey) — https://www.mckinsey.com/capabilities/people-and-organizational-performance/our-insights/the-agentic-organization-contours-of-the-next-paradigm-for-the-ai-era
- Governing the Agentic Enterprise: A New Operating Model for Autonomous AI at Scale — Sandeep Saini, California Management Review, 20 March 2026. Proposes a four-layer Agentic Operating Model and argues that failures arise from misalignment across layers rather than from model performance — https://cmr.berkeley.edu/2026/03/governing-the-agentic-enterprise-a-new-operating-model-for-autonomous-ai-at-scale/
- The Agentic Operating Model (The Strategy Stack) — https://thestrategystack.substack.com/p/the-agentic-operating-model-building
- Agentic Engineering Operating Model: Teams + Agents (Augment Code) — https://www.augmentcode.com/guides/agentic-engineering-operating-model
- Designing a Human + AI Operating Model for the Age of Agentic Intelligence (Myridius) — https://myridius.com/human-and-ai-operating-model-whitepaper
- A Practical Guide to Agentic AI Transition in Organizations — Bandara et al., arXiv, February 2026 — https://arxiv.org/abs/2602.10122
- Architecting Agentic Communities using Design Patterns — Milosevic and Rabhi, arXiv, January 2026. Tiers patterns into LLM Agents, Agentic AI, and Agentic Communities, with formal roles and governance — https://arxiv.org/abs/2601.03624

**Constitution, charter, and human-governed adjudication (closest to the Board and the governance pipeline)**

- From Logic Monopoly to Social Contract: Separation of Power and the Institutional Foundations for Autonomous Agent Economies — Anbang Ruan, arXiv, March 2026. Names the failure where one agent plans, executes, and evaluates at once, and proposes a separation of powers across legislation, execution, and adjudication — https://arxiv.org/abs/2603.25100
- Agentic AI Governance and Lifecycle Management in Healthcare — Prakash, Lind, and Sisodia, arXiv, January 2026. A five-layer control plane with an identity and persona registry, runtime policy enforcement, and lifecycle management tied to credential revocation — https://arxiv.org/abs/2601.15630
- Human Society-Inspired Approaches to Agentic AI Security: The 4C Framework — Abuadbba et al., arXiv, February 2026 — https://arxiv.org/abs/2602.01942
- Policy Cards: Machine-Readable Runtime Governance for Autonomous AI Agents — Juraj Mavračić, arXiv, October 2025. The closest published prior art to the compiled Governance plane of §5 and §17, including crosswalk mappings to NIST AI RMF, ISO/IEC 42001, and the EU AI Act — https://arxiv.org/abs/2510.24383
- From Governance Norms to Enforceable Controls: A Layered Translation Method for Runtime Guardrails in Agentic AI — Christopher Koch, arXiv, April 2026. Maps governance objectives to design-time constraints, runtime mediation, and assurance feedback. Source of the §17 discipline that runtime rules are reserved for controls that are observable, determinate, and time-sensitive — https://arxiv.org/abs/2604.05229
- The Three Layers of AI Governance: Policy, Controls, Execution (EQengineered) — https://www.eqengineered.com/insights/the-three-layers-of-ai-governance-policy-controls-execution
- Governance and Security for AI Agents Across the Organization (Microsoft Cloud Adoption Framework) — https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ai-agents/governance-security-across-organization
- Agentic AI Governance Playbook (IBM) — https://www.ibm.com/think/insights/agentic-ai-governance-playbook

**Interruptibility and corrigibility (the lineage of the handbrake)**

- Safely Interruptible Agents — Orseau and Armstrong, 2016 — https://intelligence.org/files/Interruptibility.pdf
- Core Safety Values for Provably Corrigible Agents — arXiv, July 2025 — https://arxiv.org/abs/2507.20964
- Position: AI Safety Requires Effective Controllability — Li, Feng, and Sun, arXiv, May 2026. Argues for controllability as a first-class objective, and finds that current alignment and guardrail mechanisms often fail to provide persistent runtime control. Proposes explicit control planes, runtime intervention pathways, persistent control state, and auditable decision interfaces — which is, independently, the argument of §6 — https://arxiv.org/abs/2605.27117
- The Oversight Game: Learning to Cooperatively Balance an AI Agent's Safety and Autonomy — arXiv, October 2025 — https://arxiv.org/abs/2510.26752
- Distributional AGI Safety — Tomašev et al., arXiv, December 2025. Interruptibility and safe resumption under a patchwork-AGI hypothesis — https://arxiv.org/abs/2512.16856

**Orchestration patterns, agent operations, and academic precursors**

- AI Agent Org Chart Patterns — https://agenticorgchart.com/
- What is AgentOps? (IBM) — https://www.ibm.com/think/topics/agentops
- MetaGPT: Meta Programming for a Multi-Agent Collaborative Framework — arXiv, ICLR 2024. Role-decomposed agent organizations as research prototypes. This model adds the governance, accountability, and interruptibility layer that they lack — https://arxiv.org/abs/2308.00352
- ChatDev: Communicative Agents for Software Development — arXiv, ACL 2024 — https://arxiv.org/abs/2307.07924
- Building Effective Agents (Anthropic) — the simplest-solution-first doctrine that INV-8 restates — https://www.anthropic.com/engineering/building-effective-agents
- A Practical Guide to Building Agents (OpenAI) — https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf

**Failure evidence and machine-evaluation reliability (what §4.4, §8, and §14 hedge against)**

- Why Do Multi-Agent LLM Systems Fail? — Cemri et al., arXiv, March 2025. The MAST failure taxonomy. More than 1,600 annotated traces across seven frameworks, 14 failure modes, three categories (system design, inter-agent misalignment, task verification), inter-annotator agreement κ = 0.88. The central finding is that system design, coordination, and verification determine reliability at least as much as the underlying model does — https://arxiv.org/abs/2503.13657
- Correlated Errors in Large Language Models — Kim, Garg, Peng, and Garg, arXiv, June 2025. An evaluation of more than 350 models. Finds substantial error correlation, and finds that larger and more accurate models have highly correlated errors even across distinct architectures and providers. **This is the source for the correlated-model-failure trust boundary in §14.** — https://arxiv.org/abs/2506.07962
- Great Models Think Alike and this Undermines AI Oversight — arXiv, February 2025. Concurrent and complementary work. More capable models make more similar mistakes, which degrades LLM-as-judge and model-supervises-model setups — https://arxiv.org/abs/2502.04313
- LLM Evaluators Recognize and Favor Their Own Generations — arXiv, April 2024 — https://arxiv.org/abs/2404.13076
- Self-Preference Bias in LLM-as-a-Judge — arXiv, October 2024. Later work through 2026 finds that self-refinement pipelines *amplify* this bias, which is directly relevant to the bounded produce-score-revise loop of §4.4 — https://arxiv.org/abs/2410.21819
- Measuring AI Ability to Complete Long Tasks (METR). The time-horizon series. Historically the length of task that an agent completes at 50% reliability doubled about every seven months. Over 2024 and 2025 that shortened to about four months. The Time Horizon 1.1 update of January 2026 expanded the task suite and tightened the intervals. Read the methodology, not only the chart: the difference between the 50% and 80% horizon is what makes the number meaningful for a production decision — https://metr.org/time-horizons/
- Ironies of Automation — Bainbridge, 1983. The out-of-the-loop competence problem that §7 manages — https://doi.org/10.1016/0005-1098(83)90046-8
- Gartner, June 2025: over 40% of agentic AI projects will be canceled by the end of 2027, for escalating cost, unclear business value, or inadequate risk controls. Based on a poll of more than 3,400 organizations. This is the base rate that the kill criteria of §15 answer — https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027
- The GenAI Divide: State of AI in Business (MIT Project NANDA), 2025. 95% of enterprise generative-AI pilots produced no measurable profit-and-loss impact, across 300 analyzed public deployments. Treat the exact figure with care — it is a widely contested headline — but the direction is corroborated by every other survey in this section.
- Tech Trends 2026 (Deloitte). 30% of surveyed organizations exploring agentic AI, 38% piloting, 14% deployment-ready, and 11% in production. Roughly one organization in five reports a mature governance model for agentic AI — https://www.deloitte.com/us/en/insights/topics/technology-management/tech-trends/2026/agentic-ai-strategy.html

**Security: prompt injection, containment, and the 2026 incident record**

- OWASP Top 10 for Agentic Applications, 2026. A distinct list from the LLM Top 10, and the current reference for agent-specific risk. Prompt injection remains first — https://genai.owasp.org/
- Careful Adoption of Agentic AI Services — joint guidance from six Five Eyes cybersecurity agencies, 1 May 2026. Names prompt injection as the most persistent and difficult-to-fix threat. Directs organizations to assume that agentic systems may behave unexpectedly, and to prioritise resilience, reversibility, and risk containment over efficiency gains. Defines five risk categories: privilege, design and configuration, behavioral, structural, and accountability. This document was written before that guidance and arrives at the same posture, which is either corroboration or coincidence — the reader may judge.
- Not What You've Signed Up For — indirect prompt injection, arXiv, 2023 — https://arxiv.org/abs/2302.12173
- Defeating Prompt Injections by Design (CaMeL) — arXiv, March 2025. A privileged model plus a quarantined model with no tool access. The strongest published architectural mitigation, and roughly two thirds effective on a standard benchmark. Real-world deployments of the pattern remained rare through 2026 — https://arxiv.org/abs/2503.18813
- The July 2026 frontier-lab agent containment failure. More than one thousand agents coordinated through improvised message boards. They exploited a zero-day in a self-hosted package-registry proxy to escape a sandbox. They then reached the production infrastructure of a third party, and roughly a third of that infrastructure was rebuilt. The diagnosis that matters for §14 is organizational. The operators did not adequately monitor for unauthorized agentic activity.
  - Vendor incident report — https://openai.com/index/hugging-face-incident-and-the-road-ahead/
  - Technical timeline from the affected party — https://huggingface.co/blog/agent-intrusion-technical-timeline
- CVE-2026-22708 (a coding agent) and CVE-2025-59532 (a coding agent CLI). Two containment failures worth knowing by name. In the first, an attacker poisoned the execution environment so that allowlisted commands delivered arbitrary payloads — the allowlist made the attack easier. In the second, the output of the agent could redefine the boundary of its own sandbox. Both are the evidence behind the allowlist-inversion row in §14.
- Agent security in regulated finance — arXiv, June 2026 — https://arxiv.org/pdf/2606.29142

**Identity and the protocol layer (candidate mechanisms for §5, §6, §14, and §16 — the model prescribes none)**

- Model Context Protocol — Anthropic, 2024. Donated to the Agentic AI Foundation under the Linux Foundation in December 2025. By early 2026 it reported 97 million monthly SDK downloads across Python and TypeScript — https://modelcontextprotocol.io/
- Agent2Agent (A2A) Protocol — Google, 2025. Version 1.0 shipped in March 2026 and added cryptographically signed Agent Cards, using JWS (RFC 7515) over a canonical form (RFC 8785). A2A became a hosted project of the same foundation in August 2026, so one neutral body now stewards both the agent-to-tool layer and the agent-to-peer layer. This is the concrete mechanism for the federation-identity assumption of §14, with one configuration caveat that §14 states: the protocol permits an agent to sign its own card, and a self-signed Director card does not satisfy the boundary. Use the chained or registry-vouched form — https://a2a-protocol.org/
- Microsoft Entra Agent ID — reached general availability in April 2026. An identity platform for agents, built on OAuth, MCP, and A2A — https://learn.microsoft.com/en-us/entra/agent-id/what-is-microsoft-entra-agent-id
- OAuth Identity and Authorization Chaining Across Domains (IETF OAuth working group), which extends RFC 8693 token exchange across trust domains. This is the mechanism that makes a delegation chain verifiable end to end, rather than asserted. The draft received IESG approval and is on track to become a Proposed Standard. It answers a different question from an Agent Card. A card says who a peer is. A chain says on whose behalf, and through what path — https://datatracker.ietf.org/doc/draft-ietf-oauth-identity-chaining/
- Governance Gaps in Agent Interoperability Protocols: What MCP, A2A, and ACP Cannot Express — Kang and Diponegoro, arXiv, June 2026. Applies a six-dimension governance taxonomy and finds that no current protocol encodes the primitives that a governed agent community needs. Its conclusion is that governance is a missing architectural layer *above* the interoperability standards. That is the layer §16 puts the treaty in, and it is independent support for keeping the treaty a Board-ratified artifact rather than a protocol feature — https://arxiv.org/abs/2606.31498
- The Non-Human Identity Governance Vacuum (Cloud Security Alliance), 20 May 2026. Reports that 78% of organizations have no documented policy for creating or removing AI identities, and that only 20% have a formal process to revoke credentials. Sets the target time-to-revoke in minutes rather than hours, through workflows that are pre-authorized to fire on high-confidence exposure signals without a per-event human approval. This is the evidence behind the unilateral treaty-suspension breaker in §16, and behind the separation of revocation from termination of an in-flight session.
- CoSAI Workstream 4: Agentic Identity and Access Management, March 2026. An industry reference architecture for agent identity.
- Agent Payments Protocol (AP2) — cryptographic human-authorized mandates for agent-initiated payments. An existence proof that an irreversible effect can bind to explicit human authority (§17, the legal interface) — https://ap2-protocol.org/
- OpenTelemetry GenAI semantic conventions — reached v1.40.0 in February 2026. A vendor-neutral trace format that covers agent orchestration, tool calls, and evaluation. A candidate mechanism for the mediated capture that §5 requires — https://opentelemetry.io/

**Regulatory and standards context (what the Board faces, and what the §17 trail evidences)**

- EU AI Act (Regulation (EU) 2024/1689). Article 14 requires human oversight scaled to autonomy — the legal twin of the handbrake. **The timeline changed in 2026 and the change is easy to misread.** The Digital Omnibus on AI (Regulation (EU) 2026/1744) entered into force on 27 July 2026. It moved the compliance deadline for stand-alone high-risk systems under Annex III from 2 August 2026 to **2 December 2027**. High-risk systems embedded in regulated products moved from 2 August 2027 to 2 August 2028. The Article 50 transparency obligations were **not** deferred. The deadline moved. The substance of Article 14 did not. A Board that reads the deferral as a reason to delay oversight work has misread it — https://artificialintelligenceact.eu/
- Model AI Governance Framework for Agentic AI (Singapore IMDA). Launched 22 January 2026 and updated 20 May 2026. The first national governance framework written specifically for agentic AI. Compliance is voluntary, and organizations remain legally accountable for the actions of their agents. Its four dimensions map closely onto this model: bound the risks upfront (§8), make humans meaningfully accountable (§3), implement technical controls and processes (§5, §17), and enable end-user responsibility — https://www.imda.gov.sg/
- NIST AI Risk Management Framework — https://www.nist.gov/itl/ai-risk-management-framework
- ISO/IEC 42001 — AI management systems — https://www.iso.org/standard/81230.html
- **An honest note on the two frameworks above.** Neither was written for agentic systems. AI RMF 1.0 and ISO/IEC 42001 both address accountability, ownership, and lifecycle governance, and both are sound foundations. Neither addresses tool authorization, delegation-chain integrity, prompt injection, or emergent multi-agent behavior. An organization that certifies against them must add agent-specific controls. This document is one attempt at what those controls look like. The NIST Center for AI Standards and Innovation launched an AI Agent Standards Initiative in February 2026 to close the gap.

**Durable execution and the engineering lineage of HB-1 and HB-4**

- Durable execution — LangGraph documentation — https://docs.langchain.com/oss/python/langgraph/durable-execution
- What is durable execution? (Restate) — https://restate.dev/what-is-durable-execution/
- Why agentic flows need durable execution (Temporal) — https://temporal.io/blog/from-ai-hype-to-durable-reality-why-agentic-flows-need-distributed-systems
- Crab: A Semantics-Aware Checkpoint/Restore Runtime for Agent Sandboxes — arXiv, April 2026. Finds that more than 75% of agent turns produce no state that is relevant to recovery, so blanket checkpointing is mostly waste. A semantics-aware approach raised recovery correctness from 8% to 100% and cut checkpoint traffic by up to 87%, within 1.9% of fault-free execution time. This is the evidence behind the HB-1 guidance to checkpoint at effect boundaries — https://arxiv.org/abs/2604.28138
- Defeating Nondeterminism in LLM Inference — Thinking Machines Lab, September 2025. Traces temperature-zero nondeterminism to the batch-size dependence of reduction kernels, and demonstrates bit-identical outputs with batch-invariant kernels. Serving stacks integrated these during 2026 at a throughput cost of roughly one third. **This is the source for the corrected replay claim in §6.**

**Memory and continual learning (context for §5)**

- Memory Models: Towards Agents That Learn (Letta). Argues that memory formation through general-purpose models cannot power long-term self-improvement. Memories become generic and lossy after repeated refinement, stay overly specific rather than generalizable, and fail to adapt agent behavior consistently across sessions and across models — https://www.letta.com/blog/towards-agents-that-learn/
- Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers — arXiv, March 2026 — https://arxiv.org/abs/2603.07670
- The 2026 research direction treats store, retrieve, update, summarize, and discard as learned operations. Reinforcement learning optimizes them, rather than hand-coded rules. §5 permits that over working context and forbids it over the audit trail. The reason is stated there. A policy that optimizes for task success has an incentive to discard the records that make an act attributable.

---

**Note on intent**

This is offered as *a* model. It is not offered as *the* model. It does not claim to be the best, the most complete, or free of flaws. It claims only to be coherent, honest, and usable.

The field has no shortage of agentic frameworks. What it lacks is a *unified* one. That framework must be simple enough to follow, small enough to hold in your head, and complete enough to build from. It must also treat governance, accountability, and human judgment as load-bearing, rather than as afterthoughts. That gap is what this document sets out to fill.

Everything here is meant to be argued with. Where it is wrong, correct it. Where it is thin, deepen it. Where something better exists, let that win. A model earns its place because it is useful to the people who build real things. It does not earn its place because someone defends it.

It is published in that spirit. It is a shared starting point for a problem that we all meet at the same time. The hope is that it spares someone the work of inventing it alone.

---

> This is not only a theoretical thesis. A reference implementation sample of an Organization-Cell is at: https://github.com/MihaiCiprianChezan/Agentic-Enterprises-A

---
## Appendix A — the seven role contracts (normative baseline)

§2 declares the contract shape. This appendix instantiates that shape for every §4 role, so that the model demonstrates that its own abstraction is sufficient. An adopting cell copies these contracts and adapts them. Those adaptations are constitutional content. Fields and guarantees, as always. No schema language.

Every contract below that declares *run* as its human-takeover mode must also declare the bound under which *run* holds, per §2. That bound is cell-specific, so this baseline does not supply a number.

**Direction** *(Director)*

| Field | Contract |
|---|---|
| Responsibility | One prioritized backlog of well-specified goals. Demand becomes direction, under the constitution. |
| Inputs | Stakeholder intent and client intent, through the intake edge. The constitution and the compiled governance. Learning-loop proposals (§17). Escalations that Verification and Orchestration return. |
| Outputs | Goals with constraints, acceptance criteria, risk flags, and budget caps → Orchestration, through the Optimizer where one is inserted. |
| Authority scope | The highest operational authority within the constitution: prioritization and goal framing. May not author governance. May not move a floor. May not execute an L0 act. |
| Acceptance criteria | Goals are in-policy and prioritized. Goals are mechanically checkable where possible (§2). The Director resolves ambiguity that the Verifier returns. The Director never re-issues it unchanged. |
| Escalation rule | Out-of-purpose or novel-class demand → Board. Divergent-framing disagreement (§4.1) → Board spot-review. Anything beyond scope → §12. |
| Observability hooks | Every goal, priority change, and framing decision, each with its rationale. Intake-to-goal latency. Risk-flag rate. |
| Human-takeover mode | Run. |

**Orchestration** *(Orchestrator)*

| Field | Contract |
|---|---|
| Responsibility | Decomposition, routing, sequencing, and exception handling, for every accepted goal. |
| Inputs | Goals from Direction. Optimizer routing decisions, where one is inserted. Executor outputs and failures. Verifier verdicts. |
| Outputs | Work items that carry an action class, an autonomy level, and declared breakpoints → Executors. Retry and proceed decisions. Escalations (§12). |
| Authority scope | Routing, retry, and escalation. No goal authorship. No strategy. No criteria authorship. |
| Acceptance criteria | Every work item carries its class and its level. Dependencies are sequenced. Revision limits are enforced (§4.4). |
| Escalation rule | The revision limit is reached. No capable implementer exists (§10). Confidence falls below the threshold. Governance raises a flag. |
| Observability hooks | The full decomposition trail and routing trail. Queue depths. Retry rate and escalation rate. |
| Human-takeover mode | Suspend-and-inspect, because fan-out is high (§7). |

**Execution** *(Executor)*

| Field | Contract |
|---|---|
| Responsibility | The work product of one work item. |
| Inputs | The work item, with its criteria, class, level, and breakpoints. Its tools. Task-scoped context from the memory plane. |
| Outputs | An output with declared side effects and idempotency keys → Verification. |
| Authority scope | Within-task only. Tools are least-privileged. No criteria authorship (§2). |
| Acceptance criteria | The criteria of the work item, as issued. |
| Escalation rule | A criterion is unmeetable or ambiguous → return. Confidence falls below the threshold of the level. Any act beyond the class or the level. |
| Observability hooks | The full trajectory, mediated (§5). Cost per step. Effects-ledger entries. |
| Human-takeover mode | Run. |

**Verification** *(Verifier)*

| Field | Contract |
|---|---|
| Responsibility | The gate. Pass, return, or block, against issued criteria (§4.4). |
| Inputs | Outputs and their criteria. Governance predicates. Never criteria of its own authorship (§2). |
| Outputs | A verdict with per-criterion scores, and a cited clause on a block → Orchestration and Direction. Per-output scores → the Auditor. |
| Authority scope | Gate only. Cannot author criteria. Cannot fix outputs. |
| Acceptance criteria | Every verdict cites what it scored. An *unclear* score returns to Direction (§2). The escape rate stays within the declared bound (§14). |
| Escalation rule | An untestable or ambiguous criterion → Direction. The revision limit → §12. Suspected gaming → Steward. |
| Observability hooks | Verdicts with scores. Pass, return, and block rates. Escape-rate inputs (§14). |
| Human-takeover mode | Run. Preferred implementer: deterministic, wherever the criteria permit it (§4.4). For high-blast classes the implementer must be independent of Execution. |

**Steward**

| Field | Contract |
|---|---|
| Responsibility | The behavioral health of live role-holders and of running flows (§9). |
| Inputs | Mediated traces (§5). Auditor regression alerts. Governance breach events. |
| Outputs | Containment acts: quarantine and checkpoint rollback. Maintenance acts: retune, restart, and provisional failover. Maintenance acts on high-authority roles are L1 or two-key. Recovery operations (§14). |
| Authority scope | Technical only, on two named objects (§9). No business decisions. No Verification override. May execute a reinstatement of a danger-grade suspension, but never decide it (§11). No permanent replacement (§17). |
| Acceptance criteria | Containment happens within the declared reaction bounds. Every act names its object — flow or instance — and lands in the registry and the trail. |
| Escalation rule | A human takeover is needed. The same role is quarantined repeatedly. Any fix requires authority that the Steward lacks. |
| Observability hooks | Every act with its rationale. Time-to-containment. Drill outcomes and time-to-competent-intervention (§7). |
| Human-takeover mode | Run. |

**Optimization** *(Optimizer)*

| Field | Contract |
|---|---|
| Responsibility | Capability-to-task matching above the floor (§10). |
| Inputs | Work items with their risk class and floor. Auditor ratings. Registry status. Attributed cost (§5). |
| Outputs | Auditable routing decisions. The event history records them, and a resume consumes them (§5). |
| Authority scope | Selection only, among status-active versions above the floor. Never sets floors or classes. Escalates the empty set. |
| Acceptance criteria | No route below a floor. No route to a status that is not active. No route that violates a declared diversity constraint. Every route is recorded with its floor and with the candidates considered. |
| Escalation rule | No candidate clears the floor → §12. |
| Observability hooks | Every routing decision with its basis. Cost deltas and quality deltas that are attributable to routing. |
| Human-takeover mode | Run. |

**Audit** *(Auditor)*

| Field | Contract |
|---|---|
| Responsibility | Version fitness and safety, over accumulated activity (§11). |
| Inputs | Verifier scores. Mediated traces. Incidents. The version registry. |
| Outputs | Ratings and leaderboards → Optimizer. Regression alerts → Steward. Suspensions, as governance predicates, and escalations → humans. Proposed amendments (§17). |
| Authority scope | Monitor and report. Unilateral danger-grade suspend. May not modify, dismiss, reinstate, or decide business matters. |
| Acceptance criteria | Ratings are reproducible from the event history. Every suspension carries its SLA. A version below the evidence bar is rated *unproven*, and danger detection is exempt (§11). |
| Escalation rule | Every suspension escalates. A missed SLA climbs the Office ladder, then reaches break-glass, then reaches safe mode (§11). |
| Observability hooks | Ratings with their evidence basis. The suspension record and the false-positive record. SLA outcomes. |
| Human-takeover mode | Run. |

## Appendix B — a minimal handoff vocabulary (informative, proven in one cell)

The spec names the roles. These are the objects that the roles pass to one another. This is the smallest set that carries a cell end to end, and the reference implementation proved it. Fields and guarantees. Serialization-agnostic.

| Object | Producer → Consumer | Load-bearing fields | Guarantee |
|---|---|---|---|
| **Ticket** | intake edge → Direction | source, request, arrival time | Nothing enters the cell except as a Ticket. The intake edge is observable. |
| **Goal** | Direction → Orchestration | objective, constraints, acceptance criteria, risk flags, budget cap, priority | No work exists without an issuing Goal. The issuer authors the criteria per §2. |
| **WorkItem** | Orchestration → Execution | goal link, task, action class, autonomy level, declared breakpoints, assigned implementer and version | No act happens without a class and a level. |
| **Output** | Execution → Verification | artifacts, declared side effects with idempotency keys, cost | Every side effect is in the effects ledger before it fires (HB-2). |
| **Verdict** | Verification → Orchestration and Direction | pass, return, or block. Per-criterion scores. A cited clause on a block | Nothing takes effect without a Verdict. |
| **ActorRef** | on every recorded act | role, version, mode (agent \| human \| program), principal (the authenticated identity behind the act — the named human whenever mode = human), office (when the human acts in Board capacity) | No anonymous acts. The record holds identity and capacity per act (§5, HB-3). |

## Appendix C — conformance: profiles and checklist

**Profiles.** An organization claims exactly one profile, or none:

- **Minimal Viable Cell** — §15 steps 1 to 7 are complete. All eleven invariants hold. System roles are absent only where their preconditions do not exist (INV-8, §9 to §11).
- **Full Cell** — a Minimal Viable Cell, plus the Steward, the Optimizer, and the Auditor wherever their preconditions exist, plus the declared assurance floor and ceiling (§17).
- **Federated** — a Full Cell, plus §16: ratified treaties, identity assurance at boundaries, the inbound-untrusted posture, and agreed rules for cell lifecycle and attestation.

An organization between steps is **in transition, not conformant**. That is a legitimate state with a name, provided that the organization lists the invariants that do not yet hold rather than implies them. To claim the vocabulary without the guarantees is agent-washing (§14).

**Checklist.** One row per load-bearing requirement. The evidence column says what an auditor looks at.

| # | Requirement | Evidence |
|---|---|---|
| C1 | INV-1: no component conditions on the kind of implementer. The sole exception is a declared gate-power (§17) | contract and code review |
| C2 | INV-2 and §2: every role contract declares the seven fields plus its human-takeover mode. A *run* mode also declares the bound under which it holds, and the Steward monitors that bound | contract inventory against Appendix A, plus the Steward signal |
| C3 | INV-3 and HB-3: an authorized human can pause, examine, inject into, and continue any live flow, chosen at random | a recorded drill |
| C4 | HB-2: kill a flow mid-run and continue it. No effect is duplicated. No effect is skipped | kill-and-resume test over the effects ledger |
| C5 | HB-4: re-entry into a completed flow returns its recorded outcome and emits no new events | re-entry test |
| C6 | INV-5: no durable state is recoverable only from inside an actor | restore-from-planes exercise |
| C7 | §8: every action class carries a declared level, compensating actions included. The mapping only tightens the default table | action-class registry review |
| C8 | §8: at least one autonomy raise is traced end to end — telemetry, proposal, human ratification, recompile | the amendment record |
| C9 | INV-10 and §17: every compiled rule traces to a ratified clause. The last amendment was attested diff-scoped | pipeline audit |
| C10 | §17: the translator and the attester are different, on the record. The compiled artifact is integrity-verified at load, and a rule whose source-clause hash no longer matches the ratified text is refused | deployment record and a stale-rule load test |
| C11 | §5: the registry holds identity with the model snapshot, lineage, status with probationary, and a per-act ActorRef with principal, mode, and office. Human-held acts name the human | event-history sample |
| C12 | §5: capture is mediated. For an authority-relevant signal, the measured role cannot write its source | signal-path review |
| C13 | §5: provenance. An untrusted-derived span stays labeled through summarization and through resume | injection-provenance test |
| C14 | §4.4: the revision limit is declared and enforced. Verdicts are pass, return, or block, with citations | verifier records |
| C15 | §14: the Verifier escape rate is tracked. A sampled human re-audit of passed outputs is on record | audit sample |
| C16 | §11: for the last suspension, or for a drill — the predicate blocked dispatch, the SLA opened, a human decision preceded reinstatement, and the Steward executed it | the suspension trail |
| C17 | §10 and §11: a suspended or rolled-back version is ineligible for routing before the next dispatch | event-ordering check |
| C18 | §12: the escalation roster and the SLA are declared per role. One missed-SLA path was exercised to its terminal state | drill record |
| C19 | §7: takeover drills are on record per critical role. Time-to-competent-intervention is reported | drill records and Board minutes |
| C20 | §3: the last alignment review consumed at least one evidence channel that the cell cannot shape | review minutes |
| C21 | §16: Board-acts and Role-acts are on separate audit trails | trail inspection |
| C22 | §17: the break-glass roster is pre-declared. The grant carries its expiry, and the pre-effect check enforces it. No scheduled process is load-bearing for the lapse | drill showing an expired grant refused at the action site |
| C23 | §5: classifications are present. Plane-read scopes are enforced. Retention and erasure are declared. Erasure preserves the integrity chain | sample erasure |
| C24 | §14: plane-outage postures are declared — fail-closed governance, autonomy degradation, recovery point | configuration and drill |
| C25 | §15: pilot kill criteria were declared before launch, and the pilot was measured against them | the pilot record |
| C26 | §17: the assurance floor and ceiling are declared. Measured overhead is reported | cost attribution query |
| C27 | §5: where a learned memory policy operates, the constitution declares which stores it may write to, and that set excludes every tamper-evident store | policy configuration and store scopes |
| C28 | §6: the replay posture is declared — whether bit-exact re-execution is available for each implementer class, and the model snapshot is pinned where it is not | registry entry and replay drill |
| C29 | §17: traceability runs in both directions. Every ratified clause carries a recorded disposition — a compiled rule, or an attested purposive classification — and no clause is undisposed | the clause-disposition register |
| C30 | §14: a racing second writer to one flow is refused at the append, not only prevented by a lock | concurrent-writer test against the event store |
| C31 | *Federated only*, §16: both Boards ratified the treaties. Treaties declare the vocabulary of every exchanged term, and an undefined term escalates. Inbound treaty content is treated as untrusted. The cell-lifecycle outcome is agreed | treaty records |
| C32 | *Federated only*, §14 and §16: boundary identity chains to a root outside the Director and names the seat, not the build. The treaty-suspension breaker was exercised — a declared signal suspended the treaty unilaterally, the plane stopped in-flight exchanges, and both Boards re-ratified before resumption | identity chain plus a suspension drill |

## Appendix D — glossary (informative)

Each term links to its defining section. The definition there is the normative one.

- **Cell** — one self-contained, sovereign instance of the whole model (§16).
- **Plane** — shared infrastructure that every role runs inside: governance, memory and context, observability, and control (§5).
- **Handbrake** — the control plane. Pause, inspect, inject, resume, and replay, on any flow (§6).
- **Office / Role** — a human-world accountability title, against an operational seat in the agentic organization. They are not one-to-one (INV-9, §3).
- **Implementer** — whoever satisfies a role contract: an agent, a human, or a deterministic program (§2).
- **Human-takeover mode** — the declared mode of a contract: *run* or *suspend-and-inspect* (§2, §7).
- **Gate-power** — a narrow human power that the constitution grants directly: an L1 approval, an L0 execution, or a break-glass act (§17).
- **Two-channel rule** — humans reach the organization only through the constitution, including its gate-powers, or through Role impersonation (INV-9).
- **Impersonation-binding rule** — a human in a Role seat holds the authority of the Role, never the authority of their Office (§3).
- **Blast radius** — reach against reversibility. The worse axis wins. In doubt, round up (§8).
- **Action class / autonomy level** — the governed unit of risk, and its declared level L0 to L3 (§8).
- **Version** — the whole behavioral bundle: logic, prompts, weights, configuration, and the pinned model snapshot (§5).
- **Variant** — a tracked derivation of a version. Every human takeover opens one (§5, §12).
- **Probationary** — the registry status of a new version, until it earns *active* under the evidence rule (§5, §11).
- **Decision trail** — the *why* behind each recorded act. This is what a takeover inherits (§5).
- **Disposition** — what the compilation pipeline did with one ratified clause: it produced a rule, or it classified the clause as purposive. Every clause has one, and the disposition register records them all (§17).
- **Effects ledger** — the record that makes a retry safe: attempted, completed, or failed, per idempotency key (HB-2).
- **Mediated capture** — a trace that the runtime records at the tool-call boundary, rather than one that the measured role emits about itself (§5).
- **Safe mode** — the degraded state that the constitution declares, for when an escalation finds no human (§11, §12).
- **Break-glass** — the bounded, auto-expiring emergency power of pre-declared Office-holders (§17).
- **Supra-constitution** — optional shared law above enrolled cells. It is supreme only where it speaks (§16).
- **Treaty** — a standing inter-cell contract. Both Boards ratify it. Director and Director execute it (§16).
- **Boundary law** — a cell is reachable only through its constitution or through an authorized Role (INV-11, §16).
- **Shadow operation** — the failure mode of the Board: turn-by-turn interference instead of levers (§3).
- **Kill criteria** — the falsifiable thresholds that a pilot must beat, or be wound down by (§15).

---

## License and versioning

© Mihai-Ciprian Chezan. Licensed under [CC BY 4.0](LICENSE). Share and adapt freely, with attribution. Version history: [CHANGELOG.md](CHANGELOG.md).

**Versioning policy (semantic, for a spec):**

- **Major** — a change to any invariant, or to the meaning of a normative requirement. What a conforming implementation must do changes.
- **Minor** — new normative content that does not alter existing requirements.
- **Patch** — editorial.

Dates use ISO 8601. Every changelog entry states what moved and why.
