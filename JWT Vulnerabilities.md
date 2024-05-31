# JWT Vulnerabilities
JSON Web Token (JWT) adalah token JSON yang ditandatangani secara kriptografis, yang dimaksudkan untuk berbagi klaim antar sistem. Token ini sering digunakan sebagai token autentikasi atau sesi, khususnya pada REST API. Karena digunakan untuk autentikasi, kerentanan dapat dengan mudah mengakibatkan aplikasi dikompromikan sepenuhnya.

## Challenge 15 - Find a way to forge valid JWT Tokens
- Nyalakan tool Burp Suite dan pergi ke halaman **Dashboard**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%201.JPG)

- Pada tool Burp Suite terdeteksi endpoint `/identity/api/v2/user/dashboard` yang mengakses data user

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%202.JPG)

- Klik kanan request tersebut dan pilih **Send to Repeater**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%203.JPG)

- Pindah ke tab Repeater, block JWT Token lalu klik kanan dan pilih **Copy**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%204.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%205.JPG)

- Pindah ke tab Decoder dan paste JWT Token di field yang sudah disediakan. Perlu diketahui bahwa format JWT Token adalah `Header.Payload.Signature`

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%206.JPG)

- Block header token JWT lalu pilih Decode as Base64

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%207.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%208.JPG)

- Ubah `alg` dari `RS256` menjadi `none` kemudian block dan pilih Encode as Base64

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%209.JPG)

- Hapus bagian signature pada JWT Token kemudian block seluruh JWT Token baru. Tekan `Ctrl+C` untuk mencopy

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%2010.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%2011.JPG)

- Kembali ke tab Repeater, ubah JWT Token pada bagian autorisasi dengan JWT Token yang sudah dimodifikasi

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%2012.JPG)

- Jika sudah tekan tombol **Send**. Setelah request terkirim kita berhasil ter authentikasi meskipun kita menghilangkan signature pada JWT Token

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/jwt%20vulnerabilities/jwt%2013.JPG)
