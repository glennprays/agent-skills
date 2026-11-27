# Case record template

Copy this template into the consumer project's review notes. Fill sections as needed. Keep the top section current and append round summaries in order. Use evidence pointers and small redacted excerpts so a future executor can re-open sources.

```markdown
# <case-id> — <short title>

- Objective and expected behavior
- Scope, constraints, and owner
- Persistence — <path of this record and any evidence snapshots it references>
- Current baseline and evidence pointers
- Next concrete action

## Findings

| ID | Claim and evidence | Disposition and rationale | Lifecycle on current baseline | Next action / owner |
|---|---|---|---|---|
| F-01 | <observable failure and reference> | <accepted, needs verification, or rejected> | <open, awaiting verification, verified, or needs recheck> | <action> |

## Executor notes

Record interpretations, considered fixes, and decisions. Use this section for executor synthesis and targeted follow-up only. Never copy this section into an independent reviewer brief.

## Rounds

### R<n> — <date> — <mode: independent analysis | verification | independent reassessment | targeted follow-up | self-review>

- Baseline — <repo/revision; staged, unstaged, and untracked inputs relevant to the claim; fingerprint or snapshot id when comparison matters; environment, config, feature flags, fixture, time window>
- Reviewer — <label | agent/source/model | tool boundary | actual isolation and exposure | brief reference | result reference>
- Question and brief — <text or stable local pointer; independent briefs must not include executor notes, prior conclusions, hypothesis, desired answer, or proposed fix>
- Result — <conclusion, evidence references, affected F-NN IDs, unknowns, contrary evidence>
- Change — <actual change or none pending>, <revision / diff / reference>
- Verification — <criterion | runtime|static|other | pass|fail|not run | output reference | tested baseline>
- Decision and next step — <dispositions set, what the executor does next, and the owner>
```

## Disposition and lifecycle transitions

Apply this table; do not improvise transitions.

| Event | Disposition | Lifecycle |
|---|---|---|
| New claim lacks conclusive evidence | needs verification | open |
| Evidence supports an actionable issue, no fix applied | accepted | open |
| Requested fix recorded | accepted | awaiting verification |
| All relevant acceptance criteria pass on the recorded baseline | accepted | verified |
| A required verification fails | accepted | open |
| Relevant implementation, dependency, configuration, fixture, or flag changes | preserve prior disposition | needs recheck |
| A completed check disproves the claim | rejected | verified |

An unrelated change retains prior evidence only after the executor records why it cannot affect the tested path. A lifecycle value is always attached to the baseline it was tested on; earlier verified rounds stay attached to their own baselines when the current baseline moves to `needs recheck`.
