# 🌊 AquaPOS - Sistem Kasir Laravel 12

Sistem kasir modern dengan branding warna biru aqua, dibangun menggunakan **Laravel 12** dan **Laravel Breeze** untuk autentikasi. Dilengkapi dengan fitur manajemen produk, pelanggan, dan transaksi penjualan dengan stok otomatis.

![Laravel Version](https://img.shields.io/badge/Laravel-12.x-FF2D20?style=flat-square&logo=laravel)
![PHP Version](https://img.shields.io/badge/PHP-8.2+-777BB4?style=flat-square&logo=php)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

---

## 📋 Daftar Isi

- [Fitur](#fitur)
- [Persyaratan Sistem](#persyaratan-sistem)
- [Instalasi](#instalasi)
- [Command Line Reference](#command-line-reference)
- [Struktur Database](#struktur-database)
- [Penggunaan](#penggunaan)

---

## ✨ Fitur

### 🎨 UI/UX
- **Design Minimalis** dengan nuansa biru aqua
- **Font Poppins** untuk tampilan modern
- **Bootstrap 5** untuk responsive design
- **Card Style** dengan border halus
- **Navbar Navigation** yang intuitif

### 🔐 Autentikasi (Laravel Breeze)
- **Login** dengan validasi email & password
- **Register** akun baru
- **Forgot Password** reset password via email
- **Email Verification** verifikasi email
- **Profile Management** edit profil user
- **Middleware** `auth` dan `verified` untuk proteksi halaman

### 📦 Manajemen Produk (CRUD)
- Tambah, Edit, Hapus Produk
- **Stok Otomatis** berkurang saat penjualan
- **Validasi Stok** sebelum transaksi
- Pencarian & Filter Produk

### 👥 Manajemen Pelanggan (CRUD)
- Tambah, Edit, Hapus Pelanggan
- Riwayat Transaksi per Pelanggan
- Pencarian Pelanggan

### 🛒 Manajemen Penjualan
- **Input Transaksi** dengan multiple produk
- **Detail Penjualan** otomatis tersimpan
- **Print Invoice** (format struk kasir 80mm)
- **Laporan Penjualan** dengan filter tanggal

---

## 💻 Persyaratan Sistem

- **PHP**: >= 8.2
- **Composer**: >= 2.0
- **Node.js**: >= 18.0
- **Database**: MySQL 8.0+ / MariaDB 10.5+
- **Web Server**: Apache / Nginx

### Extension PHP yang Diperlukan
```
extension=curl
extension=fileinfo
extension=gd
extension=mbstring
extension=openssl
extension=pdo_mysql
extension=tokenizer
extension=xml
extension=zip
```

---

## 🚀 Instalasi

### Langkah 1: Install Laravel 12

```bash
# Install Laravel 12 via Composer
composer create-project laravel/laravel aquapos "12.*"

cd aquapos
```

**Penjelasan:**
> `composer create-project` - Membuat project Laravel baru dengan versi 12.x

---

### Langkah 2: Install Laravel Breeze

```bash
# Install Breeze package
composer require laravel/breeze --dev

# Install Breeze dengan Blade (PHP native)
php artisan breeze:install blade
```

**Penjelasan:**
> `composer require laravel/breeze --dev` - Menginstall package Laravel Breeze untuk autentikasi
> 
> `php artisan breeze:install blade` - Setup autentikasi dengan template Blade (alternatif: livewire, react, vue)

---

### Langkah 3: Install NPM Dependencies

```bash
# Install package NPM
npm install

# Compile asset untuk development
npm run dev

# Atau compile untuk production
npm run build
```

**Penjelasan:**
> `npm install` - Menginstall semua package JavaScript (Tailwind CSS, Alpine.js, dll)
> 
> `npm run dev` - Compile asset dan jalankan Vite dev server (hot reload)
> 
> `npm run build` - Compile asset untuk production (minified)

---

### Langkah 4: Setup Environment

```bash
# Copy file environment
cp .env.example .env

# Generate application key
php artisan key:generate
```

**Penjelasan:**
> `cp .env.example .env` - Membuat file konfigurasi environment dari template
> 
> `php artisan key:generate` - Membuat APP_KEY unik untuk enkripsi session dan data

---

### Langkah 5: Konfigurasi Database

Edit file `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=aquapos
DB_USERNAME=root
DB_PASSWORD=your_password
```

Buat database:

```bash
# Login ke MySQL
mysql -u root -p

# Buat database
CREATE DATABASE aquapos CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
EXIT;
```

---

### Langkah 6: Buat Model, Migration, dan Controller

```bash
# Buat Model Produk dengan Migration dan Resource Controller
php artisan make:model Produk -mcr

# Buat Model Pelanggan dengan Migration dan Resource Controller
php artisan make:model Pelanggan -mcr

# Buat Model Penjualan dengan Migration dan Resource Controller
php artisan make:model Penjualan -mcr

# Buat Model DetailPenjualan dengan Migration dan Resource Controller
php artisan make:model DetailPenjualan -mcr
```

**Penjelasan:**
> `php artisan make:model NamaModel -mcr` - Membuat:
> - **Model** (`app/Models/NamaModel.php`)
> - **Migration** (`database/migrations/xxxx_create_nama_table.php`)
> - **Resource Controller** (`app/Http/Controllers/NamaController.php`)

**Flag:**
| Flag | Keterangan |
|------|------------|
| `-m` | Buat Migration |
| `-c` | Buat Controller |
| `-r` | Resource Controller (dengan method CRUD) |
| `-f` | Buat Factory |
| `-s` | Buat Seeder |

---

### Langkah 7: Jalankan Migration

```bash
# Jalankan semua migration
php artisan migrate
```

**Penjelasan:**
> `php artisan migrate` - Menjalankan semua file migration untuk membuat tabel di database

**Output yang diharapkan:**
```
INFO  Preparing database.  
Creating migration table .............................. 10.23ms DONE
INFO  Running migrations.  
2014_10_12_000000_create_users_table .................. 25.15ms DONE
2025_01_01_000001_create_produk_table ................. 18.42ms DONE
2025_01_01_000002_create_pelanggan_table .............. 15.67ms DONE
2025_01_01_000003_create_penjualan_table .............. 20.89ms DONE
2025_01_01_000004_create_detailpenjualan_table ........ 22.45ms DONE
```

---

### Langkah 8: Seed Data (Opsional)

```bash
# Jalankan database seeder
php artisan db:seed
```

**Penjelasan:**
> `php artisan db:seed` - Mengisi database dengan data dummy untuk testing

**Login Default:**
- Email: `admin@aquapos.com`
- Password: `password`

---

### Langkah 9: Jalankan Server

```bash
# Jalankan Laravel development server
php artisan serve
```

**Penjelasan:**
> `php artisan serve` - Menjalankan built-in PHP development server di `http://localhost:8000`

**Akses Aplikasi:**
- URL: `http://localhost:8000`
- Login: `http://localhost:8000/login`
- Register: `http://localhost:8000/register`

---

## ⌨️ Command Line Reference

### Command Dasar Laravel 12

| Command | Fungsi | Penjelasan |
|---------|--------|------------|
| `php artisan serve` | Jalankan server | Menjalankan development server di localhost:8000 |
| `php artisan optimize` | Optimasi aplikasi | Cache config, route, dan view untuk performa |
| `php artisan cache:clear` | Clear cache | Menghapus semua cache aplikasi |
| `php artisan route:list` | List route | Menampilkan daftar semua route |

### Database Migration

| Command | Fungsi | Penjelasan |
|---------|--------|------------|
| `php artisan migrate` | Jalankan migration | Menjalankan semua migration yang belum dijalankan |
| `php artisan migrate:fresh` | Reset & migrate | Menghapus semua tabel dan jalankan ulang migration |
| `php artisan migrate:rollback` | Rollback | Membatalkan migration terakhir |
| `php artisan migrate:status` | Status migration | Melihat status migration (ran/pending) |

### Make Commands (Generator)

```bash
# Model + Migration + Controller Resource
php artisan make:model Produk -mcr

# Controller saja
php artisan make:controller DashboardController

# Resource Controller
php artisan make:controller ProdukController --resource

# Migration saja
php artisan make:migration create_produk_table --create=produk

# Middleware
php artisan make:middleware CheckRole

# Seeder
php artisan make:seeder ProdukSeeder

# Factory
php artisan make:factory ProdukFactory --model=Produk
```

### Laravel Breeze Commands

```bash
# Install Breeze
composer require laravel/breeze --dev

# Setup Breeze dengan Blade
php artisan breeze:install blade

# Setup Breeze dengan Livewire
php artisan breeze:install livewire

# Setup Breeze dengan React
php artisan breeze:install react

# Setup Breeze dengan Vue
php artisan breeze:install vue
```

### NPM Commands

```bash
# Install dependencies
npm install

# Development (dengan hot reload)
npm run dev

# Production build
npm run build
```

---

## 🗄️ Struktur Database

### ERD (Entity Relationship Diagram)

```
┌─────────────┐       ┌─────────────────┐       ┌─────────────┐
│   produk    │       │  detailpenjualan │       │  penjualan  │
├─────────────┤       ├─────────────────┤       ├─────────────┤
│ PK ProdukID │◄──────┤ FK ProdukID     │       │ PK PenjualanID│
│    NamaProduk│       │ FK PenjualanID  ├──────►│ TanggalPenjualan
│    Harga    │       │    JumlahProduk │       │ TotalHarga  │
│    Stok     │       │    Subtotal     │       │ FK PelangganID├────┐
└─────────────┘       └─────────────────┘       │ FK user_id  │    │
                                                └─────────────┘    │
                              ┌─────────────┐                       │
                              │  pelanggan  │◄──────────────────────┘
                              ├─────────────┤
                              │ PK PelangganID
                              │ NamaPelanggan
                              │ Alamat
                              │ NomorTelepon
                              └─────────────┘
```

### Tabel-tabel

| Tabel | Deskripsi | Relasi |
|-------|-----------|--------|
| `users` | Tabel autentikasi (Breeze) | - |
| `produk` | Data barang/produk | hasMany → detailpenjualan |
| `pelanggan` | Data customer | hasMany → penjualan |
| `penjualan` | Header transaksi | belongsTo → pelanggan, user<br>hasMany → detailpenjualan |
| `detailpenjualan` | Item transaksi | belongsTo → penjualan, produk |

---

## 📖 Penggunaan

### Alur Kerja Sistem

```
1. Login/Register (Laravel Breeze)
        ↓
2. Dashboard (ringkasan penjualan)
        ↓
3. Kelola Produk (tambah data barang)
        ↓
4. Kelola Pelanggan (tambah data customer)
        ↓
5. Buat Transaksi (input penjualan)
        ↓
6. Print Invoice (cetak struk)
```

### Fitur Stok Otomatis

```php
// Saat transaksi dibuat:
// 1. DetailPenjualan disimpan
// 2. Stok produk otomatis berkurang

$produk = Produk::find(1);
echo $produk->Stok; // Output: 100

// Setelah penjualan 5 item:
echo $produk->fresh()->Stok; // Output: 95
```

---

## 🛠️ Troubleshooting

### Error: "No application encryption key has been specified"

```bash
php artisan key:generate
```

### Error: "Class not found"

```bash
composer dump-autoload
```

### Clear All Cache

```bash
php artisan optimize:clear
```

---

## 📄 License

This project is licensed under the MIT License.

---

**Terima kasih telah menggunakan AquaPOS! 🌊**
#   n o w  
 #   n o w  
 