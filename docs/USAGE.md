# Usage

This repository ships three versions of every rule set:

- `mini`: the recommended version for most real task use, especially as a focused skill
- `nano`: the compact fallback for very tight context budgets
- `full`: the complete reference version, best used as reference material for deep skills, audits, and focused sessions

## Start Here

Use the smallest mechanism that still changes the agent's decisions.

- Start with one primary rule set.
- Prefer skills for book-specific guidance. A `mini` file is usually the right skill body.
- Use `mini` by default when one book should shape the agent's decisions for a specific task.
- Use `nano` only when the rule set must be extremely small, permanently always-on, or portable across tools with tight context budgets.
- Use `full` for audits, one-off deep sessions, skill reference files, or for deriving smaller scoped rules.
- Prefer scoped, on-demand, or retrieval-based loading over global loading.
- Treat memories as helpers, not as the canonical source of truth.

## Delivery Patterns

| Pattern | Best for | Repo version | Notes |
| --- | --- | --- | --- |
| Skill or command | Refactoring passes, reviews, migrations, reliability work, DDD modeling, legacy changes | `mini`, optionally backed by `full` | Best default for most book-specific guidance. |
| Always-on project rule | Stable defaults that should affect most tasks | `mini` or `nano` | Use one carefully chosen `mini`; use `nano` if `mini` is too large for the tool or project. |
| Scoped rule | One directory, file type, or subsystem | `mini` or `nano` | Prefer `mini`; use `nano` for tiny path-scoped reminders. |
| On-demand rule | Refactoring passes, reviews, migrations, reliability work | `mini` | Invoke only when the task matches. |
| Retrieval or MCP | Large reference material, changing docs, external systems | `full` or source material outside the prompt | Use when the content is too large or too rarely needed for always-on context. |

## Skills First

Use skills when the rule set should activate for a kind of work rather than every message in the project.

Good skill candidates:

- `refactoring.mini.md` for a refactoring pass
- `working-effectively-with-legacy-code.mini.md` for risky legacy changes
- `domain-driven-design.mini.md` for modeling-heavy work
- `release-it.mini.md` for production reliability changes
- `designing-data-intensive-applications.mini.md` for data consistency, events, streams, and schema evolution

Recommended skill shape:

```text
project/
  .agents/
    skills/
      refactoring-pass/
        SKILL.md        # derived from refactoring.mini.md
        reference.md    # optional link or copy of refactoring.md
```

Keep the active skill concise. Put long examples, full rule files, and traceability material in reference files or retrieval, not in always-on project instructions.

## Mini vs Nano

`mini` is the optimal default for most agent work and the best starting point for skills. It usually contains enough of the book's decision pressure, trigger rules, and tradeoff handling to change implementation choices without bringing in the full source.

Use `mini` when:

- you are choosing one primary book for a task, skill, or small project-wide baseline
- you want a stable repo-wide engineering bias and the context budget can afford it
- the task is a review, refactor, migration, design pass, production fix, or modeling-heavy change
- the rule set should prevent subtle shortcuts, not just remind the agent of the headline thesis

Use `nano` when:

- the tool has a very small always-on instruction budget
- the same baseline must travel across several editors with different limits
- you only need the smallest reminder of a book's bias
- `mini` would compete with more important project-specific context

Use `full` when:

- the skill needs a deep reference file
- you are auditing a rule set or deriving a smaller skill
- the task is a focused one-off session with enough context budget
- you need traceability back to the book's structure and bias

## Portable Baseline

If your team uses more than one editor, use a portable baseline:

- Keep one canonical `AGENTS.md` with a single `mini` rule set when the supported tools can handle it.
- Use `nano` as the portable fallback only when `mini` is too large for one of the tools.
- Let Codex read that file directly.
- Let Claude Code import it from `CLAUDE.md`.
- Let Cursor either read `AGENTS.md` directly for simple projects or translate the same content into `.cursor/rules` for better scoping.
- Add editor-specific on-demand mechanisms next to that baseline instead of duplicating a large global rule file.

This gives you one cross-tool source for the base layer, while still allowing each editor to use its stronger native features.

## Codex

### Available mechanisms

- `AGENTS.md` in the repo root or nested directories
- `AGENTS.override.md` for closer overrides
- `.codex/config.toml` with `model_instructions_file`, `project_doc_fallback_filenames`, and project-scoped config
- skills in `.agents/skills/` or `~/.agents/skills/`
- hooks via `.codex/config.toml` or `hooks.json`
- MCP servers and web search for external context
- memories for learned preferences

### Preferred setup

Use Codex in two layers:

1. Use skills for book-specific workflows such as refactoring, legacy changes, production reviews, and domain modeling.
2. Put one `mini` rule set in the project layer only when you want a book to shape most tasks.
3. Fall back to `nano` only when the always-on project layer must stay extremely small.

Preferred order:

1. Turn procedures, checklists, and book-specific workflows into skills.
2. Use root `AGENTS.md` for the project-wide base layer.
3. Use `model_instructions_file` if you want Codex to point at a chosen file without renaming it to `AGENTS.md`.
4. Add nested `AGENTS.md` or `AGENTS.override.md` only where a subtree genuinely needs different pressure.
5. Use MCP or retrieval for large reference corpora instead of stuffing them into the always-on file.

### Recommended version mapping

- `mini`: preferred skill body; also usable as project-wide default in `AGENTS.md` or `model_instructions_file`
- `nano`: compact fallback for very tight always-on budgets
- `full`: skill reference, audit source, or focused-session reference

### Recommended structure

```text
project/
  AGENTS.md
  .agents/
    skills/
      refactoring-pass/
        SKILL.md
  services/
    payments/
      AGENTS.override.md
```

### Use Codex this way when

- you want a stable repo-wide engineering bias
- some subtrees need different guidance
- a workflow is repeatable enough to deserve a skill

### Avoid

- loading several `full` files globally
- putting long procedures into `AGENTS.md`
- using memories as the primary place for shared rules

## Autohand Code

### Available mechanisms

- skills in `.autohand/skills/` or `~/.autohand/skills/`
- project-level instructions when the project already has a reviewed shared baseline
- MCP servers and web search for external context

### Preferred setup

Use Autohand Code skills for book-specific workflows, especially when the rule set should activate only for refactoring, legacy-code work, reliability review, or domain modeling.

Preferred order:

1. Turn a focused `mini` rule set into a skill under `.autohand/skills/` for the current project or `~/.autohand/skills/` for global reuse.
2. Put one `mini` rule set in the project layer only when that book should shape most tasks.
3. Use `nano` only when the always-on project layer must stay extremely small.
4. Keep `full` files as skill references or retrieval material instead of loading them globally.

### Recommended version mapping

- `mini`: preferred skill body; also usable as a compact project-wide default
- `nano`: compact fallback for very tight always-on budgets
- `full`: skill reference, audit source, or focused-session reference

### Recommended structure

```text
project/
  .autohand/
    skills/
      refactoring-pass/
        SKILL.md
        reference.md
```

### Use Autohand Code this way when

- you want a book-specific skill available to Autohand Code without affecting every task
- a team wants to keep shared skill packages in the repository
- one workflow is repeatable enough to deserve an explicit skill

### Avoid

- loading several `full` files globally
- copying every book into the same always-on context
- treating local memories as reviewed team instructions

## Claude Code

### Available mechanisms

- `CLAUDE.md` or `.claude/CLAUDE.md`
- `CLAUDE.local.md` for private local additions
- `@path` imports inside `CLAUDE.md`
- `.claude/rules/` for scoped project rules
- `.claude/skills/<name>/SKILL.md`
- subagents
- hooks in settings or scoped to skills
- MCP resources and prompts
- auto memory

### Preferred setup

Claude Code works best with a small root memory file plus scoped additions.

Preferred order:

1. Keep root `CLAUDE.md` short.
2. If you want one shared cross-tool base file, put the chosen repo file at `AGENTS.md` and import it from `CLAUDE.md`.
3. Use Claude Code skills for book-specific workflows.
4. Use one `mini` rule set for always-on project context when the file stays short enough for the team.
5. Use `.claude/rules/` or path-scoped skills for `mini`.
6. Use `nano` only when the shared root file has to be much smaller.
7. Put procedures, large checklists, and long references into skills instead of the root `CLAUDE.md`.
8. Use `disable-model-invocation: true` for side-effectful manual workflows such as deploy or release flows.
9. Use subagents or `context: fork` skills when a side task would otherwise flood the main context.

### Recommended version mapping

- `mini`: preferred `.claude/skills/` body; also usable in `.claude/rules/` or a short imported base file
- `nano`: compact fallback for very tight root context
- `full`: skill reference, audit source, or narrowly imported file for a specific session

### Recommended structure

```text
project/
  AGENTS.md
  CLAUDE.md
  .claude/
    rules/
    skills/
```

Example `CLAUDE.md`:

Import the shared root `AGENTS.md` baseline by adding this line to `CLAUDE.md` in order to reuse the same project-wide rules in Claude Code.

```md
@AGENTS.md

## Claude Code

- Use skills for long procedures and checklists.
- Use scoped rules for subsystem-specific guidance.
```

### Use Claude Code this way when

- you want a cross-tool base layer plus Claude-specific scoping
- a rule only matters in one subsystem
- a rule has become a procedure rather than a fact

### Avoid

- pasting a long `full` rule file into root `CLAUDE.md`
- mixing many conflicting imports
- relying on auto memory instead of reviewed project instructions

## Cursor

### Available mechanisms

- `.cursor/rules/*.mdc` project rules
- rule types: `Always`, `Auto Attached`, `Agent Requested`, `Manual`
- root `AGENTS.md` as a simple alternative
- user rules
- `@Cursor Rules` for explicit rule application
- `/Generate Cursor Rules`
- memories
- codebase indexing
- MCP

### Preferred setup

Cursor's strongest native mechanism is `.cursor/rules`.

Preferred order:

1. Prefer `.cursor/rules` over `AGENTS.md` for serious use.
2. Use at most one project-wide `Always` rule derived from `mini` when it stays small enough.
3. Turn `mini` into `Agent Requested`, `Manual`, or `Auto Attached` rules by topic or path.
4. Use `@Cursor Rules` when you want explicit on-demand application.
5. Keep large reference material in attached files, indexed docs, or MCP, not in `Always` rules.
6. Use root `AGENTS.md` only for simple projects or when you want a portable cross-tool baseline.
7. Use `nano` only when an `Always` rule must be extremely short.

### Recommended version mapping

- `mini`: short `Always` rule, simple root `AGENTS.md`, or `Agent Requested`, `Manual`, and `Auto Attached` project rules
- `nano`: compact fallback for very tight `Always` rules
- `full`: reference only

### Recommended structure

```text
project/
  .cursor/
    rules/
      base.mdc
      payments.mdc
      refactor.mdc
      ddd.mdc
```

Suggested split:

- `base.mdc`: one short `Always` rule derived from `mini`, or from `nano` if the base must be tiny
- `payments.mdc`: `Auto Attached` for `payments/**`
- `refactor.mdc`: `Manual` for explicit refactoring passes
- `ddd.mdc`: `Agent Requested` for modeling-heavy tasks

### Use Cursor this way when

- you want strong scoping and explicit control over context
- you want different rules for different subsystems
- you want on-demand rule selection without a huge global file

### Avoid

- using one giant `Always` rule
- treating root `AGENTS.md` as the best default for complex projects
- storing large reference packs in project rules when indexing or MCP is a better fit

## Retrieval, MCP, and RAG

Use retrieval-based delivery when the material is too large, too dynamic, or too rarely needed for always-on context.

Good candidates:

- multiple books at once
- large examples and templates
- architecture docs, specs, and runbooks
- changing external guidance
- domain documents that matter only for some tasks

Recommended by editor:

- Codex: skills plus MCP or retrieval-backed tools
- Claude Code: skills plus MCP resources or prompts, optionally with subagents
- Cursor: scoped project rules plus codebase indexing or MCP

If your team already has a RAG system, keep the long reference material there and only promote decision-changing rules into always-on or scoped prompt rules.

## Decision Guide

- Need a task-specific book bias: create or invoke a skill from the relevant `mini` rule set.
- Need a steady repo-wide bias: use one `mini` rule set.
- Need an extremely small always-on baseline: use `nano`.
- Need stronger guidance for a specific task: load the relevant `mini` rule set as a skill or on-demand rule.
- Need a multi-step workflow: create a skill or command, with `full` as optional reference.
- Need subsystem-specific pressure: use scoped rules or nested files.
- Need long reference material: use retrieval, indexing, or MCP.
- Need more than one book: keep one primary always-on rule set and move the rest to on-demand mechanisms.
