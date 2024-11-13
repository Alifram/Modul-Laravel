---
sidebar_position: 1
---

# 8.1 Model 


**Model** dalam Laravel adalah representasi dari tabel dalam database. Model berfungsi untuk berinteraksi dengan database, mengambil, menyimpan, memperbarui, dan menghapus data. Model menggunakan ORM (Object-Relational Mapping) Eloquent untuk mengelola data dengan cara yang lebih intuitif dan efisien.

**Contoh Pembuatan Model:**

Gunakan perintah Artisan untuk membuat model:

```
php artisan make:model User
```

Model yang dihasilkan (`User.php`):

```
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class User extends Model {
    // Tentukan atribut yang boleh diisi
    protected $fillable = ['name', 'email', 'password'];
}
``` 

**Contoh Penggunaan Model:**

```
use App\Models\User;

// Mengambil semua pengguna
$users = User::all();

// Mengambil pengguna dengan id tertentu
$user = User::find(1);

// Membuat pengguna baru
User::create([
    'name' => 'John Doe',
    'email' => 'john@example.com',
    'password' => bcrypt('password'),
]);

// Memperbarui pengguna
$user->update(['name' => 'Jane Doe']);

// Menghapus pengguna
$user->delete();
```
