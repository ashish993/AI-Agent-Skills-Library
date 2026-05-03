---
name: csv-transform
title: CSV Transform
category: data-etl
version: 1.0.0
---

# CSV Transform

## Description

Apply a natural language transformation description to a CSV file and produce a new CSV.

## When to Use

- Non-technical users need to reshape data
- Quick ETL without writing pandas code

## Inputs

| Name | Type | Required | Description |
|------|------|---------|-------------|
| input_path | string | yes | Path to source CSV |
| instruction | string | yes | e.g. "Filter rows where sales > 1000, keep only name and sales columns" |
| output_path | string | no | Where to save result |

## Example

```python
import pandas as pd

def csv_transform(input_path: str, instruction: str, output_path: str = None) -> pd.DataFrame:
    '''
    Parse simple filter/select instructions without LLM for offline demo.
    For production, pass instruction to an LLM that writes pandas code.
    '''
    df = pd.read_csv(input_path)
    # Example: "filter rows where sales > 1000"
    if "filter" in instruction.lower() and ">" in instruction:
        import re
        m = re.search(r"(\w+)\s*>\s*([\d.]+)", instruction)
        if m:
            col, val = m.group(1), float(m.group(2))
            if col in df.columns:
                df = df[df[col] > val]
    # Example: "keep only name and sales columns"
    if "keep only" in instruction.lower():
        cols = [c.strip() for c in instruction.lower().split("keep only")[-1].split("and")]
        cols = [c.replace("columns", "").strip() for c in cols]
        valid_cols = [c for c in cols if c in df.columns]
        if valid_cols:
            df = df[valid_cols]
    if output_path:
        df.to_csv(output_path, index=False)
    return df
```
