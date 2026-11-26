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

`templates/docs/fsd.md` is the FSD's template. Follow it exactly: same headings, same fields, same order, nothing added. `### F-NN` sections appear in ID order, whatever order they were interviewed in. A section with no answer holds "Belum diputuskan."; `Notifikasi`, `Laporan dan Export`, `Pertanyaan Terbuka`, `Catatan UI`, `State dan Transisi` and `Field dan Validasi` hold "Tidak ada." when the PM/BA confirms there is nothing; in `Field dan Validasi` it is the table's only row, `| Tidak ada. | - | - | - | - |`.

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
- Read `glossary.md`, every ADR in `docs/adr/` (the `NNNN-<slug>.md` files; `README.md` holds the template, not an ADR), `docs/prd.md`, and `docs/fsd.md` if it exists.
- Compare the PRD's `Fitur` table with the FSD's `### F-NN` sections. The features with no section are the **queue**: must first, then should, then could, PRD order within each priority. An FSD section whose feature left the PRD is removed, with a `Riwayat Perubahan` line.
- List the PRD's `Pertanyaan Terbuka` entries addressed to the PM that the FSD neither answers nor lists yet. Each goes into the FSD's `Pertanyaan Terbuka` (after step 2 on a new file), tagged with the `F-NN` that should answer it.
- `architecture/` exists: read it. A `Pertanyaan Terbuka` entry addressed to the tech lead that is answered in `architecture/` or an ADR leaves the FSD, with a `Riwayat Perubahan` line naming where it is answered.
- List every ADR whose `Konsekuensi` has a `FSD perlu diubah:` line and whose number no `Riwayat Perubahan` line names yet. Each is a **pending ADR change**; its feature joins the queue, and a feature that already has a section is reopened only for the subsections that change.

Done when the queue, the carried-over questions, the answered tech-lead questions and the pending ADR changes are known, or the queue is empty and the PM/BA has named what to change.

### 2. Frame

- New file: write `docs/fsd.md` from the template with the header, `Ringkasan` from the PRD, `Daftar Fitur` copied from the PRD's `Fitur` table, `Aktor dan Hak Akses` with one row per PRD actor, and every other section as "Belum diputuskan.". `Riwayat Perubahan` gets one line: today and "Versi pertama."
- Existing file: bring `Daftar Fitur` in line with the PRD's `Fitur` table (ID, name, priority), and give each new PRD actor a row in `Aktor dan Hak Akses` holding "Belum diputuskan.". Any change adds one `Riwayat Perubahan` line.

Done when the file exists, its `Daftar Fitur` matches the PRD's `Fitur` table, and `Aktor dan Hak Akses` has a row for every PRD actor.

### 3. Grill each feature

For each feature in the queue, settle every subsection of its `### F-NN` section in template order:

- Start with the `Pertanyaan Terbuka` entries and pending ADR changes for this feature. An answered entry leaves `Pertanyaan Terbuka` and lands in the subsection it settles, often as a `BR-NNN`. An applied ADR change adds a `Riwayat Perubahan` line naming the ADR.
- A pending ADR change is a proposal: show the PM/BA the ADR's decision and ask whether to apply it. Rejected: write the PM/BA's decision into the FSD instead, and write a product ADR (`Cakupan: product`, `Pemutus: PM`, `Sumber: sesi FSD YYYY-MM-DD`) that supersedes the old one as `docs/adr/README.md` describes, with a `Konsekuensi` line `architecture/ perlu diubah: <file>, <file>: <what changes>` naming every `architecture/` file the change touches. The `Riwayat Perubahan` line names both ADRs.
- One question at a time, recommended answer first, with the reason drawn from the PRD, the ADRs, or features already specified.
- Push to concrete: a flow step that names the actor and the screen, a rule with numbers, a field with its type and error message, a state change with who may trigger it.
- Every business rule gets at least one `Kriteria Penerimaan` line in `**Dengan** ... **Ketika** ... **Maka** ...` form that names its `BR-NNN`.
- A notification or report the feature needs goes into `Notifikasi` or `Laporan dan Export`; a new actor action goes into `Aktor dan Hak Akses`.
- A technical question (database, framework, API shape, integration mechanics) goes to the tech lead: add it to `Pertanyaan Terbuka` with "tech lead" as who must answer, and move on.
- A domain term that settles goes into `glossary.md`, following the template in its header comment. The definition says what the term is, not what it does. A product decision that meets the three conditions in `docs/adr/README.md` and is confirmed goes into an ADR with `Cakupan: product`, `Pemutus: PM`, `Sumber: sesi FSD YYYY-MM-DD`.
- The answer changes the PRD (a missing feature or actor, a changed goal or priority): stop. Keep what is written, then tell the PM to run `project-grilling` and `project-prd` for that change, and `project-fsd` again afterwards to resume.

Write the feature's section the moment it settles, update `Tanggal`, and move to the next feature in the queue.

Done when every subsection of every queued feature holds a confirmed answer or a placeholder sentence, every `BR-NNN` appears in a `Kriteria Penerimaan` line, and no `{{` remains in the file.

### 4. Approve

Settle `Notifikasi` and `Laporan dan Export` across the whole document. Then give the PM/BA the path `docs/fsd.md` and a one-line summary per feature, and ask whether they have read the file and approve it. Apply corrections; a correction to an approved FSD adds a `Riwayat Perubahan` line and returns `Status` to `draft`. Set `Status` to `approved` once the PM/BA approves.

Done when `Status` is `approved`, or the PM/BA ends the session with it left as `draft`. Name the next step: `project-architecture`, run by the tech lead, who also answers the tech-lead entries in `Pertanyaan Terbuka`.
