---
name: project-architecture
description: Propose architecture/ (overview, stack, domain model, data model) from the approved FSD one file at a time, each confirmed by the tech lead, plus technical ADRs. Run after project-fsd.
disable-model-invocation: true
---

# Project architecture

The agent proposes, the tech lead decides. Each of the four files in `architecture/` is derived from the PRD, the FSD, the ADRs and any existing code, written to disk, and confirmed by the tech lead as reviewed and correct before the next file starts.

## Language

- Talk to the tech lead in Indonesian. Every file written into the project is in Indonesian.
- Use the terms in `glossary.md`. Table and column names in `data-model.md` are lowercase snake_case.

## Files

In this order; each builds on the ones before it.

| Project path | Template | Holds |
|---|---|---|
| `architecture/overview.md` | `templates/architecture/overview.md` | system context, apps under `apps/`, integrations |
| `architecture/stack.md` | `templates/architecture/stack.md` | technology per layer, non-functional targets |
| `architecture/domain-model.md` | `templates/architecture/domain-model.md` | entities, aggregates, relations, state machines |
| `architecture/data-model.md` | `templates/architecture/data-model.md` | ERD and tables |

Follow each template exactly: same headings, same fields, same order, nothing added. Repeated blocks (`### {{nama_tabel}}`, table rows) repeat as often as needed. `Tanggal` is the date of the last write. A section with no answer holds "Belum diputuskan."

The `Container` table in `overview.md` names each app's technology, so settle the technology per app while writing `overview.md`; `stack.md` then adds versions and the remaining layers.

Endpoint paths, payloads and schemas belong to `project-contract`. `overview.md` names which `contract/http/<service>.openapi.yaml` covers each integration, not its content.

## Process

### 1. Check

- `glossary.md` exists. If absent, stop and tell the user to run `project-setup`.
- `docs/fsd.md` exists with `Status: approved`. If absent or `draft`, stop and tell the user to finish `project-fsd`.
- Read `glossary.md`, every ADR in `docs/adr/` (the `NNNN-<slug>.md` files; `README.md` holds the template, not an ADR), `docs/prd.md`, `docs/fsd.md`, and every file in `architecture/`.
- `apps/` holds code: read its manifests (`package.json`, `go.mod`, `pyproject.toml`, ...), folder structure, and any schema or migration files. Existing code is the default answer: proposals follow its stack and structure unless the tech lead decides to change them through an ADR.

Done when each of the four files is marked absent or present, and the stack and structure of any existing code is known.

### 2. Propose each file

For each file, in order:

1. Present: ask the tech lead whether it has been reviewed and is correct. Yes means the file is done; otherwise take the corrections and go to step 4.
2. Absent: derive every section from the sources. Ask the tech lead only what cannot be derived, one question at a time, recommended answer first, with the reason.
3. Write the file, then ask the tech lead to review it and say whether it is correct.
4. Apply corrections and ask again, until the tech lead confirms.

While proposing:

- A decision that meets the three conditions in `docs/adr/README.md` and is confirmed by the tech lead goes into an ADR with `Cakupan: architecture`, `Pemutus: tech lead`, `Sumber: sesi arsitektur YYYY-MM-DD`. `stack.md` cites it in the `ADR` column.
- Every version in `stack.md` is checked against its source (`npm view <package> version`, the official release page) at the time of writing; a version that cannot be checked is written as "perlu dicek".
- A domain term that settles goes into `glossary.md`, following the template in its header comment. The definition says what the term is, not what it does.
- The architecture needs a change to the FSD or PRD (a business rule that cannot be built, a missing feature): stop. Keep the confirmed files, tell the user to run `project-fsd` (or `project-grilling` and `project-prd` for a PRD change), then `project-architecture` again to resume.

Done per file when the tech lead confirms it is reviewed and correct and no `{{` remains in it. Done for the step when all four are confirmed and they agree with each other and the sources: every entity uses its `glossary.md` term, every state machine cites `BR-NNN` IDs that exist in `docs/fsd.md`, every table in `data-model.md` belongs to an entity or aggregate in `domain-model.md`, or its `Keterangan` marks it as a technical table and names its owner (for example a session table), and every app in `overview.md` has a row in `stack.md`.

### 3. Close

List every `Pertanyaan Terbuka` entry in `docs/prd.md` and `docs/fsd.md` addressed to the tech lead, each with where it is now answered (an `architecture/` file or `ADR-NNNN`) or "belum terjawab". Tell the PM/BA to run `project-fsd` to clear the answered FSD entries; answered PRD entries are cleared at the next `project-grilling` and `project-prd` run.

Name the ADRs written this session and the next step: `project-contract`, run by the tech lead.
