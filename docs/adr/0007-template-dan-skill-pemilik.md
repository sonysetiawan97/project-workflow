# Template dan skill pemilik artefak

- **Tanggal:** 2026-11-26
- **Sumber:** percakapan 2026-11-26
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

Setiap Artefak punya satu Template dan satu Skill Pemilik, dan skill wajib mengikuti Template persis. Template milik satu skill disimpan di `skills/<skill>/templates/`. Template Bersama (ADR, glossary, Tiket) disalin `project-setup` ke project sebagai `docs/adr/README.md`, header `glossary.md`, dan `docs/tracker/README.md`, lalu dibaca semua skill dari project. `project-setup` tidak membuat Artefak milik skill lain.

## Opsi yang Dipertimbangkan

- **Semua template di `project-setup`, dirujuk skill lain lewat path relatif**: ditolak; link lintas skill putus saat skill di-install terpisah, seperti yang pernah terjadi di `ss-prd-division` (commit `d83b98b`).
- **`project-setup` membuat file Artefak kosong**: ditolak; file kosong lolos cek prasyarat skill berikutnya.

## Konsekuensi

- Template Bersama di project bisa berbeda dari versi repo ini jika repo diubah setelah setup.
