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

### 1. Membuat Database `lab_ci4` dan table 'artikel'
```sql
CREATE DATABASE lab_ci4;

CREATE TABLE artikel (
  id INT(11) AUTO_INCREMENT,
  judul VARCHAR(200) NOT NULL,
  isi TEXT,
  gambar VARCHAR(200),
  status TINYINT(1) DEFAULT 0,
  slug VARCHAR(200),
  PRIMARY KEY(id)
);
```
![Screenshot (132)](https://github.com/user-attachments/assets/de943d95-be89-472a-a234-01eb7b7fec74)
---

### 2. Konfigurasi `.env`
```env
# Sesuaikan dengan MySQL mu
database.default.hostname = localhost
database.default.database = lab_ci4
database.default.username = root
database.default.password = 
database.default.DBDriver = MySQLi
```
![Screenshot (133)](https://github.com/user-attachments/assets/e64e5efa-3489-4dc0-866b-479421815265)
---

### 3. Membuat Model `ArtikelModel.php`
`app/Models/ArtikelModel.php`
![Screenshot (134)](https://github.com/user-attachments/assets/c7b4997f-8c1e-4451-b6af-edc2674c618a)
---

### 4. Membuat Controller `Artikel.php`
`app/Controllers/Artikel.php`
```php
namespace App\Controllers;
use App\Models\ArtikelModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class Artikel extends BaseController
{
    public function index() {
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        $title = 'Daftar Artikel';
        return view('artikel/index', compact('artikel', 'title'));
    }
}
```

### 5. File View (`app/Views/artikel/`)
```php
<?= $this->include('template/header'); ?>

<?php if($artikel): foreach($artikel as $row): ?>
<article class="entry">
    <h2><a href="<?= base_url('/artikel/' . $row['slug']); ?>"><?= $row['judul']; ?></a></h2>
    <img src="<?= base_url('/gambar/' . $row['gambar']); ?>" alt="<?= $row['judul']; ?>">
    <p><?= substr($row['isi'], 0, 200); ?></p>
</article>
<hr class="divider" />
<?php endforeach; else: ?>
<article class="entry">
    <h2>Belum ada data.</h2>
</article>
<?php endif; ?>

<?= $this->include('template/footer'); ?>
```

### 6. Routing Tambahan `app/Config/Routes.php`
```php
$routes->get('/artikel', 'Artikel::index');
```
![Screenshot (128)](https://github.com/user-attachments/assets/0ef95bb2-6721-4f24-ab55-45320126d8f2)
---

### 7. Data Dummy SQL
```sql
INSERT INTO artikel (judul, isi, slug) VALUES
('Artikel pertama', 'Lorem Ipsum adalah contoh teks...', 'artikel-pertama'),
('Artikel kedua', 'Tidak seperti anggapan banyak orang...', 'artikel-kedua');
```
![Screenshot (129)](https://github.com/user-attachments/assets/6b5da034-4ea0-4cd2-a8f7-8b501af77c57)
---

### 8. Tambahkan Controller `Artikel.php`
- Tambahkan function view
`app/Controllers/Artikel.php`
```php
public function view($slug) {
        $model = new ArtikelModel();
        $artikel = $model->where(['slug' => $slug])->first();
        if (!$artikel) throw PageNotFoundException::forPageNotFound();
        $title = $artikel['judul'];
        return view('artikel/detail', compact('artikel', 'title'));
    }
``` 

### 9. File Detail (`app/Views/detail/`)
.
```php
<?= $this->include('template/header'); ?>

<article class="entry">
    <h2><?= $artikel['judul']; ?></h2>
    <img src="<?= base_url('/gambar/' . $artikel['gambar']); ?>" alt="<?= $artikel['judul']; ?>">
    <p><?= $artikel['isi']; ?></p>
</article>

<?= $this->include('template/footer'); ?>
```

### 10. Routing Tambahan `app/Config/Routes.php`
```php
$routes->get('/artikel/(:any)', 'Artikel::view/$1');
```
![Screenshot (130)](https://github.com/user-attachments/assets/05488b4a-7a9d-4cc3-b42a-c214aa2882b6)
---

### 11. Tambahkan Controller `Artikel.php`
- Tambahkan function admin
```php
public function admin_index() {
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        $title = 'Daftar Artikel';
        return view('artikel/admin_index', compact('artikel', 'title'));
    }
```

### 12. File admin (`app/Views/admin/artikel`)
#### `admin_index.php`
```php
<?= $this->include('template/admin_header'); ?>

<table class="table">
    <thead>
        <tr><th>ID</th><th>Judul</th><th>Status</th><th>Aksi</th></tr>
    </thead>
    <tbody>
    <?php if($artikel): foreach($artikel as $row): ?>
    <tr>
        <td><?= $row['id']; ?></td>
        <td>
            <b><?= $row['judul']; ?></b>
            <p><small><?= substr($row['isi'], 0, 50); ?></small></p>
        </td>
        <td><?= $row['status']; ?></td>
        <td>
            <a class="btn" href="<?= base_url('/admin/artikel/edit/' . $row['id']); ?>">Ubah</a>
            <a class="btn btn-danger" onclick="return confirm('Yakin menghapus data?');" href="<?= base_url('/admin/artikel/delete/' . $row['id']); ?>">Hapus</a>
        </td>
    </tr>
    <?php endforeach; else: ?>
    <tr><td colspan="4">Belum ada data.</td></tr>
    <?php endif; ?>
    </tbody>
</table>

<?= $this->include('template/admin_footer'); ?>
```

### 13. Routing Tambahan `app/Config/Routes.php`
```php
$routes->group('admin', function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```
![Screenshot (135)](https://github.com/user-attachments/assets/36431954-01f9-4f28-a867-58ac0ae8d8d9)
---

### 14. Tambahkan Controller `Artikel.php`
- Tambahkan function add
```php
public function add() {
        $validation = \Config\Services::validation();
        $validation->setRules(['judul' => 'required']);
        if ($validation->withRequest($this->request)->run()) {
            $artikel = new ArtikelModel();
            $artikel->insert([
                'judul' => $this->request->getPost('judul'),
                'isi'   => $this->request->getPost('isi'),
                'slug'  => url_title($this->request->getPost('judul')),
            ]);
            return redirect('admin/artikel');
        }
        $title = "Tambah Artikel";
        return view('artikel/form_add', compact('title'));
    }
```

### 15. File add (`app/Views/admin/artikel/add`)
#### `form_add.php` 
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p><input type="text" name="judul" placeholder="Judul Artikel"></p>
    <p><textarea name="isi" cols="50" rows="10" placeholder="Isi artikel..."></textarea></p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```
![Screenshot (136)](https://github.com/user-attachments/assets/c22c1cc9-314f-4244-8c29-08b7e3cfebbe)
---

### 16. Tambahkan Controller `Artikel.php`
- Tambahkan function edit
```php
public function edit($id) {
        $artikel = new ArtikelModel();
        $validation = \Config\Services::validation();
        $validation->setRules(['judul' => 'required']);
        if ($validation->withRequest($this->request)->run()) {
            $artikel->update($id, [
                'judul' => $this->request->getPost('judul'),
                'isi'   => $this->request->getPost('isi'),
            ]);
            return redirect('admin/artikel');
        }
        $data = $artikel->where('id', $id)->first();
        $title = "Edit Artikel";
        return view('artikel/form_edit', compact('title', 'data'));
    }
```

### 17. File edit (`app/Views/admin/artikel/edit`)
#### `edit.php`
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p><input type="text" name="judul" value="<?= $data['judul']; ?>"></p>
    <p><textarea name="isi" cols="50" rows="10"><?= $data['isi']; ?></textarea></p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```
![Screenshot (137)](https://github.com/user-attachments/assets/4c595458-526b-46e7-9f36-19c35ca150b9)
---

### 18. Tambahkan Controller `Artikel.php`
- Tambahkan function delete
```php
public function delete($id) {
        $artikel = new ArtikelModel();
        $artikel->delete($id);
        return redirect('admin/artikel');
    }
```

### 📌 Kesimpulan
CRUD berhasil dibuat menggunakan CodeIgniter 4. Konsep MVC, validasi form, routing grup admin dan view template telah diterapkan.

### Repository
- Repository ini berisi hasil praktikum modul 1 CodeIgniter.
- URL: https://github.com/Dimasi1234/Lab7Web
```
