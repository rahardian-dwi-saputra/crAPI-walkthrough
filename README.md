# crAPI Walkthrough
crAPI akan membantu Anda memahami 10 risiko keamanan API yang paling kritis. crAPI memang dirancang rentan, namun Anda dapat menjalankannya dengan aman untuk mendidik/melatih diri Anda sendiri.
- Link: https://github.com/OWASP/crAPI

## Instalasi di Ubuntu
- Sebelum menginstall crAPI, kita perlu terlebih dahulu menginstall docker
```sh
sudo apt install -y docker.io
```

- Install docker-compose
```sh
sudo apt install docker-compose
```

- Jalankan service docker
```sh
sudo systemctl enable docker --now
```

- Download file `docker-compose.yml` untuk crAPI
```sh
curl -o docker-compose.yml https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/docker-compose.yml
```

- Pull docker image
```sh
sudo docker-compose pull
```

- Buka file `docker-compose.yml` menggunakan editor kemudian ubah IP `127.0.0.1` menjadi `0.0.0.0` pada baris berikut agar website dan mailhog bisa diakses dari mesin lain


- Develop crAPI
```sh
sudo docker-compose -f docker-compose.yml --compatibility up -d
```

- Akses web crAPI di mesin kali linux dengan URL `http://IP_Server:8888` di browser

- Akses mailhog di mesin kali linux dengan tab yang berbeda di browser dengan URL `http://IP_Server:8025`


- Buat akun baru dengan menekan link **Sign Up** untuk mengakses web crAPI

- Jika sudah tekan tombol **Signup** lalu tekan tombol **OK**

- Sekarang login dengan akun baru yang sudah dibuat

- Setelah berhasil login tekan tombol **+ Add a Vehicle** dan kita akan diminta untuk memasukkan PIN Code dan PIN

- PIN Code dan PIN akan secara otomatis dikirim ke mailhog, buka mailhog maka akan terdapat email baru disana yang berisi PIN Code dan PIN

- Masukkan PIN Code dan PIN tersebut ke halaman web crAPI, setelah itu tekan tombol **Verify Vehicle Details**. Jika berhasil akan keluar detail data kendaraan dan proses instalasi selesai



## Lesson
- [Broken Object Level Authorization](Broken%20Object%20Level%20Authorization.md)

## Disclaimer
Semua materi yang disajikan disini hanya digunakan sebagai media pembelajaran. Penulis tidak bertanggung jawab atas penyalahgunaan dari materi tersebut