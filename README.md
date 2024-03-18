# Pemrograman Berbasis Framework <br>
Nama : Adhe Nur Wulandari <br>
Kelas : TI - 2D <br>
NIM : 220302073 <br>

## Codeigniter4 <br>
CodeIgniter adalah Kerangka Pengembangan Aplikasi - sebuah toolkit - untuk orang-orang yang membangun situs web menggunakan PHP.
Tujuannya adalah untuk memungkinkan Anda mengembangkan proyek jauh lebih cepat daripada jika Anda menulis kode dari awal, dengan menyediakan kumpulan perpustakaan yang kaya untuk tugas-tugas umum,
serta antarmuka sederhana dan struktur logis untuk mengakses perpustakaan ini.
CodeIgniter memungkinkan Anda fokus secara kreatif pada proyek Anda dengan meminimalkan jumlah kode yang dibutuhkan untuk tugas tertentu. <br>
### Basis Data yang Didukung <br>
=> MySQL melalui MySQLidriver (hanya versi 5.1 ke atas) <br>
=> PostgreSQL melalui Postgredriver (hanya versi 7.4 dan lebih tinggi)<br>
=> SQLite3 melalui SQLite3driver <br>
=> Microsoft SQL Server melalui SQLSRVdriver (hanya versi 2005 dan lebih tinggi) <br>
=> Oracle Database melalui OCI8driver (hanya versi 12.1 dan lebih tinggi) <br>

## 1. Installation <br>
   **Composer Installation** <br>
      Teknik pertama buka cmder pada web server, lalu ketikan seperti dibawah <br>
      ```
      $ composer create-project codeigniter4/appstarter project-root``` <br>
      project-root dapat diganti sesuai nama projek anda <br>
      contohnya : <br>
      ```
      $ composer create-project codeigniter4/appstarter ci4app``` <br>
      kemudian jalankan server <br>
      ```
      $ cd nama-root``` <br>
      atau contoh projek saya <br>
      ```
      $ cd ci4app``` <br>
      ```
      $ php spark serve 
      ``` <br>
      ![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/c26c3143-d774-4769-a95e-20dda8dcf034) <br>
      **Menjalankan aplikasi anda** <br>
      Server Pengembangan Lokal
    CodeIgniter 4 hadir dengan server pengembangan lokal, memanfaatkan server web bawaan PHP dengan routing CodeIgniter. Anda dapat meluncurkannya, 
    dengan baris perintah berikut di direktori utama: <br>
```php spark serve ``` <br>
Ini akan meluncurkan server dan sekarang Anda dapat melihat aplikasi Anda di browser Anda di http://localhost:8080 . <br>
![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/4090b6b1-d24f-4c9c-ade7-0009c871231a)  <br>
## 2. Bangun Aplikasi Pertama <br>
Tutorial ini dimaksudkan untuk memperkenalkan Anda pada framework CodeIgniter4 dan prinsip dasar arsitektur MVC. Ini akan menunjukkan kepada Anda bagaimana aplikasi dasar CodeIgniter dibangun secara langkah demi langkah.Jika Anda belum familiar dengan PHP, kami sarankan Anda membaca Tutorial PHP W3Schools sebelum melanjutkan.
Dalam tutorial ini, Anda akan membuat aplikasi berita dasar . Anda akan mulai dengan menulis kode yang dapat memuat halaman statis. Selanjutnya, Anda akan membuat bagian berita yang membaca item berita dari database. Terakhir, Anda akan menambahkan formulir untuk membuat item berita di database. <br>
Tutorial ini terutama akan fokus pada: <br>
- Dasar-dasar Model-View-Controller <br>
- Dasar-dasar perutean <br>
- Validasi formulir <br>
- Melakukan query database dasar menggunakan Model CodeIgniter <br>
**Halaman Statis**
  Buka file rute yang terletak di app/Config/Routes.php . Satu-satunya petunjuk rute untuk memulai adalah: <br>
```
<?php

use CodeIgniter\Router\RouteCollection;

/**
 * @var RouteCollection $routes
 */
$routes->get('/', 'Home::index');
```
Tambahkan baris berikut, setelah arahan rute untuk '/'. <br>
```
use App\Controllers\Pages;

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```
- Buat pengontrol halaman <br>
buat file di app/Controllers/Pages.php dengan kode berikut : <br>
```
<?php

namespace App\Controllers;

class Pages extends BaseController
{
    public function index()
    {
        return view('welcome_message');
    }

    public function view($page = 'home')
    {
        // ...
    }
}
```
- buat tampilan <br>
Buat header di app/Views/templates/header.php dan tambahkan kode berikut: <br>
```
<!doctype html>
<html>
<head>
    <title>CodeIgniter Tutorial</title>
</head>
<body>

    <h1><?= esc($title) ?></h1>
```
Sekarang, buat footer di app/Views/templates/footer.php yang menyertakan kode berikut: <br>
```
<em>&copy; 2022</em>
</body>
</html>
```
pada projek :

      
