# JWT Vulnerabilities
JSON Web Token (JWT) adalah token JSON yang ditandatangani secara kriptografis, yang dimaksudkan untuk berbagi klaim antar sistem. Token ini sering digunakan sebagai token autentikasi atau sesi, khususnya pada REST API. Karena digunakan untuk autentikasi, kerentanan dapat dengan mudah mengakibatkan aplikasi dikompromikan sepenuhnya.

## Challenge 15 - Find a way to forge valid JWT Tokens
- Nyalakan tool Burp Suite dan pergi ke halaman **Dashboard**

- Pada tool Burp Suite terdeteksi endpoint `/identity/api/v2/user/dashboard` yang mengakses data user

- Klik kanan request tersebut dan pilih **Send to Repeater**

- Pindah ke tab Repeater, block JWT Token lalu klik kanan dan pilih **Copy**


- Pindah ke tab Decoder dan paste JWT Token di field yang sudah disediakan. Perlu diketahui bahwa format JWT Token adalah `Header.Payload.Signature`

- Block header token JWT lalu pilih Decode as Base64

- Ubah `alg` dari `RS256` menjadi `none` kemudian block dan pilih Encode as Base64

- Hapus bagian signature pada JWT Token kemudian block seluruh JWT Token baru. Tekan `Ctrl+C` untuk mencopy

- Kembali ke tab Repeater, ubah JWT Token pada bagian autorisasi dengan JWT Token yang sudah dimodifikasi

- Jika sudah tekan tombol **Send**. Setelah request terkirim kita berhasil ter authentikasi meskipun kita menghilangkan signature pada JWT Token


