# SiteCustody

SiteCustody is a proposed offline-first toolkit for documenting website control, service dependencies, backup assurance, and transfer-readiness for small-business website owners.

**Current status:** engineering specification plus locally tested reference-contract examples. The owner-facing browser application is not yet a completed product.

## Problem

A business can pay for a website while domain registration, authoritative DNS, hosting, content, email, forms, billing, and backups remain spread across different vendors and accounts. SiteCustody is designed to make that control map explicit before a vendor change.

## Proposed v0.1

- browser-local guided inventory with no login or network dependency
- versioned JSON data contract
- explicit applicability and access-status states
- service dependency mapping
- evidence/provenance records that distinguish reported access from stronger recorded observations
- dated backup/restore records with limited-scope assurance
- default-redacted JSON and printable handoff report
- deterministic findings and stable action codes
- synthetic examples and reference-contract tests

## Explicit boundaries

SiteCustody is not an ownership-verification service, crawler, security scanner, backup product, migration executor, credential vault, or legal-title system. The initial release excludes live DNS/RDAP/HTTP inspection, provider APIs, credential storage, and migration actions.

## Evidence standard

The proposal separates implemented or locally tested reference behavior from planned browser functionality. A passing reference validator does not prove the human-facing application, security properties, accessibility, or user outcomes.

## Decision gate

The next justified step is a bounded offline prototype. If independent users perform the task just as well with a short checklist or spreadsheet, the project should publish the schema/checklist and stop expanding the application.

## Documentation

- [Engineering proposal](docs/ENGINEERING_PROPOSAL.md)

The Drive copy remains the archival working document. This repository contains the public engineering edition.
