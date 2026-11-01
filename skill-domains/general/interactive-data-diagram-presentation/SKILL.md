---
name: "interactive-data-diagram-presentation"
title: "Interactive Data Diagram Presentation"
description: "Turn supplied business, analytics, or architecture evidence into polished interactive HTML presentations with accessible inline SVG charts and diagrams."
domain: "general"
metadata:
  author: "Test User"
  version: "1.0.0"
trigger:
  mode: "AUTO"
  keywords: ["interactive diagram", "HTML SVG presentation", "data visualization", "architecture diagram"]
prompt:
  output_format: "One self-contained HTML5 presentation file with embedded CSS, data, and accessible inline SVG. Include a clear title, story sections, labeled units and relationships, keyboard-operable interactive controls when they add value, and visible source/assumption notes. Return the saved .html file plus a concise summary of validation and unresolved assumptions."
---

Create a customer-ready, self-contained HTML presentation from the user's supplied business, analytics, or architecture evidence. Use embedded CSS, data, and editable inline SVG. Do not depend on external scripts, fonts, images, or network access.

Evidence first: read the supplied sources and identify audience, purpose, scope, units, period, definitions, and intended interactions. Check types, missing values, duplicates, totals, denominators, and comparability. Never invent a period, currency, baseline, cause, relationship, deployment, security control, or production status. Ask up to three focused questions only when an unknown changes the meaning; otherwise make a reversible assumption and label it visibly. Distinguish verified facts, inferences, proposals, and unknowns. Name source material in visible notes.

Tell a clear story: state the finding or decision and scope; show the most useful chart or diagram with labeled units and relationships; then explain implications and caveats. Choose charts by data and question (trends for ordered time, bars for category comparisons, distributions for spread, flows for movement). Use honest scales, clear baselines, and explicit treatment of missing data. Keep incomparable periods or definitions separate.

For architecture, choose the smallest useful context, component, sequence, deployment, process, or data-flow view. Name source and destination for important arrows; label direction and purpose. A drawn boundary is not proof of a security control. Mark a diagram current, proposed, or conceptual.

Design a professional enterprise interface for the subject and audience: strong hierarchy, concise labels, restrained palette, consistent type and spacing, generous whitespace, and a clear focal point. Make charts legible at presentation size and usable at narrow widths. Use keyboard-accessible horizontal scrolling for wider diagrams. Interactions should clarify evidence; keep essential meaning visible without hover. Use semantic labeled controls, visible high-contrast focus, accessible SVG names/descriptions (<title>, <desc>), sufficient contrast, and reduced-motion preferences.

Review the saved HTML in a browser at presentation and narrow sizes. Check labels, values against source, units, legends, notes, arrow endpoints/direction, clipping, overlap, contrast, keyboard navigation, and interaction behavior. Fix defects and review again. Return the HTML file and concise notes on sources, assumptions, checks, and unresolved items.
