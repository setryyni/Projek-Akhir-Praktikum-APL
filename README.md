# DRACULA-SIM: Sistem Informasi Manajemen Hemoglobin Pendonor PMI

**DRACULA-SIM** adalah aplikasi berbasis sistem informasi yang dirancang khusus untuk memfasilitasi Palang Merah Indonesia (PMI) dalam mengelola data pendonor, memantau kadar hemoglobin, serta melacak manajemen stok darah secara efisien dan terstruktur. Sistem ini menggunakan pembagian hak akses (*multi-role*) yang membedakan fungsi antara **Admin** (pengelola pusat) dan **User** (pendonor).

---

## 🚀 Fitur Utama Sistem

### 1. Sistem Autentikasi & Keamanan (Login & Register)
* **Registrasi Akun:** Memungkinkan pendonor baru membuat akun dengan validasi otomatis untuk mencegah duplikasi *username*.
* **Login Multi-Role:** Autentikasi pintar yang secara otomatis mengarahkan pengguna ke halaman **Admin** atau **User** berdasarkan *role* akun yang terdaftar.
* **Proteksi Anti-Brute Force:** Keamanan tambahan yang mendeteksi jika terjadi kesalahan login hingga 3 kali berturut-turut. Jika tercapai, sistem akan membekukan percobaan login dan menghentikan program selama 2 menit sebelum pengguna dapat mencoba kembali.

### 2. Fitur Menu User (Pendonor)
Setelah berhasil masuk, user akan disajikan menu interaktif yang terus berulang (*looping*) hingga memilih opsi keluar:
1.  **Profil:** Menampilkan informasi data diri lengkap milik pendonor.
2.  **Cek Jadwal:** Melihat jadwal pelaksanaan kegiatan donor darah yang tersedia.
3.  **Riwayat Donor:** Menyajikan catatan historis donor darah yang telah dilakukan sebelumnya.
4.  **Informasi Edukasi:** Menu yang berisi materi edukasi kesehatan seputar hemoglobin dan pentingnya donor darah.
5.  **Hapus Akun:** Fasilitas mandiri bagi user yang ingin menghapus akun mereka dari sistem.
6.  **Logout:** Menampilkan pesan "Logout berhasil", mengakhiri sesi user, dan keluar dari program.

### 3. Fitur Menu Admin (Pengelola PMI)
Admin memiliki panel kendali penuh (*Dashboard*) untuk mengelola operasional dengan 10 fitur utama yang berjalan dalam sistem *looping*:
1.  **Tambah Akun:** Membuat akun baru langsung melalui panel admin.
2.  **Tampilkan Semua Akun:** Melihat daftar seluruh akun yang terdaftar di dalam database.
3.  **Edit Data Diri Pendonor:** Mengubah informasi profil atau data personal pendonor.
4.  **Update Riwayat Pendonor:** Memperbarui catatan riwayat donor milik pendonor tertentu.
5.  **Hapus Pendonor:** Menghapus data pendonor dari sistem.
6.  **Cek Stok Darah:** Melihat ketersediaan kuantitas stok darah berdasarkan golongan atau kategori.
7.  **Update Stok Darah:** Menambahkan jumlah stok darah yang tersedia.
8.  **Kurangi Stok Darah:** Mengurangi jumlah stok darah (misal untuk penyaluran medis).
9.  **Verifikasi Data:** Melakukan validasi data sebelum disimpan secara permanen ke database.
10. **Logout:** Menyelesaikan sesi admin dengan pesan "Sampai Jumpa" dan kembali ke menu utama.

---

## 🗺️ Penjelasan Alur Program (Flowchart)

Aplikasi ini bekerja berdasarkan tiga arsitektur flowchart utama yang saling terintegrasi:

### A. Alur Utama (Login, Registrasi, & Proteksi)
1.  Program dimulai pada **Menu Awal** dengan opsi: *Register*, *Login*, atau *Keluar*.
2.  Jika memilih **Register**, pengguna memasukkan *username* dan *password*. Sistem memeriksa database `Users`. Jika *username* sudah ada, sistem memunculkan peringatan dan meminta input ulang. Jika belum ada, data disimpan dan registrasi berhasil.
3.  Jika memilih **Login**, pengguna memasukkan kredensial. Sistem melakukan pencocokan data.
    * Jika cocok, sistem memeriksa *role*. Jika `Admin == True` masuk ke **Admin Page**, jika `False` masuk ke **User Page**.
    * Jika salah, sistem menghitung jumlah kesalahan. Pada kesalahan ke-3, program akan dibekukan (*freeze*) selama 2 menit.
4.  Jika memilih **Keluar**, program menampilkan pesan penutup dan selesai (**END**).

### B. Alur Halaman User
1.  Setelah login sebagai user, sistem memuat database user dan menampilkan **Menu User (1-6)**.
2.  Sistem menerima input pilihan angka dari pengguna.
3.  Melalui percabangan kondisi, sistem mengeksekusi fungsi yang sesuai (`Profil`, `cekJadwal`, `riwayatDonor`, `edukasi`, atau `HapusAkun`).
4.  Setelah fungsi selesai dijalankan, aliran diagram dialihkan kembali (*loop*) ke tampilan Menu User.
5.  Jika pengguna memilih opsi **6 (Logout)**, sistem menampilkan pesan "Logout berhasil" dan program berakhir (**END**).
6.  Jika input tidak valid (di luar 1-6), sistem menampilkan pesan "Pilihan tidak tersedia" dan melakukan *loop* kembali ke menu utama user.

### C. Alur Halaman Admin
1.  Setelah login sebagai admin, sistem mengarahkan ke **Admin Page** dan menampilkan **Menu Tampilan (1-10)**.
2.  Sistem menerima input pilihan dari admin.
3.  Melalui serangkaian konektor logika (`A`, `B`, dan `C`), sistem memeriksa pilihan:
    * Pilihan 1-5 mengontrol manajemen akun dan pendonor (`Buat Akun`, `Tampilkan Akun`, `Update Data Diri`, `Update Riwayat`, `Hapus Pendonor`).
    * Pilihan 6-9 mengontrol manajemen logistik darah (`Cek stok`, `Update stok`, `Kurangi stok`, `Verifikasi data`).
4.  Setiap kali suatu aksi selesai dilakukan, sistem akan melakukan *looping* kembali ke tampilan menu utama Admin.
5.  Jika pilihan bernilai **10 (Logout)**, program menampilkan output "Sampai Jumpa" dan selesai (**END**).
6.  Jika input tidak sesuai, sistem menampilkan "Pilihan tidak valid" dan melakukan *looping* kembali ke menu utama Admin.

---

## 📝 Cara Menjalankan Aplikasi
1.  Pastikan lingkungan eksekusi (*Environment*) bahasa pemrograman Anda sudah terkonfigurasi.
2.  Jalankan file program utama.
3.  Lakukan registrasi terlebih dahulu jika belum memiliki akun, atau login menggunakan akun admin bawaan (*default admin credentials*).
4.  Operasikan aplikasi dengan memasukkan angka menu yang tertera pada layar terminal atau GUI.
5.  Selalu gunakan opsi **Logout** sebelum menutup aplikasi untuk memastikan seluruh perubahan data tersimpan dengan aman pada database.