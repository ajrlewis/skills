# Skills

Reusable skills for coding agents.

## coding-agent-context

Create, reconcile, and refresh repository agent guidance: `AGENTS.md`, architecture, verified commands, workflow, doctor and security procedures, and session handoffs. Keep future work in one discoverable place instead of scattering TODO backlogs through context files.

Install using the [skills CLI](https://skills.sh/docs):

```sh
npx skills add ajrlewis/skills --skill coding-agent-context
```

Then ask your agent:

```text
Use coding-agent-context to set up agent guidance for this repository.
```

For existing context:

```text
Use coding-agent-context to doctor and refresh this repository's agent guidance.
```

Installation makes the skill available. The agent then inspects the repository and reconciles its context; existing project-specific guidance is preserved.
