---
sidebar_position: 2
---

# 1.2 Instalasi

### 1. Instalasi web server

- Link unduh XAMPP

[Instal XAMPP](https://www.apachefriends.org/download.html)

**![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeFCAOgw5PHdp76MALwq9SM2L6zOUx8qKUKt9qtoNaHlEMaYrfOo_kqJGJSf0TM2TQvXuZXJw4EMKhmj1YB5v7LW3SXuuTYvTNde1GpVZx6UhVKtz_1U5W6_d4PEbI8xOtglxhTXfnjvnDmrlsmxekExvPV?key=d3s-vJLBsYtwvRvGfZhdnw)**
- Link unduh Laragon

[Instal Laragon](https://laragon.org/download.html)

**![](https://lh7-us.googleusercontent.com/docsz/AD_4nXepmK1fQWAvGUwLl6ZRCrs1sbnmjAbm_O7odTnySL0bXg-5cn8jm8pdeCSTH-_C-CuyPJdrz_uZrlqFvaySZSoj_kZRf2ljWSzRk4EqaYC5YQ_wYo0Sx6qUc6n0zcsUboGSsDOb4Qi2yGOhlcVeUY9n5uWD?key=d3s-vJLBsYtwvRvGfZhdnw)**

### 2. Instalasi Composer

- Link unduh Composer

[Instal Composer](https://getcomposer.org/download/)

Untuk memastikan jika composer sudah terpasang atau belum silakan buka
terminal/command prompt (windows + r) lalu ketikkan perintah composer -v jika tidak
ada error maka terminal akan memberikan jawaban seperti berikut

**![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfV8SQisGLVhpEz_Eu6iPKfQR0UVUqsPoRCcnVtdESfYWQxdV59yj5dBQqQTJ07yvTDBp38vCCMGN6dJ8jWwOPNJiwMG9RoI885_W-GvK7vjqe27EAZrK5IzvgnbWUVzXPGH3R8Q-j_4TYdIco8RcVvfZ_Q?key=d3s-vJLBsYtwvRvGfZhdnw)**

### 3. Instal Laravel


#### Langkah-langkah Instalasi

1.  **Menginstal Laravel melalui Composer**
    
    Buka terminal Anda dan jalankan perintah berikut untuk mengunduh dan menginstal Laravel:
   
    ```
    composer create-project laravel/laravel nama-proyek-anda
    ``` 
    
    Perintah ini akan mengunduh dan menginstal Laravel ke dalam folder `nama-proyek-anda`.
    
2.  **Konfigurasi Environment**
    
    Setelah instalasi selesai, masuk ke direktori proyek Laravel yang baru:

    ```
    cd nama-proyek-anda
    ```
    
    Laravel menggunakan file `.env` untuk mengkonfigurasi environment aplikasi. Salin file `.env.example` ke `.env`:
    
    
    ```
    cp .env.example .env
    ``` 
    
    Buka file `.env` dan atur konfigurasi yang diperlukan, seperti pengaturan database:
    
    ```
    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=nama_database
    DB_USERNAME=nama_pengguna
    DB_PASSWORD=katasandi
    ```
    
3.  **Generate Application Key**
    
    Laravel memerlukan application key untuk enkripsi data. Generate application key dengan perintah berikut:
    ```
    php artisan key:generate
    ```
    
    Perintah ini akan memperbarui file `.env` dengan application key yang baru.
    
4.  **Menjalankan Server Development**
    
    Laravel memiliki server development built-in yang dapat Anda gunakan untuk menjalankan aplikasi:
    ```
    php artisan serve
    ```
    
    Setelah menjalankan perintah ini, Anda dapat mengakses aplikasi Laravel Anda di `http://localhost:8000`.
    

#### Instalasi Menggunakan Laravel Installer (Opsional)

Anda juga bisa menginstal Laravel menggunakan Laravel Installer, yang memungkinkan Anda untuk menginstal Laravel dengan lebih cepat.

1.  **Instal Laravel Installer**
    
    Jalankan perintah berikut untuk menginstal Laravel Installer secara global:
    
    ```
    composer global require laravel/installer
    ```
    
2.  **Menggunakan Laravel Installer**
    
    Setelah Laravel Installer terinstal, Anda dapat membuat proyek Laravel baru dengan perintah:
    
    ```
    laravel new nama-proyek-anda
    ``` 
    
    Proyek baru akan dibuat dan Anda dapat langsung masuk ke direktori proyek dan menjalankan server development:
    
    ```
    cd nama-proyek-anda
    php artisan serve
    ```
    Jika sudah mengetik **php artisan serve** pada terminal

    **![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdRixaE2_peX_RHy3dNvJQs-uYh4FmX507dm1Mv-H9CXUpXqFhZ-eqKzeI_UIZuGBHXDcXaNleht7AWTfEStDIqwWj_0sntfhu0qoCEXaj_RlXPn0jjOBB6SMk8k2mVYAO7TK8iIUrlym6TvLWuzZxDL9Ad?key=d3s-vJLBsYtwvRvGfZhdnw)**

    Setelah kita membuka url tersebut, tampilan yang akan muncul adalah sebagai berikut :
    **![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeq1AhiCHqFn6e6hxGD--vCtyUBvKGFUNtrN8CXm5vM6GEfcPc0jf_rBLWRd2riPEDPpGNzln-UKt30o9djN4gCsMG9biic7Tvjicbg6YWmf04Y0eS8KqTGI9OMvweHRWSyAqCpLDU-pTjD2M4XCs3gysYZ?key=d3s-vJLBsYtwvRvGfZhdnw)**
    

### Kesimpulan

Instalasi Laravel melibatkan penggunaan Composer untuk mengunduh dan menginstal framework, mengonfigurasi environment dengan file `.env`, dan menjalankan server development bawaan Laravel. Alternatifnya, Anda bisa menggunakan Laravel Installer untuk proses instalasi yang lebih cepat. Setelah instalasi, Anda siap untuk mulai mengembangkan aplikasi web menggunakan Laravel.