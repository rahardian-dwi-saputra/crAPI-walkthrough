# Server-Side Request Forgery (SSRF)
Kelemahan SSRF terjadi setiap kali aplikasi web mengambil sumber daya jarak jauh tanpa memvalidasi URL yang diberikan pengguna. Aplikasi target mungkin memiliki fungsi untuk mengimpor data dari URL, menerbitkan data ke URL, atau membaca data dari URL yang dapat dirusak. Hal ini memungkinkan penyerang memaksa aplikasi untuk mengirim permintaan yang dibuat ke tujuan yang tidak terduga, bahkan ketika dilindungi oleh firewall, VPN, atau jenis daftar kontrol akses jaringan (ACL) lainnya.

## Challenge 11 - Make crAPI send an HTTP call to "www.google.com" and return the HTTP response.
- Kembali ke halaman dashboard, tekan tombol **Contact Mechanic**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/server%20side%20request%20forgery/ssrf%201.JPG)

- Hidupkan Intercept pada Burp Suite

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/server%20side%20request%20forgery/ssrf%202.JPG)

- Isi form lalu tekan tombol **Send Service Requests**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/server%20side%20request%20forgery/ssrf%203.JPG)

- Setelah Burp Suite terbuka, klik kanan lalu pilih **Do intercept > Response to this request**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/server%20side%20request%20forgery/ssrf%204.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/server%20side%20request%20forgery/ssrf%205.JPG)

- Selanjutnya tekan tombol **Forward**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/server%20side%20request%20forgery/ssrf%206.JPG)

- Jika mendapatkan response berikut, klik kanan lalu pilih **Send to Repeater**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/server%20side%20request%20forgery/ssrf%207.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/server%20side%20request%20forgery/ssrf%208.JPG)

- Pindah ke tab Repeater dan tekan tombol **Send**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/server%20side%20request%20forgery/ssrf%209.JPG)

- Ubah nilai parameter `mechanic_api` menjadi `https://www.google.com` lalu tekan tombol **Send**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/server%20side%20request%20forgery/ssrf%2010.JPG)