[![Polish Repo badge](https://polish-open-source.pl/en/badges/repositories/github/ciembor/agent-rules-books.svg)](https://polish-open-source.pl/en/latest)

<div align="center">
  <img src="books-ai-rules.png" alt="AI agent rules from programming books" />
  <h1 align="center">AI agents Rules / Skills from<br />Programming Books v0.5</h1>

  <p align="center">
    <strong>AGENTS.md rules</strong> / <strong>skills</strong> for <strong>Codex</strong>, <strong>Autohand Code</strong>, <strong>Cursor</strong>, <strong>Claude Code</strong>, distilled from classic <strong>software engineering books</strong> about refactoring, architecture, DDD and code quality.
  </p>

  <p align="center">
    <a href="#about">About</a>
    ·
    <a href="#release-matrix">Rules / Skills</a>
    ·
    <a href="#books-list">Books List</a>
    ·
    <a href="docs/USAGE.md">Usage</a>
    ·
    <a href="docs/COMPATIBILITY.md">Books Compatibility</a>
  </p>
</div>

## About
MIT licensed universal project rules for coding agents.

This repository contains ready-to-use rule sets inspired by well-known books on software design, architecture, refactoring, legacy code, reliability, and data-intensive systems.

For editor-specific setup in Codex, Autohand Code, Claude Code, and Cursor, see [USAGE.md](docs/USAGE.md). It covers always-on vs on-demand usage, skills, scoped rules, MCP or RAG patterns, and the preferred setup for each editor.

Each rule set is released in three tool-agnostic Markdown versions:

- `mini`: the recommended version for most real task use
- `nano`: the compact fallback for very tight context budgets
- `full`: the canonical complete source and reference version

For constructive criticism from Reddit, see [CRITICISM.md](docs/CRITICISM.md).

For release history, see [CHANGELOG.md](CHANGELOG.md).

## Release Matrix

Metrics:

- `lines`: physical line count from `wc -l`
- `rules`: Markdown list items counted with the deterministic release convention
- `size`: raw bytes from `wc -c`

| Rule Set | Full file | Full lines | Full rules | Full size | Mini file | Mini lines | Mini rules | Mini size | Nano file | Nano lines | Nano rules | Nano size |
| --- | --- | ---: | ---: | ---: | --- | ---: | ---: | ---: | --- | ---: | ---: | ---: |
| [A Philosophy of Software Design](a-philosophy-of-software-design/) | [full](a-philosophy-of-software-design/a-philosophy-of-software-design.md) | 370 | 177 | 13561 B | [mini](a-philosophy-of-software-design/a-philosophy-of-software-design.mini.md) | 46 | 28 | 5774 B | [nano](a-philosophy-of-software-design/a-philosophy-of-software-design.nano.md) | 35 | 17 | 2258 B |
| [Clean Architecture](clean-architecture/) | [full](clean-architecture/clean-architecture.md) | 515 | 289 | 17782 B | [mini](clean-architecture/clean-architecture.mini.md) | 49 | 31 | 5486 B | [nano](clean-architecture/clean-architecture.nano.md) | 36 | 18 | 2254 B |
| [Clean Code](clean-code/) | [full](clean-code/clean-code.md) | 297 | 220 | 13851 B | [mini](clean-code/clean-code.mini.md) | 47 | 29 | 3804 B | [nano](clean-code/clean-code.nano.md) | 32 | 14 | 1235 B |
| [Code Complete](code-complete/) | [full](code-complete/code-complete.md) | 354 | 180 | 12407 B | [mini](code-complete/code-complete.mini.md) | 56 | 38 | 6717 B | [nano](code-complete/code-complete.nano.md) | 41 | 23 | 2544 B |
| [Designing Data-Intensive Applications](designing-data-intensive-applications/) | [full](designing-data-intensive-applications/designing-data-intensive-applications.md) | 393 | 205 | 16084 B | [mini](designing-data-intensive-applications/designing-data-intensive-applications.mini.md) | 55 | 37 | 6949 B | [nano](designing-data-intensive-applications/designing-data-intensive-applications.nano.md) | 34 | 16 | 2575 B |
| [Domain-Driven Design](domain-driven-design/) | [full](domain-driven-design/domain-driven-design.md) | 979 | 523 | 42424 B | [mini](domain-driven-design/domain-driven-design.mini.md) | 48 | 30 | 5683 B | [nano](domain-driven-design/domain-driven-design.nano.md) | 39 | 21 | 2266 B |
| [Domain-Driven Design Distilled](domain-driven-design-distilled/) | [full](domain-driven-design-distilled/domain-driven-design-distilled.md) | 317 | 158 | 11351 B | [mini](domain-driven-design-distilled/domain-driven-design-distilled.mini.md) | 56 | 38 | 6438 B | [nano](domain-driven-design-distilled/domain-driven-design-distilled.nano.md) | 41 | 23 | 2535 B |
| [Implementing Domain-Driven Design](implementing-domain-driven-design/) | [full](implementing-domain-driven-design/implementing-domain-driven-design.md) | 337 | 177 | 12848 B | [mini](implementing-domain-driven-design/implementing-domain-driven-design.mini.md) | 57 | 39 | 7333 B | [nano](implementing-domain-driven-design/implementing-domain-driven-design.nano.md) | 37 | 19 | 2723 B |
| [Patterns of Enterprise Application Architecture](patterns-of-enterprise-application-architecture/) | [full](patterns-of-enterprise-application-architecture/patterns-of-enterprise-application-architecture.md) | 404 | 196 | 15501 B | [mini](patterns-of-enterprise-application-architecture/patterns-of-enterprise-application-architecture.mini.md) | 54 | 36 | 8099 B | [nano](patterns-of-enterprise-application-architecture/patterns-of-enterprise-application-architecture.nano.md) | 35 | 17 | 2823 B |
| [Refactoring](refactoring/) | [full](refactoring/refactoring.md) | 433 | 242 | 17866 B | [mini](refactoring/refactoring.mini.md) | 49 | 31 | 5167 B | [nano](refactoring/refactoring.nano.md) | 37 | 19 | 1986 B |
| [Release It!](release-it/) | [full](release-it/release-it.md) | 382 | 204 | 13542 B | [mini](release-it/release-it.mini.md) | 48 | 30 | 6372 B | [nano](release-it/release-it.nano.md) | 38 | 20 | 2205 B |
| [The Pragmatic Programmer](the-pragmatic-programmer/) | [full](the-pragmatic-programmer/the-pragmatic-programmer.md) | 359 | 179 | 13398 B | [mini](the-pragmatic-programmer/the-pragmatic-programmer.mini.md) | 65 | 47 | 7165 B | [nano](the-pragmatic-programmer/the-pragmatic-programmer.nano.md) | 44 | 26 | 2263 B |
| [Working Effectively with Legacy Code](working-effectively-with-legacy-code/) | [full](working-effectively-with-legacy-code/working-effectively-with-legacy-code.md) | 371 | 193 | 13817 B | [mini](working-effectively-with-legacy-code/working-effectively-with-legacy-code.mini.md) | 50 | 32 | 5707 B | [nano](working-effectively-with-legacy-code/working-effectively-with-legacy-code.nano.md) | 35 | 17 | 1792 B |
| [Refactoring.Guru](refactoring-guru/) | [full](refactoring-guru/refactoring-guru.md) | 765 | 478 | 62561 B | [mini](refactoring-guru/refactoring-guru.mini.md) | 64 | 46 | 6287 B | [nano](refactoring-guru/refactoring-guru.nano.md) | 41 | 23 | 2593 B |

## Books List

### [A Philosophy of Software Design](https://www.goodreads.com/book/show/39996759-a-philosophy-of-software-design)

Author: [John Ousterhout](https://web.stanford.edu/~ouster/cgi-bin/home.php)

The book focuses on fighting complexity through deep modules, simple interfaces, information hiding, and design choices that reduce cognitive load. This rule set is especially useful for API design, module design, and refactoring shallow abstractions.

### [Clean Architecture](https://www.goodreads.com/book/show/18043011-clean-architecture)

Author: [Robert C. Martin](https://cleancoder.com/)

The book describes designing systems around stable boundaries, the dependency rule, and the separation of business policies from details such as frameworks, databases, and UI. This rule set helps keep code resistant to technology churn.

### [Clean Code](https://www.goodreads.com/book/show/3735293-clean-code)

Author: [Robert C. Martin](https://cleancoder.com/)

The book focuses on readability, naming, small functions, responsibilities, tests, and simplicity. This rule set is a strong default for everyday coding and code review.

### [Code Complete](https://www.goodreads.com/book/show/4845.Code_Complete)

Author: [Steve McConnell](https://www.construx.com/about-us/our-experts/steve-mcconnell/)

The book covers a broad range of software construction practices: routine design, variables, classes, control flow, defensive programming, coding standards, and testing. This rule set helps agents make disciplined implementation decisions.

### [Designing Data-Intensive Applications](https://www.goodreads.com/book/show/23463279-designing-data-intensive-applications)

Author: [Martin Kleppmann](https://martin.kleppmann.com/)

The book covers reliability, scalability, consistency, replication, partitioning, transactions, data streams, and schema evolution. This rule set is intended for systems where data ownership, event flows, and consistency semantics matter.

### [Domain-Driven Design](https://www.goodreads.com/en/book/show/179133)

Author: [Eric Evans](https://domainlanguage.com/)

The book introduces domain modeling, ubiquitous language, bounded contexts, tactical patterns, and strategic design. This rule set helps agents think in terms of the business model rather than tables, controllers, or DTOs.

### [Domain-Driven Design Distilled](https://www.goodreads.com/book/show/28602719-domain-driven-design-distilled)

Author: [Vaughn Vernon](https://vaughnvernon.com/)

The book is a short, practical introduction to DDD. It focuses on subdomains, bounded contexts, context mapping, and basic tactical patterns. This rule set is a good fit when you want the benefits of DDD without excessive ceremony.

### [Implementing Domain-Driven Design](https://www.goodreads.com/book/show/18396266-implementing-domain-driven-design)

Author: [Vaughn Vernon](https://vaughnvernon.com/)

The book shows how to apply DDD in real systems: aggregates, domain events, contexts, integrations, and application architecture. This rule set is more implementation-focused than `domain-driven-design-distilled`.

### [Patterns of Enterprise Application Architecture](https://www.goodreads.com/en/book/show/70156.Patterns_of_Enterprise_Application_Architecture)

Author: [Martin Fowler](https://martinfowler.com/)

The book catalogues enterprise application patterns: layers, service layer, transaction script, domain model, data mapper, repository, unit of work, identity map, DTO, and integration patterns. This rule set helps choose an appropriate pattern instead of mixing responsibilities accidentally.

### [Refactoring](https://www.goodreads.com/book/show/44936.Refactoring)

Author: [Martin Fowler](https://martinfowler.com/)

The book describes safe ways to improve code structure without changing observable behavior. This rule set emphasizes small steps, tests, code smell detection, and keeping refactoring separate from feature changes.

### [Refactoring.Guru](https://refactoring.guru/refactoring)

Source: [Refactoring.Guru](https://refactoring.guru/)

The site provides a practical refactoring process, code smell catalog, and catalog of refactoring techniques. This rule set is useful when an agent needs to diagnose smells, choose a safe treatment, preserve behavior, and stop before cleanup turns into uncontrolled redesign.

### [Release It!](https://www.goodreads.com/en/book/show/1069827.Release_It_)

Author: [Michael T. Nygard](https://www.michaelnygard.com/)

The book focuses on systems that survive production reality: failures, overload, timeouts, retries, circuit breakers, bulkheads, backpressure, observability, and deployment behavior. This rule set is useful for services, APIs, queues, integrations, and critical production paths.

### [The Pragmatic Programmer](https://www.goodreads.com/book/show/50701156)

Authors: [Andrew Hunt](https://toolshed.com/), [David Thomas](https://pragdave.me/)

The book describes a pragmatic approach to software development: responsibility, DRY at the knowledge level, orthogonality, automation, fast feedback, prototyping, and adaptability. This rule set works well as a general engineering layer.

### [Working Effectively with Legacy Code](https://www.goodreads.com/book/show/44919.Working_Effectively_with_Legacy_Code)

Author: [Michael Feathers](https://www.r7krecon.com/)

The book explains how to safely change difficult, poorly tested code: characterization tests, seams, dependency breaking, sprout method, wrap method, and incremental risk reduction. This rule set is best for legacy work where the first goal is regaining control.

For choosing rule sets, skills, and delivery patterns, see [USAGE.md](docs/USAGE.md). For combining multiple books, see [COMPATIBILITY.md](docs/COMPATIBILITY.md). For the book extraction workflow, see [ADDING_THE_BOOK.md](docs/ADDING_THE_BOOK.md).

## Does it work?
The first validation experiment used [vibe-coded-crap](https://github.com/ciembor/vibe-coded-crap), a deliberately generated helpdesk CLI project. The project as vibe-coded application generated with Codex, GPT-5.4 mini, reasoning medium, through continuous development across 80 tasks from `BACKLOG.md`. The project exists specifically for testing different `AGENTS.md` files and skills in refactoring workflows.

The experiment compared two separate refactors of the same application, both focused on [A Philosophy of Software Design](a-philosophy-of-software-design/):

- [`aposd-refactor-mini-rules`](https://github.com/ciembor/vibe-coded-crap/tree/aposd-refactor-mini-rules), using the `mini` rules from this repository.
- [`aposd-refactor-no-rules`](https://github.com/ciembor/vibe-coded-crap/tree/aposd-refactor-no-rules), using only this single `AGENTS.md` instruction:

```md
# OBEY A Philosophy of Software Design by John Ousterhout
```

For each branch, Codex first generated a `PLAN.md` refactoring plan with GPT-5.5, reasoning extra high. The full plan was then executed with the same model, reasoning high. The resulting codebases were passed to ChatGPT with the prompt: “which code better implements the principles from A Philosophy of Software Design, and by how much?”

**ChatGPT rated the mini rules refactor at roughly 74/100, versus 46/100 for the branch that only mentioned the book**. The result suggests that listing concrete rules from the book is more effective than merely naming the book when the goal is to make an agent apply the author's design principles during refactoring.

The result should be treated as an early qualitative signal, not a benchmark. A secondary Reek code-smell check showed only a small difference in generic static-analysis output: the original branch had 1083 detected smells, while the mini refactor had 1077. This suggests that the advantage of the mini rules did not show up clearly in raw smell counts. In this experiment, the difference was more visible in architectural judgment: module depth, responsibility boundaries, information hiding, and whether the refactor reduced the amount of code a reader needs to understand at once.

Deeper measurements and equivalent experiments for other books are not planned at this stage because they would require substantial token budget and a large amount of manual review time.

## Important Note

These rules are inspired by the books listed above. They are not official materials from the authors or publishers, and they are not a substitute for reading the books.

The files in this repository are practical engineering instructions written for AI coding tools. They intentionally avoid reproducing book text. Use them as lightweight working agreements, not as summaries or study notes.

## FAQ

### What are AI coding agent rules?

AI coding agent rules are project-level instructions that guide tools like Codex, Cursor, Claude Code, and GitHub Copilot when generating, reviewing, or refactoring code.

### What are AI coding agent skills?

AI coding agent skills are task-specific instruction packs that agents load only when a workflow needs them, such as refactoring, reviewing, legacy-code changes, reliability work, or domain modeling.

### What is AGENTS.md?

AGENTS.md is a Markdown file used to give coding agents project-specific instructions, workflows, constraints, and coding standards.

### Can I use these as Claude Code rules or skills?

Yes. You can copy selected rule sets into `CLAUDE.md` as project memory or turn a focused `mini` rule set into a Claude Code skill.

### Can I use these as Cursor rules?

Yes. You can adapt the rule sets into Cursor project rules or keep them as AGENTS.md-style instructions.

### Can I use these as GitHub Copilot custom instructions or skills?

Yes. The rules and skills are plain Markdown and can be adapted into GitHub Copilot custom instructions, prompt files, or reusable task-specific guidance.

## Related searches

**AI coding agent rules**, **Agent skills**, **AGENTS.md** examples, Claude Code rules, Cursor rules, Codex rules, GitHub Copilot custom instructions, **CLAUDE.md**, software engineering **rules for AI coding** assistants, Clean Code rules for AI, **Refactoring** rules for AI agents, **Domain-Driven Design rules**, Clean **Architecture rules**.

## License

The code and rules in this repository are released under the MIT License.

See [LICENSE](LICENSE) for details.

## Author

[Maciej Ciemborowicz](https://maciej-ciemborowicz.eu)
