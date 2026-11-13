> Public GitHub edition. Internal grading and self-assessment material from the working review copy has been omitted. Technical scope, evidence boundaries, acceptance criteria, risks, and release gates are preserved.

# SiteCustody
Website Control, Dependency, and Transfer-Readiness Documentation
Revised Executive Product and Engineering Proposal — v3.0
Prepared: November 12, 2026
Audience: Tristan, the joint project owners, executive engineering reviewers, and prospective maintainers
Project: Proposed open-source, offline-first documentation toolkit for small-business website owners
Decision requested: Approve the offline architecture and limited user-facing proof of concept; withhold authorization for network scanning or a public production release
Status: Revised written specification with a locally tested reference-contract appendix, not a completed application
Revision note (November 12, 2026): This version consolidates the verified prior engineering specification with the later research brief. It is a newly produced document, not the missing original Deep Research attachment. Technical claims about unbuilt features are acceptance requirements, not observations of working software.
## 1. Executive summary
SiteCustody helps a website owner understand which services their website depends on, what control evidence exists, what backup assurance is actually demonstrated, and which unanswered questions must be resolved before changing vendors. Its initial product is a guided offline inventory and an evidence-labeled, default-redacted handoff report. It is deliberately not an ownership verification service, a crawler, a security scanner, a backup solution, or a migration executor.
Product promise: Know what you control before you attempt to move it.
A small business can pay for a website while domain registration, authoritative DNS, hosting, site-builder accounts, source code, content, email, forms, billing, and backups are controlled through different vendors. This becomes especially painful when the business needs to change hosting providers or developers. The critical gap is not usually a missing web scan: it is missing documented access and dependencies.
The proposed release must prioritize accurate distinctions over a convenient green checkmark. For example, DNS records can show a nameserver provider but cannot establish that the business controls the DNS account. A provider invoice may show a paid service but does not demonstrate that content can be exported. A backup file may exist but be untested for restoration. SiteCustody keeps these observations separate.
Recommended approval: Begin with a small, offline proof: one synthetic business record, a functioning reference validator, a default-redacted report, and a browser-local questionnaire prototype. No public deployment, credentialed integration, live probing, or actual client-site migration is approved by this document.
## 2. Target user and validated versus unvalidated assumptions
Primary user: a nontechnical small-business owner preparing to switch website vendors or secure continuity of operations. Secondary user: an incoming developer who needs a consistent account-control and dependency handoff. Other prospective users: nonprofit administrators, freelancers taking over a website, and small agencies preparing client transitions.
Observed founder need: The project's owners have handled real questions about a business website's hosting, domain, vendor independence, and exportability. This justifies investigating a tool, but it does not prove that other owners will install software or prefer it to a spreadsheet.
User jobs:
Identify which domain, DNS, hosting, content, email, form, and backup services matter to the site.
Identify what the owner, staff, or developer says they can access, and what a human claims to have witnessed.
Map dependencies that could break during a vendor change, particularly DNS-dependent website and email routing.
Distinguish a reported backup from a dated, scope-specific restoration exercise.
Produce questions and action codes for an incoming developer without exporting contact details, account IDs, private provider notes, or credentials.
Avoid taking action against a live website while merely planning a transition.
Unvalidated hypothesis: Owners can identify more important transition blockers, and explain them more accurately, using SiteCustody than with a conventional checklist. A user study must demonstrate this before broader product investment.
Non-negotiable language boundary
SiteCustody must never display "legal ownership verified," "domain ownership certified," "backup guaranteed," "safe to migrate," or "transfer authorized" on the basis of the recorded questionnaire, manual attestations, public DNS data, or a successful limited restore test. Legal entitlement and actual administrative authority require separately established evidence beyond this software's remit.
## 3. Competitor positioning and differentiation to validate
Evidence, not marketing: The existence of related open-source projects demonstrates adjacent work, not an unmet market need. The proposed advantage is a precise, printable control map with independently classified attestation levels and privacy-preserving transfer questions. Compare actual outcomes with a spreadsheet, not only GitHub stars or developer enthusiasm.
Product stop condition: If independent owners can complete the same task equally well using a two-page checklist, publish the schema and checklist as a small public resource rather than building a larger app merely to justify its existence.
## 4. Scope: an offline first release, with network checks explicitly excluded
Proposed v0.1.0: local questionnaire and report
A single-file, offline-capable guided browser form for the nontechnical primary audience. It must work without Node, Python, a login, or a network connection on a supported browser; no telemetry or third-party fonts/scripts.
A versioned JSON data contract for an owner-entered inventory, using a fixed set of essential service roles and explicit applicability states.
An independent built-in profile, public_business_site_v1, that requires the owner to account for domain registration, authoritative DNS, site hosting, site content, backups, business email, and contact forms. Optional items may be recorded as not applicable with a reason; essential control roles cannot be silently omitted.
A typed service-to-service dependency list with references checked for existence, self-links, duplicates, exempted targets, and cycles that need human review.
Evidence observations with scope, source category, actor role, date, outcome, and whether a human-witnessed step is recorded; no claim of verified witness identity.
Dated backup-test records with coverage, result, environment, and linked observations. The system never converts a successful subset restoration into full-site assurance.
A default-redacted JSON and printable Markdown handoff report created using a field allowlist, not substring removal after rendering.
A versioned rule catalogue and deterministic findings; all network actions are disabled/absent in v0.1.
Public synthetic examples, installation-free trial instructions, automated reference-contract tests, and a release checklist.
The companion Python reference validator in the appendix demonstrates the data and redaction contract and is not presented as the eventual user-facing application. A future browser form will need its own browser, accessibility, and security tests.
Explicitly out of v0.1.0
No domain login, password storage, account recovery, DNS changes, HTTP requests, recursive crawling, SSL probes, RDAP queries, WHOIS searches, credentialed provider APIs, backups, downloads of website content, form submissions, Search Console access, email forwarding changes, domain transfers, paid monitoring, or live migration. No claim of exhaustive vendor discovery or legal title verification.
Conditional v0.2 or later
Owner-authorized public DNS observations may be examined as a separate workstream only after written security review, per-run consent design, resolved IP filtering, and mocked DNS rebinding tests. Live HTTP/HTTPS inspection is more sensitive and remains deferred even if DNS support is accepted. No retained networkConsent flag or hidden background monitoring is allowed. Any new provider integration needs its own least-privilege credential policy and explicit opt-in.
## 5. Essential service and applicability rules
The independent public_business_site_v1 profile requires seven roles:
Other providers (analytics, payment processing, and integration services) may be documented. Their absence is not evidence that the site lacks those dependencies. The UI should ask whether other critical services exist rather than assert completeness from a fixed category list.
Every role has applicability = applies | not_applicable | unknown and control.accessStatus = unknown | self_reported | human_witnessed. These are independent axes. A service can be known to exist while access is unknown. An exemption is recorded, not automatically inferred from missing files or lack of knowledge.
A canonical service ID is not an email address, login ID, or secret. A private provider label may be stored in the local inventory but never copied to the default shareable report.
## 6. Evidence and provenance semantics
The strongest architectural correction is distinguishing who reported something from what was truly verified.
Each observation has a stable ID, linked service ID, type, subject, UTC timestamp, actor role, outcome, and witness role when applicable. It contains no personal names, passwords, screenshots, account IDs, or freeform secret-bearing notes. A local record is evidence of an attestation, not proof that it occurred as described.
Referential and temporal validation
Every observation reference must exist and belong to the relevant service. Duplicates are flagged.
self_reported access needs a matching, passing operator_statement about account-control review; human_witnessed needs a matching, passing human_witnessed_step with an attested witness role. Invalid references cannot upgrade evidence status.
An explicit asOf timestamp controls deterministic freshness checks. Observations later than asOf are invalid for the snapshot; observations older than the proposed 90-day policy threshold are flagged for refresh. The threshold is configurable only through a versioned policy decision.
A report must never calculate freshness relative to the local wall clock without recording the comparison instant. Repeated runs on the same snapshot should produce identical results.
The human_witnessed label must be presented as "witnessed according to recorded information", not authenticated proof.
## 7. Dependency graph and transfer-impact review
A service dependency is typed by a consumer ID, a required-provider ID, and a reason code. Illustrative relations include a website deployment's dependence on authoritative DNS, site content's reliance on hosting or a CMS, and form delivery's reliance on an email provider.
Example: a website is served by one host but email routes through another provider. Changing DNS without documenting both consumers could interrupt email even when the website still loads. The inventory records these relationships; it does not change DNS.
Version-one checks require:
Both endpoints refer to declared services.
No self-dependency and no duplicated link.
Dependencies pointing to an explicitly N/A service trigger review.
Cycles are reported as potential issues, not automatically forbidden, because legitimate service dependencies may form a cycle.
A dependencyReview status is recorded as unknown or self_reported_reviewed, with a timestamp and reviewer role for a completed attestation.
An empty graph and unknown review state create explicit findings. A reviewed graph is still not proof that no dependencies were omitted.
The v0.1 report must show a dependency count and review status, with omissions classified as unknown, never harmless by default. Full automated discovery is an entirely separate product and not on the initial roadmap.
## 8. Backup assurance: presence is not recoverability
Backups must be tracked on separate dimensions: artifact evidence, access evidence, restore-test outcome, test environment, and data coverage. A successful restore of images and pages does not establish recovery of databases, configuration, or contact forms.
A backup-test record requires serviceId, timestamp, outcome (pass | fail | inconclusive), environment (isolated_local | staging | production), a nonempty set of coverage categories, and linked evidence. Coverage categories are pages, media, database, configuration, forms, and other.
The v0.1 shareable report uses the conservative labels:
unknown: no supported backup artifact or restore assurance.
self_reported_artifact: local attestation that an artifact was seen.
human_witnessed_artifact: record of a witnessed artifact observation.
reported_restore: a dated restore attempt reported as passing, still unverified.
witnessed_restore_limited_scope: a recorded witnessed pass, explicitly limited to the documented data scope.
Neither reported_restore nor witnessed_restore_limited_scope means "complete disaster recovery verified." The software must issue blockers for failed restore attempts and missing tests, warnings for untested coverage, and a refresh finding after the proposed 180-day test-age threshold. A production-environment restore test creates an additional review warning, because staging or an isolated environment is preferable for planning exercises.
## 9. Versioned data contract: examples and derived reporting
The technical appendix includes full JSON Schema Draft 2020-12 documents and an executable offline reference validator. All user-supplied input remains local.
Illustrative inventory excerpt (the full synthetic fixture and schemas are included in the ZIP):
{
  "schemaVersion": "1.0.0",
  "siteKey": "sample_business",
  "domain": "example.org",
  "profile": "public_business_site_v1",
  "asOf": "2026-11-11T12:00:00Z",
  "services": [
    {
      "id": "registrar",
      "role": "domain_registration",
      "applicability": "applies",
      "providerLabel": "DEMO_PRIVATE_PROVIDER_REGISTRAR",
      "control": {"accessStatus": "self_reported", "observationIds": ["ev_registrar"]}
    }
  ],
  "dependencies": [],
  "dependencyReview": {"status": "unknown"},
  "observations": [
    {
      "id": "ev_registrar",
      "serviceId": "registrar",
      "kind": "operator_statement",
      "subject": "account_controls_seen",
      "outcome": "pass",
      "observedAt": "2026-11-10T18:00:00Z",
      "actorRole": "business_owner"
    }
  ],
  "backupTests": []
}
This excerpt is schema-valid but intentionally incomplete. The validator correctly reports missing essential roles and backup tests. It does not infer that absent data means the owner has no service. The appendix includes a complete synthetic seven-role fixture that generates a reference report.
Redacted report contract excerpt:
{
  "reportVersion": "1.0.0",
  "privacyMode": "redacted",
  "networkAccess": "not_used",
  "ownershipVerification": "not_performed",
  "migrationAuthorization": "not_assessed",
  "documentationState": "gaps_present",
  "backupAssurance": "reported_restore"
}
The actual report also includes predefined area summaries, dependency-review status, and stable issue/action codes. The schema forbids domain names, provider labels, operator notes, evidence IDs, passwords, contact details, absolute paths, and raw observations in default shared output. Redaction is based on allowlisting permitted fields before serialization—not finding and deleting sensitive-looking substrings afterward.
Data and report rules
Input records and output reports have separate version numbers. Unknown major versions are rejected rather than silently reinterpreted.
Required fields, types, lengths, and enums are validated against published schemas; unknown properties are rejected to minimize accidental secret storage.
Finding codes are stable within a major report version; findings are deterministically sorted.
Redacted output uses a fixed vocabulary of statuses/action codes and never interpolates private input strings.
documentationState = documented_for_review only describes the completeness of the recorded process. Even then, ownershipVerification = not_performed and migrationAuthorization = not_assessed stay unchanged.
The appendix's CLI returns 0 only for a clean reference-contract result, 1 for a completed report with unresolved findings, and 2 for invalid local input. These are reference behavior, not yet a production installation contract.
## 10. UX: no developer tools required for the primary user
The previous proposal assumed that a small-business owner would use a Python terminal. That contradicted its target audience. The revised product will have a browser-local, no-install form distributed as a downloadable package with a small static page. Python is a reference validation implementation and optional developer workflow, not a prerequisite for completing the user-facing questionnaire.
Owner path: open the offline page; read a short explanation of what it cannot verify; select a fictional starter or enter their own domain; answer one service at a time; mark access as unknown, self-reported, or human-witnessed-as-recorded; declare dependencies; document backup and restore history; review warnings; download a redacted report by default.
Developer path: review the redacted packet, ask the owner for access via an authorized external process, and record follow-up actions. A separate, explicitly chosen owner-private JSON export may be permitted after a warning and local confirmation, but is not the default attachment handed to another vendor.
Accessibility and deployment contract: the page runs without remote fonts or scripts, supports keyboard access, visible focus states and screen readers, works at desktop and mobile widths, avoids color-only statuses, and explains unfamiliar terminology in ordinary language. The first-run workflow must be tested on current mainstream browsers in offline mode. The app should not persist questionnaire data in browser storage unless an explicit user-controlled save feature is introduced and tested.
Export privacy lifecycle
The user chooses when to download a report; nothing is uploaded or automatically synced.
Default shareable export removes the site's domain, private service IDs, provider names, timestamps, internal locations, and freeform notes, because those can identify an organization or its infrastructure.
A separate private export, if implemented, must be clearly labeled as sensitive, saved only after explicit consent, and never automatically attached to public issue reports.
The tool cannot prevent OS backups, browser downloads, external cloud-sync folders, screenshots, or users from forwarding files. It must explain these limitations and provide manual deletion instructions without promising secure erasure.
Development fixtures, screenshots, and documentation may use only invented business names and example.org-style reserved demonstration domains.
10.1 Persistence, encryption, and local-file truth-in-advertising
The first public release must not solicit or store passwords, recovery codes, API keys, private SSH material, billing card data, or arbitrary account tokens. The questionnaire records whether access was checked, not authentication material. It must not claim application-level encryption at rest unless a documented cryptographic mechanism, key-management model, and recovery test exist. Users remain responsible for the security of their device and exported inventory files; OS full-disk encryption can be recommended but is not provided by the app.
Default operation is memory-only. Progress is saved only when the user deliberately selects a local, named export destination. No silent localStorage, IndexedDB, cloud synchronization, or autosaving sensitive inventory information is permitted in v0.1. Local editable exports may contain provider labels and therefore must be clearly marked confidential; the default shareable report must use an allowlisted set of non-sensitive fields, not after-the-fact text replacement. Validate that all default exported artifacts contain no personal contacts, internal paths, secret-like values, raw DNS TXT records, or proprietary identifiers, including in hidden metadata, filenames, and error messages.
## 11. Architecture, deterministic logic, and supply chain
Proposed application: static TypeScript/HTML/CSS form packaged for local use, no server or database. A JSON Schema validator (Ajv or equivalent) performs structural checks, and a pure domain-layer reducer produces the findings and shareable export. In the development process, an independent Python jsonschema implementation serves as a contract oracle to detect divergent interpretation. The two validators must agree on supplied golden fixtures and failure classifications before release.
Modules: questionnaire, inventory_schema, evidence_rules, dependency_graph, backup_assurance, redaction, export, and accessibility. The business logic has no network dependencies and produces consistent outputs from the same snapshot.
ADR-001 — Offline is a security boundary, not marketing language. The build must complete the core workflow with networking disabled. No hidden DNS lookups, Web APIs that send form contents, analytics SDKs, CDNs, or runtime update calls.
ADR-002 — Default redacted report. Shareable outputs are constructed from a strict allowlist. There is no permissive “full report” default.
ADR-003 — No claim of legal authority. Attestation labels remain separate from verified legal ownership and actual migration authorization.
ADR-004 — Explicit snapshot time. asOf controls freshness, avoiding nondeterminism caused by the current local time.
ADR-005 — Dependency graph is declared, not discovered. Unknown relationships are not automatically marked safe.
ADR-006 — Build no network scanner in v0.1. A future public-data module requires an independently approved threat model and mocked integration tests. This protects the small-business user and reduces release risk.
Repository proposal:
sitecustody/
  app/src/{questionnaire,evidence,dependencies,backups,redaction,export}/
  contract/schemas/{inventory,shareable_report}.schema.json
  contract/sample/{inventory,expected_redacted_report}.json
  contract/reference_validator.py
  contract/tests/test_reference_contract.py
  docs/{architecture,privacy,threat-model,decision-records}/
  .github/workflows/ci.yml
  README.md
  LICENSE
  CONTRIBUTING.md
  SECURITY.md
  package.json
Supply-chain controls: pin production dependencies, review third-party licenses, use least-privilege CI, test artifacts before tagging a release, and publish an SBOM/dependency summary when operationally feasible. Avoid introducing provider-specific connectors without a maintainer and a tested revocation story.
## 12. Threat model, consent, and release blockers
Absolute release blockers: unauthorized network activity; sensitive labels appearing in default redacted output; claims of verified legal title or migration permission; unhandled secret-bearing input in publicly shared reports; or silent elevation of missing evidence to confirmed access.
Future network consent contract (not implemented)
If later authorized, a public-domain inspection would require an explicit per-run selection of the exact normalized public hostname, allowed operations, and an unambiguous consent action. Stored application data cannot authorize future probes. DNS and HTTP must never be conflated: HTTP introduces redirect, TLS SNI, DNS rebinding, IP-filter, and response-size concerns. Before any HTTP functionality ships, security reviewers must require an implementation that connects only to an approved resolved public address while preserving correct hostname/TLS validation, rechecking all redirects and retries, with mocked rebinding and IPv6 fixtures. If this cannot be shown, keep the feature disabled. See OWASP's SSRF prevention guidance.
ICANN's RDAP lookup supplies registration data for gTLDs, but registrar visibility and public record values do not establish which individual controls the account. SiteCustody should initially link to the official lookup documentation rather than retrieve or interpret account-ownership data automatically.
12.1 Consent boundaries for any later networking feature
There is no network feature in v0.1, and no stored consent bit that enables later network access. If a future revision proposes public DNS or HTTPS observations, a new architecture review must define explicit per-run purpose and target, opt-in at the moment of the operation, DNS/IP enforcement, redirect constraints, timeout limits, an audit record that does not expose secrets, and separate test evidence for rebinding and private-address rejection. Public DNS data must never be described as proof of account authority or legal ownership. Failure to prove this safety model means the feature remains excluded.
## 13. Reference contract and local QA evidence
The accompanying technical appendix provides both published JSON Schemas, a synthetic inventory, expected redacted report, a local-only Python validator, and executable pytest cases. The reference run in this proposal's preparation passed 49 out of 49 tests locally. These tests measure schema semantics, contradictory states, evidence links, restoration scope, redaction, deterministic serialization, and input errors. They do not certify the browser UI, future network transport, deployment compatibility, or any real business owner's control.
A passing reference test establishes that the sample implementation enforces a specific contract for the fixtures tested. It does not prove that the eventual TypeScript app will agree in every case. The cross-language differential suite is a required release gate.
Release-blocking acceptance matrix
SC-01 through SC-21 are chiefly data-contract/reference tests; SC-22 through SC-30 require the future user interface and full release build. It would be inaccurate to claim the latter have passed today.
Metrics proposed for a release candidate: 100% of release-blocking cases on the supported browser matrix, no known P0 privacy or access-evidence defects, no outbound network requests in offline mode, and predictable report generation for a bounded synthetic inventory (up to 100 services, 300 links, 500 observations, and 100 backup tests; maximum input 1 MiB). Actual performance limits must be measured against a published test fixture and hardware profile. A suggested initial target is under 250 ms for the domain derivation step on a reference laptop, excluding browser startup; this is a target, not a measured result.
## 14. Delivery, staffing, and decision gates
The estimate assumes one experienced application engineer plus part-time product, accessibility, and security review. These are person-day planning ranges, not delivery promises.
The numbers exclude major new integrations and fully redesigned UI concepts. A Gate 0 technical owner must revise the estimate after comparing an actual questionnaire prototype with a spreadsheet, not simply approve the original estimate by default.
External validation before investing beyond prototype
Recruit 6–10 small-business owners or nonprofit administrators without close personal involvement in development. Give each a fictional multi-vendor website scenario containing intentionally missing registrar control, an untested backup, and an email/DNS dependency. Randomize whether participants start with a simple spreadsheet or SiteCustody. Measure (a) ability to identify the planted blockers, (b) unaided completion time, (c) false confidence, (d) report readability, and (e) number of credible next actions.
Continue threshold: At least 80% can finish the local workflow unaided, at least 70% identify all three planted blockers, zero participants interpret the report as a verified legal ownership statement after reading its labels, and at least five demonstrate a practical benefit relative to the spreadsheet. These are preliminary pilot thresholds, not a statistical proof of market demand. If the spreadsheet performs as well or better, publish a lightweight template rather than enlarge the application.
## 15. Open source, asset rights, and maintenance
Proposed licensing: MIT for new original software, subject to agreement by both project owners and review of dependencies. Public example domains must be reserved demonstrations such as example.org, not screenshots or data from real clients. The terms of example graphics, sample text, and any third-party content must be documented independently; a software license does not silently license every creative asset.
Public repository contents: code, synthetic test fixtures, both JSON Schemas, reference validator and tests, sample redacted reports, docs, security policy, contributors' guidance, changelog and versioned release checks. Excluded: private provider dashboards, credentials, account identifiers, backups, client invoices, personal contact data, internal business notes, private repository history, and unpublished domain-control information.
Maintenance roles: The technical owner approves schema changes, security review, dependency updates, browser compatibility and releases. The product/UX owner approves questionnaires, plain-language warnings, sample data, user-study materials, and release copy. Both owners approve licenses and public sharing. Do not open a public issue that contains a real client's private infrastructure details.
Release documentation must state limitations prominently: this is an evidence and planning tool, not a guarantee of access, a legal determination, a backup service, or a migration tool. Users should treat exported handoffs as sensitive business information even when redacted.
## 16. Open engineering decisions for Tristan
Does the proposed public_business_site_v1 cover the right essential owner questions without making unrelated services mandatory?
Is a single offline HTML bundle feasible for supported browsers while keeping a strict no-network requirement and understandable local file export?
Will the future browser validator and the independent Python reference suite produce exactly matching findings for all golden and adversarial fixtures?
Is asOf-based freshness with a 90-day evidence warning and 180-day restore warning the correct v1 policy, or should the thresholds be configurable through an independently versioned policy file?
Is the service graph intentionally limited to manually reported relations, with no hidden discovery claims?
Should any private export exist in the first public release, or would redacted output plus an owner-held editable input be safer?
What accessibility, browser/OS, and performance evidence is required before public distribution?
Does comparative user testing justify a GUI, or is a printable worksheet the better public contribution?
Who owns schema migrations, support triage, security reports, and licensing signoff?
Recommendation: Approve G0 and the offline G1 prototype subject to these decisions. Do not approve public network inspection, credentialed services, or a release timetable within this proposal.

## 18. Final recommendation and signoff request
Proceed with SiteCustody as a carefully bounded owner-documentation project. Its defensible value is the separation of reported account access, recorded evidence, dependency mapping, and backup restoration assurance, delivered in language that a business owner can understand. The software must resist the temptation to replace uncertainty with an impressive-looking, unsupported readiness score.
The engineering proof and user trial should be evaluated before any feature expansion. If the product does not materially outperform a spreadsheet, the appropriate outcome is an openly licensed worksheet, schema, and guidance—not a larger unnecessary application.
Requested next action: Tristan reviews the revised proposal, contract appendix, and adversarial tests; jointly approves or revises the data taxonomy and privacy defaults; then authorizes only the first no-network user-facing prototype.
## References and verification resources
ICANN (January 27, 2025), RDAP supersedes WHOIS for gTLD registration information: https://www.icann.org/en/announcements/details/icann-update-launching-rdap-sunsetting-whois-27-01-2025-en
Google Search Central, changing hosting without URL changes: https://developers.google.com/search/docs/crawling-indexing/site-move-no-url-changes
Google Search Central, site moves with URL changes: https://developers.google.com/search/docs/crawling-indexing/site-move-with-url-changes
OWASP, Server Side Request Forgery Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html
JSON Schema, Draft 2020-12: https://json-schema.org/specification
Mark2Mac, site-inspector: https://github.com/Mark2Mac/site-inspector
TicketWaveHQ, website-care-checklist: https://github.com/TicketWaveHQ/website-care-checklist
GitHub, licensing a repository: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository
Document control: SiteCustody executive proposal v3.0, November 12, 2026. This document describes proposed product behavior and tested sample data contracts; it does not claim that the owner-facing application has been built or shipped.
Research review and verification note
The proposed designs rely on published technical standards and recognized security guidelines, but the application-specific engineering choices require testing. ThemeFolio references the Design Tokens Community Group format and WCAG 2.2; SiteCustody references JSON Schema, OWASP guidance, and ICANN registrar-information policy. All claims of market demand, usability savings, metadata safety, deterministic exports, and implementation readiness remain subject to the explicit gate tests above. This document intentionally does not award its own 105-point rating.
Existing approach
What it already handles
What SiteCustody proposes to add
Risk/limitation
Shared spreadsheet or printable checklist
Owner inventory and custom notes; almost no installation
Validated independent states, explicit evidence provenance, dependency consistency and safe shareable output
The spreadsheet may be sufficient for many users
Mark2Mac/site-inspector
Public site crawl, SEO, AI crawler readiness, post-change diff
Owner-focused account-control questions and human attestation provenance
SiteCustody is not a substitute for technical site auditing
TicketWaveHQ/website-care-checklist
Ongoing operational checks, backups, SSL/domain renewal and report templates
A one-time owner-vendor transfer inventory and structured redacted handoff
Overlap may limit differentiation
Host/provider account dashboards
Provider-specific account and service configuration
A vendor-neutral dependency map across unrelated providers
Cannot verify inaccessible accounts
Role
Expected owner question
Applicability contract
domain_registration
Who can manage domain registration, renewal, and transfer settings?
Required, cannot be marked N/A in v0.1
authoritative_dns
Who controls the authoritative zone and record changes?
Required, cannot be marked N/A
site_hosting
Who controls the live deployment or hosted site-builder project?
Required, cannot be marked N/A
site_content
Who can export content, media, and needed configuration?
Required, cannot be marked N/A
backups
Who can locate and test complete recoverable data?
Required, cannot be marked N/A
business_email
Does email use the domain or a related provider?
Must be answered; N/A permitted with explanation
contact_forms
Does the site rely on contact or lead-capture forms?
Must be answered; N/A permitted with explanation
Input evidence type
Meaning
What it must NOT imply
operator_statement
An operator or owner records that a step was completed
Independent verification, legal title, or continuing access
human_witnessed_step
The local record claims another person witnessed an action
Authentication of witness identity or legal authority
subject = account_controls_seen
Reported review of relevant account-control screens
Ability to transfer a domain or grant access later
subject = backup_artifact_seen
Reported observation of a backup artifact
Usable contents, retention, or restoration viability
subject = restore_executed
Reported or witnessed restoration step with outcome
All required data was restored or migration authorized
Risk
v0.1 mitigation
Residual limitation
Private infrastructure details appear in shared reports
Strict field allowlist and redacted-by-default schemas; adversarial fixtures
Users may deliberately share private exports outside the tool
Credentials or tokens end up in a questionnaire
Strict schema rejecting unknown fields; no password or access-key questions
A user might paste secrets into an allowed provider label in the local record
False claim of ownership or migration readiness
Independent status fields fixed to not_performed / not_assessed
Human attestations can still be inaccurate
Public site probe reaches private network or metadata endpoint
No network code in v0.1, including RDAP or HTTP
Any future probe requires new security review
Backup called “safe” after limited test
Separate coverage, environment, outcome and evidence; conservative assurance label
No restoration test guarantees future availability
Site dependency omitted
Required role profile and explicit unknowns; dependency-review attestation
Human reviewers may still omit an unlisted external service
JSON/CSS injection via freeform notes
No arbitrary HTML/script input; renderer uses safe text APIs, schema limits, and fixed action codes
A browser implementation must still undergo XSS testing
Offline data exists in a cloud-synced downloads folder
User-selected download, explanation, manual file lifecycle guidance
Tool cannot control the OS, sync software, or recipients
Supply-chain compromise
Minimal audited dependencies, offline-release tests, published changelog
Third-party vulnerabilities can emerge after release
ID
Acceptance test
Pass condition
SC-01
Complete sample inventory
Parses under published schema and yields expected findings
SC-02
Invalid/new schema version
Reject with a safe, actionable version failure
SC-03
Missing required core role
Independent profile reports REQUIRED_AREA_MISSING
SC-04
Domain or DNS access unknown
No confirmed ownership; explicit next action
SC-05
N/A optional area without reason
Reject or block until explained
SC-06
Core control area wrongly marked N/A
Critical policy failure
SC-07
Unmatched evidence kind or service ID
No status upgrade; evidence finding
SC-08
Duplicate service/evidence identifiers
Stable collision findings
SC-09
Future or stale observation
Explicit snapshot-based date finding
SC-10
Missing dependency target
Dependency error; no false complete map
SC-11
Self link / duplicate link / review cycle
Correct errors or review warnings
SC-12
Unreviewed dependency map
Remains unresolved even when edges exist
SC-13
Backup artifact reported only
No restoration-assurance promotion
SC-14
No restore test
Blocking BACKUP_RESTORE_NOT_TESTED
SC-15
Failed restore
Critical failure, not an aggregate green score
SC-16
Scope-limited restore
Explicit coverage warning and conservative label
SC-17
Witnessed-as-recorded restore
No legal proof or full recovery guarantee
SC-18
Production restore test
Warning requiring separate safety review
SC-19
Redacted report includes secret-like provider label in input
Secret and all identifying strings absent from shareable output
SC-20
Schema contains unexpected password/API-key field
Reject without echoing secret in error
SC-21
Redacted-report schema modified to claim ownership verified
Schema rejects unauthorized status
SC-22
No network permission in ordinary workflow
Zero outbound requests; offline test passes
SC-23
Browser 200% zoom / narrow screens
Controls and report remain usable without losing actions
SC-24
Keyboard and screen-reader workflows
Complete form operable, labels and focus visible
SC-25
Malicious strings in allowed private label
No script execution or copied sensitive text in redacted output
SC-26
Browser output vs Python reference fixtures
Identical findings and independent result fields
SC-27
Install-free start on offline device
Full inventory and report without runtime installation
SC-28
Data export/delete lifecycle
Clear user controls, no hidden persistent copy
SC-29
No explicit network request
No DNS/RDAP/HTTP traffic by application itself
SC-30
Windows/macOS/Linux and major browsers
Same semantic outcomes on supported matrix
Gate
Deliverables and owner
Estimate
Evidence required for approval
G0 — Contract signoff
Engineer + product lead: data schemas, taxonomy, threat model, privacy-default decision, competitor baseline
3–5 days
Approved ADRs, input/output contracts, golden fixtures
G1 — User-facing offline proof
Engineer: static guided questionnaire, local JSON editing/export, redacted report
8–12 days
Demonstration without Internet or developer environment; no secret disclosure
G2 — Engineering hardening
Engineer + QA: browser/reference agreement, security, access, performance and accessibility tests
10–16 days
All planned blocking tests, independent manual accessibility review
G3 — User study and revision
Product lead + engineer: 6–10 trials, compare against spreadsheet, triage issues
5–8 days
Published anonymized methodology and go/no-go evidence
G4 — Public-release gate
Maintainers: clean repo, license review, release artifact, support and security policy
3–6 days
Reproducible build, synthetic content review, final checklist
Planning total
Conditional release candidate
29–47 engineer-days
No promise without passing each gate
