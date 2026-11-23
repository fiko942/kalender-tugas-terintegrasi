# Changelog

Perubahan penting proyek dicatat di sini.

## [0.1.0] - 2026-11-23

### Ditambahkan
- Repo proyek mandiri untuk Kalender Tugas Terintegrasi.
- Aplikasi web Next.js App Router di `apps/web` dengan dashboard, daftar tugas, kalender bulanan/mingguan, form tambah/edit, detail, perubahan status, konfirmasi hapus, filter, dan pengurutan.
- Supabase Auth/PostgreSQL migration dengan row-level security untuk profil, tugas, dan reminder; serta fungsi klaim reminder due atomik dengan status `processing` yang terpisah.
- Validasi domain tugas, status terlambat turunan, penjadwalan reminder H-3/H-1 waktu lokal, dan unit tests.
- README produk berisi Product Requirements Document dan traceability AC-001 sampai AC-043.
- Konfigurasi Vercel agar aplikasi dapat dideploy dari root `apps/web`.

### Verifikasi tahap ini
- Lulus: `npm run lint`, `npm run typecheck`, dan 5 unit test domain.
- Lulus: browser desktop demo — membuat tugas, melihat jumlah konsisten di dashboard/daftar, membuka kalender bulanan dan mingguan, melihat detail dan dialog konfirmasi hapus.
- Lulus: production build Next.js menghasilkan output `standalone`; server lokal production merespons HTTP 200 pada `/`.
- Belum terverifikasi: tampilan viewport mobile (browser emulation melaporkan 390×844 tetapi snapshot tetap 1458×728), login/persistensi Supabase, penerapan migration pada Supabase live, serta pengiriman notifikasi nyata.

### Batasan yang diketahui
- Deploy produksi belum dilakukan; membutuhkan project Vercel, project Supabase, dan environment secrets milik pemilik repo.
- Pengiriman notifikasi eksternal belum diaktifkan. Saat ini aplikasi menyiapkan jadwal dan status database; delivery harus diintegrasikan dengan provider terjadwal/server-side dan diuji sebelum dianggap lulus.
- Mode demo tanpa konfigurasi Supabase menggunakan data contoh di memori browser dan tidak menyediakan persistensi, autentikasi, atau isolasi multi-pengguna.
- AC-010/AC-013/AC-019/AC-022/AC-025/AC-028/AC-032/AC-035/AC-038/AC-039/AC-042 dan pengujian produksi masih memerlukan validasi tambahan; daftar test status aktual harus diperbarui setelah seluruh QA.
