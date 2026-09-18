# Full Directive

## 1. Purpose

Maintain durable context across conversations while keeping each interaction small and relevant.

Use a progressively discoverable hierarchy:

```text
Root
└── Domain
    └── Project
        └── supporting documents / artifacts
```

The system has two kinds of memory:

- **current context**: what is true now
- **semantic history**: materially important changes over time

Git history provides technical diffs and reversibility. It does **not** replace semantic history.

---

## 2. Core files

Every live Root, Domain, and Project has:

- `context.md` — authoritative current state
- `history.md` — material semantic events, newest first

Supporting documents may be added where useful.

Use stable lowercase snake_case filesystem paths. Human-facing names remain readable.

Relative Markdown links are canonical for internal references.

---

## 3. Progressive discovery

Every conversation begins with Root.

Then load only Domains and Projects likely to materially improve the task.

Do **not** load the whole repository by default.

Routing works top-down:

1. current user request
2. Root profile / global working rules
3. Root Active Context
4. Domain keywords + Domain agentic summary stored in Root
5. Project objective + keywords + Project agentic summary stored in its canonical Domain

If the user explicitly names a known Domain or Project, traverse directly to it after Root.

Multiple Domains or Projects may be loaded when genuinely relevant.

### Agentic-summary rule

An `agentic_summary` lives **one level above the thing it describes**:

- Root summarizes Domains
- Domain summarizes Projects
- Project does not summarize itself for routing

Agentic summaries are concise routing aids, not duplicate context.

---

## 4. Canonical ownership and authority

Authority order:

```text
Current user instruction
> Project
> canonical Domain
> related Domain
> Root
```

Each Project has:

- exactly one `canonical_domain`
- zero or more `related_domains`

A Project is listed canonically only beneath its canonical Domain.

Do not duplicate the same Project under related Domains.

Store the full fact at the most specific appropriate level.

Promote only materially useful summaries upward.

**Active context propagates upward by summarization, not duplication.**

---

## 5. Confidence and persistence

Evaluate two independent questions for new information:

1. **Fact confidence** — how sure are we that it is true?
2. **Persistence confidence** — how sure are we that it belongs in durable context at this location?

### VERY HIGH

Explicit fact, correction, confirmed decision, completed action, or unambiguous state transition.

Persist autonomously.

### HIGH

Strongly established information with clear persistent value and placement.

Persist autonomously.

### MEDIUM

Likely useful but permanence, meaning, or placement remains uncertain.

Ask before persisting.

### LOW

Uncertain or weakly useful.

Do not persist.

Explicit requests to remember, record, or update authorize persistence unless the target/meaning remains ambiguous.

Explicit unambiguous corrections replace conflicting current context automatically.

---

## 6. Mandatory automatic persistence

A **material HIGH+ change to durable state is a mandatory write trigger**.

It is not merely a reason to consider updating context.

When a material HIGH+ change becomes established, the agent must:

1. update the most specific relevant canonical context automatically;
2. do so without waiting for the user to request a context update;
3. update semantic history if the change meets the history threshold;
4. propagate only materially useful summaries to affected parent contexts;
5. finish the required persistence before treating the interaction or coherent work segment as complete.

Typical material triggers include:

- decisions
- corrections
- completed actions
- confirmed state transitions
- important new durable facts
- changed plans or constraints
- milestones
- material Next Action changes
- Open Question creation/resolution
- authoritative artifact changes
- major focus changes
- lifecycle changes

Closely related changes may be batched into one checkpoint to avoid noisy micro-commits.

Batching must not become indefinite deferral.

Flush accumulated material state at:

- natural stopping points
- topic shifts
- meaningful milestones
- likely conversation rollover/compression

A rough "10 substantive exchanges" rule may be used as a **backstop reassessment**, never as the normal maintenance trigger.

Routine automatic maintenance should normally be silent unless the user must resolve ambiguity/conflict.

---

## 7. Conflict and structural changes

If contexts conflict:

1. identify the conflict;
2. propose a resolution;
3. ask the user to decide.

Do not autonomously resolve genuine authority conflicts.

Normal content maintenance is autonomous at HIGH+ confidence.

Structural changes require explicit approval, including:

- creating a new Domain
- creating a structural child node outside established patterns
- splitting or merging Projects
- moving canonical ownership between Domains
- schema migrations
- substantial restructuring

New Projects may be created deliberately when an effort is likely to span multiple conversations/days or acts as an ongoing system.

One-off outputs are normally not Projects.

---

## 8. Root contract

Root is read every conversation.

Root contains only broadly useful, compressed context.

Required sections:

1. Purpose & Discovery
2. Profile
3. How to Work With Me
4. Active Context
5. Context Map
6. Context Maintenance Protocol
7. Recent Important Provenance

### Root Profile

Keep only durable facts likely to influence decisions across multiple Domains.

### Root Context Map

Contains:

- every Domain
- every Active Project, once under its canonical Domain

Each Domain entry contains:

- link
- keywords
- short agentic summary

Each Active Project entry contains:

- link
- objective
- related domains
- keywords

Inactive Projects are omitted from active Root routing.

---

## 9. Domain contract

A Domain is a durable broad area of work/life.

Domains do not have Active/Inactive lifecycle status.

Required sections:

1. Domain Purpose
2. Domain Context
3. How to Work in This Domain
4. Active Context
5. Projects
6. Recent Important Provenance

Optional:

- Related / Child Context
- Context Maintenance

The Projects section lists only **Active Projects canonically owned by that Domain**.

Each Project routing entry contains:

- link
- objective
- related domains
- keywords
- agentic summary

Do not create Domain-level Open Questions; those belong to Projects.

---

## 10. Project contract

A Project is substantial work likely to span multiple conversations/days, or an ongoing system requiring durable state.

Lifecycle:

- `Active`
- `Inactive`

Required metadata:

```yaml
schema_type: project
schema_version: 1
name: Project Name
last_material_update: YYYY-MM-DD
last_reviewed: YYYY-MM-DD
historical_log: ./history.md
canonical_domain: Domain Name
related_domains: []
status: Active
expected_completion: "Unknown"
objective: "Short statement of why this Project exists."
```

Required sections:

1. Project Overview
2. Current Context
3. How to Work in This Project
4. Active Context
5. Open Questions
6. Next Actions
7. Key Evidence & Conclusions
8. Artifacts & Authoritative Documents
9. Related Context
10. Recent Important Provenance

Keep required sections even when empty; use `None.`.

### Current Context

Authoritative current model of the Project.

Do not write it as a conversation transcript.

### Active Context

Volatile operational state needed for current or near-term decisions.

Project has the most detail; Domain and Root carry progressively compressed summaries.

Subjective or sentimental state belongs if it materially changes decisions.

### Open Questions

Only unresolved questions that materially affect Project work.

### Next Actions

Allowed states:

- Open
- In Progress
- Blocked

There is no Done state.

When an action completes:

- remove it from Next Actions
- update current state
- record completion in history if material

### Key Evidence & Conclusions

Curated evidence, durable conclusions, and decision-relevant findings.

Avoid turning this into a research dump.

### Artifacts & Authoritative Documents

For each important artifact record:

- name
- location
- purpose

Optional:

- authority
- notes

Artifacts may live outside the context repository if agents can access them.

---

## 11. Project lifecycle

When a Project becomes Inactive:

1. set `status: Inactive`;
2. finalize meaningful current state/outcome;
3. remove stale Active Context;
4. resolve/remove remaining Next Actions;
5. record closure in Project history;
6. remove it from the canonical Domain active Project list;
7. add a concise historical reference at Domain level where useful;
8. remove/update Root active routing;
9. update related contexts where materially affected;
10. preserve the full Project directory.

Inactive Projects remain discoverable historically but are omitted from active routing.

Reactivation normally reuses the same Project and records a new history event.

---

## 12. Semantic history

Every Root, Domain, and Project requires `history.md`.

History stores materially meaningful changes, not every edit.

Typical history events:

- creation / activation / reactivation / inactivation
- important decisions and reversals
- significant corrections
- major scope changes
- framework / operating-rule changes
- meaningful milestones
- major Next Action completion or abandonment
- material promotion/demotion/restructuring

Normally do **not** log:

- wording cleanup
- formatting
- minor Active Context churn
- routine metadata-date changes
- ordinary research refinement

History is prepend-only during normal operation:

- newest entries first
- previous entries immutable
- corrections are later entries
- explicit history repair may edit old entries

Example:

```markdown
### 2026-09-18T12:34:56+01:00 — Decision changed

- Previous approach replaced by ...
- Consequence: ...
```

Use the most accurate timestamp available; never invent precision.

`Recent Important Provenance` is a rolling live summary, not the canonical historical record.

---

## 13. Metadata and schemas

All managed Markdown documents use YAML frontmatter and are self-describing.

Common fields:

```yaml
schema_type: root|domain|project|historical_log|context_review|schema_definition
schema_version: 1
name: Human-readable name
last_material_update: YYYY-MM-DD
```

Live Root/Domain/Project additionally require:

```yaml
last_reviewed: YYYY-MM-DD
historical_log: ./history.md
```

Historical log example:

```yaml
schema_type: historical_log
schema_version: 1
name: Project Name History
last_material_update: YYYY-MM-DD
linked_schema: project
linked_name: Project Name
```

`last_material_update` changes after material writes.

`last_reviewed` changes only after an actual review.

Schema upgrades are never automatic:

1. identify mismatch;
2. explain migration;
3. obtain approval;
4. migrate after approval.

---

## 14. Writing conventions

Context should be:

- concise
- declarative
- current-state oriented
- structured with bullets where appropriate
- explicit about uncertainty
- free from conversational filler
- non-duplicative
- linked to deeper material instead of copying it

Prefer current truth over narrative.

Use history for the narrative of change.

---

## 15. Review

Maintain one global review procedure.

Suggested cadence:

- Active Project: opportunistically during sustained work
- Domain: roughly monthly or after major Project changes
- Root: roughly monthly
- full tree: roughly quarterly

Review hierarchically:

`Project → canonical Domain → affected related Domains → Root`

Check for:

- stale state
- bloat
- wrong-level information
- duplicated information
- conflicts
- facts that should be promoted/demoted
- inactive/completed Projects
- stale Open Questions
- stale Next Actions
- broken links
- stale routing keywords
- stale agentic summaries
- structural split/merge opportunities
- schema mismatch

Normal HIGH+ maintenance discovered during review may be applied automatically.

Conflicts require user resolution.

Structural changes require approval.

Report review results as:

- Updated
- Needs User Resolution
- Inspected — No Change

---

## 16. Git operating model

Normal HIGH+ context maintenance commits directly to the primary branch.

One semantic checkpoint should normally equal one Git commit containing all required updates across the hierarchy.

A checkpoint may touch:

`Project → canonical Domain → related Domains (if materially affected) → Root`

Branches/PRs are useful for:

- schema migrations
- major restructuring
- explicitly reviewed changes

Git history provides diffs and rollback.

Semantic `history.md` remains mandatory.

---

## 17. Minimal bootstrap behavior

At repository entry, agents should be told:

1. read Root first;
2. use progressive discovery;
3. do not load the entire repository;
4. read the schema when creating/restructuring/validating/migrating;
5. use semantic histories rather than reconstructing important history from Git;
6. automatically persist settled material HIGH+ durable-state changes;
7. batch coherent changes but flush at stopping points/topic changes/milestones/rollover.

---

## 18. Root template

```markdown
---
schema_type: root
schema_version: 1
name: Context
last_material_update: YYYY-MM-DD
last_reviewed: YYYY-MM-DD
historical_log: ./history.md
---

# Context

## Purpose & Discovery
None.

## Profile
None.

## How to Work With Me
None.

## Active Context
None.

## Context Map
None.

## Context Maintenance Protocol
None.

## Recent Important Provenance
None.
```

---

## 19. Domain template

```markdown
---
schema_type: domain
schema_version: 1
name: Domain Name
last_material_update: YYYY-MM-DD
last_reviewed: YYYY-MM-DD
historical_log: ./history.md
---

# Domain Name

## Domain Purpose
None.

## Domain Context
None.

## How to Work in This Domain
None.

## Active Context
None.

## Projects
None.

## Recent Important Provenance
None.
```

---

## 20. Project template

```markdown
---
schema_type: project
schema_version: 1
name: Project Name
last_material_update: YYYY-MM-DD
last_reviewed: YYYY-MM-DD
historical_log: ./history.md
canonical_domain: Domain Name
related_domains: []
status: Active
expected_completion: "Unknown"
objective: "Project objective."
---

# Project Name

## Project Overview
None.

## Current Context
None.

## How to Work in This Project
None.

## Active Context
None.

## Open Questions
None.

## Next Actions
None.

## Key Evidence & Conclusions
None.

## Artifacts & Authoritative Documents
None.

## Related Context
None.

## Recent Important Provenance
None.
```

---

## 21. History template

```markdown
---
schema_type: historical_log
schema_version: 1
name: Context Name History
last_material_update: YYYY-MM-DD
linked_schema: project
linked_name: Context Name
---

# Context Name History
```

---

## 22. Design principles

Prefer the simplest structure that preserves useful continuity.

Do not create metadata or categories merely because they might theoretically be useful.

Do not bulk-load or bulk-duplicate context.

Do not make users repeatedly ask agents to maintain state.

The central invariant is:

> **Context says what is true now. History says how it changed. Agents automatically keep both current whenever material durable state changes.**
