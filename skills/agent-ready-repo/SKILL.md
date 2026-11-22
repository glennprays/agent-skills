---
name: agent-ready-repo
description: Set up, tidy, or verify a repository's structure for AI coding agents — memory, progress, collaboration, and product context. Use for new repos before first features, repos with inconsistent or drifting agent files (CLAUDE.md, scattered docs), adding a new stack playbook, or checking recorded state against git.
---

# Agent-Ready Repo

Give one target repository a consistent agent system: a canonical constitution, layered memory that survives sessions, tiered documentation, per-stack playbooks, and thin pointers for each harness in use. Work at the size of the repo — a small CLI tool needs the core layer only; a product repo earns the full doc tree. Never install more than the user approved, and never delete existing content without an explicit mapping. Code and git history are truth; recorded state is a claim to be reconciled against them.

Copy templates from this skill's `templates/` directory and adapt them in place — fill `{{PLACEHOLDER}}` markers with what you derived or interviewed for; leave unconfirmed items as clearly marked `TODO:` slots rather than inventing answers.

## 1. Detect and classify

Inspect the target repo before proposing anything. Check: git presence (`git rev-parse --is-inside-work-tree`); manifests and lockfiles (`package.json`, `bun.lockb`/`bun.lock`, `pom.xml`/`build.gradle`, `go.mod`, `Cargo.toml`, `pyproject.toml`/`requirements.txt`, `compose.yaml`, `Dockerfile`); CI config (`.github/workflows/`, `.gitlab-ci.yml`, other CI files); README; existing agent files (`AGENTS.md`, `CLAUDE.md`, `.cursor/rules`, `GEMINI.md`, `.claude/`, `.agent/`, scattered `docs/`, `docs/superpowers/` (its `specs/`/`plans/` subdirectories mark a superpowers repo)). Read what exists; report what you actually found, not what the layout implies.

Classify the repo:

- **Fresh** — no agent system at all. Install from scratch (§3 on).
- **Partial** — some agent files exist (a lone `CLAUDE.md`, a stale `ROADMAP.md`, an `adr/` folder). Install the core layer, then tidy (§7).
- **Mature** — structure already close to the standard. Audit for gaps and drift; change little.

When the user's intent is to check or reconcile an already-installed system ("verify recorded state", "memory drifted"), go straight to §8 and return to other sections only if gaps surface.

## 2. Derive, then interview

Draft first from evidence: a mission one-liner from the README and package names; the stack list from manifests and CI; module boundaries from top-level directories; quality gates from scripts and workflow files. Then interview — ask only questions whose answers change what you build, targeting three to six total:

- Mission one-liner, when the README does not state one.
- Main module boundaries, when the directory layout is ambiguous.
- Which optional doc tiers apply (§4) — product, architecture, design, delivery.
- Which harness pointers to create (§6), when detection of harness use is ambiguous.
- Anything in existing agent files that admits more than one reading.

Present your derivations alongside the questions so the user confirms or corrects rather than writes from scratch. Everything unconfirmed lands as a `TODO:` slot in the generated file, never a guess presented as fact.

## 3. Install the core layer

Always install, for every repo size, adapting from `templates/`:

- Root `AGENTS.md` — the constitution: non-negotiable behaviors (inspect first; plan before coding; never fabricate evidence; no blind implementation of unresolved decisions; one coherent concern per commit; no secrets), a per-session workflow, the boundaries section naming the detected stacks and modules, and the grounding rituals from §9. This file is canonical; harness-specific files only point at it.
- `.agent/PROJECT_MEMORY.md` — stable facts: mission, why it exists, locked stack, key invariants, documentation map.
- `.agent/CURRENT_STATE.md` — mutable snapshot: last-verified stamp, branch and HEAD, verified artifacts, next exact actions, known risks.
- `.agent/TASKS.md` — the task ledger with columns ID, Status, Phase, Slice, Acceptance criteria, Dependency — a thin index; per-task detail goes in lazy-created `.agent/tasks/<ID>.md` (from `templates/task-file.md.tmpl`) only when a row needs evidence or multi-line acceptance; DONE rows archive per the template's rules into `.agent/tasks/archive/`. Do not pre-create `tasks/` or `archive/` — first use creates them.
- `.agent/SESSION_HANDOFF.md` — the overwrite-per-session handoff with evidence rules.
- `docs/decisions/` with `ADR-0001` scaffold and `OPEN_DECISIONS.md` (D-NNN table: question, options, recommended default, owner, status).
- `templates/ADR.md`, `templates/SESSION_REPORT.md` in the target repo, for its own future use — and `templates/PR_PLAN.md` only when the repo does not use superpowers (§10): superpowers' writing-plans skill produces the execution plan, and a second plan template invites duplicate planning artifacts.

Each `.agent/` file keeps its embedded maintenance-rules header — which session events update it, what never belongs in it. Preserve those headers when adapting; they are the mechanism that keeps memory honest after you are gone.

Every file is committed versioned source of truth; nothing generated goes to `.gitignore`.

## 4. Tier the documentation areas

Beyond the core layer, create only the areas the user approved in §2, each with exactly one numbered stub adapted from `templates/docs-stub.md.tmpl` — no empty directories:

- `docs/product/` — when the repo has users, a roadmap, or product framing.
- `docs/architecture/` — services, data flow, contracts.
- `docs/design/` — UI work, design decisions.
- `docs/engineering/` — per-stack playbooks (§5).
- `docs/delivery/` — phased builds, milestone plans.
- `docs/agents/` — a short doc describing this system itself: the memory layers and how agents should use them, from `templates/agents-doc.md.tmpl`.

A CLI or library repo may reasonably get zero extra areas. Do not pre-create tiers "for later"; they are added when the need arrives.

## 5. Generate stack playbooks

For each detected stack, generate `docs/engineering/NN-<stack>.md` from `templates/engineering-stack.md.tmpl`:

- **Verified commands** — build, lint, typecheck, test. Read them from manifests, package scripts, and CI config; run each command once where feasible and record the observed result, not the claimed one. Commands you could not verify stay `TODO: verify`.
- **Conventions** — format tool, test layout, migration rules. Propose from ecosystem defaults; the user confirms or edits during §2. Unconfirmed conventions stay `TODO: confirm`.
- **Boundaries** — what belongs to this stack and what does not, from §2's boundary decisions.

When the skill runs again on a repo that gained a new stack, add only the missing playbook. Never rewrite an existing playbook without explicit approval — diff it and propose changes instead.

## 6. Create harness pointers

`AGENTS.md` is canonical. For each harness the repo actually uses — detected from existing config and dotfiles, confirmed in §2 — create the thinnest pointer that makes the harness read the canonical file:

- Claude Code: `CLAUDE.md` containing `@AGENTS.md` and one fallback line: "Read AGENTS.md first."
- Cursor: a pointer rule under `.cursor/rules` referencing `AGENTS.md`.
- Gemini CLI: `GEMINI.md` with the same import-plus-fallback pattern.

OMP and OpenCode read `AGENTS.md` natively; create nothing for them. If the repo ships skills under `.agents/skills`, note that OMP discovers them with `skills.enableAgentsProject: true`. Never create pointer files for harnesses not in use, and never duplicate constitution content into a pointer — a pointer points.

## 7. Tidy an existing structure

For partial or mature repos, produce an audit report before touching anything:

- Current layout mapped against the standard from §3–§6.
- Overlaps and conflicts (two files claiming the same role, contradictory rules).
- Task-ledger split, when an existing TASKS.md holds closed phases or >50 rows: propose moving settled DONE rows (dependents all DONE/archived) into the first `.agent/tasks/archive/<YYYY-MM>.md` batch and leaving open rows in the index — approval-gated like every other tidy item.
- Proposed `git mv` operations, each with source, destination, and reason.
- Proposed merges into standard files, each with what moves where.

Execute only the items the user approves. Use `git mv` wherever git exists so history follows the file (verify later with `git log --follow`); plain moves only in non-git directories, after approval. Content you cannot map confidently goes verbatim into `docs/agents/legacy-notes.md` — never deleted, never summarized by you — with each block headed by its origin path so a human can decide its fate later. If a merge would silently drop any existing rule, quarantine that rule the same way instead of merging it.

## 8. Reconcile drift

For any repo with the system installed — including a standalone "check/verify/reconcile" request — diff recorded claims against reality:

- `.agent/CURRENT_STATE.md`: claimed branch, commit, last-verified stamp versus actual `git status`, `git branch`, `git log`.
- `.agent/TASKS.md`: every `DONE` row versus merged PRs and commits that actually exist. Rows live in the index or in `.agent/tasks/archive/` batches — reconcile index rows (open and DONE) against git; archived rows are settled history and are checked only on explicit request.
- `.agent/SESSION_HANDOFF.md`: claimed test results versus evidence in git history and CI.
- Superpowers plans (when present): a fully checked `docs/superpowers/plans/*.md` whose TASKS.md row is not DONE — or the inverse — is drift; report both readings and let the user pick which reflects reality.

Report each stale claim with the recorded value, the observed value, and the command that produced it. Rewrite only with the user's approval, and stamp the new last-verified line with the actual command outputs, not today's date alone. When memory and git disagree, git wins; when the disagreement reveals a real problem (work claimed done but absent), surface it as a finding rather than silently re-stamping.

## 9. Embed the grounding rituals

The generated `AGENTS.md` must carry the anti-drift mechanics, because future agents read it, not you:

- **Session start.** Quote `CURRENT_STATE.md`'s last-verified line and the actual `git branch`/HEAD before any edit. Report discrepancies instead of proceeding silently; reconcile (§8) before building on stale state.
- **Session end.** `SESSION_HANDOFF.md` records commands actually run and their actual results — never claimed or expected results. If no tests ran, it says so explicitly.
- **Code and git over prose.** Where documentation and the repository disagree, the repository is truth; fix the doc or file an ADR, never the reverse.
- **Unresolved decisions are not improvisation fuel.** Anything unresolved goes to `OPEN_DECISIONS.md` with a recommended default; no agent may treat it as decided.

## 10. Coexist with superpowers

When the repo uses superpowers (obra/superpowers) — `docs/superpowers/` present, or the user says so in the §2 interview — adapt instead of replacing:

- Keep `docs/superpowers/` exactly where it is. Never propose moving it during tidy (§7): it is superpowers' native output path and its skills hardcode it. §1 detects `docs/superpowers/specs/`/`plans/` to trigger this section, not to reclassify those files.
- Fill the superpowers block of the `AGENTS.md` artifact authority map (the `{{SUPERPOWERS_BLOCK}}` section in `templates/AGENTS.md.tmpl`): keep the four superpowers lines, delete the surrounding marker and comment as part of normal template adaptation. Delete nothing else.
- Skip `templates/PR_PLAN.md` in the install (§3): superpowers' writing-plans skill produces the execution plan, and a second plan template invites duplicate planning artifacts.
- When a `.agent/TASKS.md` row is executed via a superpowers plan, record the plan path in that row's Acceptance-criteria cell (e.g. `— plan: docs/superpowers/plans/2026-11-20-auth.md`). The plan holds step-level checkboxes; TASKS.md holds lifecycle status only — status stays single-sourced in TASKS.md.
- No superpowers-side configuration needed: per `using-superpowers`, user instructions (`AGENTS.md`, `CLAUDE.md`) take precedence over skills, so the authority map is binding in superpowers sessions as written.

Verify your own run against these rituals before finishing: the files you generated should already satisfy the session-start check a next agent would perform.
