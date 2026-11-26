# {{PROJECT_NAME}}

{{PROJECT_DESCRIPTION}}

## Peta Folder

| Path | Isi | Ditulis oleh |
|---|---|---|
| `glossary.md` | bahasa domain project | `project-grilling` |
| `docs/prd.md` | PRD | `project-prd` |
| `docs/fsd.md` | FSD | `project-fsd` |
| `docs/adr/` | catatan keputusan; template di `docs/adr/README.md` | skill yang sedang memutuskan |
| `architecture/` | model domain, sistem, data, stack | `project-architecture` |
| `contract/` | OpenAPI antar-app, sumber kebenaran antarmuka | `project-contract` |
| `docs/tracker/<divisi>/<fitur>/` | tiket per divisi; template di `docs/tracker/README.md` | breakdown tiket per fitur |
| `apps/<app>/` | kode aplikasi | divisi dev |
| `skills/` | skill khusus project; aturan di `skills/README.md` | tim |

## Aturan

- Nama file dan folder huruf kecil kebab-case, kecuali `AGENTS.md`, `CLAUDE.md`, `SKILL.md`, `README.md`.
- Dokumen ditulis dalam bahasa Indonesia.
- Setiap dokumen mengikuti templatenya persis: heading dan field sama, urutan sama.
- Pakai istilah dari `glossary.md`.
- Ubah `contract/` dulu, baru kode di `apps/`.
- Keputusan yang sulit dibalik dicatat sebagai ADR.

## Workflow

1. `project-grilling`: PM, tanya jawab sampai fitur, aktor, dan scope jelas.
2. `project-prd`: PM, menulis `docs/prd.md`.
3. `project-fsd`: PM/BA, menulis `docs/fsd.md` dari PRD.
4. `project-architecture`: tech lead, menulis `architecture/` dan ADR teknis.
5. `project-contract`: tech lead, menulis `contract/`.

Setelah itu, per fitur: tiket per divisi di `docs/tracker/`.

## Commands

Belum ada. Diisi setelah app pertama ada di `apps/`.
