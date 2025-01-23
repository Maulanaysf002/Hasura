# Linux command to check RAM capacity, CPU and Hardisk speed

## Jalankan VM di Virtualbox, lalu lakukan ssh di terminal

**VirtualBox** adalah perangkat lunak virtualisasi yang memungkinkan pengguna untuk menjalankan beberapa sistem operasi (OS) secara bersamaan pada satu komputer fisik. Dengan VirtualBox, Kita dapat membuat dan mengelola mesin virtual (virtual machine/VM), yang merupakan lingkungan komputer yang terisolasi di dalam komputer utama (host).

**SSH (Secure Shell)** adalah protokol jaringan yang digunakan untuk mengakses dan mengelola perangkat atau server secara aman melalui jaringan yang tidak aman. SSH menyediakan enkripsi untuk komunikasi antara klien dan server, sehingga data yang dikirimkan terlindungi dari penyadapan atau manipulasi oleh pihak ketiga.

Hasil SSH:
![ssh server kantor 1](/img/ssh_server_kantor_1.png)

## Membuat Contoh Directory

saya membuat `Project_Sistem_Perpustakaan` dengan urutan directory seperti dibawah ini:

Direktori: Project_Sistem_Perpustakaan

Direktori Folder:

- documents
- data
- scripts
- reports

Sub-Direktori:

- Documents:
  - books
  - members
  - transactions
- Data:
  - raw_data
  - processed_data
  - backup
- Scripts:
  - python
  - bash
- Reports:
  - monthly
  - annual
- File Direktori:
  - books:
    - daftar_buku.txt
    - kategori_buku.txt
  - members:
    - anggota_aktif.txt
    - anggota_nonaktif.txt
  - transactions:
    - peminjaman.txt
    - pengembalian.txt
  - raw_data:
    - data_awal.csv
  - processed_data:
    - data_bersih.csv
  - monthly:
    - january_report.txt
    - february_report.txt
  - annual:
    - 2024_report.txt
    - 2025_report.txt

## Membuat Contoh Direktori di Linux dengan Ubuntu Server

### Membuat direktori dan sub-direktori :

perintah:

```bash
mkdir -p Project_Sistem_Perpustakaan/documents/books Project_Sistem_Perpustakaan/documents/members Project_Sistem_Perpustakaan/documents/transaction

mkdir -p Project_Sistem_Perpustakaan/data/raw_data Project_Sistem_Perpustakaan/data/processed_data Project_Sistem_Perpustakaan/data/backup

mkdir -p Project_Sistem_Perpustakaan/scripts/python Project_Sistem_Perpustakaan/scripts/bash

mkdir -p Project_Sistem_Perpustakaan/reports/monthly Project_Sistem_Perpustakaan/reports/annual
```

**penjelasan:**

perintah mkdir -p akan membuat folder serta subfoldernya.

**hasil:**
![alt](/img/membuat_folder_dan_subfolder.png)

### Membuat File Kosong Menggunakan `touch`

gunakan perintah dibawah:

```bash
touch Project_Sistem_Perpustakaan/documents/books/daftar_buku.txt Project_Sistem_Perpustakaan/documents/books/kategori_buku.txt

touch Project_Sistem_Perpustakaan/documents/members/anggota_aktif.txt Project_Sistem_Perpustakaan/documents/members/anggota_nonaktif.txt

touch Project_Sistem_Perpustakaan/documents/transaction/peminjaman.txt Project_Sistem_Perpustakaan/documents/transaction/pengembalian.txt

touch Project_Sistem_Perpustakaan/data/raw_data/data_awal.csv

touch Project_Sistem_Perpustakaan/data/processed_data/data_bersih.csv

touch Project_Sistem_Perpustakaan/reports/monthly/january_report.txt Project_Sistem_Perpustakaan/reports/monthly/februari_report.txt

touch Project_Sistem_Perpustakaan/reports/annual/2024_report.txt Project_Sistem_Perpustakaan/reports/annual/2025_report.txt
```

hasilnya:

![alt](/img/membuat_folder_dan_subfolder.png)

### menambahkan isi di dalam file

perintahnya:

```bash
echo "Daftar Peminjam Buku" > Project_Sistem_Perpustakaan/documents/transaction/peminjaman.txt

echo "Daftar Pengembalian Buku" > Project_Sistem_Perpustakaan/documents/transaction/pengembalian.txt
```

hasilnya:
![alt](/img/masukan_isi_file.png)

### Menjalankan perintah ls, mv, rm dan tree

#### menampilkan daftar directory dengan perintah `ls`

```bash
ls Project_Sistem_Perpustakaan
```

**hasilnya :**

![ls sistem perpustakaan](/img/ls_project_perpustakaan.png)

```bash
ls -l Project_Sistem_Perpustakaan
```

**hasilnya :**

![ls -l sistem perpustakaan](/img/ls_l_project_perpustakaan.png)

#### memindahkan file dengan perintah `mv`

untuk memindahkan file `2024_report.txt` dari `Project_Sistem_Perpustakaan/reports/annual` ke folder `Project_Sistem_Perpustakaan/reports/monthly/`

```bash
 mv Project_Sistem_Perpustakaan/reports/annual/2024_report.txt Project_Sistem_Perpustakaan/reports/monthly/
```

#### mengganti nama file dengan perintah `mv`

untuk mengubah nama file `anggota_nonaktif.txt` dari `Project_Sistem_Perpustakaan/documents/members` menjadi `anggota_tidakAktif.txt`

```bash
mv Project_Sistem_Perpustakaan/documents/members/anggota_nonaktif.txt Project_Sistem_Perpustakaan/documents/members/anggota_tidakAktif.txt
```

#### Menghapus Direktori dan File menggunakan perintah `rm`

untuk menghapus nama file `data_awal.csv` dari `Project_Sistem_Perpustakaan/data/raw_data/`

```bash
rm Project_Sistem_Perpustakaan/data/raw_data/data_awal.csv
```

#### Melihat Struktur Folder directory dengan `tree`

```bash
tree Project_Sistem_Perpustakaan
```

hasilnya adalah:
![alt](/img/tree_command.png)

## Mengecek Kapasitas RAM

### untuk mengecek kapasitas ram gunakan perintah:

```bash
free -h
```

Perintah free menampilkan informasi mengenai penggunaan memori di sistem.

Opsi -h (human-readable) membuat output lebih mudah dibaca dengan menampilkan ukuran dalam format yang lebih mudah dipahami (KB, MB, GB).

Hasil Output:

![alt](/img/free_h_command.png)

### Untuk menampilkan hasil lebih detail gunakan

```bash
cat /proc/meminfo
```

hasil outputnya:

![alt](/img/cat_proc_meminfo_command.png)

## Mengecek Kapasitas CPU

### Untuk mengecek kapasitas CPU dalam sistem dapat menggunakan perintah:

```bash
lscpu
```

perintah lscpu menampilkan informasi detail mengenai arsitektur CPU, jumlah core, thread, kecepatan CPU, dan banyak lagi.

Hasil Output:
![alt](/img/lscpu_command.png)

### Untuk menampilkan informasi lebih rinci dapat menggunakan perintah:

```bash
cat /proc/cpuinfo
```

Perintah ini menampilkan informasi rinci mengenai setiap core CPU, termasuk model, kecepatan, dan cache.

Hasil Outputnya:
![alt](/img/cat_proc_cpuinfo_command.png)

## Mengecek Kecepatan Hard Disk

Untuk mengecek kecepatan Baca/Tulis Hard Disk, dapat menggunakan perintah `hdparm`:

```bash
sudo hdparm -Tt /dev/sda
```

Perintah ini akan melakukan benchmark pada hard disk yang berada di /dev/sda.

Opsi -T mengukur kecepatan akses cache (buffered), sedangkan -t mengukur kecepatan baca langsung dari disk (disk read).

Hasil Outputnya:
![alt](/img/cek_kecepatan_hard_disk.png)
