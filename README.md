# AI Agent Skills Library

A community catalog of 2000+ reusable skills for AI agents.

## Skill Categories

| Category | Count |
|----------|-------|
| Developer Tools | 120+ |
| Security | 85+ |
| Data ETL | 150+ |
| Browser Automation | 95+ |
| Research/Scraping | 110+ |
| Monitoring | 60+ |
| Calendar and Email | 45+ |

## Using a Skill

```python
from skills import load_skill
skill = load_skill("github-pr-review")
result = skill.run({"repo": "owner/repo", "pr_number": 42})
```

## Contributing

See CONTRIBUTING.md. Each skill needs a directory with SKILL.md.
