---
sidebar_position: 2
---

# 8.2 Migration



**Migration** dalam Laravel adalah cara untuk mengelola skema database. Migration memungkinkan pengembang untuk membuat, memodifikasi, dan menghapus tabel serta kolom dalam database dengan menggunakan kode PHP. Migration memberikan cara yang terstruktur dan dapat dikontrol versi untuk mengelola perubahan skema database.

**Contoh Pembuatan Migration:**

Gunakan perintah Artisan untuk membuat migration:

```
php artisan make:migration create_users_table
``` 

Migration yang dihasilkan (`xxxx_xx_xx_xxxxxx_create_users_table.php`):

```
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateUsersTable extends Migration {
    public function up() {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email')->unique();
            $table->string('password');
            $table->timestamps();
        });
    }

    public function down() {
        Schema::dropIfExists('users');
    }
}
```

**Menjalankan Migration:**
```
php artisan migrate
``` 

**Contoh Mengubah Tabel dengan Migration:**

Buat migration untuk menambah kolom baru:

```
php artisan make:migration add_bio_to_users_table
``` 

Migration yang dihasilkan (`xxxx_xx_xx_xxxxxx_add_bio_to_users_table.php`):

```
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class AddBioToUsersTable extends Migration {
    public function up() {
        Schema::table('users', function (Blueprint $table) {
            $table->text('bio')->nullable();
        });
    }

    public function down() {
        Schema::table('users', function (Blueprint $table) {
            $table->dropColumn('bio');
        });
    }
}
```

Jalankan migration untuk menambahkan kolom `bio` ke tabel `users`:


```
php artisan migrate
```

### Kesimpulan

Model dan Migration dalam Laravel adalah alat penting untuk mengelola data dan skema database. **Model** berfungsi sebagai representasi tabel dalam database dan menggunakan Eloquent ORM untuk interaksi data yang lebih intuitif. **Migration** menyediakan cara terstruktur dan dapat dikontrol versi untuk membuat, memodifikasi, dan menghapus tabel serta kolom dalam database. Dengan menggunakan kedua alat ini, pengembang dapat mengelola database dengan lebih efisien dan rapi.