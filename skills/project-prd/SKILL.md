---
name: project-prd
description: Write or update docs/prd.md from the project-grilling recap in this conversation, then get PM approval. Run right after project-grilling, in the same conversation.
disable-model-invocation: true
---

# Project PRD

Synthesis, not an interview. Every fact in `docs/prd.md` comes from the `project-grilling` recap in this conversation; the PM's only job here is to correct and approve the draft.

## Language

- Talk to the PM in Indonesian. `docs/prd.md` is in Indonesian.
- Use the terms in `glossary.md`.

## Template

`templates/docs/prd.md` is the PRD's template. Follow it exactly: same headings, same fields, same order, nothing added. Replace every `{{...}}` placeholder; a section with no answer holds "Belum diputuskan." (or "Tidak ada." for `Pertanyaan Terbuka`).

| Field | Value |
|---|---|
| `Status` | `draft` until the PM approves in this session, then `approved` |
| `Tanggal` | today, `YYYY-MM-DD` |
| `Penanggung Jawab` | `PM`, as in the template |

## Process

### 1. Check

- `glossary.md` exists. If absent, stop and tell the PM to run `project-setup`.
- The `project-grilling` recap is in this conversation, with its confirmation by the PM. If it is absent or cut off, stop, write nothing, and tell the PM to run `project-grilling` again. Glossary entries and ADRs from the earlier session stay and shorten the re-run.
- Read `glossary.md` and every ADR in `docs/adr/` with `Cakupan: product`.
- `docs/prd.md` exists: this is an update. Read it.

Done when the recap is located and the mode (new or update) is known.

### 2. Write

Map the recap onto the template: one recap topic per section, features into the `Fitur` table with the recap's `F-NN` IDs, the recap's `Pertanyaan Terbuka` list into that section with who must answer each.

- New: write `docs/prd.md` from the template. `Riwayat Perubahan` gets one line: today and "Versi pertama dari sesi grilling."
- Update: change only what the recap changed. Existing feature IDs stay; a removed feature leaves its row out and the change log says so. Append one `Riwayat Perubahan` line: today, what changed, why. `Status` returns to `draft`.

Done when every section holds a recap answer or a placeholder sentence, and no `{{` remains in the file.

### 3. Approve

Show the PM the written PRD and ask for approval. Apply corrections the PM gives; a correction that changes a product decision belongs in an ADR, so write or supersede it as `docs/adr/README.md` describes. Repeat until the PM approves, then set `Status` to `approved`.

Done when the PM has approved and `Status` is `approved`, or the PM ends the session with the PRD left as `draft`. Name the next step: `project-fsd`, which reads `docs/prd.md` and can run in a new conversation.
