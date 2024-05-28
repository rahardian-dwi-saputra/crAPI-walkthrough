# Broken Function Level Authorization
Penyerang mengirimkan permintaan ke endpoint API yang seharusnya tidak boleh diakses oleh pengguna biasa atau yang tidak memiliki kewenangan. Menerapkan metode pemeriksaan yang tepat dapat bisa menjadi tugas yang membingungkan karena aplikasi modern dapat berisi banyak jenis peran, grup, dan hirarki pengguna yang kompleks (misalnya sub-pengguna, atau pengguna dengan lebih dari satu peran). Fungsi administratif adalah target utama untuk jenis serangan ini dan dapat menyebabkan pengungkapan data, kehilangan data, atau kerusakan data. Pada akhirnya, hal ini dapat menyebabkan gangguan layanan.

## Challenge 7 - Delete a video of another user
- Nyalakan tool Burp Suite dan klik foto profil untuk menuju halaman profil

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20level%20function%20authorization/bfla%201.JPG)

- Scroll ke bawah, pada bagian My Personal Video klik tanda titik tiga dan pilih **Change Video Name**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20level%20function%20authorization/bfla%202.JPG)

- Ubah judul video sesuai keinginan anda lalu tekan tombol **Change Video Name**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20level%20function%20authorization/bfla%203.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20level%20function%20authorization/bfla%204.JPG)

- Pada Burp Suite akan terdeteksi endpoint `/identity/api/v2/user/videos/id` yang digunakan untuk mengedit video

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20level%20function%20authorization/bfla%205.JPG)

- klik kanan request tersebut dan pilih Send to Repeater

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20level%20function%20authorization/bfla%206.JPG)

- Pindah ke tab Repeater, disini kita bisa mengubah jenis request `PUT` menjadi `OPTINS` untuk mengetahui jenis request apa saja yang bisa dilakukan di endpoint tersebut. Setelah itu klik tombol **Send**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20level%20function%20authorization/bfla%207.JPG)

- Endpoint tersebut ternyata mengizinkan operasi `DELETE`, jadi sekarang kita ubah tipe request `OPTINS` menjadi `DELETE` dan klik tombol **Send**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20level%20function%20authorization/bfla%208.JPG)

- Muncul pesan bahwa kita harus mengakses endpoint user admin untuk bisa melakukan operasi `DELETE`. Jadi kita perlu mengubah endpoint API dari `/identity/api/v2/user/videos/` menjadi `/identity/api/v2/admin/videos/` lalu klik tombol **Send** maka video di profil kita berhasil dihapus

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20level%20function%20authorization/bfla%209.JPG)

- Karena id nya adalah bilangan bulat, kita bisa menghapus personal video dari user lain hanya dengan mengurutkan id nya ke belakang atau ke depan. Disini kita berhasil menghapus video dengan id `20`

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20level%20function%20authorization/bfla%2010.JPG)