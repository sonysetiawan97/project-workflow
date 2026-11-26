# Contract

Sumber kebenaran antarmuka antar-app. Kode di `apps/` mengikuti file di sini.

## Struktur

- `http/<service>.openapi.yaml`: satu file per service, OpenAPI 3.1.

## Aturan

- Ubah contract dulu, baru kode.
- Selama `info.version` masih `0.x`, setiap perubahan menaikkan versi minor tanpa ADR, karena belum ada konsumen yang dirilis.
- Versi `1.0.0` ditetapkan tech lead saat app konsumen pertama dirilis. Sejak itu, perubahan yang tidak breaking menaikkan versi minor; breaking change wajib ADR dengan Cakupan `contract` dan menaikkan versi major.
- Nama schema dan field mengikuti istilah di `glossary.md`.

## Daftar Service

| Service | File | Versi | Konsumen | Tanggal |
|---|---|---|---|---|
| {{service}} | {{http/<service>.openapi.yaml}} | {{versi}} | {{app yang memakai}} | {{tanggal konfirmasi terakhir, YYYY-MM-DD}} |
