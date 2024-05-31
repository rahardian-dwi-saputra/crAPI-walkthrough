# Unauthenticated Access
Akses tanpa autentikasi mengacu pada pemberian izin kepada pengguna untuk berinteraksi dengan sistem atau aplikasi tanpa mengharuskan mereka melakukan authentikasi atau login terlebih dahulu sehingga dapat melakukan tindakan apapun tanpa memberikan kredensial.

## Challenge 14 - Find an endpoint that does not perform authentication checks for a user.
- Nyalakan tool Burp Suite dan pergi ke halaman **Shop** kemudian beli salah satu item

- Setelah itu klik tombol **Order Details**

- Pada tool Burp Suite terdeteksi endpoint `/workshop/api/shop/orders/` dengan tipe request `GET` yang berisi detail pemesanan dan pembayaran


- Klik kanan request tersebut dan pilih **Send to Repeater**


- Pindah ke tab Repeater dan klik tombol **Send**

- Sekarang kita coba hapus header autentikasi

- Jika sudah tekan tombol **Send**. Setelah request berhasil terkirim kita masih bisa mengakses data pesanan
