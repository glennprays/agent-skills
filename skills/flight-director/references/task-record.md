# Task record and revision guidance

Use the project's existing task and decision conventions. In repos initialized through `agent-ready-repo`:

| Location | Authority |
|---|---|
| `.agent/TASKS.md` | Lifecycle status and a pointer to task details. Keep its acceptance summary or pointer consistent with the project's conventions. |
| `.agent/tasks/<ID>.md` | Active direction, acceptance criteria, revision changes, and append-only execution evidence. Extend the existing task detail in place when needed. |
| `docs/decisions/OPEN_DECISIONS.md` | Material unresolved decisions. Link the entry from the task and use the established ADR process when appropriate. |
| `.agent/SESSION_HANDOFF.md` | Latest session summary. Link to the task for durable direction and evidence. |

Use the existing record elsewhere. If there is no repository convention, use one agreed task note or help the user keep the current handoff in whichever session can persist it. A chat-only director should output proposed edits and the portable handoff for the user to forward. Mark persistence as pending until the edit actually lands.

## Suggested additions to the existing task detail

Keep the template's objective, criteria, and evidence headings. Add a revision field and a concise change log where appropriate. Assign stable criterion IDs once the work needs them.

~~~markdown
## Objective
<approved outcome and scope>

Direction revision — r2

## Acceptance criteria
- AC-01 — <observable expected behavior>
- AC-02 — <observable expected behavior>

## Direction changes
- r2 — AC-02 changed from <old> to <new>. Decision — <approved basis>.
  Impact — <affected part>. Recheck — <criterion and expected result>.

## Evidence log
- <date> — r1 — AC-01 — <command or artifact reference> — <actual result>.
- <date> — r2 — AC-02 — <command or artifact reference> — <actual result>.
~~~

The director updates direction and its revision log. The executor appends observations, blockers, context needed to recover, and test results with the revision and working-tree or artifact baseline when relevant. Use targeted edits. Re-read immediately before saving, and reconcile a concurrent edit before writing overlapping content. Serialize metadata edits through the user handoff when concurrent saves cannot be coordinated. Keep the existing archival conventions.

Record private source references or redacted observations when appropriate. Store short decisions and evidence with the project. Keep brainstorming transcripts in the director session. Link an existing `second-opinion` case from the task if one is used.
