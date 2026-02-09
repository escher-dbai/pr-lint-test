# PR Lint Test

This repository enforces **Conventional Commits** PR title formatting for the Escher team. A GitHub Actions workflow automatically validates every PR title on open, edit, and reopen — blocking merges that don't follow the convention.

## PR Title Format

```
<type>(<scope>): <short description>
```

Scope is **optional**. If a change is cross-cutting, omit it:

```
feat: add global audit logging
```

## Allowed Types

| Type       | In Release Notes? | Release Notes Section |
|------------|-------------------|-----------------------|
| `feat`     | ✅ Yes            | New Features          |
| `fix`      | ✅ Yes            | Bug Fixes             |
| `perf`     | ✅ Yes            | Performance           |
| `docs`     | ✅ Yes            | Documentation         |
| `refactor` | ❌ No             | Internal only         |
| `chore`    | ❌ No             | Internal only         |
| `test`     | ❌ No             | Internal only         |
| `style`    | ❌ No             | Internal only         |

## Allowed Scopes

| Scope            | Maps To                                    |
|------------------|--------------------------------------------|
| `playbooks`      | Playbook engine and definitions            |
| `hybrid-ama`     | Quadrant Data, RAG Search                  |
| `live-ama`       | Script, LLM parsing, response consistency  |
| `analysis-agent` | Final response, Data Accuracy and quality  |
| `profile-picker` | Hybrid system components                   |
| `ui`             | Frontend / dashboard                       |
| `api`            | API layer / endpoints                      |
| `slack`          | Slack integration                          |
| `auth`           | Authentication / authorization             |
| `jira`           | Jira integration                           |
| `ci`             | CI/CD pipeline                             |
| `deps`           | Dependencies                               |
| `config`         | Configuration management                   |

## Breaking Changes

Add `!` after the type (and optional scope), before the colon:

```
feat!(api): remove deprecated v1 endpoints
```

This signals a breaking change and will be prominently highlighted in release notes.

## Description Rules

- Use **imperative mood** ("add", not "added" or "adds")
- Start with a **lowercase** letter
- Do **not** end with a period
- Keep it under **50 characters**

## What Goes in the PR Body (NOT the Title)

The PR title is for the *what*. The body is for everything else:

- **Linked tickets:** `Closes ENG-1234`
- **Context / why:** Explain motivation and trade-offs
- **Migration steps:** If the change requires action from other engineers
- **Screenshots:** For UI changes
- **Testing notes:** How to verify the change works

## Examples

### Good

```
feat(playbooks): add conditional branching for remediation workflows
fix(live-ama): resolve response consistency on multi-turn queries
chore(deps): upgrade Azure SDK to v5.3
docs(api): add authentication examples for policy engine endpoints
perf(hybrid-ama): reduce RAG search latency by 40%
feat!(api): change default escalation policy schema
```

### Bad

| Bad Title                                             | Why It's Wrong                          | Correct Version                                          |
|-------------------------------------------------------|-----------------------------------------|----------------------------------------------------------|
| `Fix bug in playbooks`                                | Missing type prefix, wrong casing       | `fix(playbooks): handle null state in retry logic`       |
| `ENG-456: Add new feature`                            | Ticket IDs go in the PR body            | `feat(ui): add incident timeline visualization`          |
| `Updated dependencies`                                | Missing type, past tense                | `chore(deps): bump axios to 1.6.0`                      |
| `WIP`                                                 | Don't merge WIP PRs — use draft PRs    | —                                                        |
| `feat(ui): Add Dashboard Component For Monitoring.`   | Starts uppercase, trailing period       | `feat(ui): add dashboard component for monitoring`       |
