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
Admin sebagai aktor tunggal

# Link Youtube 
https://github.com/Kyaraazwa/UTS_APBO_-A-/blob/main/README.md

# Usecase
![Image](https://github.com/user-attachments/assets/507c630b-6c5f-4255-b575-e28729c14d17)

# Entity Relationship Diagram
![Image](https://github.com/user-attachments/assets/5e4b844e-2946-4632-af16-2b85fcfab11d)

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
| Status           | ENUM('Diproses', 'Selesai', 'Batal') | Status pemesanan                   |
| Waktu_Pemsanan   | DATETIME                             | tanggal pemesanan                  |

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
![Image](https://github.com/user-attachments/assets/78fd9bd1-9dae-412b-b358-353dc5dd39c7)

# Sequence Diagram
SEQUENCE DIAGRAM PELANGGAN 
![Image](https://github.com/user-attachments/assets/5c820735-0ff8-4342-a8da-8e56bce1f398)

SEQUENCE DIAGRAM JENIS PAKET
![Image](https://github.com/user-attachments/assets/46c47617-a043-4f85-a67b-1327e149ad7a)

SEQUENCE DIAGRAM LAYANAN 
![Image](https://github.com/user-attachments/assets/fe421f07-3a40-4406-9a8a-d66b34158236)

SEQUENCE DIAGRAM PESANAN
![Image](https://github.com/user-attachments/assets/40ff7a35-e73a-4e09-b9e6-7dc70040efbb)

SEQUENCE DIAGRAM PEMBAYARAN 
![Image](https://github.com/user-attachments/assets/4eb6cd0b-0a38-45ed-9391-544dd4df57e5)


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
![Image](https://github.com/user-attachments/assets/bd4dedb6-b7ef-4f6f-bfa4-67a42bf38d60)

![Image](https://github.com/user-attachments/assets/3dc71f51-d844-47c9-99aa-36291fad37e1)

![Image](https://github.com/user-attachments/assets/bfd8c429-16f7-46d6-af87-5156f8149872)

![Image](https://github.com/user-attachments/assets/8d989ff3-cb9f-420e-bf91-d7bd91f061e4)

![Image](https://github.com/user-attachments/assets/4c645212-d3c1-4ec8-9521-2794a6f1a46b)

![Image](https://github.com/user-attachments/assets/b4ecc49f-9cae-4145-b83d-47abbcd4b6cf)

![Image](https://github.com/user-attachments/assets/8fe9ca78-8e02-4aa9-a0d6-ff733d547dce)

![Image](https://github.com/user-attachments/assets/2a2c9c1a-22fd-4559-970c-bda3790c47da)

![Image](https://github.com/user-attachments/assets/c7db24b7-7728-4e89-bcc2-03143e998fe2)

![Image](https://github.com/user-attachments/assets/a7cdef02-f7bc-4934-bcc0-047df21cdc93)
