# Pemrograman Berbasis Framework
Nama : Adhe Nur Wulandari
Kelas : TI - 2D
NIM : 220302073

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
```
$php spark serve ```

Ini akan meluncurkan server dan sekarang Anda dapat melihat aplikasi Anda di browser Anda di http://localhost:8080 .
      
      
