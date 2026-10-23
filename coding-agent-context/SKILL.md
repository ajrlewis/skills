---
name: coding-agent-context
description: Create, reconcile, or refresh repository guidance for coding agents, including AGENTS.md, architecture, verified commands, workflow, context doctor checks, and session handoffs. Use for agent context setup and maintenance, not ordinary application implementation.
---

# Coding Agent Context

Build concise, project-specific context from repository evidence. Preserve useful existing guidance and keep unresolved work discoverable in one place.

## Choose the operation

- **Create or reconcile context:** read [references/discovery.md](references/discovery.md), then adapt the files in [assets/templates/](assets/templates/) into the target repository. Templates are writing aids; finish with project facts rather than scaffold prose.
- **Doctor or refresh installed context:** follow the target repository's `.agents/DOCTOR.md`. If it is absent, use [the doctor template](assets/templates/.agents/DOCTOR.md). Compare guidance with current evidence and repair within the requested scope; a report-only audit does not authorize edits.
- **Prepare a session:** read current context and specifications, then turn the user's selected objective into one bounded `.agents/sessions/ACTIVE.md`. Planning alone does not authorize implementation.

Read only relevant supporting material. [references/baselines.md](references/baselines.md) covers conditional tooling, quality, security, remote protection, tracking, and service checks. [references/catalog.md](references/catalog.md) routes optional technology and capability references. Preserve project policy over generic defaults.

## Durable output

Keep root `AGENTS.md` as concise rules and routing, and `CLAUDE.md` as a compatibility pointer while preserving any existing Claude-specific intent. The `.agents/` context contains:

- `WORKFLOW.md`: adopted development and delivery process.
- `COMMANDS.md`: exact commands, prerequisites, and verification status.
- `ARCHITECTURE.md`: current components, boundaries, and invariants.
- `DOCTOR.md`: context consistency and maintenance procedure.
- `SECURITY.md`: adopted vulnerability audit procedure.
- `sessions/ACTIVE.md`: one workspace-level implementation handoff, or an explicit statement that no objective is selected.
- `sessions/DEFERRED.md`: unresolved follow-ups and possible future sessions.
- `sessions/archive/`: completed briefs, retained as historical evidence.
- `presets/git/`: only the applicable, tailored Git workflow when needed.

Create project-specific skills or other routed documents only for a demonstrated durable need. Keep canonical guidance vendor-neutral. Do not install this skill's references or entire catalogue into the target repository.

## Prevent drift

Give each fact and work item one canonical home. Keep unresolved work in `sessions/DEFERRED.md` or the project's canonical issue tracker; never mirror tracker backlogs. Do not create `sessions/future/`, competing handoffs, or TODO lists in architecture, workflow, commands, or archived briefs. Link to canonical items when context needs them.

At completion or refresh, remove resolved deferred items, merge duplicates, update stale assumptions, and consolidate scattered follow-ups without losing intent. Ordinary code comments need not become work items. Move durable facts out of session briefs into their canonical documentation.

Archive completed active briefs with a concise outcome and verification evidence. Replace `ACTIVE.md` with the next explicitly selected objective or the no-objective state. Deferred and archived work never implicitly authorizes implementation. Current code and specifications take precedence over stale briefs.

## Scope and completion

This skill changes agent context. It does not implicitly authorize application scaffolding, dependency or host-tool installation, external service connections, remote policy changes, publishing, or implementation of a backlog. Use available evidence before asking about meaningful policy conflicts.

Edit existing context in place after inspecting it. Do not run the old bootstrap installers, install `BOOTSTRAP.md`, create migration scaffolding, initialize Git, or change branches solely to write context. If legacy migration input already exists, reconcile it before proposing cleanup; never delete unrelated files.

Verify documented commands where practical and safe. Mark commands that could not be verified and explain why. Check routing, preserved project intent, lack of duplicate work queues, and the final diff. Report the files changed, checks actually run, and unresolved gaps. Installation of the skill alone does not configure a repository; the agent must perform this workflow.
