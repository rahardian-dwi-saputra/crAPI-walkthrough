# Rate Limiting
Beberapa permintaan bersamaan dapat dilakukan dari satu komputer lokal atau dengan menggunakan sumber daya komputasi awan. Beberapa API tidak menerapkan pembatasan akses. Mengingat bahwa tidak ada pembatasan akses, maka serangan brute force menjadi pilihan yang sangat tepat. Disisi lain eksploitasi pada celah keamanan ini dapat menyebabkan DoS, membuat API tidak responsif atau bahkan tidak tersedia dengan mengirim spam ke API dengan ratusan atau ribuan permintaan per detik

## Challenge 6 - Perform a layer 7 DoS using ‘contact mechanic’ feature
- Pergi ke halaman Dashboard dan klik tombol **Contact Mechanic**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/rate%20limiting/limiting%201.JPG)

- Buka tool Burp Suite dan nyalakan intercept

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/rate%20limiting/limiting%202.JPG)

- Isi form dan klik tombol **Send Service Request**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/rate%20limiting/limiting%203.JPG)

- Setelah Burp Suite terbuka, klik kanan dan pilih Do intercept > Response to this request

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/rate%20limiting/limiting%204.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/rate%20limiting/limiting%205.JPG)

- Kemudian klik tombol Forward

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/rate%20limiting/limiting%206.JPG)

- Jika menemukan response sebagai berikut, klik kanan dan pilih Send to Repeater

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/rate%20limiting/limiting%207.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/rate%20limiting/limiting%208.JPG)

- Pindah ke tab Repeater dan klik tombol **Send**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/rate%20limiting/limiting%209.JPG)

- Pada request diatas terdapat parameter `repeat_request_if_failed` yang bernilai `false` yang artinya request tidak akan diulang jika pengiriman gagal dan parameter `number_of_repeats` yang bernilai `1` yang artinya hanya diulang 1 kali. Sekarang kita coba ubah nilai paramaeter `repeat_request_if_failed` menjadi `true` yang berarti jika request gagal akan diulang dan parameter `number_of_repeats` menjadi `10000` yang berarti request akan diulang `10000` kali

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/rate%20limiting/limiting%2010.JPG)

- Jika sudah diubah klik tombol **Send** maka akan terdeteksi aktivitas DoS

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/rate%20limiting/limiting%2011.JPG)