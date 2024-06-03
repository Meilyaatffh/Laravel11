## Laravel11
***
<details>
<summary> Installation and Configuration </summary>

  
### Installation


  Untuk menginstall laravel 11, minimal versi PHP yang digunakan adalah 8.2
  anda bisa update PHP ke versi terbaru di php.net/download. Selanjutnya pindahkan versi PHP di laragon menjadi yang terbaru.
  Setelah selesai melakukan update, langkah selanjutnya adalah masuk ke terminal, kemudian jalankan perintah berikut untuk membuat   
  project laravel baru :
  ```
  composer create-project laravel/laravel laravel11
  ```
  Perintah diatas digunakan untuk membuat project laravel dengan nama laravel11. Setelah itu klik enter dan tunggu sampai proses             
  installasinya selesai.
 
  ```
  cd laravel11
  ```
  perintah diatas digunakan untuk masuk ke dalam folder project yang sudah dibuat yaitu laravel11. Setelah berhasil masuk kemudian jalankan    dengan perintah :
  ```
  php artisan serve
  ```
Jika berhasil maka akan muncul tampilan seperti dibawah ini, kemudian tekan ctrl+click untuk membuka di browser
![Screenshot 2024-06-02 223427](https://github.com/Meilyaatffh/Laravel11/assets/134565192/a1900294-ffe0-4cbe-866f-ae4e21f2677a)

### Configuration


</details>

<details>
<summary> Directory Structure and Frontend </summary>
  
### Directory Structure
  
#### The Root Directory
1. The App Directory : Untuk menyimpan kode utama dari aplikasi yang sudah dibuat
2. The Bootstrap Directory : Didalamnya terdapat file app.php yang melakukan bootstrap atau menarik aplikasi dalam framework
3. The Config Directory : Berisi semua file konfigurasi aplikasi Anda
4. The Database Directory : Direktori database berisi migrasi database Anda,
5. The Public Directory : Untuk menyimpan file file yang dapat diakses secara public. Contohnya gambar, javascript, dan css
6. The Resources Directory : Direktori resources berisi aset mentah yang belum dikompilasi seperti CSS atau JavaScript.
7. The Routes Directory : Folder dimana menyimpan file file yang bertugas melakukan rute atau penjaluran dari aplikasi kita
8. The Storage Directory : Direktori ini berisi file-file yang dihasilkan oleh aplikasi, seperti file log, file cache, dan file yang diunggah oleh pengguna.
9. The Tests Directory : Folder untuk menyimpan file file yang ada hubungannya dengan testing aplikasi kita
10. The Vendor Directory : Tempat untuk menyimpan package package yang diinstal lewat komposer

### Frontend
  
</details>

<details>
<summary> Routing </summary>
  
### Routing
Routing adalah fitur inti dari framework Laravel yang bertanggung jawab untuk mengelola lalu lintas permintaan (request) dan pengiriman respons (response) di aplikasi web. Setiap kali pengguna mengakses URL tertentu, routing menentukan bagaimana permintaan tersebut ditangani oleh aplikasi. 
Berikut contoh rute dasar yang sering digunakan dalam aplikasi Laravel :
```
Route::get('/', function () {
    return view('home');
});
```
Rute ini mengarahkan permintaan GET ke URL root (/) ke tampilan home. Jadi, ketika pengguna mengakses http://yourdomain.com/, mereka akan melihat halaman home.blade.php

## Menggunakan Resource Controller
Laravel menyediakan cara mudah untuk mendefinisikan rute yang sesuai dengan pola CRUD (Create, Read, Update, Delete) melalui resource controller. Resource controller menyederhanakan definisi rute dan menghubungkannya ke metode controller yang sesuai.
```
use App\Http\Controllers\MahasiswaController;

Route::resource('mahasiswa', MahasiswaController::class);
```

</details>


<details>
<summary> Middleware </summary>
  
### Middleware
Middleware adalah fitur penting dalam framework Laravel yang bertindak sebagai lapisan perantara antara permintaan HTTP yang masuk dan respons yang dikirim ke pengguna. Middleware memungkinkan untuk memeriksa dan memfilter permintaan sebelum mencapai controller.
Untuk membuat middleware baru, gunakan make:middleware perintahnya :
```
php artisan make:middleware EnsureTokenIsValid
```
Perintah ini akan menempatkan EnsureTokenIsValid kelas baru di dalam direktori Anda app/Http/Middleware

### Logika dalam Metode Handle:
```
if ($request->input('token') !== 'my-secret-token') {
    return redirect('home');
}

return $next($request);
```
- if ($request->input('token') !== 'my-secret-token'): Memeriksa apakah parameter token dalam permintaan tidak sama dengan nilai 'my-secret-token'.
- !==: Operator ketidaksamaan yang digunakan untuk memeriksa apakah dua nilai tidak sama.
- return redirect('home');: Jika token tidak valid, middleware akan mengarahkan (redirect) pengguna ke halaman 'home'.
- return $next($request);: Jika token valid, middleware akan melanjutkan permintaan ke middleware berikutnya atau ke controller yang menangani permintaan tersebut.

  ```
  use App\Http\Middleware\EnsureTokenIsValid;
 
->withMiddleware(function (Middleware $middleware) {
     $middleware->append(EnsureTokenIsValid::class);
})
```
Kode yang Anda berikan menunjukkan bagaimana cara menambahkan middleware EnsureTokenIsValid ke dalam aplikasi Laravel menggunakan metode withMiddleware
penjelasan kode

Impor Kelas Middleware
```
use App\Http\Middleware\EnsureTokenIsValid;
```
- Mengimpor kelas EnsureTokenIsValid yang didefinisikan di namespace App\Http\Middleware.

Metode withMiddleware:
```
->withMiddleware(function (Middleware $middleware) {
     $middleware->append(EnsureTokenIsValid::class);
})
```

- withMiddleware: Metode ini digunakan untuk menambahkan middleware ke dalam konteks tertentu, misalnya rute atau grup rute.
- function (Middleware $middleware) { ... }: Fungsi anonim yang menerima instance Middleware.
- $middleware->append(EnsureTokenIsValid::class);: Menambahkan EnsureTokenIsValid ke daftar middleware yang akan diproses.

</details>


<details>
<summary> Controllers dan Views </summary>
Controllers dan Views adalah dua komponen penting dalam pola arsitektur MVC (Model-View-Controller) yang digunakan oleh Laravel. Controllers bertanggung jawab untuk menangani logika aplikasi dan berinteraksi dengan model, sedangkan Views bertanggung jawab untuk menampilkan data kepada pengguna.
  
### Controllers
Controllers adalah kelas PHP yang digunakan untuk mengelompokkan logika penanganan permintaan HTTP terkait. Mereka membantu dalam memisahkan logika aplikasi dari logika tampilan.
Perintah untuk membuat controller :
```
php artisan make:controller MahasiswaController --resource
```

### Views
Views bertanggung jawab untuk menampilkan data yang diberikan oleh controller. Dalam Laravel, views adalah file Blade yang berada di direktori resources/views.



</details>


<details>
<summary> Blade Templates </summary>
  
### Blade Templates

Blade adalah template engine yang disertakan dengan Laravel dan memungkinkan Anda menggunakan kode PHP dengan sintaks yang bersih dan mudah dipahami.

- File Ekstensi: File Blade menggunakan ekstensi .blade.php.
- Lokasi: File template biasanya ditempatkan dalam direktori resources/views.

Anda bisa menampilkan variabel dengan sintaks kurung kurawal ganda :
```
Hello, {{ $name }}.
```



</details>


<details>
<summary> Migrations </summary>
  
### Migrations
Konsep Migration pada Laravel adalah sebuah mekanisme yang memudahkan pengelolaan struktur database dalam pengembangan aplikasi.
Perintah untuk membuat migrations :
```
php artisan make:migration create_mahasiswa_table
```
Perintah untuk menjalankan migrations :
```
php artisan migrate
```



</details>


<details>
<summary> Query Builder </summary>
  
### Query Builder
Query Builder adalah fitur dalam Laravel yang memungkinkan Anda untuk membuat kueri SQL menggunakan sintaks PHP. Ini memberikan cara yang lebih intuitif dan terstruktur untuk berinteraksi dengan database Anda.


</details>


<details>
<summary> Eloquent ORM </summary>
  
### Eloquent ORM
loquent ORM adalah ORM (Object-Relational Mapping) yang disertakan dengan Laravel. Ini menyediakan cara yang mudah dan intuitif untuk berinteraksi dengan database menggunakan model PHP. Dengan Eloquent, Anda dapat melakukan berbagai operasi database seperti membuat, membaca, memperbarui, dan menghapus data dengan mudah dan efisien. 
Untuk menggunakan Eloquent ORM, perlu membuat model yang mewakili tabel dalam database. Model-model ini biasanya ditempatkan di dalam direktori app/Models. 
Untuk membuat model baru, dapat menggunakan perintah Artisan:
```
php artisan make:model mahasiswa
```

</details>
