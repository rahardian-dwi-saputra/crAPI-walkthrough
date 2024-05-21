# Broken Object Level Authorization
Penyerang dapat mengeksploitasi endpoint API yang rentan terhadap Broken Object Level Authorization (BOLA) / IDOR (Insecure Direct Object Reference) dengan memanipulasi ID objek yang dikirimkan dalam request. ID Objek dapat berupa apa saja, mulai dari bilangan bulat berurutan, UUID, atau string. Akses tidak sah terhadap objek pengguna lain dapat mengakibatkan pengungkapan data kepada pihak yang tidak berwenang, kehilangan data, atau manipulasi data

## Challenge 1 - Access details of another user’s vehicle
- Buka tool Burp Suite lalu tekan tombol **Refresh Location** pada halaman dashboard

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%201.JPG)

- Pada tool Burp Suite akan terdeteksi endpoint API yang memuat informasi kendaraan berdasarkan ID kendaraan

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%202.JPG)

- Klik menu **Community** untuk membuka halaman Community

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%203.JPG)

- Pada halaman Community ditemukan endpoint API yang memuat ID kendaraan user lain

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%204.JPG)

- Sekarang kita kirim request endpoint API yang memuat informasi kendaraan berdasarkan ID kendaraan ke tab Repeater

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%205.JPG)

- Lalu ganti ID kendaraan dengan ID kendaraan yang ditemukan di halaman Community lalu tekan tombol **Send** maka kita berhasil mendapatkan informasi kendaraan dari pengguna lain

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%206.JPG)

## Challenge 2 - Access mechanic reports of other users
- Kembali ke halaman dashboard, tekan tombol **Contact Mechanic**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%207.JPG)

- Hidupkan Intercept pada Burp Suite

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%208.JPG)

- Isi form lalu tekan tombol **Send Service Requests**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%209.JPG)

- Setelah Burp Suite terbuka, klik kanan lalu pilih **Do intercept > Response to this request**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%2010.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%2011.JPG)

- Selanjutnya tekan tombol **Forward**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%2012.JPG)

- Jika mendapatkan response berikut, klik kanan lalu pilih **Send to Repeater**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%2013.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%2014.JPG)

- Pindah ke tab Repeater dan tekan tombol **Send**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%2015.JPG)

- Ubah request `POST` menjadi `GET` dan ubah endpoint API ke `/workshop/api/mechanic/mechanic_report?report_id=?` untuk mengakses detail report

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%2016.JPG)

- Jika sudah tekan tombol **Send** maka kita berhasil mengakses detail report yang sudah kita kirim sebelumnya

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%2017.JPG)

- Dari sini terlihat bahwa parameter `report_id` menggunakan bilangan bulat, sehingga memungkinkan kita mengubahnya dengan bilangan bulat lain seperti angka 1, 2, dan 3 untuk mengakses report yang dikirim oleh pengguna lain

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%2018.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%2019.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20object%20level%20authorization/bola%2020.JPG)