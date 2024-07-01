# UAS { Pertemuan ke 16 } <img src=https://logos-download.com/wp-content/uploads/2016/05/MySQL_logo_logotype.png width="130px" >


## Profil
| Variable | Isi |
| -------- | --- |
| **Nama** | Wawan Suwandi |
| **NIM** | 312310457 |
| **Kelas** | TI.23.A5 |
| **Mata Kuliah** | Basis data |

# ER-D
![ER-D](https://github.com/Ws529/UAS-Basis-Data./assets/147570983/b2b5f5b6-4760-47c3-a94d-0cbb12e1261c)


# Input Data
![Tabel](https://github.com/Ws529/UAS-Basis-Data./assets/147570983/a9ccae9a-e348-4f40-a450-2fde67b633a5)


# Soal praktikum
Berdasarkan ERD dan Sampel Data diatas buatlah Query SQL untuk:
1. Menampilkan Nama Karyawan yang Berada di Departemen yang Dipimpin oleh Manajer dengan Nama 'Rika'
2. Menampilkan Nama Proyek yang dikerjakan oleh Karyawan dari Departemen 'RnD'
3. Menampilkan Nama Karyawan yang Terlibat dalam Lebih dari Satu Proyek
4. Menampilkan Nama Proyek yang melibatkan Karyawan terbanyak.
5. Menampilkan Nama Proyek yang Diikuti oleh Karyawan dengan Gaji Pokok Kurang dari 3 Juta

### 1. Menampilkan Nama Karyawan yang Berada di Departemen yang Dipimpin oleh Manajer dengan Nama 'Rika'
**Script :**

```
SELECT nik, nama, id_dept
FROM karyawan
WHERE id_dept = (SELECT id_dept FROM departemen WHERE manajer_nik = 'N03');
```

**Output :**


![Cuplikan layar 2024-07-01 111944](https://github.com/Ws529/UAS-Basis-Data./assets/147570983/c13f5c3a-fa0a-4a81-bf2a-8002c62a7dad)

### 2. Menampilkan Nama Proyek yang dikerjakan oleh Karyawan dari Departemen 'RnD'
**Script :**

```
SELECT project.nama AS 'Nama Project'
From Project
INNER JOIN project_detail ON project.id_proj = project_detail.id_proj
INNER JOIN Karyawan ON karyawan.nik = project_detail.nik
INNER JOIN Departemen ON karyawan.id_dept = Departemen.id_dept
WHERE Departemen.nama = 'RnD';
```

**Output :**

![Cuplikan layar 2024-07-01 112009](https://github.com/Ws529/UAS-Basis-Data./assets/147570983/678fd22a-3c6c-4453-a3bf-026d835ac302)

### 3. Menampilkan Nama Karyawan yang Terlibat dalam Lebih dari Satu Proyek
**Script :**

```
SELECT Karyawan.nama AS 'Nama Karyawan'
FROM project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
GROUP BY Karyawan.nama
HAVING COUNT(Project_detail.id_proj) > 1;
```

**Output :**

![Cuplikan layar 2024-07-01 112032](https://github.com/Ws529/UAS-Basis-Data./assets/147570983/f8b50a85-2fd4-4315-8ee7-f5148b59c86c)

### 4. Menampilkan Nama Proyek yang melibatkan Karyawan terbanyak.
**Script :**

```
SELECT Project.nama AS 'Nama Proyek', COUNT(Project_detail.nik) AS 'Jumlah Karyawan'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
GROUP BY Project.nama
ORDER BY COUNT(Project_detail.nik) DESC
LIMIT 1;
```

**Output :**

![Cuplikan layar 2024-07-01 112047](https://github.com/Ws529/UAS-Basis-Data./assets/147570983/c97ec83d-2485-4ba2-bd11-a86efdbd804d)

### 5. Menampilkan Nama Proyek yang Diikuti oleh Karyawan dengan Gaji Pokok Kurang dari 3 Juta
**Script :**

```
SELECT DISTINCT Project.nama AS 'Nama Proyek'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Karyawan.gaji_pokok < 3000000;
```

**Output :**


![Cuplikan layar 2024-07-01 112009](https://github.com/Ws529/UAS-Basis-Data./assets/147570983/a035be00-9bfb-4679-8b7a-8690f72bb800)
