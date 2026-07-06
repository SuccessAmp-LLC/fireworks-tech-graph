# Style 9: SuccessAmp Brand

SuccessAmp agency brand — professional, blue-forward, clean. For client-facing report diagrams: web silos, infrastructure, data flows, system architecture. Extracted from successamp.com (Montserrat + Roboto Condensed, deep teal-blue primary, burnt-orange accent).

```
Background:      #ffffff  (clean white)
  alt canvas:    #f7fafc  (very light blue-gray, for grouped section backgrounds)

Brand core:
  Primary:       #004863  (deep teal-blue)   — titles, box strokes, primary arrows
  Secondary:     #00a4e4  (bright cyan)       — highlights, secondary flow
  Mid-blue:      #289bc5  (supporting blue)
  Accent:        #bb5b00  (burnt orange)      — emphasis nodes, critical path

Semantic fills (light tints, dark text — professional + readable):
  Input/Source:    #d7eefb  (pale cyan)
  Agent/Process:   #bfe3f4  (light brand blue)
  Infrastructure:  #fbe3cb  (light orange tint)
  Storage/State:   #e6ecf0  (cool light gray)
  Emphasis node:   #bb5b00 fill + #ffffff text (the accent/critical node)

Box stroke:      #004863  (brand primary)
Box radius:      10px
Text primary:    #16323f  (near-black, brand-tinted)
Text secondary:  #555555  (descriptions, arrow labels)
Layer labels:    #004863  (brand primary, 600 weight)

Arrows:
  Primary flow:    #004863  (brand blue)
  Secondary flow:  #00a4e4  (cyan)
  Critical/emphasis: #bb5b00 (burnt orange)
```

## Typography

```
font-family: 'Montserrat', 'Roboto Condensed', -apple-system, BlinkMacSystemFont,
             'Segoe UI', 'Helvetica Neue', Arial, 'PingFang SC', 'Microsoft YaHei', sans-serif
font-size:   16px node labels, 14px descriptions, 13px arrow labels, 20px title
font-weight: 700 titles, 600 node labels, 400 descriptions

NOTE: Montserrat/Roboto Condensed may not be installed for cairosvg PNG export → it falls back to
system sans (acceptable). For a fully-portable SVG, embed the font via @font-face data-URI.
NEVER use an external @import (violates the skill's no-outbound rule).
```

## Box Shapes

```xml
<!-- Agent/Process node (light brand blue) -->
<rect rx="10" ry="10" fill="#bfe3f4" stroke="#004863" stroke-width="2.5"/>

<!-- Input/Source node (pale cyan) -->
<rect rx="10" ry="10" fill="#d7eefb" stroke="#004863" stroke-width="2.5"/>

<!-- Infrastructure node (light orange tint) -->
<rect rx="10" ry="10" fill="#fbe3cb" stroke="#004863" stroke-width="2.5"/>

<!-- Storage/State node (cool light gray) -->
<rect rx="10" ry="10" fill="#e6ecf0" stroke="#004863" stroke-width="2.5"/>

<!-- Emphasis / critical node (burnt orange, white text) -->
<rect rx="10" ry="10" fill="#bb5b00" stroke="#004863" stroke-width="2.5"/>
```

## Arrows

```xml
<defs>
  <marker id="arrow-sa" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto">
    <polygon points="0 0, 8 4, 0 8" fill="#004863"/>
  </marker>
  <marker id="arrow-sa-accent" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto">
    <polygon points="0 0, 8 4, 0 8" fill="#bb5b00"/>
  </marker>
</defs>

<!-- Primary flow -->
<line stroke="#004863" stroke-width="2" marker-end="url(#arrow-sa)"/>
<!-- Critical/emphasis flow -->
<line stroke="#bb5b00" stroke-width="2.5" marker-end="url(#arrow-sa-accent)"/>
<!-- Secondary/async (dashed) -->
<line stroke="#00a4e4" stroke-width="2" stroke-dasharray="5,3" marker-end="url(#arrow-sa)"/>
```

## Arrow Semantics

| Flow Type | Color | Stroke | Dash | Usage |
|-----------|-------|--------|------|-------|
| Primary data flow | #004863 | 2px solid | none | Main request/response path |
| Critical / hero path | #bb5b00 | 2.5px solid | none | The path the report is highlighting |
| Secondary / async | #00a4e4 | 2px | `5,3` | Background, async, optional flow |

Labels technical + specific: `POST /api/x`, `retrieve(top_k=5)`, `embed(768d)`. Avoid "Process"/"Send".

## Layer Labels (for silo / layered architecture — the common report case)

```xml
<text x="30" y="130" fill="#004863" font-size="14" font-weight="600">Edge / CDN</text>
<text x="30" y="290" fill="#004863" font-size="14" font-weight="600">Application</text>
<text x="30" y="490" fill="#004863" font-size="14" font-weight="600">Data</text>
```

## Legend (when 2+ arrow types/colors)

Bottom-right, 20px margin, white box with #004863 stroke. Match the arrow-semantics table.

## SVG Template

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 960 600" width="960" height="600">
  <style>
    text { font-family: 'Montserrat','Roboto Condensed',-apple-system,BlinkMacSystemFont,'Segoe UI',Arial,sans-serif; }
    .title { fill:#004863; font-size:20px; font-weight:700; }
    .node-label { fill:#16323f; font-size:16px; font-weight:600; }
    .node-desc { fill:#555555; font-size:14px; }
  </style>
  <defs>
    <marker id="arrow-sa" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto">
      <polygon points="0 0, 8 4, 0 8" fill="#004863"/>
    </marker>
    <filter id="shadow-soft"><feDropShadow dx="0" dy="2" stdDeviation="6" flood-color="#0048630f"/></filter>
  </defs>
  <rect width="960" height="600" fill="#ffffff"/>
  <text x="480" y="40" text-anchor="middle" class="title">Diagram Title</text>
  <rect x="100" y="100" width="180" height="80" rx="10" ry="10" fill="#bfe3f4" stroke="#004863" stroke-width="2.5" filter="url(#shadow-soft)"/>
  <text x="190" y="145" text-anchor="middle" class="node-label">Component</text>
  <line x1="190" y1="180" x2="190" y2="240" stroke="#004863" stroke-width="2" marker-end="url(#arrow-sa)"/>
</svg>
```

## Design Philosophy

SuccessAmp brand style emphasizes:
- **Professional clarity** — clean white, brand-blue structure, high-contrast readable text.
- **Blue-forward brand identity** — deep teal-blue is the anchor; cyan supports; burnt orange is the single accent (use sparingly for the one thing the report wants the client to see).
- **Client-facing polish** — consistent 2.5px strokes, 10px radius, generous 80px spacing, orthogonal routing.

Avoid: rainbow palettes (stick to the brand set), overusing the orange accent (dilutes emphasis), thin strokes (<2px), external font @import.
```
