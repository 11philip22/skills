---
name: changelog
description: "Use this skill whenever the user wants to create, bootstrap, write, update, or review a CHANGELOG.md file. Triggers include: any mention of 'changelog', 'CHANGELOG', 'release notes', 'version history', or requests to document changes between versions of a project. Also use when adding a new version entry, moving Unreleased changes to a release, auditing an existing changelog for compliance with Keep a Changelog, or converting a raw git log into a proper changelog. Do NOT use for README files, commit messages, git tags, or GitHub Releases pages."
---

# CHANGELOG.md — Bootstrap & Maintenance

## Overview

A `CHANGELOG.md` follows the [Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/) standard. It is a human-readable, reverse-chronological log of notable changes per version. It is NOT a git log dump.

---

## Canonical File Structure

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- …

## [1.2.0] - 2024-06-01

### Added
- …

### Fixed
- …

## [1.1.0] - 2024-03-15

### Changed
- …

## [1.0.0] - 2024-01-10

### Added
- Initial release.

[unreleased]: https://github.com/owner/repo/compare/v1.2.0...HEAD
[1.2.0]: https://github.com/owner/repo/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/owner/repo/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/owner/repo/releases/tag/v1.0.0
```

---

## Rules

### File & Header
- Filename: **`CHANGELOG.md`** (uppercase, at repo root)
- First line: `# Changelog`
- Second block: the two-sentence boilerplate referencing Keep a Changelog and Semantic Versioning (copy verbatim from the template above)

### Version Order
- **Newest version first** (reverse chronological)
- `## [Unreleased]` always sits at the very top, above all versioned entries

### Version Heading Format
```
## [MAJOR.MINOR.PATCH] - YYYY-MM-DD
```
- Version number in square brackets
- Date in **ISO 8601** format (`YYYY-MM-DD`) — never `June 1st`, `01/06/2024`, etc.
- Yanked releases: append `[YANKED]` → `## [0.5.0] - 2024-05-01 [YANKED]`

### Change Type Subsections
Use `### ` subsections. Only include types that have entries — omit empty ones.

| Subsection | Use for |
|---|---|
| `### Added` | New features |
| `### Changed` | Changes to existing functionality |
| `### Deprecated` | Features that will be removed in a future version |
| `### Removed` | Features removed in this version |
| `### Fixed` | Bug fixes |
| `### Security` | Vulnerability patches |

### Entries
- Each entry is a **single bullet** (`- `)
- Written for **humans**, not machines — explain the *what* and *why*, not the commit hash
- Group related changes under the same subsection; do not repeat subsection headers
- Do not include: merge commits, CI changes, typo fixes, whitespace changes (unless they matter to users)

### Footer Links
Every version heading must have a corresponding comparison link at the bottom of the file:
```markdown
[unreleased]: https://github.com/owner/repo/compare/vLATEST...HEAD
[1.2.0]: https://github.com/owner/repo/compare/v1.1.0...v1.2.0
[1.0.0]: https://github.com/owner/repo/releases/tag/v1.0.0   ← first release uses /tag/, not /compare/
```

---

## Bootstrapping a New CHANGELOG.md

When a project has no changelog yet:

1. Determine the current version and repo URL from the user (or infer from `package.json`, `pyproject.toml`, `Cargo.toml`, etc.)
2. Scan git log or release history if available — ask the user to paste `git log --oneline` if needed
3. Create the file with:
   - The standard header boilerplate
   - `## [Unreleased]` section (empty subsections omitted)
   - One entry per past release, best-effort populated from git log or user input
   - Footer comparison links for all versions
4. If no version history is available, start with a single `## [X.Y.Z] - YYYY-MM-DD` entry with `### Added` / `- Initial release.`

---

## Releasing: Moving Unreleased → New Version

When the user wants to cut a release:

1. Replace `## [Unreleased]` with `## [NEW_VERSION] - TODAY_DATE`
2. Add a fresh empty `## [Unreleased]` above it
3. Update the footer links:
   - Change `[unreleased]` to compare from the new tag to HEAD
   - Add a new line for `[NEW_VERSION]` comparing from previous tag to new tag

---

## Anti-Patterns (Never Do These)

| ❌ Bad | ✅ Good |
|---|---|
| Paste raw `git log` output | Curate notable changes written for end users |
| `## 1.2.0` (no brackets, no date) | `## [1.2.0] - 2024-06-01` |
| Date as `June 1, 2024` or `01/06/2024` | Date as `2024-06-01` |
| Empty subsections (`### Fixed` with nothing under it) | Omit the subsection entirely |
| No `[Unreleased]` section | Always keep `[Unreleased]` at the top |
| No footer comparison links | Always add links for every version |
| Documenting only some breaking changes | Every breaking change **must** appear under `### Changed`, `### Removed`, or `### Deprecated` |
| Oldest version first | Newest version first |