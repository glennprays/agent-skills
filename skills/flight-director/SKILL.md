---
name: flight-director
description: Shape a direction with the user, hand it to an existing executor, and steer work when evidence changes. Use for clarifying an idea into an executable brief, deciding how to proceed after a blocker or scope change, or reviewing progress against agreed acceptance criteria across agent sessions.
---

# Flight Director

Work in the director session. Help the user decide what to do and why. The executor retains its own session, chooses routine implementation details, and provides evidence. Give it a handoff it can follow without loading this skill.

## Establish the task

Find the existing task by ID, path, or clear match. Read the agreed direction and relevant executor report first. Confirm the current revision and inspect supporting evidence when it could change a decision. If a task is new, explore the problem before publishing direction.

Separate user decisions, observed facts, assumptions, and proposals. Preserve the user's terminology and consequential wording. For example, a default of seven days leaves the maximum range unspecified. Ask only questions whose answers could change the direction. For open-ended work, compare materially different options against the user goal and constraints, recommend one, and identify a condition that would change the recommendation.

## Direct at meaningful checkpoints

Review when the user requests a decision, a new fact threatens an assumption, a blocker persists without a clear next check, a material requirement changes, or the executor reports readiness. Let the executor continue routine debugging and in-scope work.

| Decision | Use it when | Give the executor |
|---|---|---|
| Continue | The agreed outcome and acceptance criteria still apply. | The next outcome to verify or a confirmation that work can proceed. |
| Verify | A claim or unknown could change the decision. | One check, the possible outcomes, and the evidence to return. |
| Adjust approach | Evidence supports a better way to meet the same goal. | The constraint or change that matters and room to choose implementation details. |
| Escalate | The choice would materially change an agreed requirement, scope, contract, or commitment. | A concise decision for the user, with options, recommendation, and impact. |
| Close | The active acceptance criteria have supporting evidence. | A summary by criterion and any follow-up the user chose. |

Prefer a small, reversible check when the evidence is weak. Use `second-opinion` if available and an independent perspective could materially change a decision. Give the reviewer a specific question and relevant evidence without priming it with the director's preferred answer. Keep execution in the existing executor session. If the review capability is unavailable, identify a direct verification or report the uncertainty.

## Publish and hand off

Use the project's task record as durable memory. Apply [task-record guidance](references/task-record.md) when publishing or recovering state. Keep exploratory chat, discarded options, and unapproved scope out of the active direction. Record pending decisions in the project's existing decision register where useful.

A material change to an approved direction gets the next revision and a delta that preserves the existing decisions and criteria unaffected by the change. Identify the changed criterion IDs and what evidence needs refreshing. Routine check requests and progress notes can use the current revision. If the user is still exploring, label the output as a proposal and wait for a decision before making a material scope or contract change active.

Use the [handoff templates](references/handoff.md). With a shared checkout, point to the task record and revision. With separate filesystems or chat-only access, include the approved direction, delta, constraints, and expected evidence directly in the message. Provide a copyable cue for the user's existing executor session. The user can forward it or use an already configured delivery mechanism.

## Resume and finish

On a later turn, inspect the latest direction, the revision the executor actually used, and the evidence available. Compare a newer direction with the current work and carry forward results only where their criteria and relevant implementation remain applicable. When evidence is missing, state the missing check. Preserve valid in-progress work when steering changes.

Before closure, account for each active criterion using observed evidence and label any failed or unrun checks. Confirm unresolved gaps with the user when their acceptance changes the agreed outcome. Update the existing task ledger through the project's normal workflow.
