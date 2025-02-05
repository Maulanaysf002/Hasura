# Pengertian Redis

Redis adalah singkatan dari **remote dictionary server**.

Redis adalah **sistem basis data atau dbms yang berbasis key value** yang menyimpan datanya pada memory (ram).

Redis dirilis pertama kali tahun 2009 sebagai project open source.

website official redis adalah [redis.io](https://www.redis.io)

## Key-Value Database

selain database sql, dikenal juga database no-sql yang artinya adalah not only sql. Redis ini merupakan database no-sql yang berbasis pair (key-value) database.

Key mirip dengan **primary key** dari data, sedangkan value adalah isi dari datanya.

![alt](/img/redis_key_value_db.png)

pada contoh diatas terdapat 5 key (k1,k2,k3,k4,k5) yang diibaratkan primary key. lalu setiap key memiliki value yang bisa lebih dari satu dan beragam.

cara mengambil datanya menggunakan keynya tidak bisa langsung dari valuenya.

## In-memory Database

kenapa redis menyimpan datanya dalam memory bukan disk?

Redis menyimpan datanya di memory, namun kita bisa memintanya untuk menyimpan datanya secara regular permanen di disk. Data di disk hanya dijadikan backup ketika redis berjalan ulang, selama redis berjalan, redis hanya akan melakukan manipulasi data ke memory

![alt](/img/in_memori_database.png)

# Penggunaan Redis

Redis biasanya digunakan jika ada kasus tertentu.

## Kasus 1, Ketika Database Lambat

![alt](/img/kasus_redis_database_lambat.png)

pada kasus ini hasil data yang diambil dari database utama akan di chace menggunakan redis dalam waktu tertentu, hal ini dapat meringankan kinerja aplikasi, karena dalam waktu tertentu jika user melakukan query yang sama tidak akan membebani database.

## kasus 2, Ketika Aplikasi Lain lambat

![alt](/img/kasus_redis_aplikasilain_lambat.png)

pada kasus ini aplikasi lain yang terhubung pada aplikasi kita sangat lambat, sehingga menggunakan redis untuk melakukan chace data hasil query dari aplikasi lain, jika user melakukan query yang sama maka hasilnya akan diambil dari redis.

## Kasus ke 3, Ketika ada Proses berat dalam Aplikasi

![alt](/img/kasus_redis_proses_berat.png)

pada kasus ini, daripada proses yang berat dilakukan berulang kali untuk memperoleh hasil yang sama dari user yang melakukan request. hasil dari proses tersebut akan disimpan di redis dan akan diambil jika user melakukan query yang sama.

## Kasus ke 4, Membuat Delayed Job

![alt](/img/kasus_redis_membuat_delayed_job.png)

delayed job adalah proses yang mebutuhkan waktu berulang untuk mengecek data dalam database, contohnya proses pelunasan pembayaran dalam waktu tertentu, dimana aplikasi akan mengecek status pembayaran secara terus menerus di database. hal ini bisa di atasi menggunakan redis dengan melakukan chace pada data transaksi didalam redis yang akan di cek oleh scheduler.

# Cara Menginstall Redis

Redis dapat di install menggunakan docker-compose, caranya yaitu:

1. Masuk kedalam server menggunakan ssh
2. Buat folder dengan nama redis

   ![alt](/img/buat_folder_redis.png)

3. buat file docker-compose.yaml dalam folder tersebut

   ![alt](/img/perintah_nano_docker_compose_file_redis.png)

4. jalankan perintah `docker-compose up -d`

   ![alt](/img/redis_docker-compose-up.png)

5. masuk kedalam terminal container docker yang menginstall redis dengan perintah `docker exec -it redis_container redis-cli`, perintah tersebut untuk masuk kedalam redis-cli

   ![alt](/img/testing_redis.png)
