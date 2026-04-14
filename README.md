# whatsgoingon

A collection of agent skills that summarize the information feeds you deal with as a software developer. Stay on top of what's happening across your tools without context-switching away from your workflow.

## Installation

```bash
npx skills add https://github.com/pfcoperez/whatsgoingon
```

## Prerequisites

- An AI coding agent with [npx skills](https://www.npmjs.com/package/skills) support
- Skill-specific requirements listed below

## Skills

### whatsgoingon-github

Summarizes your GitHub notifications into organized, actionable reports. Instead of scrolling through dozens of individual notifications, get a grouped summary by repository and topic — with status, pending actions, and links to everything that matters.

#### Requirements

- [GitHub CLI (`gh`)](https://cli.github.com/) installed and authenticated (`gh auth login`)
  - Alternatively, set the `GITHUB_TOKEN` environment variable with a personal access token (value or path to a file containing it)

#### Usage

```
/whatsgoingon-github
```

#### Arguments

All arguments are optional:

| Argument | Default | Description |
|---|---|---|
| **Scope** | All repositories | Filter by specific repositories or organizations |
| **Period** | Last 7 days | Time range for notifications |
| **Persistence target** | `none` | Where to save the report (see below) |

#### Examples

```
/whatsgoingon-github
/whatsgoingon-github myorg/myrepo last 3 days
/whatsgoingon-github myorg last 24 hours markdown
/whatsgoingon-github all last 7 days comment at https://github.com/org/repo/issues/1
```

#### Report format

The report includes three sections:

**Grouped notifications** — Notifications grouped by (repository, topic) in a table with:

- Topic and summary
- Status
- Links to related notifications, PRs, and issues (GitHub, Linear, etc.)
- Last update timestamp and summary
- Pending actions — who is waiting for what

**Unclassified notifications** — A similar table for notifications that don't fit into clear topic groups.

**Pending comments** — Comments that require your action, including:

- Comments on your open Pull Requests
- Comments where you are mentioned
- Active conversations you've participated in

Each entry shows the conversation summary, probable requested action, and a direct link to the comment.

#### Persistence options

| Option | Behavior |
|---|---|
| `none` (default) | Report is displayed in the terminal only |
| `markdown` | Saved to `github-report-<FROM>-<TO>.md` in the working directory |
| `comment at <URL>` | Posted as a comment on the specified GitHub issue or PR |

## License

Apache License 2.0 — see [LICENSE](LICENSE) for details.
