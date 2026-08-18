# /greenfield — Inisiasi Proyek Baru

Proyek baru masuk lewat gerbang yang sama dengan request lain: **Panel Multi-POV** (`AGENTS.md` §0.2). Macro ini tidak menggantikan panel — ia hanya menyediakan checklist fondasi yang sering terlupa saat panel sudah lolos.

## Urutan

1. **Sapu Panel Multi-POV** (`skills/meta-panel/SKILL.md`). Lensa 📋 Manager yang paling menentukan di sini: masalah nyatanya apa, dan apakah proyek baru memang jawabannya (vs memakai yang sudah ada).
2. **Tentukan stack.** Belum jelas → tanya user, DILARANG menebak. Pohon keputusannya di `skills/meta-panel/references/decision-tree.md`.
3. **BERHENTI.** Tunggu persetujuan user ("Gasskan"). DILARANG menulis kode sebelum itu.
4. Setelah disetujui, eksekusi sesuai `AGENTS.md` §5 — `.gitignore` sebagai langkah pertama (`meta-git` §3), lalu batch maksimal 3–4 berkas per giliran.

## Checklist fondasi — pasang yang relevan, bukan semuanya

Ambil hanya yang benar-benar dibutuhkan proyek ini. Memaksakan `docker-compose` 3-tier untuk skrip 100 baris adalah pelanggaran KISS, dan lensa 💰 Cost akan menandainya.

| # | Pilar | Kapan relevan |
| :-: | :--- | :--- |
| 1 | **Container topology** — Tier 1 core DB/cache, profil telemetry & stress terpisah. DILARANG auto-run `docker build`/`up`. | Ada DB/cache ter-provision atau proses yang hidup terus |
| 2 | **Fail-fast config** — `.env.example` + validator yang crash saat boot bila env kurang/salah tipe. | Selalu, begitu ada env var apa pun |
| 3 | **Graceful shutdown** — tangkap `SIGINT`/`SIGTERM`, drain in-flight, flush log & trace sebelum exit. | Ada proses long-running (server, worker) |
| 4 | **Migration & idempotent seeder** — folder `migrations/` + seeder yang aman dijalankan berulang. | Ada database |
| 5 | **Task runner** — target baku `dev`, `test`, `migrate`, `seed`, dan yang dipakai proyek ini. | Selalu, begitu perintahnya lebih dari satu |

## Catatan

Korpus `skills/mastery-*/references/_protocol/greenfield.md` berstatus **arsip** — boleh dibuka sebagai rujukan dan dikutip `[fakta:path]`, tetapi tidak wajib dibaca. Untuk detail stack-spesifik, sumber yang lebih sahih adalah dokumentasi resmi versi terpasang dan source library di `vendor/`/`node_modules/`/`~/go/pkg/mod` (`AGENTS.md` §0.1).
