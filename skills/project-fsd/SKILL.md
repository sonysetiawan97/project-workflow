---
name: project-fsd
description: Interview the PM/BA feature by feature and write docs/fsd.md from the approved PRD, resuming where the last session stopped. Run after project-prd.
disable-model-invocation: true
---

# Project FSD

Relentless interview with the PM/BA, one PRD feature at a time, until every feature has a specification a dev, QC or UI/UX division can build and test from without asking. Each feature's section is written to `docs/fsd.md` as soon as it settles, so a session can stop anywhere and the next run resumes.

## Language

- Talk to the PM/BA in Indonesian. Every file written into the project is in Indonesian.
- Use the terms in `glossary.md`.

## Template

`templates/docs/fsd.md` is the FSD's template. Follow it exactly: same headings, same fields, same order, nothing added. `### F-NN` sections appear in ID order, whatever order they were interviewed in. A section with no answer holds "Belum diputuskan."; `Notifikasi`, `Laporan dan Export`, `Pertanyaan Terbuka` and `Catatan UI` hold "Tidak ada." when the PM/BA confirms there is nothing.

| Field | Value |
|---|---|
| `Status` | `draft`; `approved` only after the PM/BA approves the whole document in this session |
| `Tanggal` | date of the last write, `YYYY-MM-DD` |
| `nama produk` | the product name from `docs/prd.md` |

Business rule IDs are global: the next `BR-NNN` is the highest in the file plus one. An existing ID is never renumbered or reused.

## Process

### 1. Check

- `glossary.md` exists. If absent, stop and tell the user to run `project-setup`.
- `docs/prd.md` exists with `Status: approved`. If absent or `draft`, stop and tell the user to finish `project-prd`.
- Read `glossary.md`, every ADR in `docs/adr/`, `docs/prd.md`, and `docs/fsd.md` if it exists.
- Compare the PRD's `Fitur` table with the FSD's `### F-NN` sections. The features with no section are the **queue**: must first, then should, then could, PRD order within each priority. An FSD section whose feature left the PRD is removed, with a `Riwayat Perubahan` line.

Done when the queue is known, or the queue is empty and the PM/BA has named what to change.

### 2. Frame

New file only: write `docs/fsd.md` from the template with the header, `Ringkasan` from the PRD, `Daftar Fitur` copied from the PRD's `Fitur` table, `Aktor dan Hak Akses` with one row per PRD actor, and every other section as "Belum diputuskan.". `Riwayat Perubahan` gets one line: today and "Versi pertama."

Done when the file exists and its header and `Daftar Fitur` match the PRD.

### 3. Grill each feature

For each feature in the queue, settle every subsection of its `### F-NN` section in template order:

- One question at a time, recommended answer first, with the reason drawn from the PRD, the ADRs, or features already specified.
- Push to concrete: a flow step that names the actor and the screen, a rule with numbers, a field with its type and error message, a state change with who may trigger it.
- Every business rule gets at least one `Kriteria Penerimaan` line in `**Dengan** ... **Ketika** ... **Maka** ...` form that names its `BR-NNN`.
- A notification or report the feature needs goes into `Notifikasi` or `Laporan dan Export`; a new actor action goes into `Aktor dan Hak Akses`.
- A technical question (database, framework, API shape, integration mechanics) goes to the tech lead: add it to `Pertanyaan Terbuka` with "tech lead" as who must answer, and move on.
- A domain term that settles goes into `glossary.md`, following the template in its header comment. A product decision that meets the three conditions in `docs/adr/README.md` and is confirmed goes into an ADR with `Cakupan: product`, `Pemutus: PM`, `Sumber: sesi FSD YYYY-MM-DD`.
- The answer changes the PRD (a missing feature or actor, a changed goal or priority): stop. Keep what is written, then tell the PM to run `project-grilling` and `project-prd` for that change, and `project-fsd` again afterwards to resume.

Write the feature's section the moment it settles, update `Tanggal`, and move to the next feature in the queue.

Done when every subsection of every queued feature holds a confirmed answer or a placeholder sentence, every `BR-NNN` appears in a `Kriteria Penerimaan` line, and no `{{` remains in the file.

### 4. Approve

Settle `Notifikasi` and `Laporan dan Export` across the whole document. Then show the PM/BA the FSD and ask for approval. Apply corrections; a correction to an approved FSD adds a `Riwayat Perubahan` line and returns `Status` to `draft`. Set `Status` to `approved` once the PM/BA approves.

Done when `Status` is `approved`, or the PM/BA ends the session with it left as `draft`. Name the next step: `project-architecture`, run by the tech lead, who also answers the tech-lead entries in `Pertanyaan Terbuka`.
