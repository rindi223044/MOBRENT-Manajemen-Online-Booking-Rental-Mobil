# <p align="center" style="margin-bottom: 0px;">MOBRENT</p>
## <p align="center" style="margin-top: 0;">Manajemen Online Booking Mobil</p>

<p align="center">
  <img src="Logo Unsulbar.png" width="300" alt="Deskripsi gambar" />
</p>

### <p align="center">RINDI</p>
### <p align="center">D0223044</p></br>
### <p align="center">Framework Web Based</p>
### <p align="center">2025</p>

---

## Role dan Fitur-fiturnya

### 1. Administrator (Admin)
Administrator memiliki kontrol penuh terhadap sistem, mengelola data dan operasi seluruh platform rental mobil:

- Manajemen Akun Pengguna  
- Manajemen Armada Mobil  
- Laporan dan Analisis  
- Manajemen Pembayaran dan Transaksi  
- Pengelolaan Pengemudi (Driver)  
- Notifikasi dan Pengingat  

### 2. Customer (Pelanggan)

- Pencarian dan Pemesanan Mobil  
- Pembayaran Online  
- Pelacakan Pemesanan  
- Manajemen Profil  
- Layanan Pengiriman & Penjemputan  

### 3. Driver (Pengemudi)

- Jadwal Kerja dan Penugasan  
- Status dan Notifikasi  
- Manajemen Profil Pengemudi  
- Pemberitahuan Masalah dengan Kendaraan  

### 4. Staff (Staf)

- Manajemen Pemeliharaan Mobil  
- Proses Pengambilan dan Pengembalian Kendaraan  
- Penyelesaian Masalah Pelanggan  
- Pencatatan Inventaris Mobil  

---

## Tabel-tabel Database Beserta Field dan Tipe Datanya

### 1. Tabel `user`

| Nama Field       | Tipe Data            | Keterangan                            |
|------------------|----------------------|----------------------------------------|
| user_id          | INT (AUTO_INCREMENT) | Primary Key, ID unik pengguna         |
| name             | VARCHAR              | Nama lengkap pengguna                 |
| email            | VARCHAR              | Email pengguna, unik                  |
| passwoard        | VARCHAR              | Password terenkripsi                  |
| phone_number     | VARCHAR(20)          | Nomor telepon pengguna                |
| role             | ENUM('admin', 'customer', 'driver', 'staff') | Peran pengguna dalam sistem |
| profile_picture  | VARCHAR              | URL foto profil (opsional)            |
| created_at       | TIMESTAMP            | Tanggal pembuatan akun                |
| updated_at       | TIMESTAMP            | Tanggal pembaruan terakhir akun       |

### 2. Tabel `roles`

| Nama Field | Tipe Data            | Keterangan                             |
|------------|----------------------|----------------------------------------|
| id         | INT (AUTO_INCREMENT) | Primary Key, ID unik peran             |
| name       | VARCHAR              | Nama peran (admin, customer, dll)      |
| description| TEXT                 | Deskripsi tentang peran (opsional)     |

### 3. Tabel `user_roles` (relasi many-to-many antara pengguna dan peran)

| Nama Field    | Tipe Data            | Keterangan                             |
|---------------|----------------------|----------------------------------------|
| user_role_id  | INT (AUTO_INCREMENT) | Primary Key                            |
| user_id       | INT                  | Foreign Key ke `user_id` tabel `users` |
| role_id       | INT                  | Foreign Key ke `role_id` tabel `roles` |
| assigned_at   | TIMESTAMP            | Waktu peran diberikan                  |

### 4. Tabel `categories`

| Nama Field     | Tipe Data     | Keterangan                    |
|----------------|---------------|-------------------------------|
| category_id    | BIGINT        | Primary Key, ID unik kategori|
| category_name  | VARCHAR       | Nama kategori berita (unik)  |
| description    | TEXT          | Deskripsi kategori (opsional)|
| created_at     | TIMESTAMP     | Waktu saat dibuat            |
| updated_at     | TIMESTAMP     | Waktu saat diperbarui        |

### 5. Tabel `post`

| Nama Field    | Tipe Data            | Keterangan                              |
|---------------|----------------------|------------------------------------------|
| post_id       | INT (AUTO_INCREMENT) | Primary Key                              |
| title         | VARCHAR              | Judul postingan                          |
| content       | TEXT                 | Isi postingan                            |
| author_id     | INT                  | Foreign Key ke `user_id` tabel `users`   |
| category_id   | INT                  | Foreign Key ke `category_id` tabel `categories` |
| created_at    | TIMESTAMP            | Waktu dibuat                             |
| updated_at    | TIMESTAMP            | Waktu diperbarui                         |
| status        | ENUM('draft', 'published', 'archived') | Status postingan         |

### 6. Tabel `komentar`

| Nama Field    | Tipe Data            | Keterangan                              |
|---------------|----------------------|------------------------------------------|
| comment_id    | INT (AUTO_INCREMENT) | Primary Key                              |
| post_id       | INT                  | Foreign Key ke `post_id` tabel `posts`   |
| user_id       | INT                  | Foreign Key ke `user_id` tabel `users`   |
| content       | TEXT                 | Isi komentar                             |
| created_at    | TIMESTAMP            | Waktu dibuat                             |
| updated_at    | TIMESTAMP            | Waktu diperbarui                         |
| status        | ENUM('active', 'inactive', 'deleted') | Status komentar         |

### 7. Tabel `post_view`

| Nama Field    | Tipe Data            | Keterangan                              |
|---------------|----------------------|------------------------------------------|
| post_view_id  | INT (AUTO_INCREMENT) | Primary Key                              |
| post_id       | INT                  | Foreign Key ke `post_id` tabel `posts`   |
| user_id       | INT                  | Foreign Key ke `user_id` tabel `users`   |
| viewed_at     | TIMESTAMP            | Waktu dilihat                            |
| ip_address    | VARCHAR              | Alamat IP pengguna (opsional)            |

---

## Jenis Relasi dan Tabel yang Berelasi

| Jenis Relasi     | Relasi                                      |
|------------------|---------------------------------------------|
| One-to-Many      | users → posts                               |
|                  | categories → posts                          |
|                  | posts → comments                            |
|                  | users → comments                            |
|                  | posts → post_views                          |
| Many-to-Many     | users → user_roles ← roles                  |
|                  | cars → car_categories ← categories          |
| One-to-One       | users → user_profiles                       |
