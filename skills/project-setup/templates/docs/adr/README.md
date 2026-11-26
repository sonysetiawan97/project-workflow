# ADR

Catatan keputusan yang sulit dibalik. Setiap skill yang menulis ADR mengikuti template di file ini persis.

## Kapan Menulis ADR

Tulis ADR hanya jika ketiga syarat ini terpenuhi:

1. **Sulit dibalik**: mengubah keputusan nanti mahal.
2. **Membingungkan tanpa konteks**: pembaca berikutnya akan bertanya "kenapa begini?".
3. **Hasil trade-off nyata**: ada alternatif sungguhan yang ditolak.

Contoh yang layak: pilihan database, auth provider, monorepo, REST vs event, batas kepemilikan data, "v1 tanpa multi-tenant", penyimpangan sengaja dari jalur umum, batasan yang tidak terlihat di kode.

## Lokasi dan Penomoran

- Semua ADR ada di folder ini, satu urutan nomor untuk semua cakupan: `0001-<slug>.md`, `0002-<slug>.md`.
- Nomor baru adalah nomor tertinggi yang ada ditambah satu.
- Slug huruf kecil kebab-case.

## Cakupan dan Pemutus

| Cakupan | Ditulis oleh | Pemutus |
|---|---|---|
| `product` | `project-grilling` | PM |
| `architecture` | `project-architecture` | tech lead |
| `contract` | `project-contract` | tech lead |
| `<divisi>` (lihat `docs/tracker/README.md`) | skill divisi | lead divisi |

ADR ditulis oleh skill yang sedang berjalan, setelah Pemutus mengonfirmasi keputusan di sesi itu.

## Template

```md
# {{judul keputusan}}

- **Tanggal:** YYYY-MM-DD
- **Sumber:** {{sesi grilling, path tiket, atau tanggal percakapan}}
- **Status:** accepted | deprecated | superseded by ADR-NNNN
- **Cakupan:** product | architecture | contract | <divisi>
- **Pemutus:** {{role yang memutuskan}}

## Keputusan

{{1-3 kalimat: konteks, keputusan, alasan.}}

## Opsi yang Dipertimbangkan

{{alternatif yang ditolak, masing-masing dengan alasan kalah.}}

## Konsekuensi

{{efek turunan yang tidak terlihat jelas.}}
```

## Aturan

- Pakai template persis: heading dan field sama, urutan sama, tanpa tambahan.
- Bagian tanpa keputusan berisi "Belum diputuskan."
- `Tanggal` adalah tanggal penulisan terakhir. `Sumber` menyebut asal keputusan.
- Di dalam bagian boleh memakai list, tabel, bold, dan code block; heading tambahan tidak boleh.
- Singkat. Nilai ADR ada pada fakta *bahwa* keputusan dibuat dan *kenapa*.
- Mengganti ADR: ADR baru menyebut ADR lama di `Keputusan`, lalu `Status` ADR lama menjadi `superseded by ADR-NNNN`.
