# Satu folder ADR untuk semua cakupan

- **Tanggal:** 2026-11-26
- **Sumber:** percakapan 2026-11-26
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

Semua ADR ada di `docs/adr/` dengan satu urutan nomor. Field `Cakupan` dan `Pemutus` membedakan wilayah dan pengambil keputusan. ADR ditulis oleh skill yang sedang berjalan, setelah Pemutus mengonfirmasi keputusan di sesi itu.

## Opsi yang Dipertimbangkan

- **Folder ADR per divisi**: ditolak; nomor bisa bentrok, dan banyak keputusan menyentuh lebih dari satu divisi.
- **ADR di `architecture/decisions/`**: ditolak; ADR termasuk dokumen di `docs/`.

## Konsekuensi

- Daftar Cakupan ikut daftar Divisi di `docs/tracker/README.md`.
