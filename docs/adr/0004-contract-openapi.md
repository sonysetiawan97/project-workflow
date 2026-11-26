# Contract memakai OpenAPI

- **Tanggal:** 2026-11-27
- **Sumber:** percakapan 2026-11-26
- **Status:** accepted
- **Cakupan:** contract
- **Pemutus:** pemilik repo

## Keputusan

Contract ditulis sebagai OpenAPI 3.1, satu file per service di `contract/http/<service>.openapi.yaml`. Contract adalah sumber kebenaran antarmuka: kode di `apps/` mengikutinya, dan contract diubah lebih dulu. Breaking change wajib ADR dan menaikkan versi major, mulai versi `1.0.0`, yang ditetapkan saat app konsumen pertama dirilis; selama `0.x`, setiap perubahan cukup menaikkan versi minor.

## Opsi yang Dipertimbangkan

- **Daftar API dalam markdown**: ditolak; tidak bisa di-lint, dipakai untuk mock, atau di-generate menjadi type.
- **AsyncAPI untuk event**: belum dibutuhkan.

## Konsekuensi

- Contract bisa divalidasi dengan tool OpenAPI, dan perubahannya terlihat di diff.
