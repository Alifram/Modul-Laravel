---
sidebar_position: 1
---

# 2.1 Apa itu Routing ?

Routing adalah proses menentukan bagaimana aplikasi web merespons permintaan dari klien ke URL tertentu. Dalam konteks framework seperti Laravel, routing berfungsi sebagai penghubung antara URL permintaan dan kode yang akan dijalankan untuk menangani permintaan tersebut. Ini termasuk menentukan tindakan apa yang harus diambil oleh aplikasi ketika pengguna mengunjungi URL tertentu.


#### Fungsi Utama Routing

1.  **Menangani Permintaan HTTP**: Routing mengarahkan permintaan HTTP (GET, POST, PUT, DELETE, dll.) ke fungsi atau metode tertentu di dalam aplikasi Anda.
2.  **Mengelola URL**: Dengan routing, Anda dapat mendefinisikan pola URL yang kompleks dan menentukan bagaimana aplikasi Anda harus merespons pola-pola tersebut.
3.  **Menyederhanakan Kode**: Routing membantu menyederhanakan kode aplikasi Anda dengan memisahkan logika aplikasi dan pengelolaan URL.
4.  **Memfasilitasi Pengembangan RESTful**: Routing memungkinkan pengembangan aplikasi RESTful dengan mudah dengan menyediakan cara untuk menangani berbagai jenis permintaan HTTP pada endpoint yang sama.

#### Contoh Sederhana

Misalnya, jika Anda memiliki aplikasi yang menampilkan informasi pengguna, Anda dapat mendefinisikan rute untuk URL seperti `/user/1` yang akan menampilkan informasi untuk pengguna dengan ID 1.

```
`// routes/web.php

use Illuminate\Support\Facades\Route;

Route::get('/user/{id}', function ($id) {
    return "User ID: " . $id;
});` 
```
#### Komponen Utama Routing di Laravel

1.  **Method**: Jenis permintaan HTTP yang akan ditangani (GET, POST, PUT, DELETE, dll.).
2.  **URI**: Alamat atau endpoint yang akan dituju oleh permintaan.
3.  **Action**: Fungsi atau metode controller yang akan menangani permintaan.

`Route::get('/about', function () {
    return view('about');
});` 

Dalam contoh di atas:

-   **Method**: `GET`
-   **URI**: `/about`
-   **Action**: Menampilkan tampilan `about`.

#### Routing ke Controller

Laravel memungkinkan Anda untuk mengarahkan rute ke metode dalam controller untuk mengelola logika bisnis yang lebih kompleks.
```
use App\Http\Controllers\UserController;

Route::get('/user/{id}', [UserController::class, 'show']);
```
Di sini, permintaan `GET` ke `/user/{id}` akan diteruskan ke metode `show` dalam `UserController`.

#### Route Groups

Laravel memungkinkan pengelompokan rute untuk mengaplikasikan atribut bersama seperti middleware atau prefix.


```
use App\Http\Controllers\OrderController;
 
Route::resource('orders', OrderController::class);
```
#### Kesimpulan

Routing adalah komponen penting dalam pengembangan aplikasi web dengan Laravel. Dengan memahami dan memanfaatkan routing, Anda dapat mengelola alur kerja aplikasi Anda dengan lebih efektif, menciptakan struktur URL yang bersih dan logis, serta menyederhanakan pengelolaan permintaan HTTP yang masuk.