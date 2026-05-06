---
name: conventional-commits
description: "Use this skill whenever the user wants to write, review, validate, or explain commit messages following the Conventional Commits specification. Triggers include: any mention of 'conventional commits', 'commit message', 'commit format', writing a git commit, reviewing whether a commit message is valid, converting plain descriptions into properly formatted commit messages, or generating a commit message from a diff or description of changes. Also use when the user asks how to signal a breaking change, what type to use, or how commits map to SemVer versions. Do NOT use for CHANGELOG generation (use the changelog skill), git branching strategies, or PR descriptions unrelated to commit message format."
---

# Conventional Commits 1.0.0

## Overview

Conventional Commits is a specification for commit messages that makes history human- and machine-readable. It dovetails with [SemVer](https://semver.org): commit types determine which version number to bump.

---

## Commit Message Structure

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

Every part has strict rules. Each section below covers them exactly.

---

## 1. Type (REQUIRED)

- MUST be a noun: `feat`, `fix`, or any other agreed-upon type
- MUST be followed by the optional scope, optional `!`, then a REQUIRED `: ` (colon + space)
- Case-insensitive — but be consistent within a project

### Spec-defined types and their SemVer impact

| Type | Meaning | SemVer bump |
|------|---------|-------------|
| `feat` | Introduces a new feature | MINOR |
| `fix` | Patches a bug | PATCH |
| anything + `BREAKING CHANGE` | Breaking API change | MAJOR |

### Commonly used additional types (Angular/commitlint convention)
These carry **no implicit SemVer effect** unless they also include a breaking change:

| Type | Use for |
|------|---------|
| `build` | Build system or external dependency changes |
| `chore` | Maintenance tasks that don't modify src or test files |
| `ci` | CI configuration changes |
| `docs` | Documentation only |
| `style` | Formatting, whitespace — no logic change |
| `refactor` | Code restructure without feature or fix |
| `perf` | Performance improvements |
| `test` | Adding or correcting tests |
| `revert` | Reverting a previous commit |

Additional types beyond this list MAY be used; they are not mandated.

---

## 2. Scope (OPTIONAL)

- Provided in parentheses immediately after the type: `feat(parser):`
- MUST be a noun describing a section of the codebase
- Case-insensitive

```
feat(lang): add Polish language
fix(auth): handle expired token edge case
```

---

## 3. Breaking Change Indicator (OPTIONAL)

Two equivalent ways — MAY be combined:

**Option A — `!` in the prefix** (before the `:`):
```
feat!: drop support for Node 6
feat(api)!: send email on shipment
```
When `!` is used, `BREAKING CHANGE:` MAY be omitted from the footer. The description line itself describes the breaking change.

**Option B — `BREAKING CHANGE` footer**:
```
feat: allow config object to extend other configs

BREAKING CHANGE: `extends` key now used for extending other config files
```

**Both combined** (also valid):
```
feat!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

Rules:
- `BREAKING CHANGE` MUST be uppercase (this is the ONE case-sensitive exception in the spec)
- `BREAKING-CHANGE` (hyphenated) MUST be treated as synonymous with `BREAKING CHANGE` when used as a footer token
- BREAKING CHANGE can appear on commits of ANY type, not just `feat` or `fix`

---

## 4. Description (REQUIRED)

- MUST immediately follow the `<type>[scope][!]: ` prefix — no blank line, no delay
- A short summary of the change in imperative mood (convention, not mandated)
- Example: `fix: array parsing issue when multiple spaces were in string`

---

## 5. Body (OPTIONAL)

- MUST begin exactly one blank line after the description
- Free-form; MAY consist of any number of newline-separated paragraphs
- Used for additional contextual information about the *why* and *what*

```
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.
```

---

## 6. Footers (OPTIONAL)

- MAY provide one or more footers, each starting one blank line after the body (or after the description if no body)
- Each footer MUST follow the format: `token: value` or `token #value`
- Footer token MUST use `-` instead of spaces (e.g. `Reviewed-by`, `Acked-by`) — EXCEPT `BREAKING CHANGE` which is the explicit allowed exception
- A footer value MAY span multiple lines; parsing terminates at the next valid `token: ` or `token #` pair

```
fix: prevent racing of requests

Reviewed-by: Z
Refs: #123
Co-authored-by: Alice <alice@example.com>
```

---

## Full Annotated Examples

### Minimal — type + description only
```
docs: correct spelling of CHANGELOG
```

### With scope
```
feat(lang): add Polish language
```

### Breaking change via `!`
```
feat!: send an email to the customer when a product is shipped
```

### Breaking change via `!` + scope
```
feat(api)!: send an email to the customer when a product is shipped
```

### Breaking change via footer only
```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

### Breaking change via both `!` and footer
```
feat!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

### Body + multiple footers
```
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

Reviewed-by: Z
Refs: #123
```

### Revert
```
revert: let us never again speak of the noodle incident

Refs: 676104e, a215868
```

---

## SemVer Mapping (Quick Reference)

| Commits since last release contain… | Next version bump |
|--------------------------------------|-------------------|
| Any `BREAKING CHANGE` (footer or `!`) | MAJOR (`x+1.0.0`) |
| Any `feat` (no breaking change) | MINOR (`x.y+1.0`) |
| Only `fix`, `perf`, etc. (no breaking change, no feat) | PATCH (`x.y.z+1`) |
| Only `chore`, `docs`, `style`, `ci`, `test`, `refactor` | No release needed |

---

## Validation Checklist

When reviewing or writing a commit message, verify:

- [ ] Starts with a valid type noun
- [ ] Type is immediately followed by optional `(scope)`, optional `!`, then `: ` (colon + space — both required)
- [ ] Description follows immediately on the same line — no blank line between prefix and description
- [ ] If body is present: exactly one blank line separates it from the description
- [ ] If footers are present: exactly one blank line separates them from the body (or description)
- [ ] Footer tokens use `-` for spaces (except `BREAKING CHANGE`)
- [ ] `BREAKING CHANGE` is fully uppercase
- [ ] `feat` is used for new features, `fix` for bug fixes — not swapped
- [ ] If the change is breaking: `!` and/or `BREAKING CHANGE:` footer is present

---

## Anti-Patterns

| Wrong | Correct | Rule violated |
|---------|-----------|---------------|
| `Fix: something` with capital F | `fix: something` | Be consistent; case-insensitive but choose one |
| `feat:something` (no space) | `feat: something` | Space after colon is REQUIRED |
| `feat : something` (space before colon) | `feat: something` | No space before colon |
| `feat(parser) : something` | `feat(parser): something` | No space before colon |
| Description on next line after prefix | Description on same line as prefix | Description MUST immediately follow |
| `breaking change: …` (lowercase) | `BREAKING CHANGE: …` | MUST be uppercase |
| `BREAKING CHANGE:value` (no space) | `BREAKING CHANGE: value` | Space after colon required |
| Footer token with space: `Reviewed by: Z` | `Reviewed-by: Z` | Tokens MUST use `-` for whitespace |
| One giant commit with feat + fix + refactor | Three separate commits | One logical change per commit |
