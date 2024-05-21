# Broken Object Level Authorization
Penyerang dapat mengeksploitasi endpoint API yang rentan terhadap Broken Object Level Authorization (BOLA) / IDOR (Insecure Direct Object Reference) dengan memanipulasi ID objek yang dikirimkan dalam request. ID Objek dapat berupa apa saja, mulai dari bilangan bulat berurutan, UUID, atau string. Akses tidak sah terhadap objek pengguna lain dapat mengakibatkan pengungkapan data kepada pihak yang tidak berwenang, kehilangan data, atau manipulasi data

## Challenge 1 - Access details of another user’s vehicle
- Buka tool Burp Suite lalu tekan tombol **Refresh Location** pada halaman dashboard


- Pada tool Burp Suite akan terdeteksi endpoint API yang memuat informasi kendaraan berdasarkan ID kendaraan


- Klik menu **Community** untuk membuka halaman Community


- Pada halaman Community ditemukan endpoint API yang memuat ID kendaraan user lain


- Sekarang kita kirim request endpoint API yang memuat informasi kendaraan berdasarkan ID kendaraan ke tab Repeater


- Lalu ganti ID kendaraan dengan ID kendaraan yang ditemukan di halaman Community lalu tekan tombol **Send** maka kita berhasil mendapatkan informasi kendaraan dari pengguna lain


## Challenge 2 - Access mechanic reports of other users
- Kembali ke halaman dashboard, tekan tombol **Contact Mechanic**


- Hidupkan Intercept pada Burp Suite

- Isi form lalu tekan tombol **Send Service Requests**

- Setelah Burp Suite terbuka, klik kanan lalu pilih **Do intercept > Response to this request**

- Selanjutnya tekan tombol **Forward**

- Jika mendapatkan response berikut, klik kanan lalu pilih **Send to Repeater**

- Pindah ke tab Repeater dan tekan tombol **Send**

- Ubah request `POST` menjadi `GET` dan ubah endpoint API ke `/workshop/api/mechanic/mechanic_report?report_id=?` untuk mengakses detail report

- Jika sudah tekan tombol **Send** maka kita berhasil mengakses detail report yang sudah kita kirim sebelumnya

- Dari sini terlihat bahwa parameter `report_id` menggunakan bilangan bulat, sehingga memungkinkan kita mengubahnya dengan bilangan bulat lain seperti angka 1, 2, dan 3 untuk mengakses report yang dikirim oleh pengguna lain

