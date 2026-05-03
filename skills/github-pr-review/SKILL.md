---
name: github-pr-review
title: GitHub PR Review
category: developer-tools
version: 1.0.0
---

# GitHub PR Review

## Description

Fetch a GitHub pull request, read the diff, and produce a structured code review summary.

## When to Use

- You want an automated first-pass review before human review
- You need a quick summary of what changed in a PR

## When NOT to Use

- The PR contains generated files or lock files (too noisy)
- Security-sensitive diffs that should only be seen by authorized humans

## Inputs

| Name | Type | Required | Description |
|------|------|---------|-------------|
| repo | string | yes | "owner/repo" format |
| pr_number | int | yes | Pull request number |
| github_token | string | no | PAT for private repos |

## Outputs

| Name | Type | Description |
|------|------|-------------|
| summary | string | Plain English summary of changes |
| files_changed | list | List of changed file paths |
| risk_level | string | low/medium/high estimated risk |

## Example

```python
import os, requests

def review_pr(repo: str, pr_number: int, token: str = None) -> dict:
    headers = {"Accept": "application/vnd.github.v3+json"}
    if token:
        headers["Authorization"] = f"token {token}"

    url = f"https://api.github.com/repos/{repo}/pulls/{pr_number}/files"
    resp = requests.get(url, headers=headers)
    resp.raise_for_status()
    files = resp.json()

    changed = [f["filename"] for f in files]
    additions = sum(f["additions"] for f in files)
    deletions = sum(f["deletions"] for f in files)

    risk = "low"
    if additions + deletions > 500:
        risk = "medium"
    if any("security" in f or "auth" in f or "password" in f for f in changed):
        risk = "high"

    return {
        "summary": f"PR changes {len(changed)} files (+{additions}/-{deletions} lines)",
        "files_changed": changed,
        "risk_level": risk,
    }

# result = review_pr("owner/repo", 42, token=os.environ["GITHUB_TOKEN"])
```

## Notes

- Respects GitHub API rate limits (60 req/hr unauthenticated, 5000 with token)
- Does not post comments — only reads
