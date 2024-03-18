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
pada projek : <br>
![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/56982c9e-007e-4406-83e2-d66e694a19bc)
<br>
Sekarang, buat footer di app/Views/templates/footer.php yang menyertakan kode berikut: <br>
```
<em>&copy; 2022</em>
</body>
</html>
```
pada projek : <br>
![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/147f2f97-dbfc-458e-b3b2-0490d3b4718f)  <br>
- Menambahkan Logika ke Controller <br>
Badan halaman statis akan ditempatkan di direktori app/Views/pages. Di direktori itu, buat dua file bernama home.php dan about.php <br>
pada direktori app/Controllers/pages.php diisikan dengan kode berikut : <br>
```
<?php

namespace App\Controllers;

use CodeIgniter\Exceptions\PageNotFoundException; //untuk mengimpor kelas PageNotFoundException
//CodeIgniter\Exceptions. tidak ada folder fisik yang secara langsung menampungnya di struktur proyek standar ini berasal dari default sistem ci

class Pages extends BaseController
{
    //http://localhost:8080/pages menampilkan index() welcome_message
    public function index()
    {
        // Menampilkan halaman utama (welcome_message.php)
        return view('welcome_message');
    }

    public function view($page = 'home')
    {
        // ...

        // Mengecek apakah halaman yang diminta ada
        if (! is_file(APPPATH . 'Views/pages/' . $page . '.php')) {
            // Whoops, we don't have a page for that!
            // Jika tidak ada, lempar PageNotFoundException
            throw new PageNotFoundException($page);
        }

        // Mengatur judul halaman berdasarkan nama halaman
        $data['title'] = ucfirst($page); // Capitalize the first letter

         // Memuat template header, halaman statis (home, about), dan footer
        return view('templates/header', $data)
            . view('pages/' . $page)
            . view('templates/footer');
    }
}
```
- menjalankan aplikasi <br>
Dari baris perintah, di root proyek Anda: <br>
```
php spark serve
```
akan memulai server web, dapat diakses pada port 8080. Jika Anda mengatur field lokasi di browser Anda ke localhost:8080 , Anda akan melihat halaman selamat datang CodeIgniter. <br>
Sekarang kunjungi localhost:8080/home . <br>
![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/054377a4-0a86-4cf3-befd-2f33bf77c7df)
**bagian berita**
- buat database untuk digunakan <br>
Instalasi CodeIgniter mengasumsikan bahwa Anda telah menyiapkan database yang sesuai, sebagaimana diuraikan dalam persyaratan . Dalam tutorial ini, kami menyediakan kode SQL untuk database MySQL, dan kami juga berasumsi bahwa Anda memiliki klien yang cocok untuk mengeluarkan perintah database (mysql, MySQL Workbench, atau phpMyAdmin). <br>
<br>
Anda perlu membuat database ci4tutorial yang dapat digunakan untuk tutorial ini, dan kemudian mengkonfigurasi CodeIgniter untuk menggunakannya. <br>
<br>
Menggunakan klien database Anda, sambungkan ke database Anda dan jalankan perintah SQL di bawah ini (MySQL):   <br>

```
CREATE TABLE news (
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    title VARCHAR(128) NOT NULL,
    slug VARCHAR(128) NOT NULL,
    body TEXT NOT NULL,
    PRIMARY KEY (id),
    UNIQUE slug (slug)
);
```
pada projek :  <br>
![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/130f750d-02a7-4011-9914-5f9d743e999c)
<br>
kemudian isi kan bagian table news pada database ci4tutorial <br>

```
INSERT INTO news VALUES
(1,'Elvis sighted','elvis-sighted','Elvis was sighted at the Podunk internet cafe. It looked like he was writing a CodeIgniter app.'),
(2,'Say it isn\'t so!','say-it-isnt-so','Scientists conclude that some programmers have a sense of humor.');
```
pada projek saya : <br>
![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/99e07a7f-8654-4f8b-a1bc-c130b96c9541)
<br>
- hubungkan ke basis data anda <br>
File konfigurasi lokal, .env , yang Anda buat saat menginstal CodeIgniter, harus memiliki pengaturan properti database yang tidak diberi komentar dan disetel dengan tepat untuk database yang ingin Anda gunakan. Pastikan Anda telah mengkonfigurasi database Anda dengan benar seperti yang dijelaskan dalam Konfigurasi Database : <br>

```
database.default.hostname = localhost
database.default.database = ci4tutorial
database.default.username = root
database.default.password = root
database.default.DBDriver = MySQLi
```
pada perojek file env.: <br>
![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/0c7894c1-9cc8-4fbf-a0a7-6b0b6caa1fc8)
<br>
- buat model berita
Buka direktori app/Models dan buat file baru bernama NewsModel.php dan tambahkan kode berikut : <br>
```
<?php

namespace App\Models;

use CodeIgniter\Model;

class NewsModel extends Model
{
    protected $table = 'news';
}
```
- tambahkan metode NewsModel::getNew() <br>
Tambahkan kode berikut ke model : <br>

```
 public function getNews($slug = false)
    {
        if ($slug === false) {
            return $this->findAll();
        }

        return $this->where(['slug' => $slug])->first();
    }
```

![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/72bab21d-d3ff-42f5-8b82-0e7548a01ecc)
<br>
- tampilkan berita
Sekarang setelah kueri ditulis, model harus dikaitkan dengan tampilan yang akan menampilkan item berita kepada pengguna. Ini bisa dilakukan di Pagespengontrol yang kami buat sebelumnya, tetapi demi kejelasan, Newspengontrol baru telah ditentukan. <br>
Ubah file app/Config/Routes.php Anda , sehingga terlihat seperti berikut: <br>
```
<?php

// ...

use App\Controllers\News; // Add this line
use App\Controllers\Pages;

$routes->get('news', [News::class, 'index']);           // Add this line
$routes->get('news/(:segment)', [News::class, 'show']); // Add this line

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```
- buat perngontrol berita <br>
Buat pengontrol baru di app/Controllers/News.php <br>
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;

class News extends BaseController
{
    public function index()
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews();
    }

    public function show($slug = null)
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews($slug);
    }
}
```
kemudian pada app/Controllers/News.php, pada perintah index () diisikan kode berikut :

```
<?php

namespace App\Controllers;

use App\Models\NewsModel;

class News extends BaseController
{
    public function index()
    {
        $model = model(NewsModel::class);

        $data = [
            'news'  => $model->getNews(),
            'title' => 'News archive',
        ];

        return view('templates/header', $data)
            . view('news/index')
            . view('templates/footer');
    }

    // ...
}
```
![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/db2ccc3a-74a7-49d2-b7d1-2373df883d68)
<br>
- buat file tampilan berita/indeks
Buat app/Views/news/index.php dan tambahkan potongan kode berikutnya. <br>
```
<h2><?= esc($title) ?></h2>

<?php if (! empty($news) && is_array($news)): ?>

    <?php foreach ($news as $news_item): ?>

        <h3><?= esc($news_item['title']) ?></h3>

        <div class="main">
            <?= esc($news_item['body']) ?>
        </div>
        <p><a href="/news/<?= esc($news_item['slug'], 'url') ?>">View article</a></p>

    <?php endforeach ?>

<?php else: ?>

    <h3>No News</h3>

    <p>Unable to find any news for you.</p>

<?php endif ?>
```
![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/f9e908ef-9d52-48d7-aff5-27252400a634)
<br>
- berita lengkap::show() metode <br>
Halaman ikhtisar berita kini sudah selesai, namun halaman untuk menampilkan item berita individual masih belum ada. Model yang dibuat sebelumnya dibuat sedemikian rupa sehingga dapat dengan mudah digunakan untuk fungsi ini. Anda hanya perlu menambahkan beberapa kode ke controller dan membuat tampilan baru. <br>
Kembali ke app/controllers/news.php dan perbarui show()metode dengan yang berikut:
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class News extends BaseController
{
    // ...

    public function show($slug = null)
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews($slug);

        if (empty($data['news'])) {
            throw new PageNotFoundException('Cannot find the news item: ' . $slug);
        }

        $data['title'] = $data['news']['title'];

        return view('templates/header', $data)
            . view('news/view')
            . view('templates/footer');
    }
}
```
![image](https://github.com/adheenw/AdheNurWulandari/assets/134478214/fe15142e-45af-4cd6-b00a-b50d63ec541e)
<br>
- buatberita/lihat liha file <br>
Satu-satunya hal yang perlu dilakukan adalah membuat tampilan terkait di app/Views/news/view.php. Letakkan kode berikut di file ini. <br>
```
<h2><?= esc($news['title']) ?></h2>
<p><?= esc($news['body']) ?></p>
```
Arahkan browser Anda ke halaman “berita”, yaitu localhost:8080/news , Anda akan melihat daftar item berita, yang masing-masing memiliki link untuk menampilkan satu artikel saja. <br>


  






