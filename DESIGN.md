# Design

## Surface

NVD Envy is a noninteractive command-line program. Its output is plain text on stdout; failures go to stderr with a nonzero exit status. There are no browser, mobile, or graphical controls. The repository logo is not part of terminal output.

## Result presentation

Print a short summary with the counts of published CVEs examined, NVD entries matched, CVEs missing from the completed NVD snapshot, high-EPSS CVEs, and NVD-only entries. Print the CVE List release, NVD retrieval time, and EPSS score date before findings.

Use the headings “No NVD entry in retrieved snapshot” and “EPSS ≥ 10% (next 30 days).” Sort each group by CVE ID. Each row uses consistent plain-language labels for CVE ID, NVD state, EPSS probability or `unknown`, and source dates. A record may appear in both groups. An empty group says `0 records`.

Never use color as the only way to convey status. Default output uses no color, decorative graphics, or interactive terminal behavior. Keep identifiers intact; allow long rows to wrap naturally. Labels must distinguish absence in the retrieved NVD snapshot from a claim that no NVD entry will ever exist, and an unknown EPSS value from a low score.

## Identity

“NVD Envy” is the display name. The existing `logo.svg` is a repository mark only. Its deep teal and white palette does not constrain the terminal's user-selected foreground and background colors.
