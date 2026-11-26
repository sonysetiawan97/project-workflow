# project-workflow

Kumpulan skill untuk membangun project dari nol: skeleton, grilling PM, PRD, FSD, arsitektur, dan contract. Konsep baru, terpisah dari skill `ss-*` dan menggantikannya.

## Skill

| Urutan | Skill | Dipakai oleh | Menghasilkan | Status |
|---|---|---|---|---|
| 1 | `project-setup` | siapa pun | skeleton project | tersedia |
| 2 | `project-grilling` | PM | `glossary.md`, ADR produk | tersedia |
| 3 | `project-prd` | PM | `docs/prd.md` | tersedia |
| 4 | `project-fsd` | PM/BA | `docs/fsd.md` | tersedia |
| 5 | `project-architecture` | tech lead | `architecture/`, ADR teknis | tersedia |
| 6 | `project-contract` | tech lead | `contract/` | tersedia |

Setelah keenamnya, per fitur: tiket per divisi di `docs/tracker/<divisi>/<fitur>/`. Skill tahap ini belum dibuat.

## Struktur Project yang Dihasilkan

```
AGENTS.md            sumber utama instruksi agent
CLAUDE.md            berisi @AGENTS.md
glossary.md
architecture/        overview.md, domain-model.md, data-model.md, stack.md
contract/            README.md, http/<service>.openapi.yaml
docs/
  prd.md
  fsd.md
  adr/               README.md (template ADR), 0001-<slug>.md, ...
  tracker/           README.md (template tiket), <divisi>/<fitur>/<NN>-<slug>.md
apps/<app>/
skills/              skill khusus project
.claude/skills  ->  ../skills
.agents/skills  ->  ../skills
```

## Aturan Repo Ini

- `SKILL.md` ditulis dalam bahasa Inggris. Template, dokumen yang dihasilkan, dan sesi grilling memakai bahasa Indonesia.
- Nama file dan folder huruf kecil kebab-case, kecuali `AGENTS.md`, `CLAUDE.md`, `SKILL.md`, `README.md`.
- Satu artefak, satu template, satu skill pemilik.
- Template milik satu skill ada di `skills/<skill>/templates/`, dengan path yang mencerminkan path di project.
- Template bersama (ADR, glossary, tiket) ada di `skills/project-setup/templates/`. `project-setup` menyalinnya ke project, lalu semua skill membacanya dari project.
- Placeholder `{{HURUF_BESAR}}` diisi `project-setup`. Placeholder `{{teks biasa}}` diisi skill pemilik artefak.
- Keputusan desain repo ini ada di `docs/adr/`. Istilah ada di `glossary.md`.

## Install

Dari root repo ini:

```sh
for s in skills/*/; do
  [ -f "$s/SKILL.md" ] || continue
  ln -s "$PWD/${s%/}" ~/.claude/skills/
  ln -s "$PWD/${s%/}" ~/.agents/skills/
done
```
