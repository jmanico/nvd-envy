# Requirements

## Purpose

This document defines what the system must do. The project notes are the only source of requirements. This document does not select a design, a data provider, or a method to calculate exploit likelihood.

Requirement descriptions use short sentences, consistent terms, and `shall` for mandatory behavior. Technical terms are defined below.

## Source Notes

> * program  that will merge CVE's and NVD's  and show which CVE's do not have a NVD entry
> * which CVE's are highly likely to be exploited

| Source ID | Source intent |
| --- | --- |
| S-01 | Merge CVE records and NVD entries. |
| S-02 | Show CVE records that do not have an NVD entry. |
| S-03 | Show CVE records that are highly likely to be exploited. |

## Terms

| Term | Meaning in this document |
| --- | --- |
| CVE record | A record for a vulnerability identified by CVE. The record source and required fields are not specified. |
| NVD entry | An entry in the National Vulnerability Database. The entry source and required fields are not specified. |
| Merge | Combine CVE records and NVD entries. The matching rules and result structure are not specified. |
| Exploit likelihood | The likelihood that a vulnerability will be exploited. The measure and time period are not specified. |
| High exploit likelihood | An exploit likelihood that meets an agreed criterion for high likelihood. That criterion is not yet specified. |

## Functional Requirements

Each requirement has one obligation. Each acceptance check tests that obligation separately. An unresolved test rule is listed as an open question. These questions must be answered before the affected check can have a final pass or fail result.

### FR-001 — Merge records

**Requirement:** The system shall merge CVE records and NVD entries.

**Source:** S-01.

**Acceptance check:** Supply a defined set of CVE records and NVD entries. Compare the merge result with an expected result prepared from the agreed merge rules. The check passes when the results agree.

**Decisions required:** OQ-01, OQ-02, OQ-03.

### FR-002 — Show records without an NVD entry

**Requirement:** The system shall show which CVE records do not have an NVD entry.

**Source:** S-02.

**Acceptance check:** Supply a defined set that contains CVE records with an NVD entry and CVE records without an NVD entry. Use the agreed matching rules to prepare the expected set of records without an NVD entry. The check passes when the system identifies all and only the records in that expected set.

**Decisions required:** OQ-01, OQ-02, OQ-04, OQ-06.

### FR-003 — Show records with high exploit likelihood

**Requirement:** The system shall show which CVE records have high exploit likelihood.

**Source:** S-03.

**Acceptance check:** Supply a defined set of CVE records with the evidence required by the agreed likelihood criterion. Include records that meet the criterion and records that do not meet it. The check passes when the system identifies all and only the records that meet the criterion.

**Decisions required:** OQ-01, OQ-05, OQ-06, OQ-07.

## Non-functional Requirements

The project notes specify no non-functional requirements. Thus, this document defines no mandatory non-functional limits or acceptance checks.

Performance, capacity, availability, security, privacy, accessibility, and supported operating environments remain unresolved in OQ-08. A future requirement for any of these subjects must include a measurable acceptance condition.

## Verification Status

| Requirement | Separate test objective | Status |
| --- | --- | --- |
| FR-001 | Confirm the merge result. | Test rules are incomplete. See the listed open questions. |
| FR-002 | Confirm the set of records without an NVD entry. | Test rules are incomplete. See the listed open questions. |
| FR-003 | Confirm the set of records with high exploit likelihood. | Test rules are incomplete. See the listed open questions. |

The notes support these three obligations. They do not support fully specified test cases. No requirement is verified by this document.

## Open Questions

| ID | Unresolved decision | Affected requirements |
| --- | --- | --- |
| OQ-01 | Which CVE and NVD data sources must the system use? Which records are in scope? Which fields must be available? | FR-001, FR-002, FR-003 |
| OQ-02 | What rule determines that a CVE record has a corresponding NVD entry? How must the system treat duplicate records and identifiers that are missing or not valid? | FR-001, FR-002 |
| OQ-03 | What must the merge result contain? Which fields must it retain? How must it treat conflicting values, CVE records without NVD entries, and NVD entries without corresponding CVE records? | FR-001 |
| OQ-04 | What data coverage and data age are sufficient to conclude that an NVD entry does not exist? How must the system treat incomplete or unavailable NVD data? | FR-002 |
| OQ-05 | What evidence or method determines exploit likelihood? What criterion makes that likelihood high? What time period does the likelihood cover? | FR-003 |
| OQ-06 | How must the system show each result? Which information must it show for each identified CVE record? | FR-002, FR-003 |
| OQ-07 | Must the likelihood check cover all CVE records or only records without an NVD entry? How must the system treat missing, old, or conflicting likelihood evidence? | FR-003 |
| OQ-08 | What measurable non-functional requirements apply? Specify any required response times, data volumes, availability, security controls, privacy controls, accessibility criteria, and operating environments. | Non-functional requirements |
| OQ-09 | When must the system obtain data and produce results? Are repeated runs or data updates required? | FR-001, FR-002, FR-003 |

No answer to an open question is assumed. Add or revise requirements when these decisions are made.
