## SQL PRAKTIKUM5 

```
CREATE TABLE mahasiswa (
    nim VARCHAR(10) PRIMARY KEY,
    nama VARCHAR(50),
    jk CHAR(1),
    tgl_lahir DATE,
    jalan VARCHAR(100),
    kota VARCHAR(50),
    kodepos VARCHAR(10),
    no_hp VARCHAR(15),
    kd_ds VARCHAR(10)
);
```
```
Dosen
CREATE TABLE dosen (
    kd_ds VARCHAR(10) PRIMARY KEY,
    nama VARCHAR(50)
);
```
```
CREATE TABLE matakuliah (
    kd_mk VARCHAR(10) PRIMARY KEY,
    nama VARCHAR(50),
    sks INT
);
```
```
CREATE TABLE jadwal_mengajar (
    kd_mk VARCHAR(10),
    kd_ds VARCHAR(10),
    hari VARCHAR(10),
    jam TIME,
    ruang VARCHAR(50),
    PRIMARY KEY (kd_mk, kd_ds, hari, jam)
);
```
```
CREATE TABLE krs_mahasiswa (
    nim VARCHAR(10),
    kd_mk VARCHAR(10),
    kd_ds VARCHAR(10),
    PRIMARY KEY (nim, kd_mk)
);
```
```
INSERT INTO mahasiswa (nim, nama, jk, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds) VALUES 
('1812345', 'Ari Santoso', 'L', '1999-10-11', NULL, 'Bekasi', NULL, NULL, 'DS002'),
('1823456', 'Dina Marlina', 'P', '1998-11-20', NULL, 'Jakarta', NULL, NULL, NULL),
('1834567', 'Rahmat Hidayat', 'L', '1999-05-10', NULL, 'Bekasi', NULL, NULL, NULL),
('1845678', 'Jaka Sampurna', 'L', '2000-10-19', NULL, 'Cikarang', NULL, NULL, NULL),
('1856789', 'Tia Lestari', 'P', '1999-02-15', NULL, 'Karawang', NULL, NULL, NULL),
('1867890', 'Anton Sinaga', 'L', '1998-06-22', NULL, 'Bekasi', NULL, NULL, NULL),
('1912345', 'Listia Nastiti', 'P', '2001-10-23', NULL, 'Jakarta', NULL, NULL, 'DS004'),
('1923456', 'Amira Jarisa', 'P', '2001-01-24', NULL, 'Karawang', NULL, NULL, NULL),
('1934567', 'Laksana Mardito', 'L', '1999-04-14', NULL, 'Cikarang', NULL, NULL, NULL),
('1945678', 'Jura Marsina', 'P', '2000-05-10', NULL, 'Cikarang', NULL, NULL, NULL),
('1956789', 'Dadi Martani', 'L', '2001-08-29', NULL, 'Bekasi', NULL, NULL, 'DS005'),
('1967890', 'Bayu Laksono', 'L', '1999-07-22', NULL, 'Cikarang', NULL, NULL, 'DS004');
```
```
INSERT INTO dosen (kd_ds, nama) VALUES 
('DS001', 'Nofal Arianto'),
('DS002', 'Ario Talib'),
('DS003', 'Ayu Rahmadina'),
('DS004', 'Ratna Kumala'),
('DS005', 'Vika Prasetyo');
```
```
INSERT INTO matakuliah (kd_mk, nama, sks) VALUES 
('MK001', 'Algoritma Dan Pemrograman', 3),
('MK002', 'Praktikum Algoritma Dan Pemrograman', 1),
('MK003', 'Teknologi Basis Data', 3),
('MK004', 'Praktikum Teknologi Basis Data', 1),
('MK005', 'Pemrograman Dasar', 3),
('MK006', 'Pemrograman Berorientasi Objek', 3),
('MK007', 'Struktur Data', 3),
('MK008', 'Arsitektur Komputer', 2);
```
```
INSERT INTO jadwal_mengajar (kd_mk, kd_ds, hari, jam, ruang) VALUES 
('MK001', 'DS002', 'Senin', '10:00:00', '102'),
('MK002', 'DS002', 'Senin', '13:00:00', 'Lab. 01'),
('MK003', 'DS001', 'Selasa', '08:00:00', '201'),
('MK004', 'DS001', 'Rabu', '10:00:00', 'Lab. 02'),
('MK005', 'DS003', 'Selasa', '10:00:00', 'Lab. 01'),
('MK006', 'DS004', 'Kamis', '09:00:00', 'Lab. 03'),
('MK007', 'DS005', 'Rabu', '08:00:00', '102'),
('MK008', 'DS005', 'Kamis', '13:00:00', '201');
```
```
INSERT INTO krs_mahasiswa (nim, kd_mk, kd_ds) VALUES 
('1812345', 'MK001', 'DS002'),
('1823456', 'MK002', 'DS002'),
('1834567', 'MK003', 'DS001'),
('1845678', 'MK004', 'DS001'),
('1856789', 'MK005', 'DS003'),
('1867890', 'MK006', 'DS004'),
('1912345', 'MK007', 'DS005'),
('1923456', 'MK008', 'DS005');
```
## JOIN OPERATIONS
    ## JOIN MAHASISWA AND DOSEN
```
SELECT m.nim, m.nama AS mahasiswa_nama, m.jk, m.tgl_lahir, m.kota, d.nama AS dosen_nama
FROM mahasiswa m
LEFT JOIN dosen d ON m.kd_ds = d.kd_ds;
```
    ## JOIN MATAKULIAH AND DOSEN
```
SELECT mk.kd_mk, mk.nama AS matakuliah_nama, mk.sks, d.nama AS dosen_nama
FROM matakuliah mk
JOIN jadwal_mengajar jm ON mk.kd_mk = jm.kd_mk
JOIN dosen d ON jm.kd_ds = d.kd_ds;
```
    ## Join JadwalMengajar, Dosen, and Matakuliah
```
SELECT jm.kd_mk, mk.nama AS matakuliah_nama, jm.kd_ds, d.nama AS dosen_nama, jm.hari, jm.jam, jm.ruang
FROM jadwal_mengajar jm
JOIN dosen d ON jm.kd_ds = d.kd_ds
JOIN matakuliah mk ON jm.kd_mk = mk.kd_mk;
```
    ## Join KrsMahasiswa, Mahasiswa, Matakuliah, and Dosen
```
SELECT k.nim, m.nama AS mahasiswa_nama, k.kd_mk, mk.nama AS matakuliah_nama, mk.sks, k.kd_ds, d.nama AS dosen_nama
FROM krs_mahasiswa k
JOIN mahasiswa m ON k.nim = m.nim
JOIN matakuliah mk ON k.kd_mk = mk.kd_mk
JOIN dosen d ON k.kd_ds = d.kd_ds;
```
