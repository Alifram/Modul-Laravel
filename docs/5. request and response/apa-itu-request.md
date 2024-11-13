---
sidebar_position: 1
---

# 5.1 Request


Request (permintaan) dalam Laravel adalah objek yang merepresentasikan semua informasi yang dikirimkan oleh klien ke server melalui HTTP. Informasi ini mencakup data formulir, input pengguna, parameter URL, file yang diunggah, dan header HTTP.

Laravel menyediakan berbagai cara untuk mengakses dan memproses data dari request. Dengan menggunakan objek request, Anda dapat mengambil data yang dikirimkan oleh pengguna dan menggunakannya dalam logika aplikasi Anda.

**Contoh Mengambil Data dari Request:**

```
namespace App\Http\Controllers;

use Illuminate\Http\Request;

class UserController extends Controller {
    public function store(Request $request) {
        // Mengambil data input 'name' dari request
        $name = $request->input('name');

        // Mengambil semua data input dari request
        $data = $request->all();

        // Mengambil file yang diunggah dari request
        $file = $request->file('profile_picture');

        // Proses lebih lanjut dengan data request...
    }
}
```