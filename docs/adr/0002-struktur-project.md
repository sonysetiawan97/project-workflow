# Struktur project

- **Tanggal:** 2026-11-26
- **Sumber:** percakapan 2026-11-26
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

Project berisi `architecture/`, `contract/`, `skills/`, `docs/` (`prd.md`, `fsd.md`, `adr/`, `tracker/`), `apps/`, `glossary.md`, `AGENTS.md`, dan `CLAUDE.md`. `AGENTS.md` adalah sumber utama; `CLAUDE.md` hanya berisi `@AGENTS.md`. `skills/` hanya berisi Skill Project, datar, dan dibaca lewat symlink `.claude/skills` dan `.agents/skills` ke `../skills`.

## Opsi yang Dipertimbangkan

- **`AGENTS.md` dan `CLAUDE.md` ditulis terpisah**: ditolak, karena isi keduanya akan berbeda seiring waktu.
- **`skills/` dipecah per divisi**: ditunda sampai jumlah skill mulai menyulitkan pencarian.
- **Skill Workflow disalin ke `skills/` project**: ditolak; `skills/` khusus Skill Project.

## Konsekuensi

- Setiap anggota tim meng-install Skill Workflow sendiri, jadi versinya bisa berbeda antar-orang.
- Symlink butuh sistem Unix; seluruh tim memakai macOS atau Linux.
