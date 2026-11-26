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

Versioning follows `contract/README.md`: a new file starts at `0.1.0`. While the version is `0.x`, every change bumps the minor and needs no ADR, because no consumer has been released against it. The tech lead sets `1.0.0` when the first consumer app is released; from then on a non-breaking change bumps the minor, and a breaking change bumps the major and needs an ADR with `Cakupan: contract`, `Pemutus: tech lead`, `Sumber: sesi contract YYYY-MM-DD`.

## Process

### 1. Check

- `glossary.md` exists. If absent, stop and tell the user to run `project-setup`.
- `docs/fsd.md` exists with `Status: approved`. If absent or `draft`, stop and tell the user to finish `project-fsd`.
- All four files in `architecture/` exist. If any is absent, stop and tell the user to run `project-architecture`.
- No ADR change is pending. An ADR whose `Konsekuensi` has a `FSD perlu diubah:` line that no `Riwayat Perubahan` line in `docs/fsd.md` names, or an `architecture/ perlu diubah:` line whose named files do not all cite the ADR: stop, and tell the user to run `project-fsd` or `project-architecture` first.
- Read `glossary.md`, every ADR in `docs/adr/` (the `NNNN-<slug>.md` files; `README.md` holds the template, not an ADR), `docs/fsd.md`, every file in `architecture/`, and everything in `contract/`.
- `apps/` holds code: read its routes and request/response types. Existing routes are the default answer; changing one is a contract change under the versioning rules.
- For each confirmed service, list the upstream changes since its row's `Tanggal` in `contract/README.md`: `Riwayat Perubahan` lines in `docs/prd.md` and `docs/fsd.md` dated on or after it, and `architecture/` files whose `Tanggal` is on or after it.
- List the services: every app in `architecture/overview.md` that exposes an HTTP API. A frontend that only serves pages to the browser is a consumer, not a service.

Done when every service is marked absent, confirmed (its file has a row in `contract/README.md`), or draft (its file has no row yet: left by a run that stopped before the tech lead confirmed it), and each confirmed service's upstream changes are known.

### 2. Propose each service

For each service, in `overview.md` order:

1. Confirmed: show its upstream changes and propose the contract changes they need, if any. Then ask the tech lead whether it has been reviewed and is correct. Yes means the file is done and its row's `Tanggal` becomes today; otherwise take the change, classify it as breaking or non-breaking, and go to step 5.
2. Draft: go to step 3 with the draft as the proposal.
3. Absent: derive the paths, operations and schemas from the FSD features this service serves: flows give operations, `Field dan Validasi` gives schemas and error responses, `State dan Transisi` gives status enums. Ask the tech lead only what cannot be derived, one question at a time, recommended answer first, with the reason.
4. Write the file, check it, then ask the tech lead to review it and say whether it is correct.
5. Apply corrections, bump `info.version` as the versioning rules require, check again, and ask again, until the tech lead confirms. Then add or update the service's row in `contract/README.md` (writing the file from its template if absent) with today as `Tanggal`; the row marks the file as confirmed.

The check: the file parses as YAML, `openapi` is `3.1.0`, no `{{` remains, and every local `$ref` resolves. One command covers the parse and the `$ref`s:

```sh
python3 -c 'import sys,re,yaml; t=open(sys.argv[1]).read(); d=yaml.safe_load(t); bad=["/".join(r) for r in re.findall(r"#/components/(\w+)/([\w.-]+)", t) if r[1] not in (d.get("components") or {}).get(r[0], {})]; print("ref putus:", bad or "tidak ada"); sys.exit(bool(bad))' <file>
```

The contract needs a change to `architecture/`, the FSD or the PRD (a missing entity, an unbuildable rule): stop. Keep the confirmed files and the current draft, and name the draft in the stop message. Tell the user which skills to run, in order: a change that also adds behaviour for an actor (a setting, a screen, a flow) goes to `project-fsd` first, then `project-architecture`; a purely technical gap goes to `project-architecture` alone. Then run `project-contract` again to resume. A domain term that settles goes into `glossary.md`, following the template in its header comment. The definition says what the term is, not what it does.

Done per file when the check passes and the tech lead confirms it. Done for the step when every service is confirmed, every FSD feature that calls a service has at least one operation tagged with its `F-NN`, and every cited `BR-NNN` exists in `docs/fsd.md`.

### 3. Index

`contract/README.md` holds one `Daftar Service` row per confirmed service, written in step 2: its file, `info.version`, the apps that consume it (from `architecture/overview.md`), and the date it was last confirmed. Check the rows against the files, then ask the tech lead to confirm the index.

Done when every file in `contract/http/` has a row and the tech lead confirms. Report the ADRs written this session. The foundation is complete; the next stage is per-feature tickets in `docs/tracker/`.
