![NVD Envy logo](logo.svg)

# nvd-envy

A project to combine CVE records with National Vulnerability Database (NVD) entries and show coverage gaps and high exploit likelihood.

The repository currently contains requirements and visual design documents. No implementation is provided, and no functional requirement has been verified.

## Scope

| Requirement | Intended outcome |
| --- | --- |
| FR-001 | Merge CVE records and NVD entries. |
| FR-002 | Show CVE records without an NVD entry. |
| FR-003 | Show CVE records with high exploit likelihood. |

[REQUIREMENTS.md](REQUIREMENTS.md) is the sole source of truth for behavior, workflows, acceptance checks, and unresolved requirements. [DESIGN.md](DESIGN.md) defines visual tokens, compact presentation patterns, contrast guardrails, and unresolved design decisions. [logo.svg](logo.svg) contains the matching vector mark.

## Current decisions

Data sources, matching and merge rules, coverage criteria, likelihood evidence and thresholds, result presentation, operating environments, and update timing are TO BE DECIDED. Intended audience is UNKNOWN. “NVD Envy” is a working display name inferred from the repository name (ASSUMPTION).

Resolve the applicable open questions in REQUIREMENTS.md before defining behavior or final acceptance tests. Keep visual decisions in DESIGN.md and preserve the distinction between missing evidence and a confirmed result.
