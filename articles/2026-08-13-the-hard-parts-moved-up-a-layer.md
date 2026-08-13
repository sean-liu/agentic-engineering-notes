# The Hard Parts of Backend Engineering Didn't Disappear in Agentic Systems — They Moved Up a Layer

For most of my career, I worked on backend and distributed systems. As I started spending more time building with coding agents, I expected the new problems to be mostly about models: prompts, context windows, tool calls, retrieval.

Some of them are. But the more I dogfood agent-assisted development, the more familiar the difficult problems look.

State becomes inconsistent. Sources disagree. Old decisions remain searchable after they have been superseded. A tool completes work that another tool cannot see. A generated artifact is locally plausible but no longer preserves the meaning of the rule it replaced.

The hard part is often not getting an agent to produce code. The hard part is getting an agent to participate in a long-running engineering system without losing properties we already know serious software needs: traceability, authority boundaries, recoverability, evaluation, and controlled change.

My current working thesis is:

> **Agentic engineering does not replace traditional software-engineering concerns. It moves many of them up into the layer that manages context, state, decisions, and change.**

This is a field note from hands-on dogfooding, not a claim that I have solved these problems generally.

## Context starts looking like state management

A real coding task may depend on the current repository, an older design discussion, a pull request, a local agent session, a rule file, a failed attempt, and a decision that was later revised.

Giving the agent more context is not enough. The questions become:

- Which source is current?
- Which source is authoritative for this question?
- Which facts are historical rather than active?
- What changed since the last run?
- What evidence is missing?

That feels closer to state reconstruction than prompt composition.

In backend systems, we do not normally load more rows and hope the newest-looking value is correct. We think about ownership, freshness, ordering, consistency, and failure modes. Agent context deserves the same discipline.

## Provenance matters when agents change durable artifacts

If an agent only answers a disposable question, a plausible response may be enough. If it updates code, a specification, a rule set, or long-lived project knowledge, plausibility is not enough.

I increasingly want to be able to ask:

- Why does this statement exist?
- Which evidence supported it?
- Was it observed or inferred?
- Did it replace an older statement?
- Was the old statement wrong, or simply superseded?

Without provenance, an agent can produce a clean final artifact while quietly destroying the history needed to judge whether the artifact is trustworthy.

## Capability is not the same as authority

A model can produce a convincing rewrite and still change the meaning of a system.

A required step can become a recommendation. An owner can silently change. A rule for one environment can expand to all environments. Temporary status can leak into long-lived policy.

This has changed how I think about agent workflows: generation, recommendation, validation, and activation are different operations.

A capable model should not automatically receive authority just because it can synthesize a good-looking artifact.

That separation is familiar from deployment systems, access control, and change management. Agentic systems need equivalent boundaries.

## Evaluation needs more than "looks good"

One pattern I am exploring is historical replay.

Take an older artifact, recover the evidence and change inputs that were available at the time, hide the actual later result, and run the newer workflow as if it were operating then.

Then compare.

The comparison is not simply "different means wrong." A difference might reveal an agent defect, missing evidence, a changed policy, or even a weakness in the historical human process.

Useful evaluation dimensions can include missed required changes, unsupported additions, changed scope or ownership, semantic weakening, temporary state leaking into durable rules, and the amount of human correction required.

I do not yet have public benchmark data that supports general performance claims. But moving from "this output seems smart" toward repeatable failure analysis already changes the quality of the engineering conversation.

## Coding failures can start upstream of the code

A bad implementation is not always primarily a coding failure.

Sometimes the agent is executing the wrong abstraction, optimizing the wrong constraint, or solving a poorly framed problem very competently.

Improving an agentic development workflow therefore cannot stop at better code generation. It also needs better ways to recover intent, expose material uncertainty, identify the actual decision being made, and choose when a human checkpoint is necessary.

The abstraction boundary matters before the implementation boundary.

## Why backend experience still transfers

I no longer think of moving into agentic engineering as leaving backend engineering behind.

Many of the instincts transfer directly:

- explicit ownership;
- state management;
- versioning;
- auditability;
- failure recovery;
- controlled mutation;
- observability;
- validation before activation;
- separating durable configuration from transient state;
- designing for systems that evolve rather than tasks that run once.

The difference is that some of these concerns now apply to the agent workflow itself.

Once a coding agent can inspect repositories, run tools, edit durable artifacts, and participate across sessions, it becomes part of the engineering control surface. That deserves systems engineering, not just prompt engineering.

## What I am exploring next

My current work focuses on reusable agent capabilities and developer workflows around:

- evidence recovery across fragmented work history;
- durable state and provenance;
- safe evolution of long-lived artifacts;
- evaluation and failure analysis;
- useful agent autonomy without silent authority transfer.

The implementations are still evolving, so I am deliberately not presenting them as a finished framework.

I would rather publish engineering lessons that survive contact with real use.

That is what this repository will contain: field notes from trying to make powerful coding models more reliable participants in long-running software engineering work.
