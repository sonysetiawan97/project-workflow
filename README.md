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
- Nama file dan folder huruf kecil kebab-case, kecuali `AGENTS.md`, `CLAUDE.md`, `SKILL.md`, `README.md`, `LICENSE`.
- Satu artefak, satu template, satu skill pemilik. Pengecualian: glossary dan ADR ditulis oleh skill yang sedang berjalan.
- Template milik satu skill ada di `skills/<skill>/templates/`, dengan path yang mencerminkan path di project.
- Template bersama (ADR, glossary, tiket) ada di `skills/project-setup/templates/`. `project-setup` menyalinnya ke project, lalu semua skill membacanya dari project.
- Placeholder `{{HURUF_BESAR}}` diisi `project-setup`. Placeholder `{{teks biasa}}` diisi skill pemilik artefak.
- Keputusan desain repo ini ada di `docs/adr/`. Istilah ada di `glossary.md`.

## Prasyarat

- macOS atau Linux, karena project memakai symlink `.claude/skills` dan `.agents/skills`.
- Node.js, untuk `npx`.
- Agent yang membaca skill dari `~/.claude/skills/` (Claude Code) atau `~/.agents/skills/`.
- Parser YAML, misalnya Python 3 dengan PyYAML, untuk pengecekan di `project-contract`.

## Install

Pasang keenam skill di level user lewat [`skills`](https://www.npmjs.com/package/skills):

```sh
npx skills add sonysetiawan97/project-workflow -g --skill '*'
```

CLI menanyakan agent yang dipasangi; tambahkan `-a claude-code` untuk langsung memilih Claude Code.

- Update ke versi terbaru: `npx skills update -g`.
- Uninstall: `npx skills remove -g --skill project-setup project-grilling project-prd project-fsd project-architecture project-contract`.

## Cara Pakai

Semua skill dijalankan manual dengan mengetik namanya, misalnya `/project-setup`. Setiap skill mengecek Artefak hulunya dan berhenti jika belum ada.

1. **Siapa pun**, di folder project baru: `/project-setup`.
2. **PM**: `/project-grilling`, lalu `/project-prd` di percakapan yang sama. PRD disusun dari rekap grilling, jadi jangan membuka percakapan baru di antara keduanya.
3. **PM/BA**: `/project-fsd`, setelah PRD berstatus `approved`. Boleh dilanjutkan di percakapan baru; skill melanjutkan dari fitur yang belum ditulis.
4. **Tech lead**: `/project-architecture`, setelah FSD berstatus `approved`, lalu `/project-contract`. Setiap file diusulkan agent dan dikonfirmasi tech lead.

## Lisensi

[MIT](LICENSE).
