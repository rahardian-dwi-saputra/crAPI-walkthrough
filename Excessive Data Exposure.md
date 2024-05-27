# Excessive Data Exposure
Terkadang developer API tidak memikirkan sensitivitas data yang diekspos. Alat otomatis biasanya tidak dapat mendeteksi kerentanan jenis ini karena sulit membedakan antara data sah yang dikembalikan oleh API dan data sensitif yang tidak boleh dikembalikan tanpa pemahaman mendalam tentang aplikasinya. Insecure endpoint API tidak memerlukan autentikasi apa pun untuk mengakses data sehingga penyerang dapat mengakses data pengguna lain atau data resmi

## Challenge 4 - Find an API endpoint that leaks sensitive information of other users
- Hidupkan tool Burp Suite dan pergi ke halaman **Community**


- Pada tool Burp Suite terdeteksi bahwa halaman tersebut melakukan request ke endpoint API `/community/api/v2/community/posts/recent` yang response nya memuat data sensitif dari masing-masing user yang tampil di halaman **Community**


## Challenge 5 - Find an API endpoint that leaks an internal property of a video
- Klik foto profil untuk pergi ke halaman `/my-profile` lalu klik tanda titik tiga dan pilih Upload Video untuk mengunggah video


- Setelah berhasil mengunggah video ke halaman profil, pada tool Burp Suite terdeteksi endpoint API `/identity/api/v2/user/videos` yang mana endpoint memberikan respon berupa id dan data video yang seharusnya tidak ditampilkan ke user 
