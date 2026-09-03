---
name: context-state-governance
description: Resolve conflicting long-context, project-memory, and cross-session state by separating provenance, checking invalidated premises, escalating material conflicts to open-ended human adjudication, and producing a Validated Baseline plus Decision Ledger. Never use last-write-wins for human intent.
license: MIT
metadata:
  version: 0.1.0
---

# Context State Governance

## Purpose

Use this skill when current conversation, project memory, prior conversations, AI proposals, repeated confirmations, or historical decisions may conflict.

This is **not** a summarization skill and **not** a last-write-wins resolver.

Core rule:

> History is evidence. Current state is valid only after provenance, premises, goals, conflicts, and authority are checked.

## Trigger Conditions

Use when one or more of these are true:

- a long-running conversation crosses major stages;
- a new session must recover the real state of earlier work;
- project/workspace memory appears to influence the current session unexpectedly;
- the AI says “you previously confirmed...” and the user disputes or doubts it;
- multiple incompatible confirmations or decisions exist;
- a conclusion may have been accepted under an incorrect or incomplete premise;
- the user says they may have been led into a mistaken framing;
- the current plan repeatedly drifts back toward an abandoned route;
- a major implementation step is about to begin and current intent needs validation;
- the user explicitly asks to recover intent, inspect conflicts, or create a validated baseline.

Conversation length alone is not enough to trigger this skill.

## Provenance Classes

Keep these sources distinct:

1. Current Conversation
2. Project / Workspace Memory
3. Prior Conversation
4. Uploaded / External Source
5. System / Runtime State
6. Assistant Proposal / Analysis
7. Model Inference
8. User Explicit Statement / Confirmation

If an item is attributed to the wrong source, flag:

`SOURCE_ATTRIBUTION_CONFLICT`

Do not silently repair the attribution and continue.

## Extract Decision-Relevant Statements

Classify important statements as one or more of:

- fact
- user experience
- user preference
- user goal
- user value / principle
- assistant proposal
- exploratory hypothesis
- engineering decision
- governance decision
- confirmed user intent
- system/runtime finding
- future possibility
- rejected / superseded direction
- unresolved question

Retain when available:

- provenance;
- approximate order/time;
- who originated it;
- whether the user accepted, modified, rejected, or merely continued;
- supporting premises;
- scope;
- later challenges or revisions.

## Formation Path

For important decisions, preserve a compact path when evidence exists:

`trigger → information/proposal → challenge → user reflection → confirmation/modification → later revision`

Do not rewrite an assistant-originated phrase as user-originated merely because the user later accepted it.

## Premise Validation

A prior confirmation may lose current authority when its supporting premise collapses.

Check:

- Was the option set incomplete?
- Was a material fact missing or wrong?
- Did the user later identify the framing itself as mistaken?
- Did the assistant steer toward a route later rejected?
- Did the implementation conflict with a higher-level user goal?
- Was the confirmation merely procedural (“continue”, “okay”)?
- Did new evidence materially change the choice?

Keep historical confirmation separate from current validity:

- `historically_confirmed = true`
- `currently_validated = true | false | uncertain`

## Conflict Detection

Escalate only material conflicts that can change:

- current goals;
- implementation route;
- governance;
- permissions;
- resource policy;
- identity/ownership;
- data handling;
- user-facing behavior;
- long-term decisions.

Useful conflict types:

- `GOAL_CONFLICT`
- `IMPLEMENTATION_CONFLICT`
- `PREMISE_INVALIDATION`
- `AUTHORITY_CONFLICT`
- `IDENTITY_CONFLICT`
- `PROVENANCE_CONFLICT`
- `SCOPE_CONFLICT`
- `STATE_CONFLICT`
- `VALUE_CONFLICT`
- `RESOURCE_POLICY_CONFLICT`

Do not manufacture conflicts from harmless wording differences.

## Human Adjudication Protocol

When a material conflict cannot be resolved by evidence and established authority, present it for human adjudication.

### Number + Letter Format

Use compact identifiers:

- `1A`, `1B`, `1C`
- `2A`, `2B`
- and `D/E/F/...` when needed.

There is no fixed number of options.

Each option should be:

- materially distinct;
- written in plain language;
- comparable at the same level;
- non-leading;
- grounded in evidence.

### Not a Forced Multiple-Choice Form

The number + letter format is a **low-attention adjudication protocol**, not a single-choice constraint.

The user may:

- reply `confirm 1A`;
- combine choices, such as `1A/B`;
- modify an option: `1A, but add...`;
- choose different options for different phases;
- say several choices are partly correct;
- reject all offered options;
- request a new `1D` / `1E`;
- answer entirely in natural language.

Priority rule:

> **The user's natural-language intent outranks the letter label.**

If the user says:

`1A for now; switch to 1B when condition X is met`

do not store only `1A`. Store the phased decision and transition condition.

## Authority Rules

Use evidence to resolve factual conflicts where possible.

Use the human's authority to resolve:

- personal goals;
- personal values;
- personal cognition;
- major resource choices;
- important permissions;
- contested current intent.

AI may detect and explain conflicts, but must not invent the user's final intent.

## Validated State Rule

Never use:

- Last Write Wins
- Newest Confirmation Wins
- Old Formal Decision Wins

Use:

> **Validated State Wins**

Validate using the strongest combination of:

- correct provenance;
- surviving premises;
- current goals;
- evidence;
- formation path;
- explicit human adjudication;
- later counter-evidence;
- authority boundaries.

Recency can challenge an older state, but recency alone is not authority.

## Outputs

### A. Validated Baseline

Short and operational:

- Current Goal
- Validated Principles
- Current Decisions
- Current Scope
- Non-Goals / Prohibited Directions
- Authority Boundaries
- Resource / Cost Rules when relevant
- Validated Technical Choices when relevant
- Open Questions
- Explicitly Superseded / Invalidated Directions
- Provenance note

Downstream agents should use this by default instead of re-interpreting the full history every time.

### B. Decision Ledger

Audit-oriented:

- ID
- topic
- original states
- provenance
- premises
- conflict detected
- adjudication options
- human adjudication
- natural-language qualifiers
- current validity
- supersedes / superseded_by
- reason for change
- evidence pointers where available

### C. Raw Evidence

Do not replace raw conversations or source files.

Preferred hierarchy:

`Validated Baseline → Decision Ledger → Raw Evidence`

- Baseline prevents drift.
- Ledger prevents reinterpretation.
- Raw evidence preserves history.

## Presentation Rules

Minimize human attention cost.

Default order:

1. Material conflicts requiring human judgment.
2. What is already validated.
3. Evidence details only when needed.

Do not repeatedly ask for confirmation of already adjudicated items unless new evidence re-opens them.

## Execution Guard

Before producing a new implementation plan in a long-running project, check:

1. What is the current validated goal?
2. What directions are explicit non-goals?
3. Which historical decisions lost current authority?
4. Does the new plan match the Validated Baseline?
5. Is there already a validated mature solution for this capability?

If the plan violates a validated constraint, surface the conflict instead of silently returning to an older path.

## Verification Checklist

A successful run should satisfy:

- [ ] Current conversation and project/history provenance were not conflated.
- [ ] Assistant proposals were not rewritten as user-originated views.
- [ ] Later statements were not assumed correct merely because they were later.
- [ ] Premise-invalidated decisions remain traceable.
- [ ] Only material conflicts were escalated.
- [ ] Human adjudication accepted combinations, modifications, new options, or natural language.
- [ ] Natural-language intent was preserved over compact labels.
- [ ] A concise Validated Baseline was produced.
- [ ] A Decision Ledger was produced or updated.
- [ ] Raw evidence remained available.
- [ ] Previously adjudicated issues were not re-opened without new evidence.

## Design Boundary

This skill governs **context and decision-state recovery**.

It is:

- small;
- independent;
- memory-backend agnostic;
- compatible in principle with project memory, agent memory, long-session memory, or future systems;
- not tied to any private cognitive-system implementation.
