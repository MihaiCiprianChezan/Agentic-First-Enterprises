# The Agent-Native Enterprise — narrative summary

A companion to the specification in [README.md](README.md). This document is informative, not
normative. Where this summary and the spec diverge, the spec governs. Two versions follow: twenty
lines, then two pages.

---

## At a glance

Most companies attach AI agents to an organization that was built for humans. This model inverts
that. The organization is built for agents that run at machine speed, and it places humans
exactly where human judgment and accountability have no substitute.

Two founding ideas carry everything. First, a **role is a contract, not a person**. An agent, a
human, or a plain program can fill the same seat, and each one can replace the others. Second,
every flow carries a **handbrake**. Any authorized human can pause a flow, examine what happened
and why, inject a correction, and continue from that exact point. Interruptibility is the
architecture. It is not a feature.

Humans move to the top, into a **Board**. The Board can be a hundred people or a single founder.
It writes the **constitution**: the purpose and the boundaries of the organization. A pipeline
compiles that constitution into machine-readable rules, and every agent checks those rules before
every action. Agents never author their own rules. A human who steps into an operational seat
inherits the authority of the seat, never the authority of their title. The law binds everyone,
including its author.

Four operating roles run the value chain: Direction, Orchestration, Execution, and Verification.
Three system roles keep the machine honest. A **Steward** repairs. An **Optimizer** matches
capability to task. An **Auditor** rates versions and can stop a dangerous one, but can never
quietly restart it. To un-pause is a human act.

Risk is graduated by **blast radius**. Routine reversible work runs fully autonomous. An
irreversible outward-facing act requires a human. Autonomy is earned through evidence and
ratified by humans. It is never self-granted.

The whole unit is a **cell** — a startup, or one team inside an enterprise — sovereign at its
boundary. Cells federate through treaties between Boards. They never reach into one another. The
model also names what it cannot prevent: a corrupted Board, a compromised store, and prompt
injection. It contains those risks instead of denying them.

In one line: humans hold the Offices and write the law, agents fill the Roles and do the work, and
anything can be stopped, corrected by hand, and continued — under a law that binds everyone.

---

## The two-page version

**The problem it starts from.** Every company that experiments with AI agents today does roughly
the same thing. It takes an organization built for humans and attaches agents to it. The org
chart, the approval chains, and the meetings all assume people, and the agents are squeezed in
around the edges. This model asks the opposite question. What would an organization look like if
someone built it for agents *first*, at machine speed by default, while it kept humans exactly
where humans have no substitute?

**The two ideas that everything else grows from.** The first idea is that a **role is a contract,
not a person**. Director, Executor, and Reviewer are each defined by four things: what the role
consumes, what it produces, what it may decide, and when it must escalate. Whether an AI agent, a
human, or a plain deterministic program fulfills that contract is an implementation detail. The
rest of the system never sees it.

That is what makes the second idea possible. **Any human can step into any role at any moment.**
Every flow in the organization is built with a *handbrake*, with no exceptions. A human can pause
a flow in mid-flight, examine exactly what has happened and why, inject a correction, and continue
from that precise point. Not restart. Continue. Interruptibility is not a feature here. It is the
architecture.

**Where the humans go.** Humans do not disappear. They move. A small human layer sits above the
agentic organization, and the model calls it the **Board**. Those are the people who write the
*constitution* of the organization — its purpose, values, and boundaries — carry its legal
accountability, and face the world on its behalf.

The Board might be a hundred people or a single founder. A one-person company runs the identical
model.

The Board does not operate the business turn by turn. That would reinstate the human bottleneck
that the whole design exists to remove. Instead, a pipeline *compiles* its constitution into
machine-readable rules, and every agent checks those rules before every action. Human intent
becomes runtime law, and agents never write their own rules.

When a human does step into an operational seat, one elegant rule applies. They inherit the
authority of the *role*, not the authority of their own title. A CEO in the seat of the Director
can do exactly what the Director agent could do, and no more. Power flows through the
constitution. It never flows through rank.

**Who does the work.** Four operating roles form the value chain. **Direction** turns demand into
well-specified goals. **Orchestration** decomposes and routes the work. **Executors** produce it.
A **Verifier** gates every output before it takes effect.

Three system roles sit around them and keep the machine itself trustworthy. A **Steward** monitors
and repairs misbehaving agents, and it can make no business decisions. An **Optimizer** matches
each task to the cheapest implementer that is still *capable enough*, and it never trades safety
for cost. An **Auditor** rates agent *versions* against each other continuously, and it can stop a
dangerous release.

The checks and balances are deliberate. The Auditor can suspend, but it can never un-suspend. Only
a human decision can lift a danger-grade stop. Nothing in the system can quietly grant itself more
power.

**How risk is handled.** Not everything that an agent does carries the same stakes. Every class of
action therefore gets an autonomy level based on its *blast radius* — who is affected, and whether
the act can be undone. Routine reversible work runs fully autonomously. Anything irreversible that
faces the outside world requires a human to act.

Autonomy is *earned*. Evidence of good performance lets a human ratify a promotion. The agent
never ratifies its own. The result appears in the worked examples of the spec. The everyday path
runs fast with no human in sight. The machinery becomes visible only at the moment when something
is genuinely risky or goes wrong.

**The bigger picture.** The whole unit is a **cell**: one complete, sovereign instance of the
model. A cell can be an entire startup, or one bounded team inside a large enterprise, staffed
part-time by existing people.

Cells federate the way that countries do. They negotiate treaties between their Boards, with an
optional shared supra-constitution above them, and no cell ever reaches inside another.

The design is also honest about its limits. It names outright what it *cannot* protect against: a
corrupted Board, a compromised data store, and the fact that no current AI reliably resists prompt
injection. It contains those risks rather than pretends to prevent them.

**What the current version adds.** Version 3.0.0 put the spec through a fact-check against primary
sources and refreshed its evidence base to the September 2026 state of the art. Three things
changed that a reader of the previous version should know about.

One claim was simply wrong and is now corrected. The spec used to assert that you cannot reproduce
an LLM step. Published work has since traced that nondeterminism to a specific cause and removed
it, at a measured cost in throughput. Bit-exact replay is now an engineering choice where you
control the serving stack, rather than an impossibility. One citation pointed at the wrong paper
and now points at the right one. The EU AI Act timeline moved in July 2026, and the spec now says
plainly that the deadline moved while the substance of the human-oversight requirement did not.

The evidence base also grew sharper. The strongest empirical result of 2026 says the same thing
that this document has argued from the start: the same model, unchanged, performs radically
differently depending on the system built around it. A frontier-lab containment failure in July
2026 provided the field's clearest case study, and its diagnosis was organizational rather than
architectural — which is exactly the class of failure this model is built to catch.

Finally, the whole document is re-authored in controlled English, in the style of ASD-STE100
Simplified Technical English. The goal is one reading per sentence. An implementer — or an agent —
must be able to parse a normative requirement without an author to ask.

**The one-sentence version.** Humans hold the Offices and write the law. Agents fill the Roles and
do the work. Everything that the organization does can be stopped, corrected by hand, and
continued. And the law binds everyone, including the human who wrote it, the moment that they step
inside.

---

© Mihai-Ciprian Chezan. Licensed under [CC BY 4.0](LICENSE), like the specification it summarizes.
