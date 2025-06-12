# UTS APBO (A) KELOMPOK 2
Project ini disusun untuk memenuhi Nilai Ujian Tengah Semester Genap Matakuliah Analisis Pemrograman Berorientasi Objek, yang diampu oleh Bapak Adi Wahyu Pribadi, S.Si., M.Kom.

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
CREATE TABLE Pelanggan (
    ID_Pelanggan INT PRIMARY KEY AUTO_INCREMENT,
    Nama VARCHAR(100),
    No_HP VARCHAR(20),
    Alamat TEXT
);

| Nama Kolom   | Tipe Data                      | Keterangan             |
|--------------|--------------------------------|------------------------|
| iD_Pelanggan | INT (PK)                       | ID unik Pelanggan      |
| Nama         | VARCHAR(100)                   | Nama lengkap pelanggan |
| No_HP        | VARCHAR(20)                    | No. Handphone pelanggan|
| Alamat       | TEXT                           | Alamat pengguna        |


CREATE TABLE Layanan (
    ID_Layanan INT PRIMARY KEY AUTO_INCREMENT,
    Nama_Layanan VARCHAR(100),
    Deskripsi TEXT,
    Harga_per_Kg DECIMAL(10, 2)
); ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom     | Tipe Data     | Keterangan               |
|----------------|---------------|--------------------------|
| ID_Layanan     | INT (PK)      | ID unik Layanan          |
| Nama_Layanan   | VARCHAR(100)  | Nama Layanan             |
| Deskripsi      | TEXT          | Penjelasan Layanan       |
| Harga_per_Kg   | DECIMAL(10, 2)| Harga laundry perKg      |


CREATE TABLE Paket (
    ID_Paket INT PRIMARY KEY AUTO_INCREMENT,
    Nama_Paket VARCHAR(100)
); ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom     | Tipe Data     | Keterangan           |
|----------------|---------------|----------------------|
| ID_Paket       | INT (PK)      | ID paket Laundry     |
| nama_Paket     | VARCHAR(50)   | Nama Paket           |


CREATE TABLE Admin (
  ID_Admin int PRIMARY KEY AUTO_INCREMENT,
  Nama_Admin varchar(100) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom     | Tipe Data     | Keterangan             |
|----------------|---------------|------------------------|
| ID_Admin       | INT (PK)      | ID Admin               |
| Nama_Admin     | VARCHAR(100)  | Nama Admin             |


### 1. Table Relasi
CREATE TABLE Pemesanan (
    ID_Pemesanan INT PRIMARY KEY AUTO_INCREMENT,
    ID_Pelanggan INT,
    ID_Layanan INT,
    Status ENUM('Diproses', 'Selesai', 'Batal'),
    Waktu_Pemesanan DATETIME,
    FOREIGN KEY (ID_Pelanggan) REFERENCES Pelanggan(ID_Pelanggan),
    FOREIGN KEY (ID_Layanan) REFERENCES Layanan(ID_Layanan)
); ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom       | Tipe Data                            | Keterangan                         |
|------------------|--------------------------------------|------------------------------------|
| ID_Pemesanan     | INT (PK)                             | ID pemesanan                       |
| ID_Pelanggan     | INT (FK)                             | ID Pelanggan                       |
| ID_Layanan       | INT (FK)                             | ID Layanan                         |
| Status           | ENUM('Diproses', 'Selesai', 'Batal') | Status pemesanan          |
| Waktu_Pemsanan   | DATETIME                             | tanggal pemesanan          |

CREATE TABLE Detail_Pemesanan (
    ID_Detail_Pemesanan INT PRIMARY KEY AUTO_INCREMENT,
    ID_Layanan INT,
    ID_Paket INT,
    Berat_Kg DECIMAL(5, 2),
    Subtotal DECIMAL(10, 2),
    FOREIGN KEY (ID_Layanan) REFERENCES Layanan(ID_Layanan),
    FOREIGN KEY (ID_Paket) REFERENCES Paket(ID_Paket)
);

| Nama Kolom         | Tipe Data     | Keterangan                         |
|--------------------|---------------|------------------------------------|
| ID_Detail_Pemesanan| INT (PK)      | ID pemesanan                       |
| ID_Layanan         | INT (FK)      | ID Layanan                         |
| ID_Paket           | INT (FK)      | ID Paket                           |
| Berat_Kg           | DECIMAL(5, 2) | Total Berat Baju /Kg               |
| Subtotal           | DECIMAL(10, 2)| Total Harga Pemesanan              |


CREATE TABLE Pembayaran (
    ID_Pembayaran INT PRIMARY KEY AUTO_INCREMENT,
    ID_Karyawan INT,
    ID_Paket INT,
    Tanggal_Pembayaran DATE,
    Status_Pembayaran ENUM('Lunas', 'Belum'),
    Jenis_Pembayaran ENUM('Tunai', 'Transfer'),
    Total DECIMAL(10, 2),
    FOREIGN KEY (ID_Karyawan) REFERENCES Karyawan(ID_Karyawan),
    FOREIGN KEY (ID_Paket) REFERENCES Paket(ID_Paket)
); ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom         | Tipe Data                | Keterangan                   |
|--------------------|--------------------------|------------------------------|
| ID_Pembayaran      | INT (PK)                 | ID Peembayaran               |
| ID_Karyawan        | INT (FK)                 | ID Layanan                   |
| ID_Paket           | INT (FK)                 | ID Paket                     |
| Tanggal_Pembayaran | ENUM('Lunas', 'Belum')   | Tanggal Pembayaran           |
| Status_Pembayaran  | ENUM('Tunai', 'Transfer')| Status Pembayaran            | 
| Jenis_Pembayaran   | ENUM('Tunai', 'Transfer')| Total Harga Pemesanan        | 
| Total              | DECIMAL(10, 2)           | Total Pembayaran             | 


# Class Diagram


# Wireframe


# Mockup
