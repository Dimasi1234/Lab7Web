# Lab7Web - Praktikum Pemrograman Web 2

## Praktikum 1: PHP Framework (CodeIgniter 4)

### Tujuan
- Memahami konsep dasar framework dan MVC.
- Membuat program sederhana dengan CodeIgniter 4.

### Langkah-langkah

1. **Persiapan:**
   - Instalasi XAMPP, aktifkan ekstensi PHP (json, xml, intl, mysqlnd).
      Install XAMPP di: https://www.apachefriends.org/download.html
      ![Screenshot (115)](https://github.com/user-attachments/assets/bab72f62-6a85-438f-a32f-d484298a25a3)

   - Aktifkan ekstensi PHP (json, xml, intl, mysqlnd).
      ![Screenshot (116)](https://github.com/user-attachments/assets/320b09ef-b689-4107-9fca-6c6a970d3c71)
      ![Screenshot (110)](https://github.com/user-attachments/assets/55afb829-d31a-46c1-a38e-20c75e620d03)

   - Instalasi CodeIgniter4
      Install CI4 di: https://codeigniter.com/download
      ![Screenshot (117)](https://github.com/user-attachments/assets/59efc9ee-1cd9-4ab6-931e-86f70e901d59)

   - Buat folder `lab11_ci` di htdocs, ekstrak Zip CodeIgniter ke lab11_ci ganti namanya jadi ci4.
      ![Screenshot (118)](https://github.com/user-attachments/assets/e337838f-6bb4-4fa2-ae43-5405b82df5fc)
      ![Screenshot (119)](https://github.com/user-attachments/assets/28fb743d-f432-4dc2-b96c-741577a297f9)

2. **Persiapan:**
   - Buka folder ci4 menggunakan vs code
      ![Screenshot (120)](https://github.com/user-attachments/assets/f799c345-3c47-477c-866e-f0be60c59ffd)
   - Cari env ubah namanya menjadi .env, lalu hapus tanda # pada bagian CI_ENVIRONMENT = development. Jika belum ganti ke development ganti sendiri, itu untuk menghidupkan mode debugging
      ![Screenshot (121)](https://github.com/user-attachments/assets/40547dc8-6256-40c4-b310-a104fbf89453)
      mode debungging
      ![Screenshot (113)](https://github.com/user-attachments/assets/4c7991d2-daad-4ea7-8ab7-a8dbc415d260)

3. **Routing dan Controller:**
   - Tambah route: `/about`, `/contact`, `/faqs`, `/page/tos`
      ![Screenshot (122)](https://github.com/user-attachments/assets/d0714dd4-d508-4a71-87c9-c18b8681f15a)
   - Buat controller `Page.php` dengan method untuk setiap halaman.
      ![Screenshot (123)](https://github.com/user-attachments/assets/3a40c5bb-1c91-4eb1-8432-e290335b3b46)

4. **View dan Layout:**
   - Buat `template/header.php` dan `template/footer.php`
      ![Screenshot (124)](https://github.com/user-attachments/assets/fb959451-e037-4ea5-bb43-3493421e8daf)
      ![Screenshot (125)](https://github.com/user-attachments/assets/fa2d3a50-2fe9-4da4-8d59-8d4dc703fa15)

   - Buat view `about.php`, `contact.php`, dll. Include header & footer di setiap halaman.
      ![Screenshot (126)](https://github.com/user-attachments/assets/4f1b08ba-ddcc-4cbc-8396-c44c06347601)

5. **CSS Layout:**
   - Tambahkan `style.css` ke folder `public`.
      ![Screenshot (127)](https://github.com/user-attachments/assets/5a62015c-43eb-471e-a663-098014326164)

   - Gunakan layout praktikum 4 atau buat sendiri juga boleh.

### Hasil
> **![Screenshot (114)](https://github.com/user-attachments/assets/04d13db6-80d9-4f8f-a5ab-83db4f6a9283)**

## Praktikum 2: Framework Lanjutan (CRUD Artikel)

### Tujuan
- Memahami konsep Model
- Menerapkan operasi CRUD (Create, Read, Update, Delete)


### Repository
- Repository ini berisi hasil praktikum modul 1 CodeIgniter.
- URL: https://github.com/Dimasi1234/Lab7Web
```
