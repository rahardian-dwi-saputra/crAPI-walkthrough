# Server-Side Request Forgery (SSRF)
Kelemahan SSRF terjadi setiap kali aplikasi web mengambil sumber daya jarak jauh tanpa memvalidasi URL yang diberikan pengguna. Aplikasi target mungkin memiliki fungsi untuk mengimpor data dari URL, menerbitkan data ke URL, atau membaca data dari URL yang dapat dirusak. Hal ini memungkinkan penyerang memaksa aplikasi untuk mengirim permintaan yang dibuat ke tujuan yang tidak terduga, bahkan ketika dilindungi oleh firewall, VPN, atau jenis daftar kontrol akses jaringan (ACL) lainnya.

## Challenge 11 - Make crAPI send an HTTP call to "www.google.com" and return the HTTP response.
- Kembali ke halaman dashboard, tekan tombol **Contact Mechanic**

- Hidupkan Intercept pada Burp Suite

- Isi form lalu tekan tombol **Send Service Requests**

- Setelah Burp Suite terbuka, klik kanan lalu pilih **Do intercept > Response to this request**

- Selanjutnya tekan tombol **Forward**

- Jika mendapatkan response berikut, klik kanan lalu pilih **Send to Repeater**

- Pindah ke tab Repeater dan tekan tombol **Send**

- Ubah nilai parameter `mechanic_api` menjadi `https://www.google.com` lalu tekan tombol **Send**