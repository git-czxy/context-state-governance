# Open-ended Human Adjudication Example

## Scenario

A long-running project contains conflicting historical decisions.

- The assistant previously recommended building a custom subsystem.
- The user gave several procedural confirmations such as “continue”.
- Later, a mature external component was discovered.
- The user then states that avoiding unnecessary custom infrastructure is a higher-level goal.

A naive memory system may choose:

- the newest message;
- the most frequently repeated decision;
- the most formally worded confirmation.

This skill does none of those automatically.

## Conflict

**1A — Keep the custom subsystem**

Continue the existing implementation because it has already been started.

**1B — Adopt the mature external component**

Keep only the project's unique governance logic and reuse the mature infrastructure.

**1C — Pause and re-check the premise**

Do not choose yet; first verify whether the external component actually covers the required capability.

## Valid Human Responses

`1B`

`1A/B`

`1B for the current phase; reconsider 1A only if the external component fails requirement X`

`1A and 1C are both partly correct; my actual intent is...`

`None of these. Add 1D: ...`

## Resolution Rule

The structured label is a convenience.

The authoritative result is the user's full natural-language intent.

The Decision Ledger should preserve:

- the earlier historical decision;
- why it was once accepted;
- what premise changed;
- the adjudication options;
- the user's final intent;
- the resulting Validated State.
