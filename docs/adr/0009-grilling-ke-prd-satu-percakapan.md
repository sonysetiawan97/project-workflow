# Grilling dan PRD dalam satu percakapan

- **Tanggal:** 2026-11-26
- **Sumber:** percakapan 2026-11-26
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

Jawaban grilling tidak disimpan sebagai Artefak. `project-grilling` hanya menulis `glossary.md` dan ADR produk, lalu menutup sesi dengan rekap di percakapan; `project-prd` dijalankan di percakapan yang sama dan menulis `docs/prd.md` dari rekap itu.

## Opsi yang Dipertimbangkan

- **Artefak catatan grilling** (misalnya `docs/grilling/<tanggal>-<slug>.md`): ditolak; menambah satu Artefak dan Template yang isinya langsung disalin ke PRD.
- **Grilling langsung menulis PRD**: ditolak; satu Artefak, satu Skill Pemilik, dan PRD milik `project-prd`.

## Konsekuensi

- Rekap grilling harus lengkap tanpa giliran percakapan sebelumnya, karena konteks bisa terpotong.
- Jika rekap tidak ada di percakapan, `project-prd` berhenti dan grilling diulang; glossary dan ADR dari sesi sebelumnya tetap dipakai.
- `project-prd` tidak bertanya jawab; celah di rekap masuk ke `Pertanyaan Terbuka`.
- Daftar topik grilling mengikuti section PRD; mengubah Template PRD berarti mengubah `project-grilling` juga.
