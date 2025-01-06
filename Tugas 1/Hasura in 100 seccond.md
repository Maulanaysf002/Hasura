link ppt:
sumber bacaan :

## Mengubah Relational Database Menjadi Grapql atau RestAPI

**Relational Database** adalah salah satu jenis sistem manajemen basis data yang dirancang untuk menyimpan, mengatur, dan mengakses data dengan menggunakan struktur tabel. Data dalam database relasional diatur ke dalam baris dan kolom, dengan setiap kolom mewakili atribut (field) dan setiap baris mewakili entitas individu (record). Pendekatan ini memungkinkan pengguna untuk membuat hubungan antara tabel melalui kunci tertentu, yang disebut sebagai relasi.

**sql (Structured Query Language)** adalah sebuah bahasa yang digunakan untuk mengelola dan memanipulasi database relational. SQL memungkinkan pengguna untuk melakukan berbagai operasi seperti menyimpan, memperbarui, menghapus, dan mengambil data dari tabel.

[sumber bacaan relational database](https://dqlab.id/apa-itu-database-relasional-dalam-sql-arti-dan-fungsinya?utm_source=google&utm_medium=cpc&utm_campaign=dqlab-id-register-dsa-s_dsa&utm_term=dqlabref=google&dqlabref=google&gad_source=1&gclid=CjwKCAiA-Oi7BhA1EiwA2rIu27DDksbO4OKKfBLEVcLuUCOGtbkB4FVA5IeKfEPA0QmIuSIflHcmnBoCdSMQAvD_BwE).

> Hasura langsung mengubah struktur database relational menjadi GrapQL

**GraphQL** adalah **bahasa kueri** untuk API dan **runtime** untuk menjalankan kueri tersebut dengan data yang ada. GraphQL memungkinkan klien untuk meminta data yang tepat yang mereka butuhkan, tidak lebih dan tidak kurang. berbeda dengan REST, di mana klien sering kali harus membuat beberapa permintaan (mengakses endpoint) untuk mendapatkan semua data yang diperlukan.

kapan harus menggunakan graphQL:

- **Aplikasi mobile**: GraphQL sangat cocok untuk aplikasi mobile yang memiliki batasan bandwidth dan memerlukan data yang sangat spesifik.
- **Aplikasi dengan antarmuka yang kompleks**: GraphQL memungkinkan Anda membangun antarmuka yang dinamis dan responsif dengan mudah.
- **Tim pengembangan yang besar**: GraphQL dapat membantu meningkatkan efisiensi pengembangan dengan menyediakan satu sumber kebenaran untuk data.

[suber bacaan grapql](https://www.codepolitan.com/blog/graphql-vs-rest-api-mana-yang-harus-anda-pilih-di-2024/)

> Enduser perlu berkomunikasi dengan database untuk mendapatkan data yang perantaranya bisa berupa GraphQL atau REST API

![alur mendapatkan data](/img/alur_mendapatkan_data.png)

> **Hasura** Merupakan platform open source yang dapat menjadi perantara antara database dan client dengan langsung merubah database relational menjadi GraphQL.

![hasura dapat menjadi perantara dengan merubah langsung database relational](/img/hasura_merubah_database_menjadi_graphql.png)

## Hasura Otomatis membuat skema dan resolver

Hasura secara otomatis menghasilkan skema GraphQL berdasarkan tabel dan relasi yang ada di database.

![skema dan resolver](/img/skema_resolver_hasura.png)

**cara kerja skema**

1.  Koneksi ke Database:

    - Hubungkan Hasura ke database relasional (seperti PostgreSQL).
    - Hasura **membaca metadata** dari database (seperti tabel, kolom, dan relasi).

2.  Pembuatan Skema:

    - Hasura membuat skema GraphQL dengan q**uery, mutation, dan subscription** berdasarkan tabel di database.
      Setiap tabel di database akan memiliki:
      - **Query** untuk membaca data (misalnya, users atau products).
      - **Mutation** untuk menambah, mengubah, atau menghapus data (misalnya, insert_users, update_users, delete_users).
      - **Subscription** untuk mendengarkan perubahan data secara real-time.

3.  Relasi Otomatis:

    - Jika tabel memiliki foreign key, Hasura secara otomatis membuat relasi antar tabel sebagai bagian dari skema GraphQL.

    - Contoh: Jika ada tabel orders dengan foreign key ke users, Anda bisa mendapatkan data users yang terkait dengan setiap order melalui GraphQL.

**Cara Kerja Resolver Otomatis**

1. Mapping ke Database:

   - Hasura memetakan setiap **query**, **mutation**, dan **subscription** GraphQL langsung ke SQL query di database.
   - Resolver bawaan Hasura menangani semua operasi CRUD (**Create, Read, Update, Delete**).

2. Pengelolaan Relasi:

   - Resolver otomatis menggabungkan data dari tabel terkait berdasarkan relasi yang didefinisikan.

     Contoh: Jika Anda meminta data orders bersama dengan data users yang terhubung, resolver akan menjalankan SQL JOIN untuk mendapatkan data tersebut.

3. Authorization dan Role-Based Access Control (RBAC):

   - Anda dapat menentukan aturan berdasarkan role (misalnya, hanya admin yang dapat menghapus data).

## Koneksi Database dengan Hasura

Hasura mendukung berbagaimacam database, yaitu:

![macam macam database di hasura](/img/macam-macam_database_hasura.png)

**cara koneksikan database di hasura**

koneksi database dihasura bisa dilakukan dengan ui pada menu data, kita juga bisa membuat database dan tabel lalu mendefinisikan skema dalam hasura.

**Remote Schemas**

selain menghubungkan ke database, bisa juga menghubungkan API dari pihak ke tiga ke dalam skema. untuk membuat satu sumber untuk semua data.

![remote schemas](/img/remote_schemas.png)

Cara Kerja Remote Schemas:

1. **Registrasi Remote Schema**: menambahkan endpoint GraphQL eksternal di Hasura Console.
2. **Penggabungan Schema**: Hasura akan menggabungkan schema eksternal tersebut dengan schema bawaan Hasura, sehingga dapat diakses keduanya melalui satu GraphQL API.
3. **Resolver**: Permintaan ke remote schema diteruskan ke layanan eksternal, dan hasilnya dikembalikan melalui Hasura.

Langkah-langkah Menggunakan Remote Schemas di Hasura

1. Buka Hasura Console:

   - Akses Hasura Console dari browser Anda.

2. Tambahkan Remote Schema:

   - Masuk ke tab Remote Schemas.
     Klik Add untuk menambahkan schema baru.

3. Isi Detail Remote Schema:

   - **Remote Schema Name**: Berikan nama unik untuk schema.
   - **GraphQL Server URL**: Masukkan URL endpoint GraphQL eksternal.
   - **Headers**: Tambahkan header jika API eksternal memerlukan autentikasi atau konfigurasi khusus.
   - **Forward Client Headers (opsional)**: Aktifkan jika Anda ingin Hasura meneruskan header dari klien ke layanan eksternal.

4. Simpan Remote Schema:

   - Klik Add Remote Schema untuk menyimpan konfigurasi.

5. Gunakan Remote Schema:

   - Setelah ditambahkan, Anda dapat langsung menggunakan query dan mutation dari schema eksternal melalui Hasura GraphQL API.

Keuntungan Menggunakan Remote Schemas

- Satu API Endpoint: Anda hanya perlu berinteraksi dengan satu GraphQL endpoint, meskipun data berasal dari berbagai sumber.
- Penggabungan Data: Anda dapat menggabungkan data dari database lokal Hasura dengan layanan eksternal dalam satu query.
- Skalabilitas: Memudahkan pengembangan sistem terdistribusi dengan berbagai sumber data.

**Actions**

![actions](/img/action_hasura.png)

Actions di Hasura adalah fitur yang memungkinkan untuk menambahkan fungsi baru ke GraphQL API bawaan Hasura. Fitur ini digunakan untuk menjalankan logika khusus yang tidak langsung berhubungan dengan database. Misalnya, Anda bisa:

1. Memanggil layanan eksternal seperti API pihak ketiga.
2. Menambahkan aturan atau validasi tertentu sebelum menyimpan data.
3. Mengintegrasikan sistem lain ke dalam API Anda.

Dengan Actions, kita bisa membuat **query** atau **mutation** khusus yang sebenarnya menjalankan kode atau memanggil API lain di belakang layar, tapi tetap bisa diakses melalui satu GraphQL endpoint.

Cara Kerja Actions

1. **Definisi**: lakukan pendefinisian schema action (query atau mutation) menggunakan GraphQL SDL (Schema Definition Language).
2. **Handler**: menetapkan URL endpoint eksternal sebagai handler untuk action tersebut.
3. **Eksekusi**: Ketika action dipanggil melalui API GraphQL, Hasura meneruskan permintaan ke handler eksternal.
4. **Response**: Handler eksternal memproses permintaan dan mengembalikan respons ke Hasura, yang diteruskan ke klien.

**Event Trigger Hasura**

![event trigger](/img/event_trigger_hasura.png)

**Event Trigger** di Hasura adalah fitur yang memungkinkan Anda menjalankan kode otomatis setiap kali terjadi perubahan data di database. Perubahan ini bisa berupa **INSERT** (data baru ditambahkan), **UPDATE** (data diubah), atau **DELETE** (data dihapus).

Cara Kerjanya:

- **Setup Event Trigger**: membuat "trigger" yang mengawasi tabel tertentu di database.
- **Atur Endpoint**: menentukan URL API (handler) yang akan dipanggil ketika ada perubahan data.
- **Jalankan Otomatis**: Ketika data di tabel berubah, Hasura otomatis mengirimkan data perubahan itu ke endpoint yang di tentukan.

Contoh Sederhana:

1. Ada sebuah tabel `orders` untuk menyimpan pesanan.
2. kita ingin mengirim notifikasi setiap kali ada pesanan baru (**INSERT**).
3. membuat **Event Trigger** untuk tabel `orders`, lalu menghubungkannya ke endpoint API notifikasi.
4. Setiap kali ada pesanan baru, Hasura akan mengirim data pesanan ke API Anda, dan API Anda akan mengirimkan notifikasi.

Keuntungan:

- Semua proses berjalan otomatis tanpa perlu pengecekan manual.
- Bisa digunakan untuk menghubungkan database dengan sistem lain, seperti notifikasi, pengolahan data, atau analitik.
- Data langsung diproses begitu ada perubahan.

## Hasura Tidak Menyediakan Fitur Authentication

![hasura_tidak_menangani_user_auth](/img/hasura_tidak_menangani_user_auth.png)

**Hasura** tidak secara langsung menangani user authentication karena filosofi desainnya adalah menjadi **GraphQL Engine** yang fokus pada pengelolaan data, bukan autentikasi pengguna. Dengan cara ini, Hasura tetap ringan, fleksibel, dan dapat diintegrasikan dengan berbagai sistem autentikasi yang ada.

beberapa sistem authentication user yang dapat digunakan oleh hasura:

- Firebase Authentication
- Auth0
- Keycloak
- Custom Authentication Services

**Hasura Menyediakan Varible Sesi**

**Variable sesi** di Hasura adalah fitur yang memungkinkan Anda untuk meneruskan data tertentu (seperti informasi pengguna) dari token autentikasi atau header permintaan ke dalam query atau mutation GraphQL. Variable sesi ini sangat berguna untuk authorization (mengatur akses data) dan multi-tenancy (mengelola banyak pengguna atau organisasi dalam satu database).

## Kesimpulan

![kesimpulan](/img/kesimpulan_hasura.png)

> Hasura adalah platform yang berfungsi sebagai perantara antara database dan aplikasi Anda, memberikan fleksibilitas untuk digunakan dengan teknologi front-end apa pun serta database yang di-host di mana saja. Sebagai proyek open-source, Hasura dapat diinstal dan di-host secara mandiri atau digunakan sebagai layanan terkelola sepenuhnya dengan opsi gratis yang tersedia.
