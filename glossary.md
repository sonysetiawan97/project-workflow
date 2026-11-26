<!--
Template glosarium: sama dengan skills/project-setup/templates/glossary.md.
-->
# project-workflow

Kumpulan skill yang membangun project dari nol sampai contract siap, dengan dokumen berbahasa Indonesia.

## Istilah

**Project**:
Repo aplikasi yang dibangun dengan workflow ini, berisi `architecture/`, `contract/`, `skills/`, `docs/`, dan `apps/`.
_Hindari_: Repo, aplikasi

**Artefak**:
Dokumen yang ditulis sebuah skill ke dalam Project, misalnya PRD, FSD, ADR, atau Tiket.
_Hindari_: Output, file, dokumen hasil

**Template**:
Kerangka heading dan field yang wajib diikuti persis oleh sebuah Artefak.
_Hindari_: Format, contoh, skeleton

**Template Bersama**:
Template yang dipakai lebih dari satu skill (ADR, glossary, Tiket) dan disalin ke Project oleh `project-setup`.
_Hindari_: Template global

**Skill Pemilik**:
Satu-satunya skill yang boleh menulis sebuah Artefak; glossary dan ADR tidak punya Skill Pemilik dan ditulis oleh skill yang sedang berjalan.
_Hindari_: Writer, owner

**Divisi**:
Kelompok kerja yang mengerjakan Tiket secara paralel; default `dev`, `qc`, `ui-ux`.
_Hindari_: Tim, departemen

**Fitur**:
Kemampuan produk yang didaftarkan di PRD dengan ID `F-01`.
_Hindari_: Modul, feature

**Aturan Bisnis**:
Aturan perilaku sistem di FSD dengan ID global `BR-001`.
_Hindari_: Business rule, rule

**Tiket**:
Satu unit kerja satu Divisi untuk satu Fitur, disimpan di `docs/tracker/<divisi>/<fitur>/`.
_Hindari_: Issue, task

**Contract**:
Spesifikasi OpenAPI antar-app di `contract/` yang wajib diikuti kode.
_Hindari_: Kontrak, API spec

**Cakupan**:
Field ADR yang menyebut wilayah keputusan: `product`, `architecture`, `contract`, atau sebuah Divisi.
_Hindari_: Scope

**Pemutus**:
Role yang memutuskan isi sebuah ADR.
_Hindari_: Decider

**Skill Workflow**:
Skill `project-*` dari repo ini, di-install global oleh setiap anggota tim.
_Hindari_: Skill global

**Skill Project**:
Skill khusus satu Project yang disimpan di folder `skills/` Project itu.
_Hindari_: Skill lokal

**Setup Token**:
Placeholder huruf besar seperti `{{PROJECT_NAME}}` yang diisi `project-setup`.
_Hindari_: Variabel
