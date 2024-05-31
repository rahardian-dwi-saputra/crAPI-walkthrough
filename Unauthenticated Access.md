# Unauthenticated Access
Akses tanpa autentikasi mengacu pada pemberian izin kepada pengguna untuk berinteraksi dengan sistem atau aplikasi tanpa mengharuskan mereka melakukan authentikasi atau login terlebih dahulu sehingga dapat melakukan tindakan apapun tanpa memberikan kredensial.

## Challenge 14 - Find an endpoint that does not perform authentication checks for a user.
- Nyalakan tool Burp Suite dan pergi ke halaman **Shop** kemudian beli salah satu item

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/unauthenticated%20access/ua%201.JPG)

- Setelah itu klik tombol **Order Details**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/unauthenticated%20access/ua%202.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/unauthenticated%20access/ua%203.JPG)

- Pada tool Burp Suite terdeteksi endpoint `/workshop/api/shop/orders/` dengan tipe request `GET` yang berisi detail pemesanan dan pembayaran

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/unauthenticated%20access/ua%204.JPG)

- Klik kanan request tersebut dan pilih **Send to Repeater**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/unauthenticated%20access/ua%205.JPG)

- Pindah ke tab Repeater dan klik tombol **Send**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/unauthenticated%20access/ua%206.JPG)

- Sekarang kita coba hapus header autentikasi

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/unauthenticated%20access/ua%207.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/unauthenticated%20access/ua%208.JPG)

- Jika sudah tekan tombol **Send**. Setelah request berhasil terkirim kita masih bisa mengakses data pesanan

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/unauthenticated%20access/ua%209.JPG)
