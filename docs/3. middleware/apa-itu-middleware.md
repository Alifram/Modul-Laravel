---
sidebar_position: 1
---

# 3.1 Apa itu Middleware ? 


Middleware  adalah lapisan perantara antara permintaan  _route HTTP_ yang masuk dan  _action_  dari  `Controller`  yang akan dijalankan.  Middleware  memungkinkan kita untuk meakukan berbagai tugas baik itu sebelum ataupun sesudah tindakan dilakukan. Kita juga dapat menggunakan  _tool_  CLI  untuk membuat sebuah  Middleware  dalam Laravel. Beberapa contoh penggunaan Middleware  meliputi autentikasi, validasi, manipulasi permintaan, dan lainnya.

```
php artisan make:middleware auth
```

#### Fungsi Utama Middleware

1.  **Otentikasi**: Memverifikasi apakah pengguna yang mengirimkan permintaan telah diotentikasi.
2.  **Otorisasi**: Memastikan pengguna memiliki izin untuk mengakses sumber daya tertentu.
3.  **Pengelolaan Cache**: Menyimpan atau mengambil tanggapan dari cache untuk meningkatkan performa.
4.  **Pemfilteran Konten**: Memodifikasi atau memfilter konten permintaan atau tanggapan.
5.  **Penanganan CORS (Cross-Origin Resource Sharing)**: Mengatur kebijakan CORS untuk mengizinkan atau menolak permintaan dari domain lain.
6.  **Logging dan Debugging**: Merekam log aktivitas atau kesalahan yang terjadi selama permintaan.


### Contoh Middleware di Laravel

#### Membuat Middleware

Misalkan Anda ingin membuat middleware untuk memeriksa apakah pengguna adalah admin. Anda bisa membuat middleware dengan menggunakan perintah Artisan berikut:
```
php artisan make:middleware CheckAdmin
```

Perintah ini akan membuat file `CheckAdmin.php` di direktori `app/Http/Middleware`.

#### Mengedit Middleware

Buka file `CheckAdmin.php` dan tambahkan logika untuk memeriksa apakah pengguna adalah admin.

```
namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;

class CheckAdmin {
    /**
     * Handle an incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Closure  $next
     * @return mixed
     */
    public function handle(Request $request, Closure $next) {
        if (! $request->user() || ! $request->user()->isAdmin()) {
            return redirect('home');
        }

        return $next($request);
    }
}
```

Di sini, middleware `CheckAdmin` memeriksa apakah pengguna saat ini adalah admin. Jika tidak, pengguna akan dialihkan ke halaman `home`.

#### Mendaftarkan Middleware

Untuk menggunakan middleware yang baru dibuat, Anda perlu mendaftarkannya di file `app/Http/Kernel.php`.

```
protected $routeMiddleware = [
    // Middleware lainnya...
    'admin' => \App\Http\Middleware\CheckAdmin::class,
];
```

#### Menggunakan Middleware pada Rute

Anda dapat menerapkan middleware pada rute atau grup rute tertentu.
```
Route::get('/admin', function () {
    // Hanya dapat diakses oleh admin
})->middleware('admin');
```


### Middleware Bawaan Laravel

Laravel menyediakan beberapa middleware bawaan yang bisa Anda gunakan:

1.  **`auth`**: Memverifikasi bahwa pengguna telah diotentikasi.
2.  **`guest`**: Memastikan pengguna adalah tamu (belum diotentikasi).
3.  **`throttle`**: Membatasi jumlah permintaan yang dapat dibuat ke rute tertentu untuk mencegah penyalahgunaan.
4.  **`verified`**: Memastikan pengguna telah memverifikasi alamat email mereka.

### Middleware Global dan Grup Middleware

-   **Middleware Global**: Middleware yang diterapkan pada semua permintaan HTTP.
-   **Grup Middleware**: Kumpulan middleware yang diterapkan pada kelompok rute tertentu.

**Middleware Global**:


```
protected $middleware = [
    // Middleware lainnya...
    \App\Http\Middleware\CheckForMaintenanceMode::class,
];
```

**Grup Middleware**:

```
`protected $middlewareGroups = [
    'web' => [
        \App\Http\Middleware\EncryptCookies::class,
        \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
        \Illuminate\Session\Middleware\StartSession::class,
        // Middleware lainnya...
    ],
    
    'api' => [
        'throttle:api',
        \Illuminate\Routing\Middleware\SubstituteBindings::class,
    ],
];
```


### Kesimpulan

Middleware adalah komponen penting dalam framework Laravel yang bertindak sebagai filter atau penghubung antara permintaan HTTP yang masuk dan respon yang keluar. Middleware memungkinkan Anda untuk memproses permintaan sebelum mencapai rute atau controller, serta memodifikasi respon sebelum dikirim kembali ke klien.

Fungsi utama middleware meliputi otentikasi (memeriksa apakah pengguna telah masuk), otorisasi (memastikan pengguna memiliki izin untuk mengakses sumber daya tertentu), logging dan debugging (merekam informasi untuk keperluan debugging atau audit), pengelolaan cache (meningkatkan performa dengan mengambil dan menyimpan respon di cache), pemfilteran konten (memodifikasi permintaan atau respon sesuai kebutuhan), dan penanganan CORS (mengatur kebijakan CORS untuk mengizinkan atau menolak permintaan dari domain lain).

Untuk mengimplementasikan middleware, Anda dapat membuat middleware baru dengan perintah Artisan, seperti `php artisan make:middleware CheckAdmin`. Setelah dibuat, middleware harus didaftarkan di file `app/Http/Kernel.php`. Kemudian, middleware dapat digunakan pada rute atau grup rute dengan metode `middleware`.

Laravel juga menyediakan middleware bawaan seperti `auth`, `guest`, `throttle`, dan `verified` yang memudahkan pengelolaan otentikasi, otorisasi, dan pengaturan permintaan. Middleware bisa diterapkan secara global pada semua permintaan HTTP atau pada kelompok rute tertentu untuk manajemen yang lebih terorganisir.

Dengan memahami dan memanfaatkan middleware, Anda dapat mengelola keamanan, performa, dan manipulasi data dalam aplikasi Laravel Anda dengan cara yang lebih efisien dan terstruktur.
