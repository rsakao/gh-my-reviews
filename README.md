# gh-my-reviews

A [GitHub CLI](https://cli.github.com/) extension that lists open pull requests where **you are directly requested as a reviewer** — excluding team-based review requests.

## Why?

`gh search prs --review-requested @me` includes PRs requested via a team, which can be noisy. This extension filters down to only PRs where **you personally** are listed as a requested reviewer, giving you a clean, actionable list.

## Requirements

- [GitHub CLI (`gh`)](https://cli.github.com/) v2.0 or later
- Authenticated with `gh auth login`

## Installation

```bash
gh extension install <owner>/gh-my-reviews
```

## Usage

```bash
gh my-reviews
```

### Example output

```
🔍 Searching PRs where @yourname is directly requested as reviewer...

📌 Fix: handle nil pointer in auth middleware
   👤 alice  🔗 https://github.com/org/repo/pull/42

📌 feat: add pagination to user list API
   👤 bob  🔗 https://github.com/org/repo/pull/57
```

If there are no pending review requests:

```
✅ No pending review requests.
```

## How it works

1. Resolves your GitHub username via `gh api user`
2. Queries the GitHub GraphQL API for open PRs with `review-requested:@me`
3. Filters results to only include PRs where your **user account** (not a team) is in the `reviewRequests` list
4. Displays the PR title, author, and URL

## Uninstall

```bash
gh extension remove my-reviews
```

## License

MIT
