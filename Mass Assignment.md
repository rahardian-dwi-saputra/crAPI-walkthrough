# Mass Assignment
Framework terkadang memungkinkan developer untuk mengikat parameter request HTTP ke dalam variabel atau objek secara otomatis untuk membuat penggunaan framework tersebut mudah digunakan. Hal ini terkadang dapat menimbulkan kerugian. Penyerang terkadang dapat menggunakan metodologi ini untuk membuat parameter baru yang tidak pernah dimaksudkan oleh developer yang pada gilirannya membuat atau menimpa variabel baru dalam kode program yang tidak dimaksudkan.

## Challenge 8 - Get an item for free
- Nyalakan tool Burp Suite dan pergi ke halaman **Shop** dan beli salah satu item

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%201.JPG)

- Pada tool Burp Suite terdeteksi endpoint `/workshop/api/shop/orders` dengan tipe request `POST` yang digunakan untuk melakukan pemesanan

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%202.JPG)

- Selain itu pada tool Burp Suite terdeteksi endpoint `/workshop/api/shop/orders/all` dengan tipe request `GET` yang menampilkan detail data pesanan

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%203.JPG)

- Sekarang kita tekan tombol **Order Details**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%204.JPG)

- Pada tool Burp Suite terdeteksi endpoint `/workshop/api/shop/orders/` dengan tipe request `GET` yang berisi detail pemesanan dan pembayaran

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%205.JPG)

- Klik kanan request tersebut dan pilih **Send to Repeater**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%206.JPG)

- Pindah ke tab Repeater dan klik tombol **Send**, pada response terdapat informasi bahwa endpoint ini mendukung jenis request `GET, POST, PUT, HEAD, OPTIONS`

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%207.JPG)

- Disini status pemesanan adalah `delivered` jadi kita akan ubah statusnya menjadi `return` agar saldo kita kembali. Ubah tipe request dari `GET` menjadi `PUT` dan tambahkan parameter `status` dengan nilai `return` kemudian tekan tombol **Send**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%208.JPG)

- Dari hasil diatas status `return` tidak tersedia, status yang tersedia hanya `delivered`,`return pending` dan `returned`. Jadi kita ubah saja valuenya menjadi `returned`

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%209.JPG)

- Sekarang kita kembali ke halaman **Shop** dan saldo kita tetap seperti semula

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2010.JPG)

## Challenge 9 - Increase your balance by $1,000 or more
- Lakukan pembelian lagi dan ulangi langkah diatas hingga mengirimkan endpoint `/workshop/api/shop/orders/` ke tab Repaeter. Sekarang kita cukup menggunakan tipe request `PUT` untuk mengubah data pesanan, menambahkan parameter `status` dengan nilai `returned` agar saldo kita direfund sebanyak total pesanan dan menambahkan parameter `quantity` dengan nilai `100` sehingga saldo kita akan direfund sebanyak `100` kali lipat kemudian tekan tombol **Send**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2011.JPG)

- Sekarang kita kembali ke halaman **Shop** maka saldo kita bertambah dari `90` menjadi `1090`

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2012.JPG)

## Challenge 10 - Update internal video properties
- Nyalakan tool Burp Suite dan klik foto profil untuk menuju halaman profil

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2013.JPG)

- Jika My Personal Video anda terhapus di Challenge 7 (BFLA). Anda bisa mengunggah lagi dengan klik tanda titik tiga lalu pilih Upload Video

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2014.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2015.JPG)

- Klik tanda titik tiga lagi dan pilih **Change Video Name**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2016.JPG)

- Ubah judul video sesuai dengan yang anda mau

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2017.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2018.JPG)

- Pada Burp Suite akan terdeteksi endpoint `/identity/api/v2/user/videos/id` yang digunakan untuk mengedit video

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2019.JPG)

- Klik kanan request tersebut dan pilih Send to Repeater

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2020.JPG)

- Pindah ke tab Repeater dan klik tombol **Send**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2021.JPG)

- Disini kita bisa menambahkan parameter `conversion_params` dengan nilai `-v codec h2` lalu klik tombol **Send**. Setelah request terkirim kita berhasil mengubah nilai `conversion_params`

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/mass%20assignment/mass%2022.JPG)