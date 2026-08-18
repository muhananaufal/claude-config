# /audit — Forensic Quality Gate Audit

Audit repo / direktori kerja saat ini dengan standar exit gate §5.5 `AGENTS.md` plus pemindaian forensik di bawah.

## Yang WAJIB dipindai

| Kategori | Cari |
| :--- | :--- |
| **Placeholder** | `// TODO`, `FIXME`, `TBD`, mock, stub, kode kosong, `/* omitted */` |
| **Type-safety** | `any` (TS), unchecked `unwrap()`/`expect()` (Rust), raw `interface{}` (Go), `mixed` tanpa guard (PHP) |
| **Secret** | credential & API key hardcode, `.env` ikut ter-commit, token di log |
| **OWASP Top 10** | SQL Injection, IDOR, Mass Assignment, broken auth, input validation hilang, hashing lemah (WAJIB Argon2id/bcrypt) |
| **Performa** | N+1 query, foreign key tanpa index, goroutine/promise leak, listener & stream tidak ditutup |
| **Konkurensi** | race condition, deadlock, shared state tanpa lock, missing timeout |

## Prosedur

1. Ada `README.md`/`AGENTS.md`/`CLAUDE.md` di root proyek → WAJIB dibaca lebih dulu (`AGENTS.md` §7).
2. Jalankan test + linter stack terkait. Laporkan output APA ADANYA. DILARANG mengklaim lulus tanpa menampilkan bukti.
3. Susun laporan dengan format di bawah. Tiap temuan WAJIB berlabel epistemik (`AGENTS.md` §3) — temuan hasil pembacaan kode nyata `[fakta:path:baris]`, dugaan pola `[inferensi]`.
4. **DILARANG memperbaiki temuan tanpa persetujuan user**, KECUALI user menulis "sekalian perbaiki". Perbaikan apa pun tetap lewat Panel Multi-POV (`AGENTS.md` §0.2) sebelum dieksekusi.

## Format laporan WAJIB

```markdown
## Temuan Kritis
| # | Berkas:baris | Masalah | Dampak | Tingkat |

## Temuan Non-Kritis

## Hasil Test & Linter
<!-- perintah yang dijalankan + output apa adanya -->

## Rekomendasi Perbaikan
<!-- menyangkut arsitektur? WAJIB ≥3 opsi netral + trade-off, sesuai §4 AGENTS.md -->
```
