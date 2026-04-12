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

- Scope: Repositories or organizations to fetch notifications from.
- Period: Time range for notifications (e.g., last 7 days).

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

# Memory

- Store the list of all the notifications you have tracked (`tracked_notifications.md`) in a file under the project directory. It contains a list of links to the notification.
