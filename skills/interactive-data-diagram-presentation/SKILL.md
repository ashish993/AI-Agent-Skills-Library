---
name: interactive-data-diagram-presentation
title: Interactive Data Diagram Presentation
category: content
version: 1.0.0
author: ashish993
---

# Interactive Data Diagram Presentation

## Description

Turn supplied business, analytics, or architecture evidence into a polished, interactive, self-contained HTML presentation with accessible inline SVG.

## When to Use

- You need to explain a data finding, process, system architecture, or data flow to a customer or executive.
- You need an interactive HTML/SVG diagram that can be presented in a browser and edited later.
- A source dataset needs to become a clear, evidence-grounded visual story.

## When NOT to Use

- The user needs a static image, spreadsheet, or slide deck and did not ask for an HTML experience.
- The available data is too incomplete to support the requested claim or comparison; ask for the missing information first.
- A diagram would imply production deployment, security controls, causality, or a confirmed relationship that the evidence does not establish.

## Inputs

| Name | Type | Required | Description |
|------|------|----------|-------------|
| source_data | string, JSON object, CSV, or file reference | yes | The data, source material, or system facts to visualize |
| purpose | string | yes | The decision, question, or story the presentation must answer |
| audience | string | no | Intended viewers and their level of technical detail |
| format_preferences | object | no | Brand, layout, palette, page size, interaction, or file-location preferences |

## Outputs

| Name | Type | Description |
|------|------|-------------|
| html_file | file path | Self-contained HTML presentation with embedded CSS, data, and inline SVG |
| source_notes | list of strings | Sources, assumptions, limitations, and unresolved questions shown in the presentation |
| review_summary | list of strings | Visual, data, accessibility, and interaction checks performed |

## Workflow

### 1. Establish what the evidence supports

Identify the audience, purpose, source, units, time period, definitions, scope, and requested interactions. Read the supplied data before choosing the visual. Validate types, units, date ranges, duplicates, missing values, denominators, totals, and whether categories or periods are comparable.

Ask up to three focused questions if a missing fact changes the comparison, flow direction, trust boundary, or architecture meaning. Otherwise use a reversible assumption and label it visibly. Never infer a period, currency, baseline, causal link, deployment, security control, or production status from appearance alone. Keep unlike periods or definitions separate. Label a diagram as current, proposed, or conceptual. Distinguish fact, inference, proposal, and unknown.

### 2. Choose the clearest visual story

Answer the audience's question in this order:

1. State the finding or decision and the scope.
2. Show the most useful chart or diagram with labeled units and relationships.
3. Explain the evidence, implications, and material caveats.

Choose a chart by the question and data type: trends for ordered time, bars for category comparisons, distributions for spread, and flows for movement. Use honest scales and clear baselines; show units, period, category names, and denominators when needed. Treat missing data explicitly and avoid visual effects that exaggerate differences.

For architecture, choose the smallest useful context, component, sequence, deployment, process, or data-flow view. Name the source and destination of important connections and label direction and purpose. A drawn boundary does not establish a security control.

### 3. Build the HTML presentation

Create one self-contained `.html` file. Embed CSS, data, and editable inline SVG; do not depend on external scripts, fonts, images, or network access. Use multiple presentation sections only when each answers a distinct question.

Design for the subject and audience rather than a generic dashboard. Set a compact palette, type scale, spacing, and alignment. Use strong hierarchy, concise labels, generous space, and one visual focal point. Keep the diagram legible at presentation size and usable on narrow screens. If a diagram is wider than the viewport, provide keyboard-accessible horizontal scrolling.

Interactions must clarify evidence: for example, selecting a series, switching compatible views, highlighting connected flows, revealing source notes, or navigating sections. Keep essential meaning visible without hover. Use semantic controls with clear labels and visible keyboard focus. Give SVG an accessible name and description with `role="img"`, `<title>`, and `<desc>`. Check contrast and respect `prefers-reduced-motion`; motion should explain a user-requested change.

### 4. Render and review before delivery

Open the saved HTML in a browser at presentation size and a narrow viewport. Inspect every section and trace each arrow from its source to its intended destination. Check that labels, axes, units, legend, notes, and controls are readable; text and connectors do not overlap or clip; and interactions work with mouse and keyboard. Compare every displayed value against the input and confirm assumptions are visible. Fix defects and render again.

Deliver the HTML file and a concise review summary that states the checks performed and unresolved assumptions.

## Example

This standalone snippet demonstrates a keyboard-operable flow highlight using inline SVG and no external dependencies. Use the same accessible pattern when a flow interaction helps explain the supplied system.

```html
<!doctype html>
<html lang="en">
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Order data flow</title>
<style>
  body { font: 16px system-ui, sans-serif; color: #17233b; }
  button { padding: .6rem .9rem; border: 1px solid #5268d8; border-radius: .5rem; background: white; color: #253d9b; }
  button:focus-visible { outline: 3px solid #f0a52b; outline-offset: 3px; }
  .flow { stroke: #72809a; stroke-width: 3; }
  .flow.active { stroke: #3155d9; stroke-width: 6; }
  .node { fill: #edf1fa; stroke: #71809b; stroke-width: 2; }
  text { font: 16px system-ui, sans-serif; fill: #17233b; }
</style>
<button id="toggle" type="button" aria-pressed="false" aria-controls="diagram">Highlight data flow</button>
<svg id="diagram" role="img" aria-labelledby="title desc" viewBox="0 0 560 150" width="100%">
  <title id="title">Order data flow</title>
  <desc id="desc">The order service sends order records to the analytics platform.</desc>
  <defs><marker id="arrow" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L0,6 L9,3 z" fill="context-stroke"/></marker></defs>
  <rect class="node" x="20" y="45" width="180" height="60" rx="12"/>
  <text x="110" y="81" text-anchor="middle">Order service</text>
  <path class="flow" d="M200 75 H350" marker-end="url(#arrow)"/>
  <text x="275" y="58" text-anchor="middle">order records</text>
  <rect class="node" x="350" y="45" width="190" height="60" rx="12"/>
  <text x="445" y="81" text-anchor="middle">Analytics platform</text>
</svg>
<script>
  const button = document.querySelector("#toggle");
  const flow = document.querySelector(".flow");
  button.addEventListener("click", () => {
    const active = button.getAttribute("aria-pressed") !== "true";
    button.setAttribute("aria-pressed", String(active));
    flow.classList.toggle("active", active);
  });
</script>
</html>
```

## Notes

- Keep every value, relationship, and claim traceable to a named source or visibly qualified.
- Provide visible source and assumption notes in the presentation.
- Keep all essential meaning available to keyboard and screen-reader users.
- Do not include private data in a public output unless the user explicitly intends that disclosure.

## Acceptance Checklist

- Story, audience, scope, and diagram type are clear.
- Values and claims match the supplied evidence; assumptions and unknowns are labeled.
- Chart scale and encoding are honest; flow endpoints and arrowheads are correct.
- HTML is self-contained; inline SVG is accessible; controls work by keyboard.
- Desktop and narrow layouts have been visually inspected.

## Common Mistakes

- Combining values whose time periods, currencies, or definitions are unknown.
- Treating a conceptual flow as a confirmed deployment or inferring security from a boundary.
- Using color or hover as the only way to understand a chart or relationship.
- Shrinking text, hiding caveats, or skipping visual review to meet a deadline.
- Adding third-party libraries or remote fonts that make the delivered HTML depend on a network.
