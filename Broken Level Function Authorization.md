# Broken Function Level Authorization
Penyerang mengirimkan permintaan ke endpoint API yang seharusnya tidak boleh diakses oleh pengguna biasa atau yang tidak memiliki kewenangan. Menerapkan metode pemeriksaan yang tepat dapat bisa menjadi tugas yang membingungkan karena aplikasi modern dapat berisi banyak jenis peran, grup, dan hirarki pengguna yang kompleks (misalnya sub-pengguna, atau pengguna dengan lebih dari satu peran). Fungsi administratif adalah target utama untuk jenis serangan ini dan dapat menyebabkan pengungkapan data, kehilangan data, atau kerusakan data. Pada akhirnya, hal ini dapat menyebabkan gangguan layanan.

## Challenge 7 - Delete a video of another user
- Nyalakan tool Burp Suite dan klik foto profil untuk menuju halaman profil

- Scroll ke bawah, pada bagian My Personal Video klik tanda titik tiga dan pilih **Change Video Name**

- Ubah judul video sesuai keinginan anda lalu tekan tombol **Change Video Name**

- Pada Burp Suite akan terdeteksi endpoint `/identity/api/v2/user/videos/id` yang digunakan untuk mengedit video

- klik kanan request tersebut dan pilih Send to Repeater

- Pindah ke tab Repeater

- Disini kita bisa mengubah jenis request `PUT` menjadi `OPTINS` untuk mengetahui jenis request apa saja yang bisa dilakukan di endpoint tersebut. Setelah itu klik tombol **Send**

- Endpoint tersebut ternyata mengizinkan operasi `DELETE`, jadi sekarang kita ubah tipe request `OPTINS` menjadi `DELETE` dan klik tombol **Send**


- Muncul pesan bahwa kita harus mengakses endpoint user admin untuk bisa melakukan operasi `DELETE`. Jadi kita perlu mengubah endpoint API dari `/identity/api/v2/user/videos/` menjadi `/identity/api/v2/admin/videos/` lalu klik tombol **Send** maka video di profil kita berhasil dihapus

- Karena id nya adalah bilangan bulat, kita bisa menghapus personal video dari user lain hanya dengan mengurutkan id nya ke belakang atau ke depan. Disini kita berhasil menghapus video dengan id `20`