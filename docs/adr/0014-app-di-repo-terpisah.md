# App di repo terpisah

- **Tanggal:** 2026-11-27
- **Sumber:** percakapan 2026-11-27
- **Status:** accepted
- **Cakupan:** architecture
- **Pemutus:** pemilik repo

## Keputusan

Setiap app di `apps/<app>/` punya repo git sendiri. Repo Project hanya menyimpan dokumen, contract, dan skill, jadi `.gitignore` dari `project-setup` mengabaikan isi `apps/` kecuali `apps/.gitkeep`.

## Opsi yang Dipertimbangkan

- **Kode app ikut di repo Project (monorepo)**: ditolak; setiap app dikelola di repo terpisah.

## Konsekuensi

- Repo Project tidak mencatat versi app mana yang cocok dengan contract; setiap orang meng-clone app sendiri ke `apps/<app>/`.
- Skill yang membaca `apps/` tetap bekerja selama app sudah di-clone di sana.
