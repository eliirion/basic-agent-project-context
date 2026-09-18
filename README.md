# Basic Agent Project Context

A small, reusable pattern for giving AI agents durable context without loading everything into every conversation.

The core hierarchy is:

`Root → Domain → Project → supporting docs`

The model separates **current truth** from **semantic history**, uses progressive discovery, and requires agents to persist material high-confidence state changes automatically rather than waiting to be reminded.

## Files

- [BASIC_PROMPT.md](BASIC_PROMPT.md) — the shortest usable operating prompt.
- [INTERVIEW_PROMPT.md](INTERVIEW_PROMPT.md) — a short prompt for deriving a context system interactively in a new environment.
- [FULL_DIRECTIVE.md](FULL_DIRECTIVE.md) — the complete abstract specification: hierarchy, schemas, discovery, authority, persistence, history, lifecycle, review, Git behavior, and templates.

## How to use it

Use **BASIC_PROMPT** when the structure already exists and you mainly need to tell an agent how to work with it.

Use **INTERVIEW_PROMPT** when starting from scratch. Let the agent interview you in small steps to discover appropriate Domains, Projects, rules, and initial content.

Use **FULL_DIRECTIVE** when you want the complete operating model to be explicit and reproducible.

The repository intentionally contains no personal or organization-specific context. Adapt it locally.
