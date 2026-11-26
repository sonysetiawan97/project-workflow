# Skills

Skill khusus project ini: pengetahuan yang hanya berlaku di sini, misalnya cara menambah endpoint di codebase ini, format test case project ini, atau cara memakai design token project ini.

## Struktur

- Satu folder per skill: `skills/<nama-skill>/SKILL.md`, datar tanpa subfolder kategori.
- `<nama-skill>` huruf kecil kebab-case.
- Prefix `project-` milik skill workflow global; skill di sini memakai nama lain.
- Claude Code membaca folder ini lewat `.claude/skills`, agent lain lewat `.agents/skills`. Keduanya symlink ke `skills/`.

## Kapan Dipecah

Folder ini sengaja datar. Pecah per divisi hanya jika jumlah skill mulai menyulitkan pencarian.
