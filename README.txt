OpenCode Skills
===============

Reusable skill definitions for OpenCode and Codex-style coding agents. Each
skill is a small, task-specific instruction pack that helps the agent choose the
right workflow, constraints, and supporting references for a request.

Included Skills
---------------

- `changelog/` - Create, update, and review `CHANGELOG.md` files using Keep a
  Changelog and Semantic Versioning conventions.
- `create-readme/` - Create concise, useful project `README.md` files after
  reviewing the project structure and audience.
- `hero-generator-cli/` - Generate deterministic README banner PNGs with the
  published `hero-generator` CLI.

Repository Layout
-----------------

Each skill lives in its own directory:

  skill-name/
    SKILL.md
    references/

`SKILL.md` is the main instruction document. Optional `references/` files hold
longer lookup material, command references, examples, or exact values that do
not need to be loaded for every task.

Current structure:

- `changelog/SKILL.md`
- `create-readme/SKILL.md`
- `hero-generator-cli/SKILL.md`
- `hero-generator-cli/references/cli-reference.md`

Install
-------

Put this repository, or a symlink to it, in your OpenCode skills directory:

```bash
ln -s /path/to/this/repo ~/.config/opencode/skills
```

If you use a different agent or runtime, point its skills configuration at this
repository or copy the individual skill directories into the location it scans.

How Skills Are Loaded
---------------------

OpenCode reads the available skill directories, inspects each `SKILL.md`, and
loads a skill when the user's task matches its `name` or `description`.
Supporting references stay local to the skill and are loaded only when the
workflow needs them.

Authoring Conventions
---------------------

- Keep the frontmatter `name` stable and descriptive.
- Make the `description` specific enough for reliable skill selection.
- Put the primary workflow in `SKILL.md`.
- Move long tables, examples, and exact command references into `references/`.
- Keep instructions practical and task-focused.
- Avoid duplicating broad coding-agent behavior that belongs in system or
  project-level instructions.

Notes
-----

- Generated outputs should usually stay outside this repository unless they are
  intentional examples or fixtures.
- Skills should remain independent. A skill may reference another workflow, but
  it should not require loading unrelated skills to perform its core task.

Reference
---------

- https://github.com/mattpocock/skills
- https://github.com/github/awesome-copilot/tree/main/skills
- https://github.com/addyosmani/agent-skills