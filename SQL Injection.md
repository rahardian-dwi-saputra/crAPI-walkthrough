# SQL Injection
Serangan SQL Injection adalah jenis serangan injeksi, di mana perintah SQL dimasukkan ke dalam input data untuk memengaruhi eksekusi perintah SQL yang telah ditentukan sebelumnya. Serangan SQL Injection yang berhasil dapat membaca data sensitif dari database, memodifikasi data database, atau menjalankan operasi administrasi pada database. Secara umum, cara aplikasi web membuat query SQL adalah dengan melibatkan sintaks SQL yang ditulis oleh programmer dicampur dengan data yang disediakan oleh pengguna. 

## Challenge 13 - Find a way to redeem a coupon that you have already claimed by modifying the database
- Di Challenge 12 (No SQL Injection) kita berhasil mendapatkan kode kupon. Sekarang nyalakan tool Burp Suite dan pergi ke halaman **Shop**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/sql%20injection/sqli%201.JPG)

- Masukkan kode kupon yang telah didapat dari challenge sebelumnya dan tekan tombol **Validate**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/sql%20injection/sqli%202.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/sql%20injection/sqli%203.JPG)

- Pada tool Burp Suite akan terdeteksi endpoint `/workshop/api/shop/apply_coupon` untuk mengaplikasikan kode kupon

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/sql%20injection/sqli%204.JPG)

- Klik kanan request tersebut lalu pilih **Send to Repeater**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/sql%20injection/sqli%205.JPG)

- Pindah ke tab Repeater

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/sql%20injection/sqli%206.JPG)

- Sekarang kita coba mengganti parameter `coupon_code` dengan nilai `1'` lalu klik tombol **Send** maka muncul pesan bahwa server mengalami error

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/sql%20injection/sqli%207.JPG)

- Kita bisa mencoba mengubah nilai parameter `coupon_code` dengan salah satu payload SQL Injection seperti `1' or '1'='1` lalu klik tombol **Send** maka muncul pesan bahwa kode kupon sudah diklaim yang menandakan bahwa query bernilai `true` meskipun kita tidak memasukkan kode kupon yang valid

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/sql%20injection/sqli%208.JPG)

- Sekarang kita ubah nilai parameter `coupon_code` dengan nilai `1'; select version() --+` lalu tekan tombol **Send**. Setelah request berhasil terkirim kita berhasil mendapatkan informasi database yang digunakan

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/sql%20injection/sqli%209.JPG)