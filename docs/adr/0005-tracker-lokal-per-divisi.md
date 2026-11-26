# Tracker lokal per divisi

- **Tanggal:** 2026-11-26
- **Sumber:** percakapan 2026-11-26
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

Tiket berupa file markdown di `docs/tracker/<divisi>/<fitur>/<NN>-<slug>.md`, dengan divisi default `dev`, `qc`, `ui-ux`. Status: `todo`, `in-progress`, `blocked`, `review`, `done`. Tiket dirujuk dengan `<divisi>/<fitur>/<NN>`, Fitur dengan `F-01` dari PRD, dan Aturan Bisnis dengan `BR-001` global dari FSD.

## Opsi yang Dipertimbangkan

- **Issue di GitHub atau GitLab**: ditolak; tracker disimpan lokal di repo.
- **Satu folder tiket tanpa pemisahan divisi**: ditolak; divisi bekerja paralel pada fitur yang sama.
- **Nomor BR per fitur**: ditolak; rujukan dari tiket menjadi ambigu.

## Konsekuensi

- Ketergantungan lintas divisi dicatat di field `Diblokir oleh`, misalnya `ui-ux/login/02`.
- QC bisa menulis test case dari Kriteria Penerimaan FSD tanpa menunggu dev.
