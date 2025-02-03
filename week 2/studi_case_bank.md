## Login ke Console Hasura

![alt](/img/console_hasura.png)

## Tambah Database

Setelah berhasil Login kehalaman console hasura, maka arahkan pada halaman data untuk menambah database baru. database yang digunakan adalah postgres yang sudah ditambahkan setting variable pada file docker-compose.yaml .

![alt](/img/tambah_database_hasura.png)

## Tambah Tabel

Pada studi case ini saya membuat 3 tabel yang berguna untuk menyimpan data nasabah bank.

1. Tabel Nasabah

   ![alt](/img/struktur_tabel_nasabah.png)

2. Tabel Rekening

   pada tabel rekening terdapat relasi ke tabel nasabah didalam column nasabah_id. relasi ini digunakan untuk mengaitkan data nasabah dengan data rekening.

   ![alt](/img/struktur_tabel_rekening.png)

3. Tabel Transaksi

   pada tabel transaksi terdapat relasi ke tabel rekenening dengan column rekening_id, relasi ini digunakan untuk mengaitkan data transaksi dengan data no rekening yang digunakan.

   ![alt](/img/struktur_tabel_transaksi.png)

## Insert data dalam tabel dengan SQL

1.  data nasabah

    ```
    INSERT INTO nasbah (name, email, phone, address)
    VALUES
    ('Budi Santoso', 'budi@email.com', '08123456789', 'Jakarta'),
    ('Siti Aisyah', 'siti@email.com', '08223456789', 'Bandung'),
    ('John Doe', 'john@email.com', '08323456789', 'Surabaya'),
    ('Rina Ayu', 'rina@email.com', '08423456789', 'Medan'),
    ('Mark Zuckerberg', 'mark@email.com', '08523456789', 'Semarang'),
    ('Elon Musk', 'elon@email.com', '08623456789', 'Yogyakarta'),
    ('Steve Jobs', 'steve@email.com', '08723456789', 'Malang'),
    ('Bill Gates', 'bill@email.com', '08823456789', 'Solo'),
    ('Larry Page', 'larry@email.com', '08923456789', 'Makassar'),
    ('Sergey Brin', 'sergey@email.com', '09023456789', 'Denpasar');
    ```

    hasilnya:

    ![alt](/img/hasil_insert_nasabah.png)

2.  data rekening

    ```
    INSERT INTO rekening (nasabah_id, no_rekening, type, saldo)
    VALUES
    (1, '1234567890', 'tabungan', 1000000),
    (2, '1234567891', 'tabungan', 1500000),
    (3, '1234567892', 'giro', 2000000),
    (4, '1234567893', 'tabungan', 3000000),
    (5, '1234567894', 'giro', 2500000),
    (6, '1234567895', 'tabungan', 500000),
    (7, '1234567896', 'giro', 750000),
    (8, '1234567897', 'tabungan', 1200000),
    (9, '1234567898', 'giro', 450000),
    (10, '1234567899', 'tabungan', 200000);
    ```

    hasilnya:

    ![alt](/img/hasil_insert_rekening.png)

3.  data transaksi

    ```
    INSERT INTO transaksi (rekening_id, type, total, description)
    VALUES
    (1, 'kredit', 500000, 'Setor tunai'),
    (2, 'debit', 300000, 'Tarik tunai'),
    (3, 'kredit', 1000000, 'Setor tunai'),
    (4, 'debit', 500000, 'Pembayaran tagihan'),
    (5, 'kredit', 800000, 'Setor tunai'),
    (6, 'debit', 250000, 'Tarik tunai'),
    (7, 'kredit', 500000, 'Setor tunai'),
    (8, 'debit', 150000, 'Pembayaran tagihan'),
    (9, 'kredit', 300000, 'Setor tunai'),
    (10, 'debit', 100000, 'Pembayaran tagihan');
    ```

    hasilnya:

    ![alt](/img/hasil_insert_transaksi.png)

## Query, Mutation, & Subcription

### Query

Melakukan query pada tabel nasabah, untuk mendapatkan data id, name, email, phone, address, created_at. hasilnya adalah:

![alt](/img/query_data_nasabah.png)

Melakukan query pada tabel rekening, yang memiliki relasi ke tabel nasabah, hasilnya adalah:

![alt](/img/query_data_rekening.png)

Melakukan query pada tabel transaksi yang mempunyai relasi dalam tabel transaksi, yang juga bisa mengambil data nasabah, hasilnya adalah:

![alt](/img/query_data_transaksi.png)
