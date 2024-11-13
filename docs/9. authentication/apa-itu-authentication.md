---
sidebar_position: 1
---

# 9.1 Apa itu Authentication ?

**Authentication (autentikasi)** adalah proses verifikasi identitas pengguna untuk memastikan bahwa mereka adalah pihak yang berhak mengakses sistem atau layanan. Dalam konteks aplikasi web, autentikasi memastikan bahwa hanya pengguna yang memiliki kredensial (seperti username dan password) yang benar dapat mengakses fitur atau data tertentu.

Di Laravel, autentikasi adalah salah satu fitur penting yang biasanya digunakan untuk mengamankan aplikasi dengan memastikan bahwa hanya pengguna terdaftar dan terotorisasi yang dapat mengakses halaman atau data tertentu.

### Jenis-jenis Authentication

1.  **Authentication Berbasis Password**  
    Pengguna diminta memasukkan username/email dan password untuk mengakses aplikasi.
    
2.  **Authentication Berbasis Token**  
    Menggunakan token seperti **JWT (JSON Web Token)**, di mana token ini dikirim bersama setiap request untuk memverifikasi identitas.
    
3.  **Authentication Dua Faktor (2FA)**  
    Selain username dan password, pengguna harus memasukkan kode verifikasi yang dikirim melalui SMS, email, atau aplikasi otentikasi.
    
4.  **Social Authentication**  
    Pengguna dapat masuk menggunakan akun sosial seperti Google, Facebook, atau GitHub.

### Cara Kerja Authentication di Laravel

1.  **Login**: Pengguna memasukkan kredensial seperti email dan password.
2.  **Verifikasi**: Aplikasi memeriksa apakah email dan password sesuai dengan data di database.
3.  **Session/Token**: Jika valid, server menyimpan informasi pengguna dalam **session** atau memberikan **token**.
4.  **Akses Lanjutan**: Pada setiap request berikutnya, session/token digunakan untuk memverifikasi akses pengguna.

### Implementasi Authentication 

#### 1. Instalasi Authentication Bawaan Laravel
```
composer require laravel/ui
php artisan ui bootstrap --auth
npm install && npm run dev
```
Perintah di atas akan menghasilkan **view** untuk login, register, dan dashboard, serta rute autentikasi otomatis.

#### 2. Contoh Rute Authentication

Setelah menjalankan perintah di atas, Laravel akan membuat rute bawaan seperti:
```
Route::get('login', [LoginController::class, 'showLoginForm'])->name('login');
Route::post('login', [LoginController::class, 'login']);
Route::post('logout', [LoginController::class, 'logout'])->name('logout');
```

#### 3. Middleware Authentication

Laravel menggunakan middleware untuk melindungi rute agar hanya pengguna yang telah terotentikasi yang dapat mengakses.

Contoh Middleware:
```
Route::middleware('auth')->group(function () {
    Route::get('/dashboard', function () {
        return view('dashboard');
    });
});
```

#### 4. Custom Guard atau Token-Based Authentication (JWT)

Untuk aplikasi API, Kamu bisa menggunakan JWT sebagai metode autentikasi.

### Kesimpulan

Authentication adalah proses penting dalam aplikasi web untuk memastikan bahwa hanya pengguna yang berhak yang dapat mengakses fitur dan data tertentu. Laravel memudahkan penerapan autentikasi dengan menyediakan alat bawaan untuk login, register, dan middleware. Selain autentikasi berbasis session, Laravel juga mendukung autentikasi token seperti JWT untuk API, serta integrasi dengan layanan autentikasi sosial.