# Secure Coding

## Secure-Coding Inputs

- Read `REQUIREMENTS.md`, `DESIGN.md`, and `ARCHITECTURE.md`. No existing `SECURITY.md` was present. The candidate security notes are the Manicode pack list in the task.
- Confirmed: the system merges CVE records with NVD entries (FR-001), shows records without an NVD entry (FR-002), and shows records with high exploit likelihood (FR-003). `ARCHITECTURE.md` proposes source adapters, a classification core, and result delivery across external-data and possible client boundaries. `DESIGN.md` forbids presenting unresolved evidence as a confirmed result.
- Confirmed developer inputs recorded in `ARCHITECTURE.md`: “Node.js” as server framework, “fastify” as server runtime, and React.js as client framework. Node.js and Fastify have reversed technical roles in those labels; resolution is TO BE DECIDED. Versions are UNKNOWN. A graphical client surface is UNKNOWN.
- Sources, record schema, matching, coverage, likelihood method, presentation medium, access model, persistence, deployment environment, and measurable security expectations remain TO BE DECIDED (`REQUIREMENTS.md` OQ-01–OQ-09; `ARCHITECTURE.md` AQ-1–AQ-9). These gaps do not establish candidate-pack applicability.

## Selected Manicode Prompts

- Corpus root: `/Users/jmanico/Dropbox/github/aegis/secure-coding-knowledge`.
- Direct selections: **none**. Node.js, Fastify, and React.js are named without versions; `js/nodejs/26` and `js/fastify/5.12` cannot be selected. React.js does not confirm React Native, so `js/react-native/0.87` cannot be selected. No authoritative document confirms Better Auth, Keycloak, Android SDK, iOS SDK, Cedar, OpenFGA, SpiceDB, Open Policy Agent, Zod, Prisma, or Dockerfile, let alone their candidate versions. All direct candidates remain unselected pending OD-1 or OD-2.
- Transitive eligibility checked from each candidate's manifest. `js/nodejs/26` includes `js/javascript/ES2026`; `js/react-native/0.87` includes `js/react/19`, `js/typescript/7`, then `js/javascript/ES2026`; `js/fastify/5.12`, `js/better-auth/1.7`, and `js/prisma/7.10` include `js/nodejs/24`, `js/typescript/7`, then `js/javascript/ES2026`; `js/zod/4` includes `js/typescript/7`, then `js/javascript/ES2026`; `jvm/keycloak/26.7` includes `jvm/java/25`; `jvm/android-sdk/37` includes `jvm/kotlin/2.4`; `swift/ios-sdk/27` includes `swift/swift/6.4`. The four `policy/*` candidates and `infra/dockerfile/1` have no parents. No parent is independently selected. In particular, Fastify's candidate parent Node.js 24 does not establish Node.js 24 for this project.
- Ordered composition: **none** (zero direct and zero transitive packs). Consequently there are no selected pack prompt or source paths. Candidate files were inspected as `content/<pack>/manifest.json`; any future selected pack must list both `content/<pack>/prompt.md` and `content/<pack>/sources.md` here, in resolver order.
- Preamble, listed separately: `content/preamble.md`. It applies as general guidance without selecting a technology pack.

## Secure-Coding Rules

**SC-001 — Keep classifications in the core**
- **Status:** ACTIVE
- **Rule:** The Fastify result-delivery layer and any client MUST use the core's NVD-presence and likelihood outcomes; they MUST NOT independently infer those outcomes from missing fields or display values.
- **Enforcement:** Proposed merge and classification core; Fastify result delivery; conditional presentation adapter.
- **Evidence:** `ARCHITECTURE.md` DR-2 and Components and Flows; `DESIGN.md` Components; `content/preamble.md` (apply rules to touched code and verify access or validation logic).
- **Verification:** For a test input with unresolved matching or likelihood evidence, result delivery and any client preserve the core's unresolved state and do not emit a confirmed absence or high-likelihood label.

**SC-002 — Keep source formats outside the core**
- **Status:** ACTIVE
- **Rule:** Source adapters MUST interpret externally obtained records before passing them to the core; the core MUST NOT use source-specific parsing or transport behavior to decide matching or classification.
- **Enforcement:** Proposed source-adapter boundary and merge and classification core.
- **Evidence:** `ARCHITECTURE.md` Trust boundaries and DR-1; `REQUIREMENTS.md` FR-001–FR-003; `content/preamble.md` (apply rules to touched code and verify validation logic).
- **Verification:** A source-format change is handled in its adapter, and a malformed or uninterpretable source record cannot produce a confirmed NVD-absence or high-likelihood outcome.

**SC-003 — Preserve uncertainty in rendered results**
- **Status:** ACTIVE
- **Rule:** A presentation implementation MUST NOT render incomplete NVD coverage or unresolved likelihood evidence as a confirmed absence or high-likelihood finding.
- **Enforcement:** Conditional presentation adapter, with result-state authority in the core.
- **Evidence:** `DESIGN.md` Components; `ARCHITECTURE.md` Main flow and DR-2; `content/preamble.md` (apply rules to touched code and run relevant checks).
- **Verification:** Rendered results for incomplete coverage and missing likelihood evidence use unresolved states; neither case displays a confirmed absence or high-likelihood label.

**SC-004 — Access enforcement**
- **Status:** BLOCKED — Access rules and whether authentication or sessions exist are TO BE DECIDED (OD-3). No implementation instruction applies yet.

**SC-005 — Version-specific implementation controls**
- **Status:** BLOCKED — Confirmed technologies lack versions and other candidate technologies lack adoption evidence (OD-1, OD-2). No candidate prompt can supply an applicable implementation rule yet.

**SC-006 — Source and result handling controls**
- **Status:** BLOCKED — Source identity, required fields, data sensitivity, coverage, freshness, persistence, and security obligations are TO BE DECIDED (OD-4). Specific validation, storage, and retention rules cannot yet be stated.

## Open Security Decisions

- **OD-1:** Confirm the Node.js/Fastify role-label conflict and exact versions, if chosen. Evidence: corrected authoritative architecture inputs or implementation decision. Affects SC-005; candidates `js/nodejs/26`, `js/fastify/5.12` and their transitive parents. Owner: UNKNOWN.
- **OD-2:** Confirm the target presentation surface, client technology and version, and adoption and versions of any other candidate technology. Evidence: updated `REQUIREMENTS.md`/`ARCHITECTURE.md` and, for browser behavior, `DESIGN.md`. Affects SC-005 and client coverage; candidates `js/react-native/0.87`, `js/better-auth/1.7`, `jvm/keycloak/26.7`, `jvm/android-sdk/37`, `swift/ios-sdk/27`, `policy/cedar/4.12`, `policy/openfga/1.19`, `policy/spicedb/1.56`, `policy/open-policy-agent/1.20`, `js/zod/4`, `js/prisma/7.10`, and `infra/dockerfile/1` with their transitive parents. Owner: UNKNOWN.
- **OD-3:** Decide whether access restrictions, authentication, sessions, or authorization are required and where they apply. Evidence: behavior and users in `REQUIREMENTS.md`, then interfaces in `ARCHITECTURE.md`. Affects SC-004 and auth-related candidate packs. Owner: UNKNOWN.
- **OD-4:** Decide data sources and fields, matching and coverage rules, likelihood evidence, data sensitivity, persistence, freshness, and measurable security obligations. Evidence: resolved `REQUIREMENTS.md` OQ-01–OQ-09 and corresponding architecture boundaries. Affects SC-006 and refinement of SC-001–SC-003. Owner: UNKNOWN.
