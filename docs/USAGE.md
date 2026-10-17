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
- Prefer scoped or on-demand loading over global loading.
- Treat memories as helpers, not as the canonical source of truth.

## Delivery Patterns

| Pattern | Best for | Repo version | Notes |
| --- | --- | --- | --- |
| Skill or command | Refactoring passes, reviews, migrations, reliability work, DDD modeling, legacy changes | `mini`, optionally backed by `full` | Best default for most book-specific guidance. |
| Always-on project rule | Stable defaults that should affect most tasks | `mini` or `nano` | Use one carefully chosen `mini`; use `nano` if `mini` is too large for the tool or project. |
| Scoped rule | One directory, file type, or subsystem | `mini` or `nano` | Prefer `mini`; use `nano` for tiny path-scoped reminders. |
| On-demand rule | Refactoring passes, reviews, migrations, reliability work | `mini` | Invoke only when the task matches. |
| External knowledge system | Large private docs, changing references, or organization-specific knowledge | Outside this repository | Keep it separate from these static rule files. |

For large private documentation or organization-specific knowledge, use your team's existing documentation or search system outside this repository.

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

Keep the active skill concise. Put long examples, full rule files, and traceability material in reference files, not in always-on project instructions.

## Install Existing Skills

Each book directory contains a standard `SKILL.md` entrypoint. The skill points at the corresponding `mini` rule set for normal use and keeps the `full` file available as deeper reference material.

Prerequisite: install Node.js with npm. You can run the Skills CLI through `npx` without installing `skills` separately.

Install all book skills with the open Agent Skills CLI:

```sh
npx skills add ciembor/agent-rules-books --all
```

List available skills without installing:

```sh
npx skills add ciembor/agent-rules-books --list
```

Install one selected skill:

```sh
npx skills add ciembor/agent-rules-books --skill refactoring
```

Use CLI-installed skills when you want the same package to work across supported agents. Use the manual patterns below when you need tighter control over project scope, always-on behavior, or editor-specific rules.

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
- `.codex/config.toml` with `project_doc_fallback_filenames`, `project_doc_max_bytes`, project-scoped config, and hooks
- skills in `.agents/skills/` or `~/.agents/skills/`
- hooks via `.codex/config.toml` or `hooks.json`
- web search for external context
- memories for learned preferences

### Preferred setup

Use Codex in two layers:

1. Use skills for book-specific workflows such as refactoring, legacy changes, production reviews, and domain modeling.
2. Put one `mini` rule set in the project layer only when you want a book to shape most tasks.
3. Fall back to `nano` only when the always-on project layer must stay extremely small.

Preferred order:

1. Turn procedures, checklists, and book-specific workflows into skills.
2. Use root `AGENTS.md` for the project-wide base layer.
3. Use `project_doc_fallback_filenames` if you want Codex to read another project instruction filename when `AGENTS.md` is missing.
4. Add nested `AGENTS.md` or `AGENTS.override.md` only where a subtree genuinely needs different pressure.
5. Keep large reference corpora out of the always-on file.

### Recommended version mapping

- `mini`: preferred skill body; also usable as project-wide default in `AGENTS.md`
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

### Optional current API documentation

Book rules guide design decisions; a refactor may also need current public documentation for the installed library version. [Parallel Search MCP](https://docs.parallel.ai/integrations/mcp/search-mcp) provides optional web search and page fetching without an account or API key. Anonymous search uses Fast mode and is subject to service limits.

Add this table to your trusted project's existing `.codex/config.toml`, preserving other settings and MCP servers:

```toml
[mcp_servers.parallel-search]
url = "https://search.parallel.ai/mcp"
```

Restart Codex and use `/mcp` to confirm that the server exposes `web_search` and `web_fetch`. See [Codex MCP configuration](https://developers.openai.com/codex/mcp) for configuration scope and available settings.

For example, with the `refactoring` skill installed:

```text
Use the refactoring skill. Before changing our HTTP client wrapper, inspect the
dependency manifest and lockfile to identify the library and installed version.
Use Parallel's web_search to find that version's official timeout and retry docs.
Use web_fetch on the relevant pages if the search excerpts are insufficient.
Cite the source URLs and propose a small behavior-preserving refactor with tests
before editing.
```

Keep retrieved pages in task context rather than copying them into `AGENTS.md` or the static book rule files. Search public documentation only; keep private code and internal documentation in your team's approved knowledge system.

### Avoid

- loading several `full` files globally
- putting long procedures into `AGENTS.md`
- using memories as the primary place for shared rules

## Claude Code

### Available mechanisms

- `CLAUDE.md` or `.claude/CLAUDE.md`
- `CLAUDE.local.md` for private local additions
- `@path` imports inside `CLAUDE.md`
- `.claude/rules/` for scoped project rules
- `.claude/skills/<name>/SKILL.md`
- subagents
- hooks in settings or scoped to skills
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

- `.agents/skills/` or `.cursor/skills/` for Agent Skills
- `.cursor/rules/*.mdc` project rules
- rule types: `Always Apply`, `Apply Intelligently`, `Apply to Specific Files`, `Apply Manually`
- root `AGENTS.md` as a simple alternative
- user rules
- `@rule-name` for explicit manual rule application
- `/create-rule`, `/create-skill`, and `/migrate-to-skills`
- memories
- codebase indexing

### Preferred setup

Cursor supports both Agent Skills and project rules. Use skills for book-specific workflows and `.cursor/rules` for always-on or path-scoped prompt context.

Preferred order:

1. Use Agent Skills for book-specific workflows such as refactoring, legacy changes, production reviews, and domain modeling.
2. Prefer `.cursor/rules` over `AGENTS.md` when you need Cursor-specific always-on, intelligent, manual, or file-scoped prompt rules.
3. Use at most one project-wide `Always Apply` rule derived from `mini` when it stays small enough.
4. Turn `mini` into `Apply Intelligently`, `Apply Manually`, or `Apply to Specific Files` rules by topic or path.
5. Use explicit skill invocation or `@rule-name` when you want on-demand application.
6. Keep large reference material in attached files or indexed docs, not in `Always Apply` rules.
7. Use root `AGENTS.md` only for simple projects or when you want a portable cross-tool baseline.
8. Use `nano` only when an always-on rule must be extremely short.

### Recommended version mapping

- `mini`: preferred skill body; also usable as a short `Always Apply` rule, simple root `AGENTS.md`, or `Apply Intelligently`, `Apply Manually`, and `Apply to Specific Files` project rules
- `nano`: compact fallback for very tight always-on rules
- `full`: reference only

### Recommended structure

```text
project/
  .agents/
    skills/
      refactoring/
        SKILL.md
  .cursor/
    skills/
      release-it/
        SKILL.md
    rules/
      base.mdc
      payments.mdc
      refactor.mdc
      ddd.mdc
```

Suggested split:

- `base.mdc`: one short `Always Apply` rule derived from `mini`, or from `nano` if the base must be tiny
- `payments.mdc`: `Apply to Specific Files` for `payments/**`
- `refactor.mdc`: `Apply Manually` for explicit refactoring passes
- `ddd.mdc`: `Apply Intelligently` for modeling-heavy tasks

### Use Cursor this way when

- you want strong scoping and explicit control over context
- you want different rules for different subsystems
- you want on-demand rule selection without a huge global file

### Avoid

- using one giant `Always Apply` rule
- treating root `AGENTS.md` as the best default for complex projects
- storing large reference packs in project rules when indexed docs are a better fit

## Decision Guide

- Need a task-specific book bias: create or invoke a skill from the relevant `mini` rule set.
- Need a steady repo-wide bias: use one `mini` rule set.
- Need an extremely small always-on baseline: use `nano`.
- Need stronger guidance for a specific task: load the relevant `mini` rule set as a skill or on-demand rule.
- Need a multi-step workflow: create a skill or command, with `full` as optional reference.
- Need subsystem-specific pressure: use scoped rules or nested files.
- Need long reference material: keep it out of always-on rules and use your editor's normal docs or indexing flow.
- Need more than one book: keep one primary always-on rule set and move the rest to on-demand mechanisms.
