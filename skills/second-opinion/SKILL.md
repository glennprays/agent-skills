---
name: second-opinion
description: Use when a user asks for an independent review, fresh diagnosis or design assessment, a follow-up on a finding, or verification of a requested fix across sessions.
---

# Second Opinion

The executor owns the task. The executor writes the case record, runs consequential checks, applies source changes only when the user explicitly requests implementation, and reconciles reviewer output. An analysis-only invocation never edits source. Recording an applied fix moves the related finding to `awaiting verification`, never directly to `verified`. The reviewer examines evidence; it never writes the case record, edits source, or allocates finding IDs.

A question about an existing case can continue after the executor or reviewer session ends. The case record is the durable handoff, not chat history.

## 1. Resolve the case and round

Find the case by ID, path, or a clear match in project review notes. Reuse the project's case or incident notes convention. In a writable project with no convention, create `.second-opinion/<case-id>.md` only when the first round needs persistence. Never put a case record in an installed skill directory. Store evidence pointers and redacted excerpts — never secrets, credentials, or raw sensitive payloads. In a read-only session or when no durable path exists, return the record for later use and say so.

Use the [case record template](references/case-record.md). Keep stable `F-NN` finding IDs. Preserve earlier rounds. Before appending, re-read the case; if another update appeared, append a later round rather than rewriting historical evidence. The executor writes the record, including results from parallel reviewers. A time-critical request is not an exemption: an answer that exists only in chat is lost to the next session, so write the record first if only a stub round fits the deadline.

| Request | Round | Reviewer input |
|---|---|---|
| "Give me a second opinion" or "look at this from scratch" | Independent analysis | Question, established requirements, observations, and original sources. Withhold prior interpretations, prior conclusions, and preferred fixes. |
| "Check again after the fix" | Verification | Finding in observable terms, original failure scenario, acceptance criteria, current change, and evidence. |
| "The issue still happens. Look for other explanations." | Independent reassessment | Latest symptoms and evidence plus relevant earlier test observations with their original baselines. Compare past conclusions only after the reviewer responds. |
| "Dig deeper into F-02" | Targeted follow-up | Finding, evidence references, and precise follow-up question. Use the same reviewer when available. Recreate the brief from the case record after a restart. |

## 2. Identify the source baseline

A baseline identifies: the repository and source revision; relevant staged, unstaged, and untracked inputs; a source/artifact fingerprint or immutable snapshot identifier when comparison matters; and relevant environment, configuration, feature flags, fixtures, and the time window. A commit hash alone is insufficient for a dirty workspace.

Check that the reviewer can see the intended revision, including the uncommitted changes it needs. Use an identified snapshot if edits are still in flight, or verify the relevant inputs at the end and mark the round stale if they changed. Record the reviewer agent, resolved model, harness, and skill revision when known. When comparing conclusions across models, versions, or configurations, hold the brief, evidence snapshot, permissions, and acceptance criteria constant; treat differing conclusions as a prompt to resolve evidence, not as a verdict to reuse.

## 3. Give the reviewer a neutral brief

Use the [reviewer input and output contract](references/reviewer-protocol.md). Give direct references to original evidence and room to inspect nearby code. Separate confirmed requirements from observations. Preserve material constraints confirmed by the user. For independent analysis and reassessment, the brief must not contain executor notes, prior conclusions, the current hypothesis, the desired answer, or a proposed fix. Ask an open question that admits competing explanations.

Prefer one fresh reviewer. Use two when distinct perspectives could change the decision (for example API contract versus recovery behavior); give both the same factual baseline with their specific questions, and collect both results before sharing either with the other.

Delegation must be truthful about isolation. Before each review, inspect the live `task` tool schema and its Available Agents list in the active runtime. Do not assume a bundled role is read-only. Select a reviewer marked read-only only when its shown runtime tool policy is actually read-only. In current OMP the default `reviewer` role is prompt-shaped, not tool-enforced: its declared tools include `bash` and `lsp`, so it must not be presented as an enforced read-only channel. For each reviewer, record the agent name, its source, the resolved model when surfaced, the tool boundary, and any dispatch errors.

For independent analysis, pass a neutral, curated brief to a newly spawned reviewer, and withhold executor theories, prior conclusions, and proposed fixes. A `task` child starts without the parent's chat history but still inherits the workspace: project rules, repository files (including anything the executor just wrote), shared `local://` artifacts, and any approved-plan references. Record these possible exposures alongside the actual isolation. When inherited exposure would defeat independence, curate the needed evidence into a neutral location for the reviewer, or use a genuinely fresh session with only the curated inputs.

If no runtime-enforced read-only reviewer exists, use a curated fresh session when available. Otherwise perform a same-session pass and label it `self-review` in the case record, with its limitations — including when a delegated reviewer dispatch fails, which leaves an executor-only round. A fresh session is not automatically an independent review: classify each round from the actual reviewer setup and recorded exposure. Never create a consumer-project agent merely to claim production isolation.

## 4. Analyze and verify

Apply the method that fits the question:

- **Diagnosis** — Compare explanations the evidence supports. Give a check whose expected observations differ between the plausible explanations.
- **Design or decision** — Compare viable options against the same user goals and constraints; state trade-offs and what new information would change the decision.
- **Verification** — Recheck the original failure scenario against the current version. The executor runs checks where authorized and records the actual result tied to the baseline. Static inspection may support static claims; it cannot produce a runtime pass. Record each acceptance criterion as pass, fail, or not run, with method (`runtime`, `static`, or another concrete method), output reference, and tested baseline.
- **Targeted follow-up** — Narrow to the unresolved claim; carry forward relevant evidence and recheck that it still applies to the current baseline.

Ask reviewers for concise conclusions, references, limitations, and the next discriminating check. One focused review is the default. Deepen when evidence conflicts, effects cross boundaries, or the decision is expensive to reverse.

## 5. Reconcile and continue

Check claims that could change the decision against their sources. Record a disposition (`accepted`, `needs verification`, `rejected`) and reason for each consequential finding. Keep a proposed fix separate from the decision to implement it. When implementation was requested, apply it and record the actual change; the finding then sits at `awaiting verification` until the required checks run against the recorded baseline. Use the disposition/lifecycle transition table in the [case record template](references/case-record.md); do not improvise transitions.

Return the case ID or path, the main conclusion, any fix made, the verification method and result, and the next concrete action with its owner. On resume, re-read the case record and current evidence, and continue from the last relevant round. When evidence conflicts across runs, tie each observation to its actual baseline and name the one check that makes the comparison fair.
