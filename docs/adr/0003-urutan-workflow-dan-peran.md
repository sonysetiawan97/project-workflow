# Urutan workflow dan pembagian peran

- **Tanggal:** 2026-11-26
- **Sumber:** percakapan 2026-11-26
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

Enam skill fondasi berjalan berurutan: `project-setup`, `project-grilling` (PM), `project-prd` (PM), `project-fsd` (PM/BA), `project-architecture` (tech lead), `project-contract` (tech lead). PRD ditulis sebelum FSD, dan FSD merujuk PRD. Architecture dan contract adalah skill teknis tersendiri, terpisah dari grilling PM dan dari satu sama lain.

## Opsi yang Dipertimbangkan

- **PRD ditulis dari FSD**: ditolak; PRD menjawab apa dan kenapa, jadi PRD ada di hulu.
- **Architecture dan contract diisi saat grilling PM**: ditolak; PM tidak bisa menjawab pertanyaan teknis, sehingga agent akan menebak.
- **Architecture dan contract digabung jadi satu skill**: ditolak; keduanya dipisah.

## Konsekuensi

- Setiap skill mengecek Artefak hulunya sebelum berjalan.
- Tahap per fitur (grilling fitur, triage, spec, tiket) baru berjalan setelah fondasi ini selesai.
