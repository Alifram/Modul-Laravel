---
sidebar_position: 1
---

# 6.1 Apa itu Blade Templates ?

Blade Templates adalah sistem templating yang digunakan oleh framework Laravel untuk memudahkan pembuatan dan pengelolaan tampilan (view) dalam aplikasi web. Blade memungkinkan pengguna untuk menggunakan logika PHP dalam template dengan sintaks yang lebih bersih dan mudah dibaca. Berikut adalah beberapa fitur dan contoh sintaks dari Blade Templates:

### 1. Inheritance

Blade mendukung pewarisan template, memungkinkan pengguna untuk membuat layout utama dan mewariskan tampilan yang berbeda dari layout tersebut.

Contoh:

#### Layout Utama (layouts/master.blade.php)

```
<!DOCTYPE html>
<html>
<head>
		<title> App Name - @yield('title')</title>
</head>
<body>
		<div class="container">
				@yield('content')
		</div>
</body>
</html>
```

2. Echoing Data
Blade menyediakan cara yang aman untuk menampilkan data dengan menggunakan kurung kurawal ganda `{{  }}`.

Contoh:

```
<h1>{{ $name }}</h1>
```

Untuk menampilkan data tanpa escaped, gunakan kurung kurawal tripel `{{ !! !! }}`.

Contoh:
```
<h1>{!! $htmlContent !!}</h1>
```


3. Control Structures
Blade mendukung berbagai struktur kontrol seperti `if, for, foreach, dan while.`

Contoh:
```
If-Else
@if ($user)
    Welcome, {{ $user->name }}.
@else
    Welcome, Guest.
@endif

For Loop
@for ($i = 0; $i < 10; $i++)
    <p>This is iteration {{ $i }}</p>
@endfor

Foreach Loop
@foreach ($users as $user)
    <p>This is user {{ $user->name }}</p>
@endforeach
```

4. Including Sub-Views
Blade memungkinkan penyertaan sub-view dalam view utama dengan menggunakan direktif `@include.`

Contoh:
```
@include('shared.header')

<div class="content">
    @yield('content')
</div>

@include('shared.footer')
```

5. Displaying Data and Raw PHP
Blade juga mendukung penyisipan kode PHP langsung dalam template.

Contoh:
```
<p>The current UNIX timestamp is {{ time() }}.</p>

@php
    $counter = 1;
@endphp

<p>Counter: {{ $counter }}</p>
```

6. Blade Components and Slots
Blade mendukung pembuatan komponen yang dapat digunakan kembali dengan slot.

Contoh:

Membuat Komponen `(resources/views/components/alert.blade.php)`
```
<div class="alert alert-{{ $type }}">
    {{ $slot }}
</div>
```

Menggunakan Komponen `(welcome.blade.php)`
```
<x-alert type="error">
    <strong>Whoops!</strong> Something went wrong!
</x-alert>
```

Blade Templates sangat membantu dalam menyusun dan mengelola tampilan dengan lebih terstruktur dan efisien. Dengan berbagai fitur yang ditawarkan, pengembangan aplikasi web dengan Laravel menjadi lebih mudah dan terorganisir.
