# OpenCode Skills

Reusable skill definitions for OpenCode, Codex, and other coding agents that support the open Agent Skills format.

Each skill is a small, task-specific instruction pack. Agents inspect the `SKILL.md` metadata, load the matching workflow when a request calls for it, and only pull in supporting references when they are needed.

## Included Skills

| Skill | Purpose |
| --- | --- |
| [`changelog`](changelog/SKILL.md) | Create, update, and review `CHANGELOG.md` files using Keep a Changelog and Semantic Versioning conventions. |
| [`create-readme`](create-readme/SKILL.md) | Create concise, useful project `README.md` files after reviewing the project structure and audience. |
| [`hero-generator-cli`](hero-generator-cli/SKILL.md) | Generate deterministic README banner PNGs with the published `hero-generator` CLI. |

## Quick Start

Install every skill for OpenCode:

```bash
npx -y skills add github.com/11philip22/skills -a opencode --skill '*'
```

Install every skill for Codex:

```bash
npx -y skills add github.com/11philip22/skills -a codex --skill '*'
```

Install the skills globally instead of into the current project:

```bash
npx -y skills add github.com/11philip22/skills -a opencode --global --skill '*'
```

> [!TIP]
> Use a project install when the skills should travel with one repository. Use `--global` when you want the same skills available across all projects on your machine.

## Install Individual Skills

Install only the changelog skill:

```bash
npx -y skills add github.com/11philip22/skills -a opencode --skill changelog
```

Install only the README skill:

```bash
npx -y skills add github.com/11philip22/skills -a opencode --skill create-readme
```

Install only the hero banner skill:

```bash
npx -y skills add github.com/11philip22/skills -a opencode --skill hero-generator-cli
```

Switch `-a opencode` to `-a codex` when installing for Codex.

## Repository Layout

```text
.
|-- changelog/
|   `-- SKILL.md
|-- create-readme/
|   `-- SKILL.md
|-- hero-generator-cli/
|   |-- SKILL.md
|   `-- references/
|       `-- cli-reference.md
`-- README.md
```

Each skill directory contains a `SKILL.md` file with frontmatter metadata and the main workflow. Optional `references/` files hold longer lookup material, command references, examples, or exact values that do not need to be loaded for every task.

## Authoring Guidelines

- Keep the frontmatter `name` stable and descriptive.
- Make the `description` specific enough for reliable skill selection.
- Put the primary workflow in `SKILL.md`.
- Move long tables, examples, and exact command references into `references/`.
- Keep instructions practical and task-focused.
- Avoid duplicating broad coding-agent behavior that belongs in system or project-level instructions.

## References

- [vercel-labs/skills](https://github.com/vercel-labs/skills)
- [mattpocock/skills](https://github.com/mattpocock/skills)
- [github/awesome-copilot skills](https://github.com/github/awesome-copilot/tree/main/skills)
- [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)
