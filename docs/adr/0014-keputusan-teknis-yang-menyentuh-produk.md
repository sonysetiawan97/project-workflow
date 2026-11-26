# Keputusan teknis yang menyentuh produk

- **Tanggal:** 2026-11-27
- **Sumber:** percakapan 2026-11-27, uji coba `project-architecture` di project dummy
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

Keputusan teknis yang juga menyentuh perilaku produk, kepatuhan, atau data pribadi punya dua jalur yang dipilih tech lead: diputuskan sekarang lewat ADR dengan baris Konsekuensi `FSD perlu diubah: <F-NN>, <apa yang berubah>`, atau dikembalikan ke PM lewat `project-fsd` lebih dulu. `project-fsd` membawa ADR itu ke PM sebagai usulan. Jika PM menolak, keputusan PM langsung masuk FSD, dan `project-fsd` menulis ADR produk yang menggantikan ADR tech lead dengan baris `architecture/ perlu diubah: <apa yang berubah>`.

## Opsi yang Dipertimbangkan

- **Tech lead memutuskan tanpa jalur ke FSD**: ditolak; perubahan FSD yang dibutuhkan mudah terlewat.
- **Penolakan PM dikembalikan ke tech lead untuk ADR pengganti**: ditolak; butuh dua run tambahan, sementara PM adalah Pemutus perilaku produk.

## Konsekuensi

- Keputusan yang menyentuh produk ditulis sebagai ADR tersendiri, supaya penolakan PM hanya menggantikan keputusan itu.
- Baris `FSD perlu diubah:` dianggap diterapkan jika nomor ADR-nya disebut di `Riwayat Perubahan` FSD; baris `architecture/ perlu diubah: <file>, <file>: <apa yang berubah>` dianggap diterapkan jika setiap file yang disebut merujuk nomor ADR-nya.
- `project-contract` berhenti selama masih ada baris yang belum diterapkan, sehingga contract tidak dibangun dari FSD atau arsitektur yang usang.
- Alasan teknis tech lead bisa dikalahkan PM; tech lead hanya menyesuaikan `architecture/` di run berikutnya.
