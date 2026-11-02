## Tabel Test Case Validasi

Berikut adalah 5 test case pengujian skenario input yang salah berdasarkan kode HTML form registrasi event IT 2026:

| No | Field / Input | Skenario Input Uji | Output & Pesan Validasi Browser yang Diharapkan | Status / Keterangan |
| :---: | :--- | :--- | :--- | :---: |
| **1** | **Nama Lengkap** | Diisi kurang dari 3 karakter (contoh: `A`). | Browser menolak pengiriman form dan memunculkan pesan: *"Please lengthen this text to 3 characters or more (you are currently using 1 character)."* | **PASSED** (Atribut `minlength="3"`) |
| **2** | **Email** | Diisi format email tidak valid (contoh: `nama@` atau `nama.com`). | Browser menolak pengiriman form dan memunculkan pesan: *"Please include an '@' in the email address."* atau *"Please enter an email address."* | **PASSED** (Atribut `type="email"`) |
| **3** | **Nomor Telepon** | Diisi format angka yang salah (contoh: `08123` [kurang digit] atau `1234567890` [tidak diawali `08`]). | Browser menolak pengiriman form dan memunculkan pesan: *"Please match the requested format."* | **PASSED** (Atribut `pattern="^08[0-9]{8,11}$"`) |
| **4** | **Kategori Peserta** | Menolak pilihan dan membiarkan opsi default (`Pilih Kategori` dengan `value=""`). | Browser menolak pengiriman form dan memunculkan pesan: *"Please select an item in the list."* | **PASSED** (Atribut `required` pada `<select>`) |
| **5** | **Kartu Identitas** | Tidak memilih/mengunggah berkas sama sekali. | Browser menolak pengiriman form dan memunculkan pesan: *"Please select a file."* | **PASSED** (Atribut `required` pada `type="file"`) |

## Validasi Wajib Dilakukan di Server

Meskipun validasi client-side (HTML5 / JavaScript) memberikan respon langsung kepada pengguna, validasi di sisi server (server-side) tetap wajib dilakukan karena alasan berikut:

1. Pengabaian Validasi Client (Bypass):
Pengguna dapat dengan mudah memanipulasi atau menghapus atribut validasi HTML5 (seperti required, pattern, minlength) menggunakan Developer Tools browser (F12) sebelum mengirimkan data.

2. Keamanan Unggah File:
Atribut accept pada HTML hanya memfilter pilihan berkas di tampilan dialog file picker. Server wajib memeriksa ulang MIME-type, ekstensi asli, serta ukuran berkas untuk mencegah pengunggahan berkas berbahaya (seperti skrip .php atau .exe).

3. Pencegahan Serangan:
Pembersihan data pada server sangat krusial untuk mencegah serangan SQL Injection pada database dan Cross-Site Scripting dari teks input.

4. Validasi Keunikan Data:
Pengecekan keunikan data (seperti memastikan email atau nomor telepon belum terdaftar) hanya dapat dilakukan di server melalui kueri basis data.
