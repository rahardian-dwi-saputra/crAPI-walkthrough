# NoSQL Injection
Serangan NoSQL Injection dapat dijalankan di area aplikasi yang berbeda dibandingkan SQL Injection biasa. Jika SQL Injection akan dijalankan di dalam mesin basis data, varian NoSQL dapat dijalankan di dalam lapisan aplikasi atau lapisan basis data, tergantung API NoSQL yang digunakan dan model data. Biasanya serangan NoSQL Injection akan dijalankan ketika string serangan diurai, dievaluasi, atau digabungkan menjadi panggilan API NoSQL.

## Challenge 12 - Find a way to get free coupons without knowing the coupon code.
- Nyalakan tool Burp Suite dan pergi ke halaman **Shop**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/no%20sql%20injection/nosqli%201.JPG)

- Klik tombol **Add Coupuns** lalu masukkan kode kupon apapun dan tekan tombol **Validate**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/no%20sql%20injection/nosqli%202.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/no%20sql%20injection/nosqli%203.JPG)

- Pada tool Burp Suite akan terdeteksi endpoint API `/community/api/v2/coupon/validate-coupon` yang digunakan untuk validasi kode kupon

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/no%20sql%20injection/nosqli%204.JPG)

- Klik kanan request tersebut lalu pilih **Send to Repeater**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/no%20sql%20injection/nosqli%205.JPG)

- Pada referensi https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/NoSQL%20Injection payload NoSQL Injection adalah not equal ($ne). Jadi kita akan gunakan payload `{ "$ne": 1 }`. Pergi ke tab Repeater, ubah nilai parameter `coupon_code` menjadi `{ "$ne": 1 }` lalu klik tombol **Send**. Setelah request berhasil terkirim kita berhasil mendapatkan kode kupon yang valid dari sistem yaitu `TRAC075` yang berjumlah `75` 

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/no%20sql%20injection/nosqli%206.JPG)