---
sidebar_position: 1
---

# 10.1 Apa Itu Filament? ?


**Filament** adalah paket Laravel berbasis PHP yang digunakan untuk membangun antarmuka (interface) administrasi dengan cepat dan mudah dalam aplikasi Laravel. Filament menyediakan berbagai komponen dan fitur siap pakai, seperti manajemen data, pembuatan tabel, form input, serta integrasi dengan model Eloquent, yang sangat membantu pengembang untuk membangun panel admin tanpa perlu menulis banyak kode dari awal.

### Fitur Utama Filament

1.  **Manajemen Data CRUD**  
    Filament menyediakan komponen untuk operasi CRUD (Create, Read, Update, Delete) yang memungkinkan pengembang untuk membuat, mengedit, menghapus, dan menampilkan data dengan antarmuka yang intuitif.
    
2.  **Pembuat Formulir dan Validasi**  
    Komponen form di Filament memudahkan pembuatan form yang terhubung langsung dengan model Eloquent, lengkap dengan opsi validasi.
    
3.  **Pembuatan Tabel Otomatis**  
    Filament menyediakan komponen tabel yang dapat disesuaikan, mendukung fitur seperti pencarian, penyortiran, dan paginasi, sehingga sangat memudahkan dalam menampilkan data.
    
4.  **Desain Responsif**  
    Tampilan antarmuka yang dihasilkan oleh Filament modern dan responsif, dapat diakses dengan baik di perangkat desktop maupun mobile.
    
5.  **Relasi Eloquent**  
    Filament mendukung relasi antar model Eloquent seperti one-to-many dan many-to-many, sehingga Anda bisa mengelola data yang memiliki relasi dengan lebih mudah.
    
6.  **Keamanan dan Autentikasi**  
    Filament mendukung integrasi dengan fitur autentikasi Laravel untuk melindungi akses ke panel administrasi, memastikan hanya pengguna tertentu yang bisa mengakses data penting.
    

### Cara Instalasi Filament

1.  **Menambahkan Paket Filament ke dalam Proyek Laravel**
    
    ```
    composer require filament/filament
    ```
    
2.  **Menjalankan Perintah untuk Menyiapkan Admin Panel** Setelah instalasi, Anda dapat membuat admin panel yang terhubung dengan model. 
    ```
    php artisan make:filament-user
    ```
    
3.  **Mengakses Admin Panel** Setelah konfigurasi, admin panel Filament dapat diakses melalui URL seperti `yourapp.com/admin`.
    

### Contoh Implementasi CRUD dengan Filament

**Menambahkan Resource (Misalnya untuk Model `Product`):**
```
php artisan make:filament-resource Product
``` 

Perintah ini akan menghasilkan resource untuk model `Product`, lengkap dengan form, tabel, dan controller yang dapat disesuaikan sesuai kebutuhan aplikasi.


### Kesimpulan

Filament adalah solusi cepat dan mudah untuk membangun admin panel dalam aplikasi Laravel. Dengan berbagai komponen seperti form, tabel, dan validasi otomatis, Filament menghemat waktu pengembangan dan menghasilkan tampilan yang profesional serta responsif, membuatnya ideal untuk aplikasi yang memerlukan manajemen data internal yang rapi dan efisien.