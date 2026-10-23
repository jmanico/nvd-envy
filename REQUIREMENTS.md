# Requirements

## Purpose and scope

NVD Envy is a local command-line program for comparing all published CVE records with NVD entries and highlighting CVEs with high predicted exploit likelihood. It is a public-data research tool, not an asset-specific risk score.

| ID | Requirement | Acceptance check |
| --- | --- | --- |
| FR-001 | The program MUST merge every published record in the official CVE List V5 snapshot with NVD CVE API 2.0 entries by exact CVE ID. | Given published and rejected CVE fixtures and NVD fixtures, the merged set contains each published CVE once, excludes rejected records, and attaches an NVD entry only for an exact ID match. |
| FR-002 | The program MUST show published CVEs with no entry in a completed NVD snapshot. | Given a complete NVD fixture, the missing-NVD list contains exactly the published CVE IDs absent from it; an incomplete NVD fixture yields no absence claims. |
| FR-003 | The program MUST show published CVEs whose FIRST EPSS probability is at least 0.10. | Given dated EPSS fixtures around 0.10, the high-likelihood list contains exactly records with scores at or above 0.10; missing scores are never classified high or low. |
| FR-004 | The program MUST report the provenance and retrieval date of each source used in a result. | A completed run identifies the CVE List release, NVD retrieval time, and EPSS score date. |
| FR-005 | The program MUST fail without publishing a new result when any source download or completeness check fails and no complete cache younger than 24 hours exists. | With a truncated source and expired cache, the command exits nonzero, explains which source failed, and prints no findings. |

## Data and decisions

- **CVE universe:** All `PUBLISHED` records in the latest available midnight baseline release of the [official CVE List V5](https://github.com/CVEProject/cvelistV5/blob/main/README.md). `REJECTED` and `RESERVED` records are outside the result universe. A duplicate or malformed ID or invalid archive checksum invalidates the new snapshot.
- **NVD source:** The [NVD CVE API 2.0](https://nvd.nist.gov/developers/vulnerabilities), retrieved across all pages without a CVE filter. Pages must have contiguous offsets, consistent `totalResults`, and exactly that many unique entries; otherwise the refresh fails. Match exact, case-normalized CVE IDs. NVD-only IDs do not create CVE-list results; count them in a diagnostic summary. Duplicate or malformed NVD IDs invalidate the new snapshot. An absent entry means absent from the completed NVD retrieval, not proof that NVD will never publish it.
- **Exploit likelihood:** The complete [FIRST EPSS daily CSV](https://www.first.org/epss/data.html). Use its `epss` probability, not its percentile. EPSS estimates exploitation observed in the next 30 days; 0.10 is this project's display threshold, not an official FIRST cutoff. Check all published CVEs, whether or not NVD has an entry. An absent score remains `unknown`; a malformed or duplicate row or invalid gzip checksum invalidates the new EPSS snapshot. A low score is not a safety guarantee. [FIRST explains the measure and lack of a universal threshold](https://www.first.org/epss/faq).
- **Merge result:** One record per published CVE ID containing the source CVE record, optional exact-ID NVD entry, optional EPSS probability/date, and explicit NVD and likelihood states. Preserve source-specific fields separately; never resolve conflicting source values by overwriting one with the other.
- **Timing:** On each invocation, use a complete local snapshot bundle only while every source retrieval in it is less than 24 hours old; otherwise download a fresh CVE baseline, all NVD pages, and the latest EPSS CSV. Publish a replacement bundle only after every source validates. Show each source's actual date because publication times need not coincide. No background scheduler or historical store is required.
- **Output:** Print a summary and two CVE-ID-sorted groups: “No NVD entry in retrieved snapshot” and “EPSS ≥ 10% (next 30 days).” An ID can appear in both groups. Each row shows CVE ID, NVD state, EPSS probability or `unknown`, and relevant source dates. Print `0 records` for an empty group. Print data errors to stderr and exit nonzero; do not emit findings based on incomplete data.

## Operating and quality requirements

- The target is a local terminal on a supported Node.js 26 host with outbound HTTPS and enough local space for full public-source snapshots. Store the cache under the invoking user's home directory in `.cache/nvd-envy`, with user-only access. No web, mobile, API, account, session, or server surface is required. The operator starts each run explicitly.
- Handle the full published CVE corpus with bounded streaming or pagination rather than loading all raw source documents at once. A successful run must complete all records, with no arbitrary top-N cut-off. No response-time or availability service-level target applies to this local command.
- Treat downloaded records as untrusted. No personal or regulated data is intentionally collected. Keep cache and result files local to the invoking user; do not send CVE findings to another service. Use official HTTPS source locations.
- Terminal output uses plain text, stable headings, intact identifiers, and explicit status words. It must remain readable without color or terminal interaction.

## Source notes and decision basis

The initial project notes asked to merge CVEs with NVD, show gaps, and identify CVEs likely to be exploited (S-01–S-03). The user selected a command-line application and all available CVEs, then delegated remaining decisions. The named sources and 0.10 threshold are project decisions made under that delegation; the external source documentation does not mandate the threshold.
