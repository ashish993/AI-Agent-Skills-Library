---
name: skill-slug
title: Skill Title
category: developer-tools
version: 1.0.0
author: your-github-handle
---

# Skill Title

## Description

One sentence: what this skill does.

## When to Use

- Scenario 1
- Scenario 2

## When NOT to Use

- Anti-pattern 1
- Anti-pattern 2

## Inputs

| Name | Type | Required | Description |
|------|------|---------|-------------|
| param1 | string | yes | Description |
| param2 | int | no | Description |

## Outputs

| Name | Type | Description |
|------|------|-------------|
| result | string | Description |

## Example

```python
from skills import load_skill

skill = load_skill("skill-slug")
output = skill.run({
    "param1": "value",
})
print(output["result"])
```

## Notes

Any caveats, rate limits, auth requirements.
