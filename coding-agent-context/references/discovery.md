# Discover and Reconcile Repository Context

## Inspect before editing

Read existing root and nested agent guidance and discover vendor-specific instructions, contributor docs, skills, and handoffs. Inspect manifests, lockfiles, task runners, CI, representative source and tests, migrations, deployment configuration, product specifications, and useful Git history. Do not execute arbitrary setup scripts merely to discover commands.

Distinguish implemented facts, maintainer-declared requirements, and derived conclusions. A README-only project may declare architecture and acceptance criteria without implementing them. Keep its README as the product specification, label planned components accurately, and do not invent verified commands.

Identify existing workflow, stack, repository topology, architecture, data flows, external capabilities, recurring procedures, verification, and security conventions. Ask only for material unknowns or conflicting policies that evidence cannot resolve.

## Reconcile existing guidance

Preserve project-specific intent, including rules in agent-specific files. Resolve compatible duplication by moving facts into their natural home and routing to them. Do not silently choose between conflicting policies. Existing conventions take precedence over bundled presets.

If `.coding-agent-bootstrap/existing/` already exists from a previous installation, inspect it as recoverable migration input. Preserve unresolved requirements before any cleanup. Do not create fresh migration state or rerun an installer.

Inspect legacy handoffs such as `NEXT_SESSION.md`, `DEFERRED_SESSION.md`, product-local active files, and future-session folders. Reconcile their meaning against current code and specifications. Preserve unfinished intent, archive completed briefs, and consolidate unselected work into `DEFERRED.md` or its canonical tracker. Do not mechanically delete legacy files or infer a priority from their existence.

## Write project-specific context

Use [the templates](../assets/templates/) as source material, not files to overwrite existing guidance wholesale. Rewrite the workflow, command, and architecture writing aids into concise project facts. Tailor doctor and security procedures to adopted tools and policy. Keep useful existing rules in `AGENTS.md`; ensure every routed path exists.

Keep a single workspace-level `ACTIVE.md`, including in monorepos. Nested `AGENTS.md` files may add local rules but do not introduce separate active queues. Unless the maintainer has selected an implementation objective, use the no-objective state. Record only genuine unresolved follow-ups; do not fill deferred work with speculative improvements.

Read relevant [baseline checks](baselines.md) after discovering the project's adopted workflows. Prefer existing Git policy. If none exists, use the Git preset matching the remote host, tailoring all default-branch names and commands. For other hosts, derive guidance from actual conventions rather than forcing GitHub or Azure policy.

Consult [the catalogue](catalog.md) only for technologies and capabilities the project actually uses. Templates do not authorize connecting services, installing tools, or changing remote settings. Document capability boundaries in architecture or workflow rather than copying generic integration definitions by default.

## Validate and finish

- Validate documented commands when practical and safe; distinguish verified results, discovered invocations, and unavailable checks. Do not execute deployments, database mutations, or other external writes merely to verify documentation.
- Check that architecture and workflow describe current facts, with requirements and unverified assumptions explicitly identified.
- Confirm one active handoff, one home per unresolved item, no `sessions/future/`, no hidden TODO backlogs, and no duplicated tracker content.
- Check all routes, links, selected presets, and directory contents. Do not leave writing aids, unused preset directories, bootstrap-only instructions, or unsupported version markers in the generated context.
- Review the diff for lost existing intent and unintended changes. Report verification and unresolved gaps. Configuration completion is not application implementation completion.
