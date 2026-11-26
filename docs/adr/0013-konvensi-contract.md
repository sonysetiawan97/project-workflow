# Konvensi penulisan contract

- **Tanggal:** 2026-11-27
- **Sumber:** percakapan 2026-11-27
- **Status:** accepted
- **Cakupan:** contract
- **Pemutus:** pemilik repo

## Keputusan

Field dan parameter di contract memakai snake_case, sama dengan kolom di `architecture/data-model.md`. Path memakai kebab-case dan nama schema PascalCase, semuanya dari istilah `glossary.md`. Setiap operation diberi tag `F-NN` dan menyebut BR yang ditegakkan di `description`. Contract cukup divalidasi dengan parse YAML dan cek `openapi: 3.1.0`.

## Opsi yang Dipertimbangkan

- **Field camelCase**: ditolak; snake_case membuat field dan kolom database bernama sama.
- **Operation tanpa rujukan ke FSD**: ditolak; dev dan QC perlu melacak endpoint ke fitur dan aturan bisnis.
- **Lint dengan Redocly**: ditolak; butuh Node dan internet, sementara parse YAML tidak butuh tool tambahan.

## Konsekuensi

- Kesalahan struktur OpenAPI yang tetap YAML valid (misalnya `$ref` putus) tidak tertangkap oleh pengecekan skill.
