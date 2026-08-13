# Agent Instructions

This repository is a **public publication surface** for Sean's agentic-engineering notes.

Everything committed here must be safe to expose publicly. Do not use this repository as a drafting scratchpad for private material.

## Purpose

Publish concise, technically substantive field notes derived from hands-on work with coding agents, reusable agent capabilities, durable state, evaluation, and developer workflows.

The repository exists to make engineering reasoning externally legible. It is not a mirror of Sean's private architecture, private history, internal project state, or confidential work.

## Publication authority

New public content requires explicit publication intent from Sean before merge to `main`.

Examples of sufficient intent include:

- "publish this";
- "发布" / "发出去";
- an explicit instruction to add a named article to this public repository;
- another unambiguous instruction that the specific outward-facing artifact should become public.

Discussion, drafting, review, or a suggestion that something could become an article does not by itself authorize publication.

Repository-maintenance changes may be prepared through the normal repository-delivery workflow, but content publication remains a separate explicit gate.

## Source material

Useful source material may originate in private conversations or repositories such as career/advisor discussions, Sean with Kai, Agentic Systems Lab, RCA, project repositories, local coding-agent sessions, or other authorized evidence.

Private-source eligibility does **not** imply copy permission. Public writing must be a curated derivative.

Before publishing, perform a disclosure review and remove or generalize material that would expose:

- credentials, tokens, private URLs, local-machine secrets, or account details;
- employer, client, collaborator, or friend-company confidential information;
- private repository contents or private conversation text that was not explicitly selected for publication;
- internal prompts, Project Instructions, Rulebooks, Skills, or operating instructions in reproducible detail;
- core private system topology or implementation mechanics whose disclosure would make the internal system readily reproducible;
- unpublished datasets, private eval corpora, sensitive traces, or proprietary examples;
- unnecessary personal information.

Prefer describing the engineering problem, observed failure mode, design principle, trade-off, experiment, or result rather than exposing the full internal recipe.

## Claim discipline

Public notes must distinguish among:

- observed behavior;
- interpretation or hypothesis;
- implemented mechanism;
- validated result;
- planned work.

Do not present architecture ideas as shipped systems, self-dogfooding as external adoption, anecdotal success as a benchmark, or an internal experiment as a general result.

When evidence is incomplete, narrow the claim rather than polishing uncertainty away.

## Article style

Prefer field-note quality over marketing language.

A strong article normally has:

1. a concrete engineering problem or observation;
2. a clear thesis;
3. evidence from hands-on use or an explicitly labeled hypothesis;
4. engineering implications and trade-offs;
5. current limits / what remains unproven;
6. useful next questions.

Write in natural English unless Sean explicitly chooses another language for a publication.

Avoid recruiter-targeted keyword stuffing. External career signal should come from the quality and specificity of the engineering reasoning itself.

## Repository structure

- `README.md` — public purpose and article index;
- `articles/` — published outward-facing articles.

Do not add a public `drafts/` directory containing material that has not passed disclosure review. Keep sensitive or exploratory drafting in the natural private workspace and move only the reviewed outward-facing artifact here.

## Delivery workflow

Use the current repository-delivery / RCA engineering workflow for repository changes: inspect current state, work on a branch, validate the complete diff, open a PR, self-review, and respect the publication gate above.

Before merging a publication PR, review the **entire final rendered Markdown source** for accidental disclosure, misleading maturity claims, broken links, and copy/paste artifacts.
