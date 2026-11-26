# Tracker

Tiket kerja per divisi. Setiap skill yang menulis atau mengubah tiket mengikuti template di file ini persis.

## Divisi

{{DIVISIONS}}

## Lokasi

- Path tiket: `docs/tracker/<divisi>/<fitur>/<NN>-<slug>.md`, satu file per tiket.
- `<fitur>` dan `<slug>` huruf kecil kebab-case.
- `<NN>` dua digit mulai `01`, berurutan per folder fitur, tiket penghalang lebih dulu.

## ID dan Rujukan

- Tiket dirujuk dengan `<divisi>/<fitur>/<NN>`, misalnya `ui-ux/login/02`.
- Fitur dirujuk dengan ID `F-01` dari `docs/prd.md`.
- Aturan bisnis dirujuk dengan ID `BR-001` dari `docs/fsd.md`. Nomor BR global, bukan per fitur.

## Status

| Status | Arti |
|---|---|
| `todo` | belum dikerjakan |
| `in-progress` | sedang dikerjakan |
| `blocked` | menunggu tiket lain atau informasi |
| `review` | selesai dikerjakan, menunggu review |
| `done` | selesai dan diterima |

Tiket siap dikerjakan jika semua tiket di `Diblokir oleh` berstatus `done`.

## Template

```md
# {{nomor}} {{judul tiket}}

- **Divisi:** {{divisi}}
- **Status:** todo
- **Rujukan:** {{F-01, BR-003}}
- **Diblokir oleh:** {{ui-ux/login/02, atau "Tidak ada."}}
- **Penanggung Jawab:** {{nama, atau "Belum ada."}}

## Tujuan

{{hasil yang diharapkan dari tiket ini.}}

## Kriteria Penerimaan

{{daftar kondisi yang bisa dicek; rujuk BR dari FSD.}}

## Catatan

{{konteks tambahan, atau "Tidak ada."}}

## Komentar
```

## Aturan

- Pakai template persis: heading dan field sama, urutan sama, tanpa tambahan.
- Komentar ditambahkan di bawah `## Komentar`, terbaru paling bawah, diawali tanggal `YYYY-MM-DD`.
