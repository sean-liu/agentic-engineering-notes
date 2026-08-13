---
title: "From Reusable Skills to Durable Capabilities: A Git-Backed Distribution Layer for My Agent Projects"
published_at: 2026-08-13
platform: LinkedIn
status: published
source_url: https://www.linkedin.com/pulse/from-reusable-skills-durable-capabilities-git-backed-distribution-4shfc/
---

# From Reusable Skills to Durable Capabilities: A Git-Backed Distribution Layer for My Agent Projects

While publishing a reusable repository-delivery Skill across my own agent projects this week, I realized that I had quietly built something broader than the Skill itself.

I had built a small distribution and governance layer for reusable agent capabilities.

This was not something I set out to design.

It emerged from dogfooding.

And that distinction matters.

## The problem did not start as “skill sharing”

I use several long-lived ChatGPT and Codex environments for different kinds of work.

Over time, some workflows became reusable across projects:

- specification-driven development;
- repository delivery;
- artifact synthesis;
- project governance;
- other recurring agent workflows.

The naive solution is straightforward:

> Copy the reusable instructions into every project that needs them.

That works until the first meaningful change.

Then several questions appear:

- Which copy is canonical?
- Which project has the newest version?
- If one project improves the workflow, should the others inherit it?
- How do I distinguish a source artifact from a runtime-installed copy?
- How do I know that a project is actually using the version I think it is?
- If the capability evolves, what owns the authority to change it?
- How do I avoid silently creating several slightly different “canonical” versions?

At that point, the problem is no longer prompt reuse.

It becomes a state, authority, distribution, and verification problem.

## The architecture that emerged

I ended up separating the system into several layers.

*Figure 1. Simplified capability distribution architecture. A Git-backed canonical capability is explicitly delegated by project bootstraps, projected into execution runtimes, and independently verified.*

The important decision was that a consuming project should reference the reusable capability rather than own another copy of it.

The project keeps the authority that is actually project-specific.

The Skill keeps the reusable workflow semantics.

The two should not silently absorb each other.

## A concrete example: Repository Delivery

The first capability that made this architecture obvious was a Skill I call repository-delivery.

Its job is to take one bounded repository change from recovered context through:

- semantic routing;
- implementation readiness;
- authorized execution;
- proportionate validation;
- bounded repair;
- optional review-artifact stabilization;
- final handoff.

It can route work through several paths depending on the unresolved decision state:

- DIRECT
- CHECKPOINTED
- PROGRESSIVE SDD
- RECOVERY

The important part for this article is not the internal workflow.

It is what happened when I promoted it from a project-specific design into a reusable capability.

Instead of copying the Skill into every project that needed repository delivery, I promoted one canonical source and changed the consuming project to delegate to it.

Conceptually:

```text
project-specific repository policy
            │
            │ delegates reusable mechanics
            ▼
    canonical repository-delivery Skill
```

The project still owns its own:

- authorization;
- risk policy;
- repository-specific rules;
- merge/release behavior;
- project authority.

The shared Skill owns the reusable delivery orchestration.

That boundary turned out to be more important than the file-sharing mechanism itself.

## “Published” turned out to be an overloaded word

The next problem appeared immediately.

If a Skill exists in Git, is it available?

Not necessarily.

If a project points to it, is it installed in every runtime?

Not necessarily.

If it has been copied into a runtime directory, do I know that the target runtime can actually discover and use it?

Again, not necessarily.

So I stopped treating “published” as a single state.

I now distinguish four states:

### 1. Canonical

The authoritative Skill source exists in the durable source repository.

This answers:

> Where does this capability actually live?

### 2. Project-linked

A project or bootstrap explicitly delegates to the canonical capability.

This answers:

> Does this project know which source owns the reusable behavior?

### 3. Runtime-available

The capability has been projected into a runtime that can use it.

This answers:

> Can this execution environment actually reach the capability?

### 4. Verified

Current evidence confirms that the intended runtime projection is present and usable.

This answers:

> Do I know that the system state matches the desired state?

*Figure 2. Capability state model. Source state, consumer state, and runtime state are related but should not be treated as equivalent.*

The distinction seems small until something fails.

Then it becomes the difference between:

> “The Skill should be there.”

and:

> “Here is the evidence that this runtime currently has the expected capability.”

That is a familiar distinction in traditional infrastructure engineering.

I did not expect to encounter it again while managing agent instructions.

## This is not a replacement for native Skills

OpenAI already has a native Skills model for reusable and shareable workflows.

This experiment is not an attempt to recreate that product layer.

My problem appeared at a different boundary:

> How do I maintain a durable, version-controlled source of truth for reusable capabilities across several long-lived personal agent projects, while preserving project authority and keeping runtime state explicit?

Git happened to be a natural source-of-truth mechanism because it already gives me:

- version history;
- diffs;
- review;
- rollback;
- provenance;
- stable paths;
- reproducible recovery.

The interesting part is not “Git can store a SKILL.md file.”

Of course it can.

The interesting part is the semantic separation between capability ownership, project delegation, runtime projection, and verification.

## Why copying instructions was the wrong abstraction

A copied instruction file looks harmless.

But copying creates another owner unless the system has an explicit model saying otherwise.

Once two copies independently evolve, several forms of drift become possible:

```text
semantic drift
authority drift
version drift
runtime drift
```

This is especially dangerous for agent workflows because much of the behavior is expressed as natural-language policy.

Two files can look nearly identical while differing in one sentence that materially changes:

- who has authority;
- when execution may start;
- what must be validated;
- whether a confirmation is required;
- which failure state is acceptable.

Text similarity is not authority equivalence.

That observation has started influencing how I think about agent infrastructure more generally.

## A reusable capability has a lifecycle

I originally thought of a Skill as an instruction artifact.

I now think that is incomplete.

A reusable agent capability has at least several distinct concerns:

```text
design
  ↓
candidate
  ↓
promotion
  ↓
canonical ownership
  ↓
distribution / projection
  ↓
runtime availability
  ↓
verification
  ↓
dogfood evidence
  ↓
revision
```

The SKILL.md file is only one artifact moving through that lifecycle.

This matters because a system can be correct at one layer and broken at another.

The canonical source can be correct while the runtime is stale.

The runtime can contain the Skill while a project still delegates to obsolete project-local instructions.

The project can reference the canonical Skill while that Skill itself has not yet been adequately validated.

Those are different failure modes and should remain distinguishable.

## What I have actually built — and what I have not

I want to be precise about the current maturity of this experiment.

Today, this is a single-user, Git-backed capability distribution and governance pattern that I use across my own agent environments.

It has real dogfood usage.

It has a canonical Skill source.

It has project-level delegation.

It has explicit runtime-state semantics.

It has already been used to move reusable repository-delivery behavior out of project-specific governance and into a shared capability.

But it is not:

- a multi-tenant Skill registry;
- a package manager;
- a large-scale synchronization service;
- a team permission system;
- an enterprise rollout mechanism;
- a production observability platform.

There is no telemetry layer.

There is no fleet-scale deployment system.

There is no claim that this architecture would survive unchanged at organizational scale.

Those are not small missing implementation details.

They are different problem regimes.

## Questions I would test next

If this pattern needs to grow, several questions become much more interesting than simply copying files faster.

### Version selection

Should every consumer automatically track the latest canonical version?

Probably not.

When should a project pin a capability version?

When should it intentionally lag?

### Compatibility

How should a capability declare the assumptions it makes about:

- tools;
- runtime;
- host authority;
- project state;
- external integrations?

### Verification

What evidence is sufficient to claim that a capability is really available in a target runtime?

File presence alone may not be enough.

### Rollout

If twenty projects consume one capability and its behavior changes materially, should promotion and rollout remain the same operation?

Probably not.

### Observability

When a reusable Skill contributes to a failure, how do I determine whether the defect belongs to:

- the Skill;
- the project policy;
- runtime projection;
- missing context;
- the model;
- or the surrounding orchestration?

### Multi-user authority

A personal Git repository gives one user a relatively simple authority model.

A team does not.

Who may publish?

Who may approve?

Who may pin?

Who may override?

Who owns a local variation?

That is where this small personal architecture would have to become something substantially different.

## The larger lesson for me

I started this work thinking mostly about agent prompts and workflows.

Dogfooding is gradually pushing me toward a different view:

> Agent capabilities are not merely prompts.

Once they are reused across long-lived systems, they begin to acquire many of the same properties as other software artifacts:

- ownership;
- versions;
- dependencies;
- distribution;
- runtime state;
- compatibility;
- provenance;
- validation;
- lifecycle.

That does not mean agent Skills should become traditional software packages.

It means that reusability creates systems problems.

And those systems problems begin to matter long before the number of users becomes large.

## Why I am publishing this early

This architecture is still evolving.

I am deliberately publishing the idea before it becomes polished enough to look inevitable.

If this turns out to be nothing more than a useful personal workaround, I would rather discover that early.

If the pattern generalizes, I want the evolution trail—including the assumptions that later turn out to be wrong—to remain visible.

For me, that is part of the experiment.

The most useful outcome of publishing this is not agreement.

It is better counterexamples.

I am especially interested in how other people building long-lived agent systems are handling:

- canonical ownership of reusable capabilities;
- version and authority drift;
- project-specific overrides;
- runtime projection;
- verification;
- and the boundary between reusable agent behavior and host-specific policy.

If you have already run into these problems, I would be very interested to compare notes.
