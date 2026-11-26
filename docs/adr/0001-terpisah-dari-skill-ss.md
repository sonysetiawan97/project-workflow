# project-workflow terpisah dari skill ss

- **Tanggal:** 2026-11-26
- **Sumber:** percakapan 2026-11-26
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

project-workflow adalah konsep baru yang ditulis ulang, terpisah dari `ss-workflow` dan `ss-prd-division`, dan menggantikan keduanya. Dari skill ss hanya template yang diambil: ADR dan glossary.

## Opsi yang Dipertimbangkan

- **Memperluas `ss-workflow`**: ditolak, karena konsep baru tidak mau terikat konvensi lama seperti `docs/plan/tickets/`.
- **Memakai ulang skill ss untuk tahap per fitur dan per divisi**: ditolak dengan alasan yang sama.

## Konsekuensi

- Skill tahap per fitur (grilling fitur, triage, spec, tiket) ditulis ulang di repo ini.
- Skill di repo ini tidak merujuk file di repo ss.
