---
sidebar_position: 2
---

# 7.2 Error Handling (Penanganan Kesalahan)

Laravel memiliki sistem penanganan kesalahan yang kuat dan fleksibel. Penanganan kesalahan di Laravel bisa melibatkan beberapa hal, seperti logging kesalahan, memberikan respons yang tepat kepada pengguna, dan menangani pengecualian yang tidak tertangani.

1. **Handling Validation Errors:** Kesalahan validasi secara otomatis ditangani oleh Laravel dan akan mengembalikan respons ke halaman sebelumnya dengan pesan kesalahan.

```
public function store(Request $request)
{
    $validatedData = $request->validate([
        'title' => 'required|max:255',
        'body' => 'required',
    ]);

    // Jika validasi lolos, lanjutkan proses penyimpanan data
    Post::create($validatedData);

    return redirect()->route('posts.index');
}
```

Jika validasi gagal, Laravel akan mengarahkan kembali pengguna ke halaman sebelumnya dengan pesan kesalahan yang sesuai.

2. Global Error Handling: Laravel menangani semua pengecualian yang tidak tertangani dalam file app/Exceptions/Handler.php. Kita bisa menyesuaikan penanganan kesalahan global ini sesuai kebutuhan.

Di dalam `Handler.php`
```
public function render($request, Throwable $exception)
{
    if ($exception instanceof CustomException) {
        return response()->view('errors.custom', [], 500);
    }

    return parent::render($request, $exception);
}
```

3.Logging Errors: Laravel menggunakan Monolog untuk logging. Konfigurasi logging dapat diatur di file `config/logging.php.`

Contoh logging kesalahan
```
Log::error('Something went wrong!', ['error' => $exception->getMessage()]);
```

Contoh Kasus:

Misalkan kita memiliki sebuah aplikasi blogging yang memerlukan validasi untuk memastikan bahwa setiap postingan blog memiliki judul dan isi.



Membuat Controller dan Form Request:
- Membuat Controller

```
php artisan make:controller PostController
```

- Membuat Form Request
```
php artisan make:request StorePostRequest

```
2.Mengisi aturan validasi di `Form Request (StorePostRequest):`
```
namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;

class StorePostRequest extends FormRequest
{
    public function authorize()
    {
        return true;
    }

    public function rules()
    {
        return [
            'title' => 'required|max:255',
            'body' => 'required',
        ];
    }
}
```
3.Menggunakan `Form Request di Controller:`

```
namespace App\Http\Controllers;

use App\Http\Requests\StorePostRequest;
use App\Models\Post;

class PostController extends Controller
{
    public function store(StorePostRequest $request)
    {
        // Validasi dilakukan otomatis, lanjutkan proses penyimpanan data
        Post::create($request->validated());

        return redirect()->route('posts.index');
    }
}
```

4.Menangani Kesalahan Validasi:
Kesalahan validasi akan secara otomatis dikembalikan ke pengguna dengan pesan kesalahan yang relevan. Tidak perlu tambahan kode untuk ini karena Laravel menanganinya secara otomatis.


5.Custom Error Handling:
```
namespace App\Exceptions;

use Illuminate\Foundation\Exceptions\Handler as ExceptionHandler;
use Throwable;

class Handler extends ExceptionHandler
{
    public function render($request, Throwable $exception)
    {
        if ($exception instanceof CustomException) {
            return response()->view('errors.custom', [], 500);
        }

        return parent::render($request, $exception);
    }
}
```
Dengan menggunakan validasi dan penanganan kesalahan yang tepat, kita dapat memastikan bahwa aplikasi berjalan lancar dan pengguna mendapatkan informasi yang relevan ketika terjadi kesalahan.




