# Arsitektur diusulkan per file

- **Tanggal:** 2026-11-27
- **Sumber:** percakapan 2026-11-27
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

`project-architecture` tidak mewawancarai tech lead dari nol. Agent menurunkan usulan satu file dari PRD, FSD, ADR, dan kode yang ada, menulisnya, lalu bertanya apakah file itu sudah direview dan sesuai. File berikutnya baru dikerjakan setelah tech lead mengonfirmasi. Skill hanya berjalan dari FSD berstatus `approved`.

## Opsi yang Dipertimbangkan

- **Tanya jawab satu per satu seperti grilling**: ditolak; tech lead bisa menilai usulan teknis, dan sebagian besar isi bisa diturunkan dari FSD.
- **Mengabaikan kode yang sudah ada di `apps/`**: ditolak; usulan mengikuti kode yang ada, dan penyimpangan diputuskan lewat ADR.

## Konsekuensi

- Template arsitektur tidak punya field `Status`, jadi run berikutnya menanyakan ulang setiap file yang sudah ada.
- Jawaban untuk Pertanyaan Terbuka di PRD dan FSD dicatat di `architecture/` atau ADR; PM/BA yang menghapusnya dari dokumen mereka.
