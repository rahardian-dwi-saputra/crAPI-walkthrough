# Excessive Data Exposure
Terkadang developer API tidak memikirkan sensitivitas data yang diekspos. Alat otomatis biasanya tidak dapat mendeteksi kerentanan jenis ini karena sulit membedakan antara data sah yang dikembalikan oleh API dan data sensitif yang tidak boleh dikembalikan tanpa pemahaman mendalam tentang aplikasinya. Insecure endpoint API tidak memerlukan autentikasi apa pun untuk mengakses data sehingga penyerang dapat mengakses data pengguna lain atau data resmi

## Challenge 4 - Find an API endpoint that leaks sensitive information of other users
- Hidupkan tool Burp Suite dan pergi ke halaman **Community**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/excessive%20data%20exposure/exposure%201.JPG)

- Pada tool Burp Suite terdeteksi bahwa halaman tersebut melakukan request ke endpoint API `/community/api/v2/community/posts/recent` yang response nya memuat data sensitif dari masing-masing user yang tampil di halaman **Community**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/excessive%20data%20exposure/exposure%202.JPG)

## Challenge 5 - Find an API endpoint that leaks an internal property of a video
- Klik foto profil untuk pergi ke halaman `/my-profile` lalu klik tanda titik tiga dan pilih Upload Video untuk mengunggah video

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/excessive%20data%20exposure/exposure%203.JPG)

- Setelah berhasil mengunggah video ke halaman profil, pada tool Burp Suite terdeteksi endpoint API `/identity/api/v2/user/videos` yang mana endpoint memberikan respon berupa id dan data video yang seharusnya tidak ditampilkan ke user 

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/excessive%20data%20exposure/exposure%204.JPG)