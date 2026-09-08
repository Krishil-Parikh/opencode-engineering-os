# OpenCode Engineering OS

A layered multi-agent setup for OpenCode: one orchestrator, seven
specialists, a shared skill library, and a handful of workflow commands —
built against OpenCode's native **V2** `agents` / `permissions` / `skills`
schema.

No standalone research agent. `architect`, `deep-thinker`, `builder`, and
`auditor` each keep their own read-only `webfetch`/`websearch` access for
the odd doc lookup or CVE check, so nothing loses the ability to check a
fact online — there just isn't a dedicated role for it, and the other four
agents (`decomposer`, `test-engineer`, `reviewer`, `validator`) stay
repo-only on purpose, since their whole job is judging what's already in
front of them.

## Install

Pick one:

**Global** (this becomes your personal setup everywhere):
```bash
cp -r agents commands skills AGENTS.md opencode.jsonc ~/.config/opencode/
```

**Project-local** (this repo only):
```bash
mkdir -p .opencode
cp -r agents commands skills .opencode/
cp AGENTS.md opencode.jsonc ./
```
(Project config can also live at `.opencode/opencode.jsonc` instead of the
repo root — see OpenCode's [Config docs](https://opencode.ai/v2/docs/config)
if you already have one there and need to merge instead of overwrite.)

Either way, **open `opencode.jsonc` and swap in your actual `provider/model`
strings** — the ones shipped here are placeholders naming the tier each
agent needs, not a guarantee they're what you have configured.

## The eight agents

| Agent | Mode | Job |
|---|---|---|
| `architect` | primary | Understands the request, delegates, only reports done once validation + review pass. Your default agent. |
| `deep-thinker` | subagent | Hard reasoning on architecture, tradeoffs, and ambiguity. Never proposes an implementation. |
| `decomposer` | subagent | Turns a goal into an ordered, dependency-aware, risk-flagged task list. |
| `builder` | all | Implements. Minimal diffs, preserves existing behavior, delegates test-writing to `test-engineer`. |
| `test-engineer` | subagent | Writes tests from the actual implementation, not the ticket. Can't touch application code. |
| `reviewer` | subagent | Correctness, maintainability, design quality. P0-NIT findings with file:line + scenario. |
| `validator` | subagent/all | Objective build/type/lint/test check. No opinions — just PASS/FAIL. |
| `auditor` | subagent | Adversarial security/reliability/data pass, including AI/ML-specific risks. |

`architect` is `default_agent`. Everything else it delegates to as needed —
see `agents/architect.md`'s "How deep to go" section for when it skips
straight to `builder → validator` versus running the full pipeline.

## The seven commands

| Command | What it does |
|---|---|
| `/build <task>` | Full pipeline: plan → implement → test → validate → review → fix. |
| `/investigate <problem>` | Planning only — deep-thinker + decomposer, zero code changes. |
| `/review [scope]` | Independent reviewer + test-engineer + auditor pass on current changes. |
| `/audit [scope]` | Read-only security/reliability/architecture report. Nothing gets fixed. |
| `/refactor <target>` | Behavior-preserving refactor with a validation + review gate. |
| `/validate [scope]` | Straight to validator — build/type/lint/test report, no fixes. |
| `/ship <change>` | Final gate: diff review, full verification, security check, summary. |

## The skills

Reusable procedures any agent can load on demand: `problem-solving`,
`task-decomposition`, `architecture`, `debugging`, `incident-debugging`,
`code-review`, `security-audit`, `validation`, `testing`, `performance`,
`refactoring`, `git`, `api-design`, `database-design`, `ai-ml`,
`dependency-analysis`, `documentation`.

Add project- or language-specific ones (`python`, `fastapi`, `pytorch`,
`kubernetes`, whatever the repo actually uses) as you need them — the
directory layout is `skills/<name>/SKILL.md`. Don't load a dozen
language skills globally just in case; the more that are advertised to the
model, the noisier the catalog gets. Project-scoped skills in a repo's own
`.opencode/skills/` only show up for that repo anyway.

## Permission design

Every agent's `permissions` block only grants what its job actually needs
— `reviewer` can't edit, `decomposer` can't touch the network, `validator`
can't push to git. Where an agent *does* get a broad `allow` (`builder`'s
`edit: *`, several agents' `shell: *`), the risky specifics
(`rm -rf *`, `git push --force*`, `.env*`, `*secret*`) are denied again
**inside that same agent's own permission list**, after the broad allow.

That repetition is deliberate, not copy-paste sloppiness: permission
matching is "last matching rule wins" across the merged rule list, and an
agent's own rules are merged in *after* the global `opencode.jsonc`
defaults. A broad allow inside an agent's own block would otherwise be the
last (and winning) match for everything the global config tried to guard.
Repeating the specific denies at the end of each risky agent's block is
what actually makes them stick — see the comments in `opencode.jsonc` and
in `agents/builder.md` for the concrete example.

`test-engineer`'s edit permission is additionally scoped to test-file-like
paths (`*test*`, `*.spec.*`, `*_test.*`) rather than `edit: *` — loosen or
tighten those globs once you know your project's actual test layout, since
a pattern like `*test*` can also match an unrelated file that happens to
contain that substring.

## Model tiering

`opencode.jsonc`'s `agents` block sets `model` per agent by tier:
`architect` / `deep-thinker` / `auditor` get your best reasoning model,
`builder` / `test-engineer` get your best coding model, `decomposer` /
`reviewer` get something strong but not necessarily your top-tier model,
and `validator` gets your fastest/cheapest one — it's only ever running
`build`/`test`/`lint`, not thinking hard about anything.

## Extending this

- To add a ninth agent, drop a new `.opencode/agents/<name>.md` in and give
  it an explicit `mode`, a scoped `permissions` list, and a `description`
  (subagents are only as discoverable as their description is clear).
- If you add an agent that itself needs to delegate further, remember
  `experimental.subagent_depth` in `opencode.jsonc` caps total nesting —
  raise it deliberately, not by accident.
- Keep new commands thin: they should name *which* agents run and in what
  order, not re-describe how each one does its job — that description
  already lives in `agents/`.
