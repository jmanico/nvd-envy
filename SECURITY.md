# Secure Coding

## Secure-Coding Inputs

- Read `REQUIREMENTS.md`, `ARCHITECTURE.md`, and `DESIGN.md`. The confirmed surface is a local Node.js 26 command-line program using three public HTTPS data sources and a local cache. There is no server, browser client, account, session, or database.
- The source data is untrusted until the adapters validate it. A complete validated snapshot is required for an NVD absence claim. The core owns classification, and the terminal presenter owns only output formatting.

## Selected Manicode Prompts

- Corpus root: `/Users/jmanico/Dropbox/github/aegis/secure-coding-knowledge`.
- Direct selection: `js/nodejs/26`, confirmed by `ARCHITECTURE.md` Required Architecture Inputs and Technology decisions. Prompt `content/js/nodejs/26/prompt.md`; sources `content/js/nodejs/26/sources.md`.
- Ordered composition: (1) transitive `js/javascript/ES2026`, prompt `content/js/javascript/ES2026/prompt.md`, sources `content/js/javascript/ES2026/sources.md`; (2) direct `js/nodejs/26`, prompt and sources above. Resolved with `scripts/resolve_prompt.py --json js/nodejs/26`.
- Preamble, separately: `content/preamble.md`.
- Fastify, React Native, Better Auth, Keycloak, Android SDK, iOS SDK, Cedar, OpenFGA, SpiceDB, Open Policy Agent, Zod, Prisma, and Dockerfile candidates are not selected because their technologies are absent from the chosen architecture. Their transitive packs are not selected through them.

## Secure-Coding Rules

**SC-001 — Keep classifications in the core**
- **Status:** ACTIVE
- **Rule:** The CLI and terminal presenter MUST use the core's NVD-presence and EPSS outcomes and MUST NOT infer them from missing display fields.
- **Enforcement:** Merge and classification core; terminal presenter.
- **Evidence:** `ARCHITECTURE.md` DR-2; `REQUIREMENTS.md` FR-002–FR-003; `content/preamble.md`.
- **Verification:** An incomplete NVD fixture yields no absence finding; an absent EPSS score yields `unknown`, never high or low.

**SC-002 — Validate source data before use**
- **Status:** ACTIVE
- **Rule:** Source adapters MUST bound and validate downloaded JSON/CSV and reject malformed or duplicate CVE IDs, unexpected states, invalid EPSS probabilities, and incomplete NVD pagination before publishing a snapshot.
- **Enforcement:** CVE, NVD, and EPSS source adapters at the network-to-snapshot boundary.
- **Evidence:** `REQUIREMENTS.md` Data and decisions; `ARCHITECTURE.md` Components and data flow; `content/js/javascript/ES2026/prompt.md` Validation and Structured data and queries; `content/js/nodejs/26/prompt.md` Filesystem and paths.
- **Verification:** Oversized, malformed, duplicated, out-of-range, or truncated fixtures are rejected and cannot replace the last complete snapshot.

**SC-003 — Render untrusted text safely**
- **Status:** ACTIVE
- **Rule:** Terminal output MUST treat downloaded text as data and neutralize control characters before printing it; it MUST NOT execute source-provided content or use source text as a format string.
- **Enforcement:** Terminal presenter and error formatter.
- **Evidence:** `DESIGN.md` Surface and Result presentation; `content/js/javascript/ES2026/prompt.md` Asynchrony and logs; `content/js/nodejs/26/prompt.md` Child processes, addons, and FFI.
- **Verification:** A fixture containing newline, escape, or other control characters cannot add a forged finding or change terminal formatting.

**SC-004 — Keep the run local**
- **Status:** ACTIVE
- **Rule:** The program MUST NOT start an inbound listener, collect credentials, or send CVE findings to any destination; network requests MUST target only the three selected public data sources and approved redirects.
- **Enforcement:** CLI entry and source adapters.
- **Evidence:** `REQUIREMENTS.md` Operating and quality requirements; `ARCHITECTURE.md` Required Architecture Inputs and DR-5; `content/js/javascript/ES2026/prompt.md` URLs and SSRF.
- **Verification:** Network interception shows only source downloads; no listening socket or outbound results request is created.

**SC-005 — Use a supported runtime**
- **Status:** ACTIVE
- **Rule:** Builds and releases MUST run an up-to-date Node.js 26 security release and MUST fail the runtime check when the installed 26.x version is affected by a known security advisory.
- **Enforcement:** Build and release checks for the CLI.
- **Evidence:** `ARCHITECTURE.md` Technology decisions; `content/js/nodejs/26/prompt.md` Release line and upgrade posture; `content/js/nodejs/26/sources.md` Node.js security releases and runtime-check references.
- **Verification:** A vulnerable runtime fixture fails the release check; the checked and packaged runtime versions are recorded.

**SC-006 — Publish only complete snapshots**
- **Status:** ACTIVE
- **Rule:** The snapshot manager MUST write a refreshed bundle privately and replace the usable cache only after all three source snapshots pass validation; it MUST NOT emit findings from an expired or partial bundle.
- **Enforcement:** Snapshot manager and CLI exit path.
- **Evidence:** `REQUIREMENTS.md` FR-004–FR-005; `ARCHITECTURE.md` DR-4; `content/js/nodejs/26/prompt.md` Filesystem and paths.
- **Verification:** Interrupting or corrupting a refresh preserves the prior complete cache, and an expired cache causes a nonzero exit without findings.
