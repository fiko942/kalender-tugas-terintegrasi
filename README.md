# Kalender Tugas Terintegrasi

> Aplikasi mandiri untuk mahasiswa yang ingin mencatat tugas kuliah, melihat sebaran tenggat, memantau progres, dan menyiapkan pengingat dalam satu tempat.

**Status:** implementasi awal (`0.1.0`) · **Aplikasi:** [`apps/web`](apps/web) · **Perubahan:** [`CHANGELOG.md`](CHANGELOG.md)

## Menjalankan aplikasi

Persyaratan lokal, environment Supabase, skrip pengujian, dan langkah deploy ada di [`apps/web/README.md`](apps/web/README.md). Aplikasi memakai Next.js App Router, Supabase Auth/PostgreSQL, dan Vercel sebagai target deployment yang dikonfigurasi. Deployment produksi serta pengiriman notifikasi membutuhkan konfigurasi akun/provider.

---

# Product Requirements Document (PRD)

## Fitur: Kalender Tugas Terintegrasi

**Versi:** 1.0 · **Status dokumen sumber:** Draft · **Jenis produk:** aplikasi mandiri manajemen tugas akademik mahasiswa

## 1. Product Overview

### 1.1 Latar Belakang
Mahasiswa sering menghadapi kesulitan mengelola berbagai tugas akademik dari mata kuliah berbeda. Informasi tenggat tersebar di berbagai sumber, seperti LMS, grup komunikasi kelas, dan pengumuman dosen. Kondisi tersebut berpotensi membuat mahasiswa lupa tenggat, sulit menentukan prioritas, dan menumpuk tugas menjelang akhir minggu. Produk ini menyediakan satu tempat untuk mencatat, melihat, dan memantau tenggat serta pengingat otomatis tiga hari dan satu hari sebelumnya.

### 1.2 Product Vision
Menyediakan satu pusat pengelolaan tenggat waktu akademik yang membantu mahasiswa mengorganisasi tugas, mengatur waktu pengerjaan, dan menyelesaikan tugas tepat waktu.

### 1.3 Target Pengguna
Mahasiswa aktif yang mengikuti beberapa mata kuliah dan memiliki berbagai tugas dengan tenggat berbeda.

## 2. User Problem

Permasalahan utama menurut PRD sumber:
- Mahasiswa kesulitan mengingat seluruh tenggat tugas.
- Informasi tugas tersebar di berbagai platform.
- Tidak ada tampilan terpusat untuk memantau jadwal pengumpulan.
- Tugas sering menumpuk menjelang akhir minggu.
- Mahasiswa membutuhkan pengingat sebelum tenggat agar dapat mempersiapkan pengerjaan.

**Problem statement:** Mahasiswa membutuhkan sistem pengelolaan tugas terpusat yang dapat menampilkan seluruh tenggat waktu dan memberikan pengingat otomatis agar mereka dapat mengatur waktu pengerjaan dan mengumpulkan tugas tepat waktu.

## 3. User Persona

**Budi, 20 tahun, mahasiswa aktif.** Mengikuti beberapa mata kuliah, menerima tugas dari beberapa dosen, menggunakan smartphone dan laptop, serta memiliki jadwal kuliah dan kegiatan organisasi.

**Goals:** mengetahui seluruh tenggat, menghindari keterlambatan, mengatur prioritas, dan mengurangi penumpukan pekerjaan.

**Pain points:** sering lupa tenggat, kesulitan memantau banyak tugas, dan tidak memiliki pengingat terorganisasi.

## 4. Product Goals & Success Metrics

- Memusatkan informasi tenggat seluruh tugas mahasiswa.
- Memudahkan pemantauan tugas berdasarkan tanggal pengumpulan.
- Membantu mengidentifikasi tugas yang mendekati tenggat.
- Memberikan pengingat otomatis sebelum tenggat.
- Memudahkan pemantauan progres penyelesaian tugas.

| Indikator | Target awal |
| --- | --- |
| Tugas tercatat memiliki tenggat | 100% |
| Pengingat H-3 dan H-1 berhasil dijadwalkan | 100% |
| Tugas selesai sebelum tenggat | Meningkat dibanding baseline |
| Mahasiswa memakai kalender setiap minggu | ≥ 70% pengguna aktif |

Target adalah hipotesis awal dan perlu divalidasi melalui pengujian produk.

## 5. Functional Requirements

### FR-01 — Manajemen Tugas
Pengguna dapat menambah, melihat detail, mengubah, dan menghapus tugas. Data terdiri atas nama tugas, mata kuliah, deskripsi, tanggal dan waktu tenggat, status pengerjaan, dan tanggal pembuatan.

### FR-02 — Kalender Tugas Terintegrasi
Kalender bulanan dan mingguan menampilkan tugas sesuai tenggat; jumlah tugas tiap tanggal; pemilihan tanggal untuk melihat daftar tugas; serta tugas mendatang.

### FR-03 — Pengingat Otomatis
Jadwalkan H-3 dan H-1, hanya untuk tugas belum selesai dan hanya jika waktunya belum berlalu. Pengingat memuat nama tugas, mata kuliah, dan tenggat. Catat status pengiriman.

### FR-04 — Status Pengerjaan
Setiap tugas memiliki satu status: **Belum Dikerjakan**, **Sedang Dikerjakan**, atau **Selesai**. Pengguna dapat mengubah status manual.

### FR-05 — Daftar Tugas
Daftar mendukung semua tugas, belum dikerjakan, sedang dikerjakan, selesai, mendekati tenggat, dan terlambat; pengurutan sekurangnya berdasarkan tenggat terdekat.

## 6. Non-Functional Requirements

- **NFR-01 Performance:** kalender dimuat cepat; perubahan status diperbarui tanpa reload penuh jika memungkinkan.
- **NFR-02 Usability:** mudah digunakan mahasiswa; tenggat mudah ditemukan; penambahan tugas sederhana.
- **NFR-03 Responsive:** dapat digunakan di desktop, tablet, dan smartphone; kalender menyesuaikan ukuran layar.
- **NFR-04 Reliability:** tugas tersimpan persisten; scheduler konsisten; kegagalan pengiriman dapat dicatat.
- **NFR-05 Security:** pengguna hanya dapat mengakses dan mengelola tugas miliknya melalui autentikasi dan otorisasi.

## 7. Business Rules

1. Nama tugas, mata kuliah, dan tenggat wajib diisi.
2. Tenggat baru harus berada di masa depan.
3. Setiap tugas memiliki satu status pengerjaan.
4. Pengingat H-3 dan H-1 dijadwalkan dari tenggat.
5. Status **Selesai** membatalkan pengingat berikutnya.
6. Tenggat yang diubah menyebabkan jadwal pengingat diperbarui.
7. Tugas yang dibuat kurang dari tiga hari sebelum tenggat hanya memperoleh pengingat yang masih relevan.
8. Tugas lewat tenggat tetap ditampilkan di kalender dan daftar.
9. **Terlambat adalah keadaan turunan** dari tenggat yang lewat dan status yang belum selesai, bukan status tersimpan keempat.
10. Waktu pengingat default pukul **09.00 waktu lokal** pengguna.

## 8. User Stories

- **US-01 Menambahkan Tugas:** sebagai mahasiswa, saya ingin mencatat tugas dan tenggat agar kewajiban akademik terkumpul.
- **US-02 Melihat Kalender:** saya ingin melihat seluruh tenggat pada kalender agar tahu jadwal pengumpulan.
- **US-03 Menerima Pengingat:** saya ingin menerima pengingat H-3 dan H-1 agar tidak lupa mengerjakan tugas.
- **US-04 Memperbarui Status:** saya ingin mengubah status pengerjaan agar dapat memantau progres.
- **US-05 Mengubah Tenggat:** saya ingin memperbarui tenggat ketika jadwal dosen berubah.
- **US-06 Melihat Tugas Terdekat:** saya ingin melihat tenggat terdekat agar dapat menentukan prioritas.

## 9. Scope

### In Scope
Tambah, ubah, lihat, hapus tugas; kalender bulanan dan mingguan; daftar berdasarkan status; pengingat H-3/H-1; pengelolaan status; tampilan responsif; dan penjadwalan ulang ketika tenggat berubah.

### Out of Scope
Integrasi Google Calendar; sinkronisasi LMS eksternal; pengumpulan file; kolaborasi mahasiswa; pembagian tugas kelompok; dan rekomendasi prioritas berbasis AI.

## 10. Assumptions & Dependencies

### Asumsi produk dari PRD
- Mahasiswa sudah memiliki akun dan login.
- Pengguna memasukkan tugas secara manual.
- Setiap tugas memiliki satu tenggat tanggal-waktu.
- Pengguna memakai zona waktu lokal pada akun.

### Keputusan tahap ini
- Produk dibangun sebagai aplikasi mandiri.
- Next.js App Router digunakan untuk web; Supabase Auth/PostgreSQL untuk identitas dan persistensi; Vercel disiapkan sebagai platform deployment web.
- Pilihan provider pengiriman notifikasi belum ditentukan; aplikasi tidak menyatakan pesan terkirim tanpa konfirmasi provider.

### Dependensi
Sistem autentikasi, database, scheduler, layanan notifikasi, serta izin notifikasi jika memakai Web Push. Konfigurasi Supabase dan Vercel diperlukan untuk deployment produksi.

## 11. Expected Deliverables

- Dashboard tugas.
- Halaman kalender tugas.
- Form tambah/edit.
- Halaman atau panel detail.
- Daftar tugas berdasarkan status.
- Sistem pengingat otomatis H-3/H-1.
- Perubahan status.
- Penyimpanan persisten.

## 12. Acceptance Criteria

AC-001 — **Create Task** *(Must Have)*: tugas valid tersimpan dengan ID unik, status awal Belum Dikerjakan, konfirmasi sukses, dan tampil pada daftar serta kalender.

AC-002 — **Required Field Validation** *(Must Have)*: field wajib kosong ditolak, pesan tampil pada field terkait, dan input lainnya tetap terjaga.

AC-003 — **Past Deadline Validation** *(Must Have)*: tenggat masa lalu untuk tugas baru ditolak dengan pesan kesalahan.

AC-004 — **Edit Task** *(Must Have)*: perubahan tersimpan dan tampil pada seluruh halaman terkait.

AC-005 — **Delete Task** *(Must Have)*: setelah konfirmasi tugas terhapus, reminder tertunda dibatalkan, tugas hilang dari seluruh tampilan, dan konfirmasi sukses muncul.

AC-006 — **Cancel Delete** *(Must Have)*: batal menutup dialog dan mempertahankan tugas.

AC-007 — **Monthly Calendar** *(Must Have)*: kalender bulanan benar, menandai tanggal bertugas, menghitung jumlah tugas, dan menandai hari ini.

AC-008 — **Calendar Navigation** *(Must Have)*: navigasi bulan sebelumnya/berikutnya menampilkan periode yang benar tanpa kehilangan data.

AC-009 — **Date Selection** *(Must Have)*: pemilihan tanggal menampilkan tugas pada tanggal itu.

AC-010 — **Weekly Calendar** *(Should Have)*: tampilan mingguan menampilkan tugas per hari.

AC-011 — **Update Task Status** *(Must Have)*: status tersimpan dan diperbarui pada semua halaman.

AC-012 — **Completed Task** *(Must Have)*: status Selesai membatalkan seluruh pengingat tertunda.

AC-013 — **Reactivate Completed Task** *(Should Have)*: aktivasi ulang menghitung kembali pengingat yang masih relevan.

AC-014 — **H-3 Reminder** *(Must Have)*: pada jadwal H-3, sistem mengirim reminder untuk tugas belum selesai.

AC-015 — **H-1 Reminder** *(Must Have)*: pada jadwal H-1, sistem mengirim reminder untuk tugas belum selesai.

AC-016 — **Reminder Cancellation** *(Must Have)*: pengingat tugas yang dihapus/selesai tidak dikirim.

AC-017 — **Reminder Rescheduling** *(Must Have)*: perubahan tanggal/waktu tenggat membatalkan jadwal lama dan membuat jadwal relevan baru.

AC-018 — **No Duplicate Reminder** *(Must Have)*: satu jadwal reminder tidak menghasilkan notifikasi duplikat.

AC-019 — **Notification Failure** *(Should Have)*: kegagalan provider tercatat dan tidak menghilangkan data tugas.

AC-020 — **Dashboard Summary** *(Must Have)*: dashboard memuat total, status belum dikerjakan/sedang dikerjakan/selesai, tugas mendatang, dan terlambat.

AC-021 — **Upcoming Tasks** *(Must Have)*: tugas mendatang diurutkan menurut tenggat terdekat.

AC-022 — **Summary Navigation** *(Should Have)*: kartu ringkasan membuka daftar dengan filter sesuai.

AC-023 — **Filter by Status** *(Must Have)*: daftar menampilkan hanya tugas sesuai filter.

AC-024 — **Overdue Filter** *(Must Have)*: filter Terlambat menampilkan tenggat lampau berstatus belum selesai; terlambat dihitung, tidak disimpan sebagai status baru.

AC-025 — **Sorting** *(Should Have)*: urutan mengikuti pilihan tanpa menghilangkan filter aktif.

AC-026 — **Consistent Navigation** *(Must Have)*: navigasi utama membuka halaman benar dan menandai menu aktif.

AC-027 — **Feedback** *(Must Have)*: tindakan penting memberi umpan balik yang dapat dipahami.

AC-028 — **Empty State** *(Should Have)*: data kosong atau filter tanpa hasil menampilkan pesan dan tindakan relevan.

AC-029 — **Responsive Layout** *(Must Have)*: desktop/tablet/mobile menyesuaikan tanpa overflow yang mengganggu; tombol, field, dan informasi tetap terbaca.

AC-030 — **Form Error Recovery** *(Must Have)*: kesalahan tidak menghapus nilai input lain yang telah diisi.

AC-031 — **Color Consistency** *(Must Have)*: warna konsisten dengan design system.

AC-032 — **Typography Consistency** *(Should Have)*: tipografi dan hierarki mengikuti design system.

AC-033 — **Component Consistency** *(Must Have)*: button, input, card, badge, modal, dan komponen lain konsisten.

AC-034 — **Status Indicator** *(Must Have)*: setiap status memiliki indikator visual yang konsisten dan dapat dibedakan.

AC-035 — **Performance** *(Should Have)*: halaman utama target maksimal tiga detik pada kondisi wajar; interaksi responsif; penyimpanan menampilkan loading.

AC-036 — **Data Persistence** *(Must Have)*: data tetap tersedia setelah reload atau login ulang.

AC-037 — **Data Isolation** *(Must Have)*: pengguna hanya dapat mengakses tugas miliknya.

AC-038 — **Accessibility** *(Should Have)*: fungsi utama dapat dipakai dengan keyboard; label, fokus, pesan error jelas; status tidak hanya dibedakan warna.

AC-039 — **Task Created Less Than Three Days Before Deadline** *(Must Have)*: jadwalkan hanya reminder yang masih relevan dan belum lewat.

AC-040 — **Task Becomes Overdue** *(Must Have)*: tugas belum selesai setelah tenggat ditampilkan sebagai terlambat tanpa mengubah status tersimpan.

AC-041 — **Multiple Tasks on the Same Date** *(Must Have)*: pemilihan tanggal menampilkan seluruh tugas pada tanggal itu.

AC-042 — **Network Failure During Save** *(Must Have)*: kegagalan koneksi menampilkan pesan, mempertahankan input, dan mencegah duplikasi saat percobaan ulang.

AC-043 — **Delete Task with Pending Reminder** *(Must Have)*: pengingat tidak dikirim setelah penghapusan berhasil.

## 13. Release Acceptance

Versi 1.0 dapat diterima bila seluruh AC Must Have lulus, tidak ada bug kritis, CRUD dan persistensi berjalan, kalender akurat, reminder H-3/H-1 dan rescheduling terbukti berfungsi, UI responsif, serta tidak ada masalah keamanan kritis. Kriteria yang belum dipenuhi harus dilaporkan sebagai **Fail**, **Blocked**, atau **Not Tested**, bukan diklaim selesai.

## 14. Test Execution Report

Setiap acceptance criterion perlu memiliki hasil dan bukti. Status yang diperbolehkan: **Pass**, **Fail**, **Blocked**, **Not Tested**. Status Pass hanya diberikan setelah pengujian membuktikannya. Status implementasi awal dan batasan integrasi dicatat di [`CHANGELOG.md`](CHANGELOG.md) dan laporan tahap berikutnya.
