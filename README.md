# crAPI Walkthrough
crAPI akan membantu Anda memahami 10 risiko keamanan API yang paling kritis. crAPI memang dirancang rentan, namun Anda dapat menjalankannya dengan aman untuk mendidik/melatih diri Anda sendiri.
- Link: https://github.com/OWASP/crAPI

## Instalasi di Ubuntu
- Sebelum menginstall crAPI, kita perlu terlebih dahulu menginstall docker
```sh
sudo apt install -y docker.io
```

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/1.JPG)

- Install docker-compose
```sh
sudo apt install docker-compose
```

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/2.JPG)

- Jalankan service docker
```sh
sudo systemctl enable docker --now
```

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/3.JPG)

- Download file `docker-compose.yml` untuk crAPI
```sh
curl -o docker-compose.yml https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/docker-compose.yml
```

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/4.JPG)

- Pull docker image
```sh
sudo docker-compose pull
```

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/5.JPG)

- Buka file `docker-compose.yml` menggunakan editor kemudian ubah IP `127.0.0.1` menjadi `0.0.0.0` pada baris berikut agar website dan mailhog bisa diakses dari mesin lain

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/6.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/7.JPG)

- Develop crAPI
```sh
sudo docker-compose -f docker-compose.yml --compatibility up -d
```

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/8.JPG)

- Akses web crAPI di mesin kali linux dengan URL `http://IP_Server:8888` di browser

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/9.JPG)

- Akses mailhog di mesin kali linux dengan tab yang berbeda di browser dengan URL `http://IP_Server:8025`

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/10.JPG)

- Buat akun baru dengan menekan link **Sign Up** untuk mengakses web crAPI

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/11.JPG)

- Jika sudah tekan tombol **Signup** lalu tekan tombol **OK**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/12.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/13.JPG)

- Sekarang login dengan akun baru yang sudah dibuat

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/14.JPG)

- Setelah berhasil login tekan tombol **+ Add a Vehicle** dan kita akan diminta untuk memasukkan PIN Code dan PIN

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/15.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/16.JPG)

- PIN Code dan PIN akan secara otomatis dikirim ke mailhog, buka mailhog maka akan terdapat email baru disana yang berisi PIN Code dan PIN

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/17.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/18.JPG)

- Masukkan PIN Code dan PIN tersebut ke halaman web crAPI, setelah itu tekan tombol **Verify Vehicle Details**. Jika berhasil akan keluar detail data kendaraan dan proses instalasi selesai

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/19.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/instalasi/20.JPG)

## Lesson
- [Broken Object Level Authorization](Broken%20Object%20Level%20Authorization.md)

## Disclaimer
Semua materi yang disajikan disini hanya digunakan sebagai media pembelajaran. Penulis tidak bertanggung jawab atas penyalahgunaan dari materi tersebut