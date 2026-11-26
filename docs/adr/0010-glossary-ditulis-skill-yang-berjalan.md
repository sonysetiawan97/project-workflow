# Glossary ditulis skill yang sedang berjalan

- **Tanggal:** 2026-11-27
- **Sumber:** percakapan 2026-11-27
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

`glossary.md` diperlakukan seperti ADR: tidak punya satu Skill Pemilik, dan istilah ditulis oleh skill yang sedang berjalan saat istilah itu disepakati, mengikuti template di header `glossary.md`. Ini pengecualian dari ADR-0007 untuk glossary dan ADR saja.

## Opsi yang Dipertimbangkan

- **Hanya `project-grilling` yang menulis glossary**: ditolak; istilah seperti nama entity dan status baru muncul di FSD, dan memaksa grilling ulang untuk setiap istilah memperlambat sesi.

## Konsekuensi

- Template di header `glossary.md` menjadi satu-satunya penjaga konsistensi entri antar-skill.
