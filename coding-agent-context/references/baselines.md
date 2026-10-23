# Conditional Setup Checks

Read only the sections relevant to the repository: GitHub or Azure protection, external tracking, service boundaries, host tooling, quality, and security. These checks document adopted workflows; changes beyond agent documentation require their own authorization.

## GitHub Flow Protection

When the repository adopts GitHub Flow:

1. Detect whether `origin` is hosted on GitHub and identify the remote default branch instead of assuming it is named `main`.
2. Inspect the default branch's current GitHub ruleset or branch protection through an authenticated GitHub API client when access is available.
3. For a shared repository, require pull requests with at least one approving review, enforce the rule for administrators, and block force pushes and branch deletion. These settings must prevent direct pushes to the default branch.
4. In a solo repository, surface that authors cannot approve their own pull requests and ask the maintainer whether to require an external approval. Still require pull requests and prevent direct and force pushes unless the maintainer explicitly adopts another policy.
5. Obtain explicit maintainer authorization before creating or changing remote repository settings. Local workflow instructions do not by themselves authorize an external mutation.
6. Verify the effective settings after any change. If authentication, repository administration permission, or supported GitHub access is unavailable, record the unresolved protection work in `.agents/sessions/DEFERRED.md`, report it clearly, and do not claim remote protection was configured.

Do not add GitHub CLI or another provider SDK as a project dependency solely for this check. Remote protection belongs to the agent-led context setup procedure, not the mechanical file installer.

## Azure Repos Protection

When the repository is hosted in Azure Repos:

1. Identify the Azure DevOps organization, project, repository, and actual remote default branch instead of assuming it is named `main`.
2. Adopt and tailor `.agents/presets/git/azure-devops.md`. Verify existing Azure CLI and `azure-devops` extension availability before using its commands; do not install or update host tooling without authorization.
3. Inspect effective branch policies with `az repos policy list` when authenticated Azure DevOps Services access is available. Azure DevOps Server does not support these CLI commands, so use its supported administration interface instead.
4. For shared repositories, require pull requests, at least one approving reviewer, comment resolution, and successful build validation when relevant pipelines exist. Do not count the author's vote unless project policy explicitly permits it.
5. Inspect branch security as well as policies. Do not grant ordinary contributors `Bypass policies when pushing` or `Force push`, which also controls branch deletion; restrict all policy-bypass permissions to explicitly authorized administrators while preserving normal pull-request contribution access.
6. Obtain explicit maintainer authorization before changing remote policies or permissions, then verify the effective result. If authentication, administration permission, or suitable tooling is unavailable, record the unresolved protection work in `.agents/sessions/DEFERRED.md`, report it clearly, and do not claim the branch is protected.

Do not add Azure CLI or its extension as a project dependency solely for this check. Remote protection belongs to the agent-led context setup procedure, not the mechanical file installer.

## External Work Tracking

When Linear or another external tracker is the canonical backlog:

1. Inspect existing contributor guidance, integrations, issue identifiers in branch or pull-request history, and available external capabilities before asking how work is tracked.
2. Keep the external tracker as the single source of truth. Do not copy its backlog or issue bodies into `.agents/sessions/DEFERRED.md` or create another durable mirror in the repository.
3. Document the adopted tracker and required access boundary in `.agents/WORKFLOW.md`. Grant the narrowest workspace, team, project, and write access that supports the adopted workflow.
4. Document the issue-to-branch-to-pull-request lifecycle in `.agents/WORKFLOW.md`, including actual status transitions and any existing automation.
5. Use one branch per work item by default and include its stable identifier. Choose the branch prefix from the change type, such as `feature/ENG-123-add-export`, `fix/ENG-124-handle-empty-response`, or `chore/ENG-125-update-dependencies`; do not classify every tracked item as a chore.
6. Fetch current work-item details through the configured capability before implementation. Link the pull request to the canonical item and update external state only when the corresponding work actually begins or completes.
7. Preserve existing tracker-to-Git automation instead of producing duplicate status changes or comments. Ask the maintainer only when the canonical tracker, state mapping, or mutation authority remains unclear.

## External Service Boundaries

When the project adopts hosted secrets, deployment, data, or documentation services:

1. Inspect repository configuration, existing integrations, deployment history, and available external capabilities before asking which services are authoritative.
2. Identify the canonical source for each kind of state. Keep code, migrations, deployment configuration, and docs-as-code in the repository unless the project explicitly establishes another source.
3. If Doppler is the canonical secret manager, document its outbound syncs and avoid separately managed copies in Vercel, Supabase, CI, or other destinations.
4. Document service relationships and environment boundaries in `.agents/ARCHITECTURE.md`; put exact verified local or CI commands in `.agents/COMMANDS.md`.
5. Document adopted capabilities and least-privilege boundaries in `.agents/ARCHITECTURE.md` or `.agents/WORKFLOW.md`. Do not store credentials or silently install host integrations.
6. Prefer project-scoped, read-only, development access for inspection. Require explicit authorization for secret writes, deployments, production access, database mutations, domain changes, or authenticated documentation edits.
7. Verify external changes through the provider after making them. If access or permission is unavailable, report the limitation and record genuine unresolved setup work in `.agents/sessions/DEFERRED.md`.

## Tooling And Host Capabilities

Reconcile tools only after determining which project workflows and external capabilities the target actually adopts:

1. Inspect manifests, lockfiles, task runners, version-manager files, container configuration, CI, existing setup docs, and available host tools before proposing installation.
2. Separate installer prerequisites, project command dependencies, provider CLIs, local MCP runtimes, and remote MCP connections. A remote OAuth MCP server does not imply that its provider CLI must be installed.
3. Verify each required executable with a non-mutating lookup and version command, using `command -v` on POSIX systems or `Get-Command` on PowerShell where appropriate.
4. Prefer repository-pinned development dependencies and existing tool managers over global installations. Preserve the project's package manager and lockfile rather than introducing another one for a CLI.
5. Document only adopted, verified invocations and version constraints in `.agents/COMMANDS.md`. Keep host-specific MCP configuration outside repository context unless the project deliberately owns it.
6. Do not install Homebrew, a language runtime, global npm packages, provider CLIs, credentials, or user-level MCP configuration without explicit authorization. Do not treat the presence of a capability template as authorization to connect it.
7. If a required project command cannot run because a tool or authenticated capability is unavailable, report the exact gap and record genuine unresolved setup work in `.agents/sessions/DEFERRED.md`. Do not claim the command or integration was verified.

## Quality Baseline

Context setup must account explicitly for the repository's behavior verification and static checks. Do not treat a missing test, lint, format, typecheck, or build command as evidence that it is unnecessary.

1. Inspect package scripts, dependency manifests, tool configuration, source layout, CI workflows, representative tests, coverage configuration, and API documentation conventions.
2. Identify the smallest appropriate baseline. Application, service, and library code normally need typed callable contracts, useful public API documentation, focused unit tests, boundary integration tests, coverage reporting, and relevant static checks. Documentation, configuration, generated-code, or similarly specialized repositories may use build, schema, link, integration, or other focused validation instead of unit tests.
3. Preserve established tools and conventions. Do not introduce a second toolchain for a check the repository already performs.
4. If a necessary category is absent, surface it as a material context setup decision. Obtain maintainer approval before adding dependencies, configuration, CI workflows, or representative tests.
5. When approved, establish the minimum ecosystem-native baseline and define focused, unit, integration, coverage, fast, and full verification in `.agents/COMMANDS.md` as applicable.
6. Set a high, repository-appropriate coverage expectation and prioritize changed code, branch behavior, and important failure paths. Do not optimize for a percentage while leaving meaningful behavior untested.
7. Run each documented command before recording it as known-good. Add stable baseline checks to CI and required-check guidance in proportion to repository risk.
8. If documentation or a check is intentionally absent or cannot yet be added, document the rationale and record actionable unresolved work in `.agents/sessions/DEFERRED.md`. Do not silently omit it or claim the baseline is complete.

## Security Baseline

Context setup must establish how the target repository checks third-party components and first-party code for vulnerabilities. Use `.agents/SECURITY.md` as the durable audit procedure.

1. Inventory manifests, lockfiles, container definitions, infrastructure configuration, existing security tools, hosted scanners, dependency-update automation, CI checks, and security policy documentation.
2. Prefer existing ecosystem-native or repository-pinned tools. Do not add a scanner, hosted service, source upload, credential, or CI integration without maintainer authorization.
3. Identify commands that inspect resolved direct and transitive dependency versions against current advisories, plus applicable static code, secret, container, and infrastructure checks. Record only adopted, verified commands in `.agents/COMMANDS.md`.
4. Agree on severity and release thresholds appropriate to the project. Propose no known exploitable critical or high findings as the default release baseline, with explicit triage for medium and low findings, but do not silently turn that proposal into policy.
5. Decide where unresolved findings are tracked, how accepted risks are documented and revisited, and which checks should block CI. Preserve an existing canonical security workflow when one exists.
6. If a necessary category is unavailable or cannot be verified, state the coverage gap and record actionable setup work in `.agents/sessions/DEFERRED.md`; do not equate a missing or incomplete scan with safety.
