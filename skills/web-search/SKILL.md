---
name: web-search
title: Web Search
category: developer-tools
version: 1.0.0
---

# Web Search

## Description

Execute a web search and return structured results (title, URL, snippet) for an agent to consume.

## When to Use

- Agent needs current information beyond its training cutoff
- Researching a topic or verifying facts

## When NOT to Use

- Searching for credentials or private data
- High-frequency automated scraping (respect robots.txt)

## Inputs

| Name | Type | Required | Description |
|------|------|---------|-------------|
| query | string | yes | Search query |
| num_results | int | no | Number of results (default 5) |

## Outputs

| Name | Type | Description |
|------|------|-------------|
| results | list | List of {title, url, snippet} dicts |

## Example

```python
import requests

def web_search(query: str, num_results: int = 5, api_key: str = None) -> list:
    '''
    Uses SerpAPI or DuckDuckGo HTML scraping as fallback.
    For production use, get a SerpAPI key.
    '''
    if api_key:
        url = "https://serpapi.com/search"
        params = {"q": query, "num": num_results, "api_key": api_key}
        data = requests.get(url, params=params).json()
        return [
            {"title": r.get("title"), "url": r.get("link"), "snippet": r.get("snippet")}
            for r in data.get("organic_results", [])[:num_results]
        ]
    # Fallback: return placeholder (avoid scraping in examples)
    return [{"title": "Result placeholder", "url": "https://example.com", "snippet": query}]

# results = web_search("Python asyncio tutorial", num_results=3)
# for r in results:
#     print(r["title"], r["url"])
```
