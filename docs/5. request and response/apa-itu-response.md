---
sidebar_position: 2
---

# 5.2 Response


Response (respon) dalam Laravel adalah objek yang dikirimkan kembali oleh server kepada klien setelah memproses request. Respon ini bisa berupa halaman HTML, data JSON, file, atau bahkan redirect ke URL lain. Laravel menyediakan cara yang fleksibel dan mudah untuk membuat berbagai jenis respon.

**Contoh Membuat Berbagai Jenis Response:**

```
namespace App\Http\Controllers;

use Illuminate\Http\Request;

class UserController extends Controller {
    // Mengembalikan view sebagai respon
    public function show($id) {
        $user = User::findOrFail($id);
        return view('users.show', compact('user'));
    }

    // Mengembalikan data JSON sebagai respon
    public function getUserData($id) {
        $user = User::findOrFail($id);
        return response()->json($user);
    }

    // Redirect ke URL lain sebagai respon
    public function redirectToHome() {
        return redirect('/');
    }

    // Mengembalikan file sebagai respon
    public function downloadFile() {
        $pathToFile = storage_path('app/public/file.pdf');
        return response()->download($pathToFile);
    }
}
```