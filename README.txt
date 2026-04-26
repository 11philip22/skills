OpenCode Skills Repository
==========================

This repository contains reusable skill definitions for OpenCode.
OpenCode loads these skills to provide specialized instructions and workflows for specific tasks.

What This Repo Contains
-----------------------

- `hero-generator-cli/` for generating README banner PNGs with the `hero-generator` CLI

How OpenCode Uses These Files
-----------------------------

- Reads skill directories from the configured OpenCode skills location
- Uses each skill's `SKILL.md` file as the main instruction document
- Loads a skill when a task matches the skill description
- Allows skills to include references and supporting files in subdirectories

Recommended Use
---------------

- Put this repo, or a symlink to it, under `~/.config/opencode/skills/`
- Keep each skill in its own directory
- Store task-specific references under that skill's directory

Example:

  ln -s /path/to/this/repo ~/.config/opencode/skills

Skill Design Conventions In This Repo
-------------------------------------

- Keep skill descriptions specific enough for OpenCode to select the right skill
- Put the main workflow in `SKILL.md`
- Put detailed references in a `references/` directory when exact values or longer documentation are useful
- Prefer concise, actionable instructions over broad tutorials

Current Structure
-----------------

- `hero-generator-cli/SKILL.md` contains the workflow for creating hero banner PNGs
- `hero-generator-cli/references/` contains supporting CLI reference material

References
----------

- https://github.com/mattpocock/skills

Notes
-----

- Skills are task-specific and should not duplicate broad coding rules
- Supporting references should stay close to the skill that uses them
- Keep generated outputs outside this skills repository unless they are intentional examples or fixtures
