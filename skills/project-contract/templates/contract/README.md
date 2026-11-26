# Contract

Sumber kebenaran antarmuka antar-app. Kode di `apps/` mengikuti file di sini.

## Struktur

- `http/<service>.openapi.yaml`: satu file per service, OpenAPI 3.1.

## Aturan

- Ubah contract dulu, baru kode.
- Breaking change: buat ADR dengan Cakupan `contract`, lalu naikkan versi major di `info.version`.
- Perubahan yang tidak breaking menaikkan versi minor.
- Nama schema dan field mengikuti istilah di `glossary.md`.

## Daftar Service

| Service | File | Versi | Konsumen |
|---|---|---|---|
| {{service}} | {{http/<service>.openapi.yaml}} | {{versi}} | {{app yang memakai}} |
