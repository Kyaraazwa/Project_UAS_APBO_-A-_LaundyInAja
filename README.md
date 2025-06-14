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
# Use Case


# Wireframe
![Image](https://github.com/user-attachments/assets/904ab6b2-ec24-47f7-8a99-9b86a4ea1c45)

![Image](https://github.com/user-attachments/assets/8513ffba-bc96-4982-b6b3-44271ae3a89c)

![Image](https://github.com/user-attachments/assets/e51077fe-1a5e-41cd-86ec-6af0639eafa7)

![Image](https://github.com/user-attachments/assets/af05abbb-3907-44e0-ac4f-1861f2ffd105)

![Image](https://github.com/user-attachments/assets/64e2c110-3314-4d72-b241-dffbfce3b219)

![Image](https://github.com/user-attachments/assets/a094190c-e1a7-4701-8bac-37a89cb55817)

![Image](https://github.com/user-attachments/assets/90b37728-1399-4ad1-933b-fce1dcadc494)

![Image](https://github.com/user-attachments/assets/7ef4d7a8-285f-49d8-89e1-05f71eb258af)

![Image](https://github.com/user-attachments/assets/7547d69e-2f42-470e-9c40-ecb4b81df5bd)

![Image](https://github.com/user-attachments/assets/cb2d398b-2fe6-4710-ab7f-f3801c1bf18a)

# Mockup
![Image](https://github.com/user-attachments/assets/c6cc8bd8-9266-4826-be1e-872c821c93b1)

![Image](https://github.com/user-attachments/assets/bacc034a-d270-40d9-a035-01aa4725ba33)

![Image](https://github.com/user-attachments/assets/3257dfa4-ead8-4eb6-a1e0-7dcab12eba7e)

![Image](https://github.com/user-attachments/assets/62661e1f-6325-4e42-9a13-d9fe0ed09e8b)

![Image](https://github.com/user-attachments/assets/8a4312b0-0ed2-406e-976e-c103caaf38d2)

![Image](https://github.com/user-attachments/assets/6fa669b5-4d00-49ea-9765-94518f6f6872)

![Image](https://github.com/user-attachments/assets/013f7b5c-e683-4d82-b40d-07193ed5490f)

![Image](https://github.com/user-attachments/assets/b8b3f12a-3a4c-4970-adaa-03fbd2ee3f08)

![Image](https://github.com/user-attachments/assets/292b4e34-1046-4175-86cf-60a8044b7fed)

![Image](https://github.com/user-attachments/assets/36809176-3323-4dcf-8c1b-4a3576c66588)
