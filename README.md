# Context State Governance

A small, memory-backend-agnostic skill for recovering **validated current state** from conflicting long-context, project-memory, and cross-session history.

## Why

Long-memory systems can remember more and still reason worse if they confuse:

- where a statement came from;
- whether its premise still holds;
- whether a user really confirmed it;
- whether a later statement was formed under a bad framing;
- whether historical evidence should still guide current execution.

The core idea is simple:

> **Remembering is not the same as knowing what is still valid.**

This project adds a governance step above memory retrieval:

`Provenance → Premise Check → Conflict Detection → Human Adjudication → Validated Baseline`

## Key Ideas

- **Validated State Wins** — not last-write-wins.
- **Provenance separation** — current chat, project memory, prior sessions, AI proposals, and user confirmations are not interchangeable.
- **Premise invalidation** — a historically confirmed decision can lose current authority without being erased.
- **Open-ended adjudication** — `1A / 1B / 1C / ...` is a low-attention protocol, not a forced multiple-choice form.
- **Natural language outranks labels** — `1A/B`, phased choices, modified options, new options, or free-form answers are all valid.
- **Three-layer evidence model**:
  - Validated Baseline — what guides current execution
  - Decision Ledger — why
  - Raw Evidence — what actually happened

## Example

A project has conflicting history:

- Earlier state: build an in-house subsystem.
- Later discovery: a mature open-source component already solves it.
- Several “continue” confirmations occurred while the assistant was still reasoning under the old framing.

The skill does **not** say “the newest answer wins.”

Instead:

**1A** — continue the in-house build.

**1B** — keep only the unique governance layer and adopt the mature component.

**1C** — pause both and re-evaluate the premise.

The user may answer:

- `1B`
- `1A/B`
- `1B for now, switch to 1A if condition X occurs`
- `none of these; my actual intent is...`

The final natural-language intent becomes authoritative.

## Files

- [`SKILL.md`](SKILL.md) — the portable English skill definition
- [`SKILL.zh-CN.md`](SKILL.zh-CN.md) — the semantically aligned Simplified Chinese skill definition
- [`README.zh-CN.md`](README.zh-CN.md) — Chinese documentation
- [`examples/adjudication.md`](examples/adjudication.md) — anonymized example

## Status

**v0.1.0** — early, deliberately small, based on a real long-context failure pattern and generalized for public use.

## License

MIT
