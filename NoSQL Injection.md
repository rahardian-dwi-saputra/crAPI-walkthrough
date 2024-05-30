# NoSQL Injection
Serangan NoSQL Injection dapat dijalankan di area aplikasi yang berbeda dibandingkan SQL Injection biasa. Jika SQL Injection akan dijalankan di dalam mesin basis data, varian NoSQL dapat dijalankan di dalam lapisan aplikasi atau lapisan basis data, tergantung API NoSQL yang digunakan dan model data. Biasanya serangan NoSQL Injection akan dijalankan ketika string serangan diurai, dievaluasi, atau digabungkan menjadi panggilan API NoSQL.

## Challenge 12 - Find a way to get free coupons without knowing the coupon code.
- Nyalakan tool Burp Suite dan pergi ke halaman **Shop**

- Klik tombol **Add Coupuns** lalu masukkan kode kupon apapun dan tekan tombol **Validate**

- Pada tool Burp Suite akan terdeteksi endpoint API `/community/api/v2/coupon/validate-coupon` yang digunakan untuk validasi kode kupon

- Klik kanan request tersebut lalu pilih **Send to Repeater**

- Pada referensi https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/NoSQL%20Injection payload NoSQL Injection adalah not equal ($ne). Jadi kita akan gunakan payload `{ "$ne": 1 }`. Pergi ke tab Repeater, ubah nilai parameter `coupon_code` menjadi `{ "$ne": 1 }` lalu klik tombol **Send**. Setelah request berhasil terkirim kita berhasil mendapatkan kode kupon yang valid dari sistem yaitu `TRAC075` yang berjumlah `75` 

