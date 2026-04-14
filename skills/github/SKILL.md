---
name: github
description: Summarize GitHub notifications, grouping them by (repository, topic) and providing updates by group.
allowed-tools: Bash(gh api *) Bash(gh auth *) Bash(for *)
---

Goal: Summarize GitHub notifications, grouping them by (repository, topic) and providing updates by group.

# Requirements

- gh CLI tool installed and authenticated, or a valid GitHub token for API access.

# Input

# User provided input

- Scope: [Optional, default: all] Repositories or organizations to fetch notifications from.
- Period: [Optional, default: last 7 days] Time range for notifications (e.g., last 7 days).
- Persistence target: [Optional, default: none] Whether to save the report in a markdown file (`markdown`) or a GitHub issue/PR comment (`comment at <URL>`) or not persisting it at all (`none`).

# Sources

GitHub API, CLI or GitHub web interface.

## Authentication

Use `gh auth login` for authentication with GitHub CLI. 

Alternatively, accept a GitHub token for authentication:

Use `GITHUB_TOKEN` environment variable for authentication. It might contain either:

- The token content directly.
- A file path to a file containing the token. In this case, read it with `cat $GITHUB_TOKEN`.

# Output

All outputs should include:

- A summary
- The results, shown in tables whenever possible.  

## Grouped notifications

Group notifications by (repository, topic) with summary of each group theme, topic or issue. Present this information in a table with the following columns:

- Topic
- Summary of the topic
- Status
- Links to grouped notifications.
- Links to related Pull Requests
- Links to related Issues either at GitHub, Linear or any other issue tracking system 
- Last update: Timestamp and summary of the last update
- Pending actions: Waiting for review? Response? Approval? By whom?

## Unclassified notifications

Produce a similar table to that of grouped notifications, but for unclassified notifications.

## Pending comments

Produce a table of pending comments that require user action, with the following columns:

- Issue or Pull Request
- Summary of the conversation
- Last update timestamp
- Probable requested action: e.g: If it was a question, what is asked? If it is a review comment, a summary of the requested changes. 
- Last comment: With link to the comment

A pending comment is a comment that requires response from the authenticated user. These are any of these:

- Comments on Pull Requests open by the authenticated user.
- Last comment where the authenticated user is mentioned.
- Last comment on a conversation where the authencated user has actively participated. Specially if the conversation is started by the authenticated user.

# Report persistence

## Markdown file

If `Persistence target` is set to `markdown`:

Write down the report in markdown format to a file in the working directory with name: `github-report-<FROM>-<TO>.md` where `<FROM>` and `<TO>` are dates in `YYYY-MM-DD` format for the beginning and end of the reporting period.

## GitHub issue or pull request

If `Persistence target` is set to `comment at <URL>`:

Write down the report as a comment in a GitHub issue or pull request at the specified URL.

If no URL is provided, do nothing and just return the report in the output.