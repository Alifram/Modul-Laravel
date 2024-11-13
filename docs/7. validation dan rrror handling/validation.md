---
sidebar_position: 1
---

# 7.1 Validation (Validasi)


**Validation** dan **Error Handling** adalah dua aspek penting dalam pengembangan aplikasi menggunakan Laravel. Keduanya berfungsi untuk memastikan bahwa data yang diterima aplikasi sesuai dengan yang diharapkan dan mengelola kesalahan yang mungkin terjadi selama proses tersebut.

## Validation (Validasi)
Validasi dalam Laravel digunakan untuk memastikan bahwa data yang diterima oleh aplikasi memenuhi aturan tertentu sebelum diproses lebih lanjut. 

Laravel menyediakan beberapa cara untuk melakukan validasi:

**Menggunakan** validate **Method** pada Request: Metode ini digunakan langsung dalam controller untuk memvalidasi data request.

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

2. Menggunakan Form Request: Laravel juga memungkinkan kita untuk membuat kelas Form Request yang terpisah, yang dapat digunakan untuk memvalidasi data.

Membuat Form Request
```
php artisan make:request StorePostRequest
```
Di dalam StorePostRequest
```
public function rules()
{
    return [
        'title' => 'required|max:255',
        'body' => 'required',
    ];
}

// Di dalam Controller
public function store(StorePostRequest $request)
{
    // Validasi dilakukan otomatis, lanjutkan proses penyimpanan data
    Post::create($request->validated());

    return redirect()->route('posts.index');
}
```
