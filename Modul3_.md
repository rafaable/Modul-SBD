## Modul X CHATGPT X W3SCHOOL
1. Tipe data & Parameter
   ```sql
   CREATE TABLE mahasiswa (
    id INT AUTO_INCREMENT PRIMARY KEY,                -- ID pakai primary key
    nim VARCHAR(15) NOT NULL,                         -- nim & nama NOT NULL
    nama VARCHAR(100) NOT NULL,
    age INT,
    CONSTRAINT chk_PersonAge CHECK (Age >= 18 AND City = 'Sandnes') 
    email VARCHAR(100) UNIQUE,                        -- email unique
    jenis_kelamin ENUM('L', 'P')                      -- cara pakai ENUM
    tanggal_lahir DATE,
    ipk DECIMAL(2,1)                                  -- desimal 2 digit, 1 angka di belakang koma
    alamat TEXT,
    status_aktif TINYINT(1) DEFAULT 1,                -- status pakai TINYINT
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
    City varchar(255) DEFAULT 'Sandnes'               -- ini cara pakai DEFAULT
   );
   ```
   
2. Constraint   
   PRIMARY KEY  
   FOREIGN KEY  
   NOT NULL  
   UNIQUE  
   CHECK  
   ```sql
   -- CHECK dalam range
   nilai INT CHECK (nilai >= 0 AND nilai <= 100)

   -- CHECK pilihan tertentu
   jenis_kelamin VARCHAR(1) CHECK (jenis_kelamin IN ('L', 'P'))

   -- Validasi panjang teks
   username VARCHAR(20) CHECK (CHAR_LENGTH(username) >= 5)
   ```
   DEFAULT  
   AUTO_INCREMENT
   ```sql
   ALTER TABLE Persons
   AUTO_INCREMENT = 100;
   -- maksudnya increment mulai angka 100
   ```
   
4. CREATE
   ```sql
   CREATE DATABASE IF NOT EXISTS kelas_a;

   CREATE TABLE mahasiswa (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100),
    email VARCHAR(100),
    tanggal_lahir DATE
   );

   DELIMITER //
   CREATE FUNCTION hitung_umur(tgl_lahir DATE)
   RETURNS INT
   DETERMINISTIC
   BEGIN
   RETURN YEAR(CURDATE()) - YEAR(tgl_lahir);
   END //
   DELIMITER ;

   DELIMITER //
   CREATE PROCEDURE tampil_mahasiswa()
   BEGIN
   SELECT * FROM mahasiswa;
   END //
   DELIMITER ;
   -- cara panggilnya kayak gini
   CALL tampil_mahasiswa();
5. Alter
   - Nambah kolom
     ```sql
     ALTER TABLE mahasiswa
     ADD alamat TEXT;
     ```
   - Hapus kolom
     ```sql
     ALTER TABLE mahasiswa
     DROP COLUMN alamat;
     ```
   - MODIFY tipe data kolom
     ```sql
     ALTER TABLE mahasiswa
     MODIFY nama VARCHAR(150);
     ```
   - CHANGE nama kolom
     ```sql
     ALTER TABLE mahasiswa
     CHANGE COLUMN nama nama_lengkap VARCHAR(150);
     ```
     kalau dari w3school kek gini
     ```sql
     ALTER TABLE table_name
     RENAME COLUMN old_name to new_name;
     ```
   - Nambahin constraint CHECK
     ```sql
     ALTER TABLE Members
     ADD CONSTRAINT CHK_Age CHECK (Age >= 18);
     ```
   - Nambahin constraint DEFAULT
     ```sql
     ALTER TABLE Persons
     ADD CONSTRAINT df_City DEFAULT 'Sandnes' FOR City;
     ```
   - DROP CONSTRAINT
     ```SQL
     ALTER TABLE Persons
     DROP CONSTRAINT df_City;
     ```
   - Nambah constraint "PK" ke kolom yang sudah ada
     ```sql
     CREATE TABLE mahasiswa (
     nim VARCHAR(15),
     nama VARCHAR(100)
     );

     ALTER TABLE mahasiswa
     ADD PRIMARY KEY (nim); 
     ```
   - Nambahin "composite key"  
     Cara 1
     ```sql
     CREATE TABLE Persons (
     ID int,
     LastName varchar(255),
     FirstName varchar(255),
     Age int,
     CONSTRAINT PK_Person PRIMARY KEY (ID, LastName)
     );
     ```
     Cara 2 
     ```sql
     CREATE TABLE krs (
     nim VARCHAR(15),
     kode_mk VARCHAR(10)
     );

     ALTER TABLE krs
     ADD PRIMARY KEY (nim, kode_mk);
     ```
   - Ganti PK
     ```sql
     CREATE TABLE produk (
     id INT,
     nama VARCHAR(100),
     PRIMARY KEY (id)
     );

     ALTER TABLE produk
     DROP PRIMARY KEY,
     ADD PRIMARY KEY (nama);
     ```
   - Nambah constraint "FK"
     ```sql
     ALTER TABLE orders
     ADD CONSTRAINT fk_user
     FOREIGN KEY (user_id) REFERENCES users(id);
     -- user_id itu nama kolom di tabel orders
     ```
     Nambahin FK bisa error kalau `user_id` belum di index, errornya kayak gini :  
     > Cannot add foreign key constraint  
     Kita harus cek dulu
     ```sql
     SHOW INDEX FROM orders;
     ```
     Kalau user_id nggak ada, berarti belum di-index
     ```sql
     -- solusinya gini, tambahin index dulu
     ALTER TABLE orders
     ADD INDEX (user_id);
     
     -- baru nambahin fk
     ALTER TABLE orders
     ADD FOREIGN KEY (user_id) REFERENCES users(id);
     ```
   - Hapus/DROP constraint FK
     Cara cek constraint kalau sebelumnya belum buat
     ```sql
     SHOW CREATE TABLE orders;
     ```
     Nanti bakal muncul  
     > CONSTRAINT `orders_ibfk_1` FOREIGN KEY (`user_id`) ...  
     Baru deh dihapus, hapusnya pakai nama constraint, jadi kita udah harus tau constraintnya
     ```sql
     ALTER TABLE orders
     DROP FOREIGN KEY orders_ibfk_1;
     ```
   - Nambah FK dengan aturan ( CASCADE )
     ```sql
     ALTER TABLE orders
     ADD CONSTRAINT fk_user
     FOREIGN KEY (user_id) REFERENCES users(id)
     ON DELETE CASCADE
     ON UPDATE CASCADE;
     ```
     misal di kolom user kita hapus/update yang id = 1,  
     otomatis di kolom orders, baris yang user_id = 1 ikut kehapus/keupdate
   - Ubah constraint, misal dari NOT NULL ke NULL
     ```sql
     ALTER TABLE Persons
     MODIFY COLUMN Age int NULL; 
     ```
   - Rename tabel
     ```sql
     ALTER TABLE mahasiswa
     RENAME TO mahasiswa_baru;
     ```
   - Drop tabel
     ```sql
     DROP TABLE table_name;
     ```
   - Tambah kolom dengan posisi tertentu
     ```sql
     ALTER TABLE mahasiswa
     ADD umur INT AFTER nama;
     ```
   - Notes soal ALTER PK & FK
     - ADD itu harus sebut tipe data dan batas parameternya ya!
     - MODIFY itu ubah tipe data CHANGE itu ubah nama & tipe.   
       Hari hari kalau ubah tipe data, apalagi kalau kolom udah keisi,  
       nanti bisa error/kepotong  
     - misal kolom `nama` dijadikan PK, berarti `nama` harus unik dan tidak NULL
   - Create Index
     ```sql
     CREATE INDEX idx_lname_fname
     ON Persons (LastName, FirstName);
     ```
   - Drop index
     ```sql
     ALTER TABLE table_name
     DROP INDEX index_name;
     ``` 
  6. Ceritanya bikin tabel baru GermanCustomers yang ngefilter dari tabel Customers
     ```sql
     CREATE TABLE GermanCustomers AS
     SELECT * FROM Customers
     WHERE Country = 'Germany';
     ```
### Latsol Seslab
```sql
CREATE DATABASE IF NOT EXISTS data_kampus;
USE data_kampus;


-- Membuat tabel parent untuk contoh FOREIGN KEY
CREATE TABLE jurusan (
    id_jurusan INT PRIMARY KEY,
    nama_jurusan VARCHAR(50) NOT NULL UNIQUE
);


-- Membuat tabel mahasiswa dengan IMPLEMENTASI SEMUA CONSTRAINTS di Modul 3
-- Yaitu: PRIMARY KEY, NOT NULL, UNIQUE, CHECK, DEFAULT, & FOREIGN KEY
CREATE TABLE mahasiswa (
    nrp VARCHAR(15) PRIMARY KEY,
    nama_mahasiswa VARCHAR(100) NOT NULL,
    nomor VARCHAR(15) UNIQUE,
    tanggal_lahir DATE,
    jenis_kelamin CHAR(1) CHECK (jenis_kelamin IN ('L', 'P')),
    status_aktif VARCHAR(20) DEFAULT 'Aktif',
    id_jurusan INT,
    FOREIGN KEY (id_jurusan) REFERENCES jurusan(id_jurusan)
);


-- Memasukkan data awal (INSERT)
INSERT INTO jurusan (id_jurusan, nama_jurusan) VALUES
(1, 'Informatika'),
(2, 'Sistem Informasi');


INSERT INTO mahasiswa (nrp, nama_mahasiswa, nomor, tanggal_lahir, jenis_kelamin, id_jurusan)
VALUES
('5025211001', 'Arif Rahman', '08111111111', '2003-05-14', 'L', 1),
('5025211002', 'Bunga Larasati', '08222222222', '2002-11-20', 'P', 2),
('5025211003', 'Citra Kirana', '08333333333', '2003-01-05', 'P', 1),
('5025211004', 'Dika Pratama', '08444444444', '2001-08-17', 'L', 2);
```
### Latsol Asistensi
<img width="649" height="435" alt="image" src="https://github.com/user-attachments/assets/9db5c797-a57e-49b2-9fda-57401403a758" /><br>  
- buat tabel di sql, wajib beserta constraint nya
- buat report pengerjaan kalian yang berisi querry” yang kalian buat
- buat simulasi drop table merchant, dan truncate AKUN, serta add column alamat di tabel AKUN

```sql
-– buat database
CREATE DATABASE IF NOT EXISTS e_commerce;
USE e_commerce;

-– buat tabel yang tidak butuh foreign key lebih dulu, satu per satu
CREATE TABLE akun (
id_akun INT PRIMARY KEY,
nama_akun VARCHAR(50) NOT NULL,
no_telepon VARCHAR(15) UNIQUE,
email VARCHAR(100) UNIQUE,
password VARCHAR(20)
);

CREATE TABLE merchant (
id_merchant INT PRIMARY KEY,
nama_merchant VARCHAR(50) NOT NULL,
rating_merchant INT
CHECK (rating_merchant IN (‘1’, ‘2’, ‘3’, ‘4’, ‘5’)),
lokasi_merchant VARCHAR(100)
);

CREATE TABLE driver (
id_driver INT PRIMARY KEY,
nama_driver VARCHAR(50) NOT NULL,
rating_driver INT
CHECK (rating_driver IN (‘1’, ‘2’, ‘3’, ‘4’, ‘5’))
);

-– buat junction table
CREATE TABLE pesanan (
id_pesanan INT PRIMARY KEY,
FOREIGN KEY (id_akun) REFERENCES akun(id_akun),
FOREIGN KEY (id_merchant) REFERENCES merchant(id_merchant),
FOREIGN KEY (id_driver) REFERENCES driver(id_driver),
tanggal_pemesanan DATE
);

–- tabel ini dibuat terakhir karena butuh FK dari junction table, shg junction table dibuat lebih
dulu
CREATE TABLE pembayaran (
id_pembayaran INT PRIMARY KEY,
FOREIGN KEY (id_pesanan) REFERENCES pesanan(id_pesanan),
Metode_pembayaran VARCHAR(10)
CHECK (metode_pembayaran IN (‘transfer’, ‘cash’, ‘qris’),
Total INT
);

-- Untuk drop tabel bisa menggunakan
ALTER TABLE pesanan
DROP FOREIGN KEY pesanan_ibfk_2;
DROP TABLE merchant;

-- Untuk truncate akun
TRUNCATE TABLE akun;

-- Untuk add column alamat di akun
ALTER TABLE akun
ADD ALAMAT VARCHAR(100);
```



     
     
