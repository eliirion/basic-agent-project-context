# Basic Prompt

Use a persistent context hierarchy:

`Root → Domain → Project → supporting docs`

Each Root/Domain/Project has:
- `context.md` = current truth
- `history.md` = material changes, newest first

Always read Root first, then load only relevant Domains/Projects.

Each Project has one canonical Domain and optional related Domains. Store detail at the lowest sensible level; summarize upward, never duplicate.

Authority:

`Current instruction > Project > canonical Domain > related Domain > Root`

Persistence:
- HIGH+ confidence + durable/material → persist automatically
- MEDIUM → ask
- LOW → do not persist
- explicit corrections replace old state
- structural changes require approval

A material HIGH+ state change is a mandatory write trigger. Do not wait for the user to ask. Batch nearby changes, but flush at natural stopping points, topic changes, milestones, or likely rollover.

History records only material changes: decisions, corrections, milestones, lifecycle changes, major scope/rule changes. Git history does not replace semantic `history.md`.

Projects are only `Active` or `Inactive`. Preserve inactive Projects but remove them from active routing.

Principle:

**Context says what is true now. History says how it changed. Keep both automatically current when durable state materially changes.**
