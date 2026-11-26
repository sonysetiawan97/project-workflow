# FSD: {{nama produk}}

- **Rujukan:** `docs/prd.md`
- **Status:** draft | approved
- **Tanggal:** YYYY-MM-DD

## Ringkasan

{{1 paragraf: apa yang dispesifikasikan dokumen ini.}}

## Aktor dan Hak Akses

| Aktor | Aksi yang Boleh |
|---|---|
| {{aktor dari PRD}} | {{aksi}} |

## Daftar Fitur

| ID | Nama | Prioritas |
|---|---|---|
| {{F-01 dari PRD}} | {{nama fitur}} | {{prioritas dari PRD}} |

## Spesifikasi Fitur

### {{F-01}} {{nama fitur}}

#### Tujuan

{{apa yang dicapai aktor dengan fitur ini.}}

#### Alur Pengguna

{{langkah bernomor, jalur utama.}}

#### Aturan Bisnis

- **{{BR-001}}**: {{aturan; nomor BR global di seluruh dokumen.}}

#### Field dan Validasi

| Field | Tipe | Wajib | Aturan | Pesan Error |
|---|---|---|---|---|
| {{field}} | {{tipe}} | {{ya atau tidak}} | {{aturan}} | {{pesan}} |

#### State dan Transisi

{{status entity, transisi yang boleh, dan siapa yang boleh memicunya.}}

#### Edge Case dan Error

{{kondisi tidak normal dan perilaku sistem.}}

#### Kriteria Penerimaan

- **Dengan** {{kondisi awal}} **Ketika** {{aksi}} **Maka** {{hasil}}

#### Catatan UI

{{layar terkait dan catatan tampilan, atau "Tidak ada."}}

## Notifikasi

{{pemicu, penerima, kanal, isi; atau "Tidak ada."}}

## Laporan dan Export

{{laporan atau export yang dibutuhkan, atau "Tidak ada."}}

## Pertanyaan Terbuka

{{pertanyaan yang belum terjawab, atau "Tidak ada."}}

## Riwayat Perubahan

- {{YYYY-MM-DD}}: {{apa yang berubah dan kenapa.}}
