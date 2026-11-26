# Bahasa dan penamaan file

- **Tanggal:** 2026-11-26
- **Sumber:** percakapan 2026-11-26
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

`SKILL.md` ditulis dalam bahasa Inggris. Template, dokumen project, dan sesi grilling memakai bahasa Indonesia. Nama file dan folder huruf kecil kebab-case, kecuali `AGENTS.md`, `CLAUDE.md`, `SKILL.md`, dan `README.md`.

## Opsi yang Dipertimbangkan

- **`SKILL.md` dalam bahasa Indonesia**: ditolak; instruksi berbahasa Inggris diikuti model lebih presisi.
- **Semua nama file huruf kecil tanpa pengecualian**: ditolak; tool mencari keempat nama itu persis, dan di Linux `claude.md` tidak terbaca.

## Konsekuensi

- Nilai enum seperti status tiket dan Cakupan tetap memakai token yang disepakati (`todo`, `accepted`, `architecture`).
- macOS tidak membedakan huruf besar-kecil, Linux membedakan; nama yang salah kapital baru ketahuan di Linux atau CI.
