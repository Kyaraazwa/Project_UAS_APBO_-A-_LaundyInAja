# UTS APBO (A) KELOMPOK 2
Project ini disusun untuk memenuhi Nilai Ujian Tengah Semester Genap Matakuliah nalisis Pemrograman Berorientasi Objek, yang diampu oleh Bapak Adi Wahyu Pribadi, S.Si., M.Kom.

Kami dari Kelompok 2 mengangkat topik Perancangan Aplikasi Laundry.In Aja, sebuah sistem berbasis aplikasi yang dirancang untuk mempermudah proses pengelolaan operasional usaha laundry. Melalui perancangan sistem ini, diharapkan aktivitas bisnis laundry dapat dilakukan secara lebih efisien, terstruktur, dan terdokumentasi dengan baik. Fitur-fitur utama yang kami implementasikan mencakup pencatatan data pemesanan layanan laundry, rincian berat dan subtotal layanan, pengelolaan informasi paket dan pembayaran, serta integrasi data karyawan sebagai bagian dari proses operasional.

Dengan adanya aplikasi ini, kami berharap dapat memberikan solusi sederhana namun efektif dalam mendigitalisasi proses manajemen usaha laundry secara menyeluruh.

# Anggota Kelompok 2
| No | Nama Anggota          | NPM         |
|----|-----------------------|-------------|
| 1  | Irmawati Pakpahan     | 4523210052  |
| 2  | Karin Lina Safitri    | 4523210056  |
| 3  | Kyara Azwa Humayra    | 4523210058  |
| 4  | Lintang Triandini     | 4523210060  |
 

# Aktor yang menggunakan aplikasi Laundri.In Aja
1. Admin sebagai aktor tunggal

# Usecase


# Entity Relationship Diagram


# Table Master dan Relasi
### 1. Table Master
CREATE TABLE user (
  id_user int NOT NULL,
  nama_user varchar(50) DEFAULT NULL,
  email varchar(50) DEFAULT NULL,
  password varchar(50) DEFAULT NULL,
  role enum('Super Admin','Admin') DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom   | Tipe Data                      | Keterangan             |
|--------------|--------------------------------|------------------------|
| id_user      | INT (PK)                       | ID unik pengguna       |
| nama_user    | VARCHAR(50)                    | Nama lengkap pengguna  |
| email        | VARCHAR(50)                    | Alamat email           |
| password     | VARCHAR(50)                    | Kata sandi             |
| role         | ENUM('Super Admin','Admin')    | Peran pengguna         |


| Nama Kolom            | Tipe Data     | Keterangan                               |
|-----------------------|---------------|------------------------------------------|
| id_detail_penjualan   | INT (PK)      | ID detail penjualan                      |
| jumlah_produk         | INT           | Jumlah produk terjual                    |
| harga_satuan          | INT           | Harga satuan per produk                  |
| id_transaksi_penjualan| INT (FK)      | Referensi ke tabel transaksi_penjualan |
| id_produk             | INT (FK)      | Referensi ke tabel produk              |


CREATE TABLE supplier (
  id_supplier int NOT NULL,
  nama_supplier varchar(50) DEFAULT NULL,
  telepon varchar(15) DEFAULT NULL,
  email varchar(50) DEFAULT NULL,
  alamat text
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom     | Tipe Data     | Keterangan               |
|----------------|---------------|--------------------------|
| id_supplier    | INT (PK)      | ID unik supplier         |
| nama_supplier  | VARCHAR(50)   | Nama supplier            |
| telepon        | VARCHAR(15)   | Nomor telepon            |
| email          | VARCHAR(50)   | Alamat email             |
| alamat         | TEXT          | Alamat lengkap           |

CREATE TABLE kategori (
  id_kategori int NOT NULL,
  nama_kategori varchar(50) DEFAULT NULL,
  keterangan text
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom     | Tipe Data     | Keterangan           |
|----------------|---------------|----------------------|
| id_kategori    | INT (PK)      | ID kategori produk   |
| nama_kategori  | VARCHAR(50)   | Nama kategori        |
| keterangan     | TEXT          | Deskripsi kategori   |

CREATE TABLE produk (
  id_produk int NOT NULL,
  nama_produk varchar(50) DEFAULT NULL,
  harga_jual int DEFAULT NULL,
  harga_beli int DEFAULT NULL,
  stok int DEFAULT NULL,
  id_kategori int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom     | Tipe Data     | Keterangan             |
|----------------|---------------|------------------------|
| id_produk      | INT (PK)      | ID produk              |
| nama_produk    | VARCHAR(50)   | Nama produk            |
| harga_jual     | INT           | Harga jual produk      |
| harga_beli     | INT           | Harga beli produk      |
| stok           | INT           | Stok tersedia          |
| id_kategori    | INT (FK)      | Referensi kategori     |

### 1. Table Relasi
CREATE TABLE pembelian (
  id_pembelian int NOT NULL,
  tanggal date DEFAULT NULL,
  total_pembelian int DEFAULT NULL,
  id_supplier int DEFAULT NULL,
  id_user int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom       | Tipe Data     | Keterangan                         |
|------------------|---------------|------------------------------------|
| id_pembelian     | INT (PK)      | ID pembelian                       |
| tanggal          | DATE          | Tanggal pembelian                  |
| total_pembelian  | INT           | Total nilai pembelian              |
| id_supplier      | INT (FK)      | Referensi ke tabel supplier      |
| id_user          | INT (FK)      | Referensi ke tabel user          |

---

CREATE TABLE detail_pembelian (
  id_detail_pembelian int NOT NULL,
  id_pembelian int DEFAULT NULL,
  id_produk int DEFAULT NULL,
  jumlah_pembelian int DEFAULT NULL,
  harga_satuan int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom         | Tipe Data     | Keterangan                              |
|--------------------|---------------|-----------------------------------------|
| id_detail_pembelian | INT (PK)     | ID detail pembelian                     |
| id_pembelian        | INT (FK)     | Referensi ke tabel pembelian          |
| id_produk           | INT (FK)     | Referensi ke tabel produk             |
| jumlah_pembelian    | INT          | Jumlah produk yang dibeli               |
| harga_satuan        | INT          | Harga satuan per produk                 |

CREATE TABLE transaksi_penjualan (
  id_transaksi_penjualan int NOT NULL,
  total_penjualan int DEFAULT NULL,
  tanggal date DEFAULT NULL,
  metode_pembayaran enum('Tunai','E-Wallet') DEFAULT NULL,
  id_user int DEFAULT NULL
) 

| Nama Kolom            | Tipe Data                        | Keterangan                          |
|-----------------------|----------------------------------|-------------------------------------|
| id_transaksi_penjualan| INT (PK)                         | ID transaksi penjualan              |
| total_penjualan       | INT                              | Total nilai penjualan               |
| tanggal               | DATE                             | Tanggal transaksi                   |
| metode_pembayaran     | ENUM('Tunai','E-Wallet')         | Metode pembayaran                   |
| id_user               | INT (FK)                         | Referensi ke tabel user           |


CREATE TABLE detail_penjualan (
  id_detail_penjualan int NOT NULL,
  jumlah_produk int DEFAULT NULL,
  harga_satuan int DEFAULT NULL,
  id_transaksi_penjualan int DEFAULT NULL,
  id_produk int DEFAULT NULL
)

| Nama Kolom            | Tipe Data                        | Keterangan                            |
|-----------------------|----------------------------------|---------------------------------------|
| id_transaksi_penjualan| INT (PK)                         | ID transaksi penjualan                |
| total_penjualan       | INT                              | Total nilai penjualan                 |
| tanggal               | DATE                             | Tanggal transaksi                     |
| metode_pembayaran     | ENUM('Tunai','E-Wallet')         | Metode pembayaran                     |
| id_user               | INT (FK)                         | Referensi ke tabel user             |

# Class Diagram


# Wireframe


# Mockup
