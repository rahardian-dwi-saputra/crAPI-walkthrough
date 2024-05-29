# Mass Assignment
Framework terkadang memungkinkan developer untuk mengikat parameter request HTTP ke dalam variabel atau objek secara otomatis untuk membuat penggunaan framework tersebut mudah digunakan. Hal ini terkadang dapat menimbulkan kerugian. Penyerang terkadang dapat menggunakan metodologi ini untuk membuat parameter baru yang tidak pernah dimaksudkan oleh developer yang pada gilirannya membuat atau menimpa variabel baru dalam kode program yang tidak dimaksudkan.

## Challenge 8 - Get an item for free
- Nyalakan tool Burp Suite dan pergi ke halaman **Shop** dan beli salah satu item


- Pada tool Burp Suite terdeteksi endpoint `/workshop/api/shop/orders` dengan tipe request `POST` yang digunakan untuk melakukan pemesanan


- Selain itu pada tool Burp Suite terdeteksi endpoint `/workshop/api/shop/orders/all` dengan tipe request `GET` yang menampilkan detail data pesanan

- Sekarang kita tekan tombol **Order Details**

- Pada tool Burp Suite terdeteksi endpoint `/workshop/api/shop/orders/` dengan tipe request `GET` yang berisi detail pemesanan dan pembayaran

- Klik kanan request tersebut dan pilih **Send to Repeater**

- Pindah ke tab Repeater dan klik tombol **Send**, pada response terdapat informasi bahwa endpoint ini mendukung jenis request `GET, POST, PUT, HEAD, OPTIONS`

- Disini status pemesanan adalah `delivered` jadi kita akan ubah statusnya menjadi `return` agar saldo kita kembali. Ubah tipe request dari `GET` menjadi `PUT` dan tambahkan parameter `status` dengan nilai `return` kemudian tekan tombol **Send**

- Dari hasil diatas status `return` tidak tersedia, status yang tersedia hanya `delivered`,`return pending` dan `returned`. Jadi kita ubah saja valuenya menjadi `returned`

- Sekarang kita kembali ke halaman **Shop** dan saldo kita tetap seperti semula


## Challenge 9 - Increase your balance by $1,000 or more
- Ulangi langkah diatas hingga mengirimkan endpoint `/workshop/api/shop/orders/` ke tab Repaeter. Sekarang kita cukup menggunakan tipe request `PUT` untuk mengubah data pesanan, menambahkan parameter `status` dengan nilai `returned` agar saldo kita direfund sebanyak total pesanan dan menambahkan parameter `quantity` dengan nilai `100` sehingga saldo kita akan direfund sebanyak `100` kali lipat kemudian tekan tombol **Send**


- Sekarang kita kembali ke halaman **Shop** maka saldo kita bertambah dari `90` menjadi `1090`

## Challenge 10 - Update internal video properties
- Nyalakan tool Burp Suite dan klik foto profil untuk menuju halaman profil

- Jika My Personal Video anda terhapus di Challenge 7 (BFLA). Anda bisa mengunggah lagi dengan klik tanda titik tiga lalu pilih Upload Video

- Klik tanda titik tiga lagi dan pilih **Change Video Name**

- Pada Burp Suite akan terdeteksi endpoint `/identity/api/v2/user/videos/id` yang digunakan untuk mengedit video

- Klik kanan request tersebut dan pilih Send to Repeater

- Pindah ke tab Repeater dan klik tombol **Send**

- Disini kita bisa menambahkan parameter `conversion_params` dengan nilai `-v codec h2` lalu klik tombol **Send**. Setelah request terkirim kita berhasil mengubah nilai `conversion_params`