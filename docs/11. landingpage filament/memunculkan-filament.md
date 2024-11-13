---
sidebar_position: 1
---

# 11.1 Bagaimana Cara Agar Data yang Dibuat Pake Filament Muncul di Landing Page ?

Filament adalah paket Laravel yang sangat membantu dalam membuat antarmuka administrasi secara cepat dan mudah. Namun, terkadang kita ingin data yang dibuat melalui Filament ini juga muncul di halaman publik seperti landing page. Berikut adalah **cara untuk menampilkan data dari Filament di halaman landing page** Laravel kamu.

### Langkah-Langkah Menampilkan Data dari Filament ke Landing Page

1.  **Pastikan Data Telah Dibuat di Filament**  
    Pastikan bahwa data yang kamu buat di Filament, misalnya untuk model `Course` atau `Product`, sudah ada dan tersimpan dalam database. Filament memudahkan kita dalam membuat data melalui antarmuka CRUD yang lengkap.
2.  **Membuat Route untuk Landing Page**  
    Di file `routes/web.php`, buat route untuk landing page kamu yang akan menampilkan data dari model yang telah kamu buat melalui Filament. Contoh:

    ```
    Route::get('/', [LandingController::class, 'index'])->name('landing');
    ```

3.  **Menambahkan Logic di Controller**  
    Di `LandingController.php`, buat method `index` untuk mengambil data dari model dan mengirimkannya ke view landing page:

    ```
    namespace App\Http\Controllers;

    use App\Models\Course; // Atau model lainnya sesuai data yang ingin ditampilkan
    use Illuminate\Http\Request;

    class LandingController extends Controller
    {
        public function index()
        {
            $courses = Course::where('is_published', true)->get(); // Hanya menampilkan data yang diterbitkan
            return view('landing', compact('courses'));
        }
    }
    ```

4.  **Membuat Tampilan di Blade View**  
    Di dalam file `resources/views/landing.blade.php`, gunakan kode berikut untuk menampilkan data `courses` yang sudah dikirim dari controller:

    ```
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Landing Page</title>
    </head>
    <body>
        <h1>Daftar Kursus</h1>
        <div class="course-list">
            @foreach($courses as $course)
                <div class="course-item">
                    <h2>{{ $course->title }}</h2>
                    <p>{{ $course->description }}</p>
                    <span>Harga: Rp{{ number_format($course->price, 0, ',', '.') }}</span>
                </div>
            @endforeach
        </div>
    </body>
    </html>
    ```

5.  **Menyaring Data Berdasarkan Status Publikasi**  
    Dalam contoh ini, kita menggunakan kondisi `is_published` untuk memastikan hanya data yang sudah diterbitkan yang muncul di landing page. Pastikan kamu telah menambahkan atribut `is_published` atau kolom serupa di model yang sesuai.

### Contoh Implementasi Menampilkan Data dengan Filament

Jika kita ingin membuat sebuah `resource` di Filament untuk model `Course`, misalnya, kita bisa menggunakan perintah berikut di terminal:

```
php artisan make:filament-resource Course
```

Perintah ini akan menghasilkan resource lengkap dengan form, tabel, dan controller untuk mengelola model `Course` di panel admin Filament.

### Kesimpulan

Dengan mengikuti langkah-langkah di atas, kamu dapat membuat data melalui Filament dan menampilkannya di landing page Laravel. Pendekatan ini memanfaatkan fungsi CRUD dari Filament untuk membuat data dengan mudah, sekaligus memungkinkan data yang dibuat muncul di halaman publik, seperti landing page. Filament memudahkan proses administrasi data, sementara integrasi dengan controller dan Blade view Laravel menjadikannya fleksibel untuk menampilkan data di berbagai bagian aplikasi.
