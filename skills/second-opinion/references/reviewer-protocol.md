# Reviewer brief and result

Use this contract for every reviewer assignment, whether the reviewer is a delegated agent, a fresh session, or a same-session `self-review`. Include prior findings only for verification or targeted follow-up. Label any fixture or hypothesis explicitly.

## Input

An independent or reassessment brief must NOT contain: executor notes, prior conclusions, the current hypothesis, the desired answer, or a proposed fix.

- **Question and round mode** — One open question and the review type.
- **Expected behavior** — User-confirmed outcome, acceptance criteria, and material constraints.
- **Observed behavior** — What was seen or measured, with source, time, and environment when relevant.
- **Baseline** — Revision or snapshot, relevant local edits, flags/config/fixtures, and the available evidence.
- **Access and boundaries** — Sources the reviewer may inspect, checks that are permitted, the reviewer's actual tool boundary, and known exposure of the reviewer to executor context.
- **Target for verification or follow-up** — The relevant `F-NN` and the original failure scenario. Omit in independent analysis and reassessment.
- **Assignment** — Inspect the evidence read-only. Return grounded findings in the output format below.

## Output

1. **Question, scope, and inspected version** — Name the inputs actually inspected. Call out missing or changed artifacts, and any exposure to earlier conclusions when apparent.
2. **Conclusion and evidence** — State the best-supported answer or that the question remains open. Distinguish observation from inference. Cite stable source evidence: path and line or symbol, log event and timestamp, test result, or equivalent. State contrary evidence that affects the conclusion.
3. **Findings** — For each significant finding: claim, impact, evidence, uncertainty. Use the existing `F-NN` when verifying or following up; reviewer output never allocates new IDs — the executor does.
4. **Next check** — The smallest discriminating check. For competing diagnoses: what different outcomes would imply. For a decision: the condition that would change the recommendation.
5. **Verification** — For each criterion: `pass`, `fail`, or `not run`, the method (`runtime`, `static`, or other concrete method), the relevant output, and the tested baseline. Static evidence supports static claims only; it cannot produce a runtime pass.

## Executor handoff

After the reviewer responds, the executor checks claims against sources, allocates `F-NN` IDs, updates the case record (disposition, lifecycle, next action), and records the reviewer setup and exposure verbatim from the round. When a second review disagrees, compare claims, versions, and evidence baselines; resolve with a direct check when possible; preserve material disagreements that remain open.
