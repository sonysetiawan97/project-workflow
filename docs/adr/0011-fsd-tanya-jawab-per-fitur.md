# FSD lewat tanya jawab per fitur

- **Tanggal:** 2026-11-27
- **Sumber:** percakapan 2026-11-27
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

`project-fsd` mewawancarai PM/BA satu fitur demi satu fitur, karena grilling tidak membahas alur, aturan bisnis, field, state, edge case, dan kriteria penerimaan. Section setiap fitur langsung ditulis ke `docs/fsd.md` begitu disepakati, sehingga sesi bisa dilanjutkan di percakapan lain. FSD hanya berjalan dari PRD berstatus `approved`, dan berhenti jika jawabannya mengubah PRD.

## Opsi yang Dipertimbangkan

- **FSD disusun dari PRD tanpa tanya jawab**: ditolak; detail FSD tidak ada di PRD, sehingga agent akan menebak.
- **Satu sesi untuk semua fitur, ditulis di akhir**: ditolak; jawaban hilang jika sesi terputus.
- **FSD mencatat perubahan PRD lalu lanjut**: ditolak; FSD akan dibangun di atas PRD yang sudah tidak benar.

## Konsekuensi

- Fitur yang belum punya section di `docs/fsd.md` adalah antrean run berikutnya; file yang belum lengkap tetap sah.
- Perubahan PRD di tengah FSD memutar balik ke `project-grilling` dan `project-prd`.
