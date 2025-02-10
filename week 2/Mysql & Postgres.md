# MySQL

MySQL adalah sistem manajemen basis data relasional (RDBMS) open-source yang berbasis Structured Query Language (SQL). MySQL digunakan untuk menyimpan, mengelola, dan mengambil data dalam berbagai jenis aplikasi, mulai dari website hingga sistem perusahaan skala besar.

Fitur Utama MySQL

- **Relational Database**: Menggunakan tabel dengan hubungan antar tabel.
- **SQL-Based**: Menggunakan SQL untuk manipulasi data.
- **Open-Source**: Gratis digunakan, tetapi juga tersedia versi berbayar dengan fitur tambahan (MySQL Enterprise).
- **Cepat dan Efisien**: Cocok untuk berbagai aplikasi, dari website kecil hingga sistem besar.
- **Support Multi-User**: Bisa digunakan oleh banyak pengguna secara bersamaan.
- **Keamanan Tinggi**: Mendukung otentikasi dan enkripsi data.

## installasi MySQL di Docker

1. pull image mysql dari docker-hub

   `docker pull mysql:latest`

   lalu periksa dengan perintah:

   `docker images`

   hasilnya adalah:

   ![alt](/img/pull_image_mysql.png)

2. buat sebuah container untuk image mysql dengan perintah

   `docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=mypw123 -d mysql:latest`

   - docker run: Perintah untuk menjalankan container . --name mysql-container: Memberi nama container sebagai mysql-container.

   - -e MYSQL_ROOT_PASSWORD=mypw123: Mengatur password root MySQL. (Bisa Pakai password sendiri)

   - -d: Menjalankan container di background.

   - mysql:latest: Menentukan image yang digunakan, dalam hal ini mysql versi latest.

   hasilnya adalah:

   ![alt](/img/run_container_mysql.png)

3. Masuk ke dalam shell yang ada dalam container mysql untuk mengelola mysql.

   perintahnya adalah:

   `docker exec -it mysql-container mysql -u root -p`

   - docker exec: Perintah untuk menjalankan command di dalam container.

   - -it: Membuka sesi interaktif (interactive terminal).

   - mysql-container: Nama container yang ingin diakses.

   - mysql -u root -p: Perintah untuk masuk ke shell MySQL dengan user root

   - setelah mengeksekusi perintah tersebut akan diminta untuk memasukan password yang sudah ditetapkan saat membuat container.

   hasilnya:

   ![alt](/img/masuk_ke_mysql.png)

## Membuat database

untuk membuat database baru bisa menggunakan perintah sql seperti biasanya. contohnya membuat database mahasiswa.

`CREATE DATABASE mahasiswa;`

lalu lihat database dengan perintah:

`SHOW DATABASES;`

hasilnya adalah:

![alt](/img/membuat_database_mysql.png)

## Membuat tabel dan memasukan data

langkah pertama masuk kedalam database yang ingin digunakan dengan perintah

`USE <database name>;`

contoh membuat tabel baru menggunakan perintah sql:

```sql
CREATE TABLE kelas (
id INT AUTO_INCREMENT PRIMARY KEY,
nama_kelas VARCHAR(100) NOT NULL,
lokasi VARCHAR(100) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
)
```

hasilnya adalah:

![alt](/img/membuat_table_di_mysql.png)

insert data dalam tabel yang sudah ada:

```
INSERT INTO kelas (nama_kelas, lokasi) VALUES
('Kelas A', 'Gedung 1'),
('Kelas B', 'Gedung 2'),
('Kelas C', 'Gedung 3');
```

hasilnya adalah:

![alt](/img/insert_data_mysql.png)

## Melihat data dalam tabel

lihat data dalam database menggunakan perintah sql:

`SELECT * FROM kelas`

hasilnya adalah

![alt](/img/menampilkan_data_tabel_kelas.png)

# PostgreSQL

PostgreSQL (sering disebut Postgres) adalah sistem manajemen basis data relasional (RDBMS) open-source yang kuat dan fleksibel. PostgreSQL terkenal karena kepatuhannya terhadap standar SQL, fitur tingkat lanjut, serta dukungan untuk data dalam jumlah besar dan transaksi yang kompleks.

Fitur Utama PostgreSQL:

- **Relational & Object-Oriented** – PostgreSQL mendukung model basis data relasional dan fitur pemrograman berbasis objek.
- **ACID Compliance** – Mendukung transaksi yang aman dan konsisten dengan properti Atomicity, Consistency, Isolation, Durability (ACID).
- **Extensibility** – Bisa diperluas dengan tipe data, fungsi, dan prosedur yang didefinisikan oleh pengguna.
  JSON & NoSQL Support – PostgreSQL mendukung JSONB untuk menyimpan data semi-terstruktur, sehingga bisa digunakan untuk skenario mirip NoSQL.
- **Concurrency Control** – Menggunakan MVCC (Multi-Version Concurrency Control) untuk menghindari locking saat banyak transaksi terjadi.
- **Full-Text Search** – Mendukung pencarian teks yang efisien, mirip dengan fitur search engine.
- **Replication & High Availability** – Mendukung master-slave replication dan failover untuk memastikan sistem tetap berjalan saat terjadi gangguan.

## installasi Postgres di Docker

1. pull image dari docker-hub

   `docker pull postgres:latest`

2. membuat container postgres

   `docker run --name postgres-container -e POSTGRES_PASSWORD=mypw123 -d postgres:latest`

3. hubungkan ke shell yang ada di container postgres

   `docker exec -it postgres-container psql -U postgres`

   untuk postgres database saya sudah menginstallnya menggunakan docker-compose bersamaan saat install hasura. maka perintah yang saya gunakan adalah

   `docker exec -it hasura-postgres-1 psql -U postgres`

   hasilnya adalah:

   ![alt](/img/menjalankan_postgres_dicontainer.png)

## Membuat database

untuk membuat database di postgres dapat menggunakan perintah:

`CREATE DATABASE kampus;`

hasilnya adalah

![alt](/img/postgres_create_database_kampus.png)

melihat database dalam postgres dengan perintah

`\l`

hasilnya adalah:

![alt](/img/postgres_melihat_database.png)

## Membuat tabel dan memasukan data

membuat tabel dalam postgres bisa menggunakan sql hanya saja beberapa tipe data berbeda dari mysql. langkahnya adalah:

1. masuk ke database yang ingin digunakan

   `\c <database-name>`

   hasilnya:

   ![alt](/img/postgres_gunakan_database_kampus.png)

2. membuat tabel untuk kelas

   ```sql
   CREATE TABLE kelas (
    id SERIAL PRIMARY KEY,
    nama_kelas VARCHAR(100) NOT NULL,
    lokasi VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

   hasilnya adalah:

   ![alt](/img/postgres_create_table_kelas.png)

3. memasukan value ke dalam tabel kelas

   ```sql
   INSERT INTO kelas (nama_kelas, lokasi) VALUES
   ('Informatika A', 'Gedung 1'),
   ('Sistem Informasi B', 'Gedung 2'),
   ('Teknologi Informasi C', 'Gedung 3');
   ```

   hasilnya adalah:

   ![alt](/img/postgres_insert_tabel_kelas.png)

## Melihat data dalam tabel

untuk melihat datanya bisa menggunakan perintah sql seperti

`SELECT * FROM kelas`

![alt](/img/postgres_select_from_kelas.png)
