---
name: project-contract
description: Propose contract/ (one OpenAPI 3.1 file per service, plus contract/README.md) from the FSD and architecture/, one service at a time, each confirmed by the tech lead. Run after project-architecture.
disable-model-invocation: true
---

# Project contract

The agent proposes, the tech lead decides. Each service's OpenAPI file is derived from the FSD, `architecture/`, the ADRs and any existing routes, written to disk, and confirmed by the tech lead as reviewed and correct before the next service starts. The contract is the source of truth for every interface: code in `apps/` follows it, and it changes first.

## Language

- Talk to the tech lead in Indonesian. Every `description` and `summary` in the contract is in Indonesian.
- Use the terms in `glossary.md`.

## Files

| Project path | Template |
|---|---|
| `contract/http/<service>.openapi.yaml` | `templates/contract/http/service.openapi.yaml` |
| `contract/README.md` | `templates/contract/README.md` |

`<service>` is the app's folder name under `apps/`, as listed in `architecture/overview.md`. Follow each template exactly: keep its keys and order, fill every `{{...}}`, and add OpenAPI content only under `paths` and `components`.

## Conventions

| Item | Rule | Example |
|---|---|---|
| Path segment | lowercase kebab-case | `/data-pelanggan/{id}` |
| Schema name | PascalCase glossary term | `Pelanggan` |
| Field and parameter | snake_case, matching the column in `architecture/data-model.md` when one exists | `tanggal_lahir` |
| Operation tags | the `F-NN` of every FSD feature it serves | `tags: [F-01]` |
| Operation `description` | ends with the BR IDs the operation enforces | `Menegakkan BR-003, BR-007.` |

Versioning follows `contract/README.md`: a new file starts at `0.1.0`; a non-breaking change bumps the minor; a breaking change bumps the major and needs an ADR with `Cakupan: contract`, `Pemutus: tech lead`, `Sumber: sesi contract YYYY-MM-DD`.

## Process

### 1. Check

- `glossary.md` exists. If absent, stop and tell the user to run `project-setup`.
- `docs/fsd.md` exists with `Status: approved`. If absent or `draft`, stop and tell the user to finish `project-fsd`.
- All four files in `architecture/` exist. If any is absent, stop and tell the user to run `project-architecture`.
- Read `glossary.md`, every ADR in `docs/adr/`, `docs/fsd.md`, every file in `architecture/`, and everything in `contract/`.
- `apps/` holds code: read its routes and request/response types. Existing routes are the default answer; changing one is a contract change under the versioning rules.
- List the services: every app in `architecture/overview.md` that serves HTTP to another app or to a client.

Done when every service is marked absent or present in `contract/http/`.

### 2. Propose each service

For each service, in `overview.md` order:

1. Present: ask the tech lead whether it has been reviewed and is correct. Yes means the file is done; otherwise take the change, classify it as breaking or non-breaking, and go to step 4.
2. Absent: derive the paths, operations and schemas from the FSD features this service serves: flows give operations, `Field dan Validasi` gives schemas and error responses, `State dan Transisi` gives status enums. Ask the tech lead only what cannot be derived, one question at a time, recommended answer first, with the reason.
3. Write the file, check it, then ask the tech lead to review it and say whether it is correct.
4. Apply corrections, bump `info.version` as the versioning rules require, check again, and ask again, until the tech lead confirms.

The check: the file parses as YAML (`python3 -c 'import sys, yaml; yaml.safe_load(open(sys.argv[1]))' <file>`, or any other YAML parser), `openapi` is `3.1.0`, and no `{{` remains.

The contract needs a change to `architecture/`, the FSD or the PRD (a missing entity, an unbuildable rule): stop. Keep the confirmed files, tell the user which skill to run first, then `project-contract` again to resume. A domain term that settles goes into `glossary.md`, following the template in its header comment.

Done per file when the check passes and the tech lead confirms it. Done for the step when every service is confirmed, every FSD feature that calls a service has at least one operation tagged with its `F-NN`, and every cited `BR-NNN` exists in `docs/fsd.md`.

### 3. Index

Write or update `contract/README.md` from its template: one `Daftar Service` row per service with its file, `info.version`, and the apps that consume it (from `architecture/overview.md`). Ask the tech lead to confirm it.

Done when every file in `contract/http/` has a row and the tech lead confirms. Report the ADRs written this session. The foundation is complete; the next stage is per-feature tickets in `docs/tracker/`.
