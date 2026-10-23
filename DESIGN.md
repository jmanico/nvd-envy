---
version: alpha
name: NVD Envy
description: Restrained visual identity for CVE and NVD results.
colors:
  primary: "#123C45"
  neutral: "#FFFFFF"
typography:
  heading:
    fontFamily: system-ui, sans-serif
    fontSize: 1.5rem
    fontWeight: 700
    lineHeight: 1.3
  body:
    fontFamily: system-ui, sans-serif
    fontSize: 1rem
    fontWeight: 400
    lineHeight: 1.5
rounded:
  sm: 4px
spacing:
  sm: 8px
  md: 16px
  lg: 24px
components:
  result:
    backgroundColor: "{colors.neutral}"
    textColor: "{colors.primary}"
    typography: "{typography.body}"
    padding: "{spacing.md}"
  status:
    backgroundColor: "{colors.neutral}"
    textColor: "{colors.primary}"
    typography: "{typography.body}"
    rounded: "{rounded.sm}"
    padding: "{spacing.sm}"
  logo:
    backgroundColor: "{colors.neutral}"
    textColor: "{colors.primary}"
---

## Overview

[REQUIREMENTS.md](REQUIREMENTS.md) is the sole authority for behavior and workflows. This document selects visual treatments only; it does not resolve requirement questions. Audience: UNKNOWN. Product display name: TO BE DECIDED; “NVD Envy” is a working label derived from the repository name (ASSUMPTION).

The selected direction is quiet, precise, and flat. Typography and explicit labels carry meaning. Component patterns are conditional on the result presentation decision in OQ-06; no graphical interface or navigation workflow is assumed.

## Colors

Use deep teal `primary` for all foregrounds and white `neutral` for all backgrounds. This is the only permitted foreground/background pairing, including text, borders, meaningful graphics, and focus indicators. Its contrast is 11.95:1 (rounded), exceeding WCAG 2.2 AA minima of 4.5:1 for normal text and 3:1 for large text, UI components, focus indicators, and meaningful graphics. Preserve full opacity in every state; do not add tinted surfaces or muted text.

Color does not encode NVD presence or exploit likelihood. Use explicit words, with classification semantics governed by REQUIREMENTS.md.

## Typography

Use `heading` for result-group headings and `body` for records and labels. Keep identifiers intact and readable; wrap surrounding content. Use sentence case, relative text sizing, and the local system font. No external font assets are required.

## Layout

Use a single reading order, with headings before their associated records. Apply `sm` between related labels, `md` within result groups, and `lg` between groups. Allow content to wrap and reflow without clipping at enlarged text sizes. Fields, grouping, ordering, and the actual presentation medium remain TO BE DECIDED under DQ-1.

## Elevation & Depth

Use spacing, heading weight, and primary-colored boundaries on white to establish hierarchy. No shadows, overlays, gradients, or opacity changes.

## Shapes

Use `sm` corners on status containers. The logo is one continuous geometric N-shaped path, representing the working name without suggesting a verified security outcome. Its white backing preserves contrast across embedding contexts. Keep the square aspect ratio and clear space built into the viewBox; do not crop, recolor, or add detail.

## Components

| Pattern | Compact presentation rule | Requirement boundary |
| --- | --- | --- |
| Result | Heading followed by consistently aligned record content; use `result` tokens. | FR-001; fields and merge structure await OQ-01–03. |
| NVD status | Plain-language status beside the corresponding record; use `status` tokens. | FR-002; absence claims await matching and coverage decisions, OQ-02/04. |
| Likelihood status | Plain-language classification beside the corresponding record; use `status` tokens. | FR-003; evidence, criterion, period, and scope await OQ-05/07. |
| Logo | Use root `logo.svg` as a single mark; supply its title or equivalent accessible image name. | Visual identity only. |

Do not present unresolved evidence as a confirmed absence or a high/low classification. Exact unresolved-result treatment remains TO BE DECIDED. If a chosen presentation includes interactive elements, retain the same colors across states, use underlining for text links, and provide a visible primary-colored focus outline separated from the element by white space. This does not prescribe new controls.

## Do's and Don'ts

- Do trace result semantics to FR-001–003 and their open questions.
- Do use UNKNOWN for unprovided facts, TO BE DECIDED for pending decisions, and ASSUMPTION for unsupported inferences.
- Do retain textual distinctions and the approved contrast pairing at every size and state.
- Don't invent scores, thresholds, data sources, record fields, update timing, or interaction workflows.
- Don't imply the logo or a status label certifies safety or exploitability.

## Open Questions

| ID | Decision | Status / dependency |
| --- | --- | --- |
| DQ-1 | Presentation medium, record fields, grouping, and ordering | TO BE DECIDED; OQ-01/03/06/08. |
| DQ-2 | Labels for incomplete data, unmatched records, and unresolved likelihood | TO BE DECIDED; OQ-02/04/05/07. |
| DQ-3 | Audience and final product display name | Audience UNKNOWN; name TO BE DECIDED. |
| DQ-4 | Supported environments and measurable accessibility acceptance conditions beyond this visual contrast guardrail | TO BE DECIDED; OQ-08. |
| DQ-5 | Presentation of result timing and updates, if required | TO BE DECIDED; OQ-09. |

Format reference: [official Google DESIGN.md specification](https://github.com/google-labs-code/design.md/blob/main/docs/spec.md). These visual choices do not close any requirements question.
