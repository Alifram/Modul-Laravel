---
sidebar_position: 1
---

# 4.1 Apa itu Controller ? 


### Apa itu Controller?

Controller adalah salah satu komponen inti dari MVC yang berfungsi sebagai penghubung antara request user (View) ke model yang nantinya akan di kembalikan lagi ke View dalam bentuk response. Controller ini akan banyak berisi logika – logika dalam menyusun suatu fungsi tertentu. Contohnya adalah aktivitas CRUD (Create, Read, Update, Delete) yang prosesnya berjalan di dalam Controller.

### Fungsi Utama Controller

1.  **Mengelompokkan Logika**: Mengelompokkan logika aplikasi yang terkait dengan permintaan tertentu.
2.  **Berinteraksi dengan Model**: Mengambil dan memanipulasi data dari database melalui model.
3.  **Mengembalikan View**: Mengembalikan view yang berisi data yang diambil dan diproses dari model.
4.  **Mengatur Alur Kerja**: Menyederhanakan pengaturan alur kerja aplikasi dengan mengelompokkan logika bisnis dan pemrosesan data.

### Membuat Controller

Anda dapat membuat controller menggunakan perintah Artisan berikut:
```
php artisan make:controller UserController
```

Ini akan membuat file controller baru di direktori `app/Http/Controllers`.

### Contoh Penggunaan Controller

Misalkan Anda memiliki `UserController` dengan beberapa metode untuk menangani berbagai permintaan terkait pengguna.

**Contoh `UserController`:**

```
namespace App\Http\Controllers;

use App\Models\User;
use Illuminate\Http\Request;

class UserController extends Controller {
    // Menampilkan daftar pengguna
    public function index() 
    {
        $users = User::all();
        return view('users.index', compact('users'));
    }

    // Menampilkan detail pengguna
    public function show($id) 
    {
        $user = User::findOrFail($id);
        return view('users.show', compact('user'));
    }

    // Menampilkan form untuk membuat pengguna baru
    public function create() 
    {
        return view('users.create');
    }

    // Menyimpan pengguna baru ke database
    public function store(Request $request) 
    {
        $request->validate([
            'name' => 'required',
            'email' => 'required|email|unique:users',
            'password' => 'required|min:8',
        ]);

        User::create($request->all());
        return redirect()->route('users.index')->with('success', 'User created successfully.');
    }

    // Menampilkan form untuk mengedit pengguna
    public function edit($id) 
    {
        $user = User::findOrFail($id);
        return view('users.edit', compact('user'));
    }

    // Memperbarui pengguna di database
    public function update(Request $request, $id) 
    {
        $request->validate([
            'name' => 'required',
            'email' => 'required|email|unique:users,email,' . $id,
            'password' => 'nullable|min:8',
        ]);

        $user = User::findOrFail($id);
        $user->update($request->all());
        return redirect()->route('users.index')->with('success', 'User updated successfully.');
    }

    // Menghapus pengguna dari database
    public function destroy($id) 
    {
        $user = User::findOrFail($id);
        $user->delete();
        return redirect()->route('users.index')->with('success', 'User deleted successfully.');
    }
}
```


### Mengaitkan Controller dengan Rute

Untuk menggunakan controller pada rute, Anda dapat mengaitkan rute ke metode controller dengan sintaks berikut:

```
use App\Http\Controllers\UserController;

Route::get('/users', [UserController::class, 'index'])->name('users.index');
Route::get('/users/create', [UserController::class, 'create'])->name('users.create');
Route::post('/users', [UserController::class, 'store'])->name('users.store');
Route::get('/users/{id}', [UserController::class, 'show'])->name('users.show');
Route::get('/users/{id}/edit', [UserController::class, 'edit'])->name('users.edit');
Route::put('/users/{id}', [UserController::class, 'update'])->name('users.update');
Route::delete('/users/{id}', [UserController::class, 'destroy'])->name('users.destroy');`
```

### Resource Controller

Laravel menyediakan cara yang lebih sederhana untuk menangani controller dengan banyak metode CRUD (Create, Read, Update, Delete) melalui resource controller. Anda dapat membuat resource controller dengan perintah berikut:
```
php artisan make:controller UserController --resource
```

Kemudian, Anda dapat mendefinisikan rute resource dengan satu baris kode:

```
Route::resource('users', UserController::class);
```

Ini secara otomatis akan membuat rute untuk semua tindakan CRUD yang biasa (index, create, store, show, edit, update, destroy).


### Kesimpulan

Controller di Laravel adalah kelas yang menangani logika aplikasi dan mengelompokkan rute terkait dalam satu tempat. Dengan menggunakan controller, Anda dapat mengatur kode Anda dengan lebih baik, membuatnya lebih mudah untuk dikelola dan dipelihara. Controller berinteraksi dengan model untuk mengelola data dan mengembalikan view untuk menampilkan data kepada pengguna.