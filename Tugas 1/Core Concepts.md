## Data Layer

- Pada aplikasi apapun, `Data Layer` adalah tempat aplikasi berinteraksi dengan `Database`.
- `Data Layer` menangani **Storage** (Penyimpanan), **Retrieval** (Pengambilan), and **Manipulation** (manipulasi) of Data (**Data Layer menangani Penyimpanan, Pengambilan, dan Manipulasi Data**).

**peran penting data layer**

1. Memastikan aplikasi dapat memperoleh data.
2. Memastikan aplikasi dapat menambah data baru kedalam database.

### Cara Hasura Mengelola Data Layer

Hasura menangani "Data Layer" dengan cara, otomatis merubah `database` menjadi `graphQL`. artinya pada saat kita mengkoneksikan Hasura dengan database, Hasura akan membuat serangkaian alat yang memungkinkan membuat **query** & **memodifikasi data** tanpa perlu membuat API secara manual.

**Alur kerja Hasura pada Data Layer**

1.  Membuat API secara Instant
    - **API (Application Programming Interface)** adalah sebuah penghubung yang memungkinkan aplikasi perangkat lunak untuk berkomunikasi satu sama lain.
    - Pada konteks **Hasura**, API memungkinkan aplikasi kita (seperti Web atau Mobile App) untuk berkomunikasi dengan Database atau untuk mendapatkan Data atau Memperbarui Data.
    - Pada Hasura, "Instant API Generation" secara otomatis membuat **API**, segera setelah kita menghubungkan ke Database, **tanpa perlu menulis Backend Code**
2.  Permission

    - dalam hasura kita bisa menerapkan "Fine-Grained" Access Control Rules (aturan kontrol Akses yang terperinci). dimana user atau role yang berbeda dapat memiliki **tingkat akses** yang berbeda ke data kita. **hal ini memastikan keamanan dengan hanya mengizinkan orang yang tepat untuk mengakses data.**
    - perbedaan antara **Fine-Grained Aceess Control (FGAC)** dan **Coarse-Grained Access Control** yaitu: pada FGAC menerapkan aturan kontrol yang sangat spesifik. pada Coarse-Grained Access Control menyediakan akses izin yang luas tanpa aturan spesifik.
    - **contoh:**

      **pada FGAC**

      - Elementary School Students (Siswa SD) hanya bisa meminjam buku dari Kid's Section.

      - Middle School Students (Siswa SMP) dapat meminjam buku dari Kid's Section & Young Adult Section.

      - Teachers (Guru) dapat mengakses semua Book Section.

      **pada Coarse-Grained Access Control:**

      - All Students dapat meminjam buku

3.  Realtime Data

    - Hasura memiliki fitur `subscription` yang canggih. dimana aplikasi yang terhubung dengan hasura dapat secara otomatis diperbarui dengan data baru tanpa perlu melakukan refresh manual.
    - contoh:

      jika mau mendapatkan update data terbaru dari table `products` secara otomatis maka menggunakan `subscription`, contoh:

      ```graphQL
      subscription{
         products {
          id
          name
          price
          stock
         }
      }
      ```

      jika ingin mendapatkan data terbaru, dari table product dengan menambahkan kondisi maka caranya adalah

      ```graphQL
      subscription{
         products(where: {price: {_eq: 1000}}){
            id
            name
            stock
         }
      }
      ```

      penjelasan:

      graphQL diatas artinya jika terdapat data products baru/ data update baru dengan harga 1000 maka berikan notifikasi ke aplikasi.

    - cara kerja Subscription Hasura

      1. **Client Subcsribes**

         Client mengirimkan query `Query GraphQL Subscription` query ini dibutuhkan untuk melacak perubahan.

      2. **Hasura Listen For Change**

         Setelah subcription aktif, Hasura akan memantau database untuk setiap perubahan (seperti New Messages, Updated Records, atau Deleted Data).

      3. **Real Time Update**

         Saat terdapat perubahan pada database, Hasura secara otomatis Push data yang di-update ke Aplikasi secara realtime. yang mana dengan hal ini, Aplikasi tidak perlu mengirim Request baru atau melakukan Refresh Page untuk mendapatkan Data yang baru.

    - Bagaimana Cara Hasura Mengelola Subscription

      Hasura Menghandle Subscription dengan, `Websocket`.

      > **Websocket** merupakan protokol komunikasi dua arah secara real-time antara klien dan server melalui satu koneksi yang berkelanjutan. **WebSocket** menjadi bagian dari spesifikasi HTML5 dan didukung oleh semua browser web modern.
      >
      > [Sumber Bacaan Websocket](https://www.revou.co/kosakata/websocket)

      begini cara kerjanya:

      1. saat aplikasi kita memulai subscription, maka koneksi websocket dibuka antara Hasura dengan Aplikasi.
      2. Selama Koneksi WebSocket ini aktif, Hasura dapat mengirim Update ke aplikasi kapanpun data mengalami perubahan.
      3. Jika Koneksi WebSocket nya Lost (terputus) atau Closed (ditutup), maka aplikasi dapat melakukan Restart pada Subscription untuk bisa menerima Update (Perubahan Data).

    - Alur Kerja Websocket

    - Perbedaan Traditional HTTP Response dengan Websocket

      ![Http vs Websocket](/img/http_vs_websocket.png)

      > Pada http connection, koneksi baru selalu dibuat untuk setiap permintaan. sedangkan websocket selalu mempertahankan koneksi terbuka.

      **Memahami HTTP Traditional**

      Komunikasi HTTP tradisional bergantung pada serangkaian siklus permintaan-respons, di mana klien mengirimkan permintaan data atau sumber daya, dan server meresponsnya.

      setiap permintaan dan respons bersifat independen dan harus berisi semua informasi yang diperlukan agar dapat dipahami. **Akibatnya, koneksi baru dibuat untuk setiap interaksi antara klien dan server. Model permintaan-respons ini dapat menyebabkan latensi lebih tinggi, terutama jika diperlukan beberapa permintaan untuk mengakses data yang diperlukan.**

      **Perbedaan HTTP dengan Websocket**

      **Model Komunikasi**

      - Websocket mendukung komunikasi dua arah (full-duplex), memungkinkan klien dan server mengirim dan menerima data secara bersamaan tanpa menunggu tanggapan.
      - HTTP tradisional menggunakan model permintaan-respons, di mana klien mengirimkan permintaan dan menunggu respons dari server sebelum memulai permintaan lain.

      [Sumber Bacaan perbedaan traditional HTTP dengan Websocket](https://appmaster.io/id/blog/soket-web-vs-http-tradisional)

    - sumary cara kerja Subscription

      1. Client menjaga agar "WebSocket Connection" tetap aktif agar bisa menerima Update Perubahan Data secara Real-Time

      2. Client mengirimkan "Subscription Query" untuk melakukan Subscribes ke Perubahan Data tertentu.

      3. Hasura Server "Listens" (mendengarkan) setiap perubahan pada Data yang di-subscribes.

      4. Hasura Server mendeteksi adanya perubahan pada Data.

      5. Hasura Server mengirim perubahan data ke semua Client yang terhubung (Connected Clients) yang melakukan Subscribes ke Data tersebut.

      6. Setiap Client menerima Update Perubahan Data melalui WebSocket Connection mereka masing-masing

# Subgraph

**Subgraph** adalah unit independen yang dirancang untuk bekerja secara mandiri oleh tim terpisah. Namun, unit-unit ini dapat digabungkan menjadi API terpadu, sehingga memungkinkan pengembangan yang terdistribusi, kolaboratif, dan efisien.

Subgraph menggunakan **metadata** yaitu Informasi atau konfigurasi yang diperlukan untuk mendefinisikan bagaimana Subgraph bekerja. **termasuk definisi skema, resolvers, sumber data, permissions, dan konfigurasi lainnya.**

Subgraph adalah unit mandiri yang memiliki semua komponen yang diperlukan untuk berfungsi tanpa bergantung langsung pada sistem lain. **Misalnya, Subgraph untuk "Produk" akan mencakup skema, query, dan resolvers terkait produk saja.**

Subgraph dapat dihubungkan ke Unified API menggunakan teknik seperti GraphQL Federation. Unified API adalah API tunggal yang menyatukan semua Subgraph sehingga klien dapat mengakses data dari berbagai Subgraph melalui satu endpoint.

Contoh Penerapannya:

- **Tim E** membuat Subgraph untuk `Products`.
- **Tim F** membuat Subgraph untuk `Inventory` (stok barang).
- Keduanya dihubungkan ke Unified API. Klien dapat melakukan query ke Unified API untuk mendapatkan data products dan inventori tanpa mengetahui detail bagaimana masing-masing Subgraph bekerja.

<br>

penjelasan video [From Monolith to Supergraph](https://www.youtube.com/watch?v=bTbkdUdsUUE) tentang pengertian subgraph. di menit 16:10.

![Potongan Video tentang subgraph](/img/video_tentang_subgraf_1610.png)

## Bagaimana Cara Membuat Subgraph dalam Hasura

1. subgraph terkoneksi dengan data layer menggunakan data connector. subgraph tersusun dari data source terkait baik dari database ataupun sebagai Custome Business Logic.

   Hasura DDN (versi ke 3 Hasura) menggunakan sejumlah data connector yang terhubung dengan database, services, dan API.

   Subgraph dapat menyertakan **Custom Business Logic** sendiri sebagai fungsi `TypeScript` yang mengembalikan atau mengubah data secara langsung melalui GraphQL API.

2. Setelah menghubungkan Data Source , kemudian dapat membuat metadata menggunakan Hasura CLI dan ekstensi Hasura VS Code. Metadata ini kemudian dibangun pada Hasura DDN Instance Anda, yang digunakan untuk serve GraphQL API Anda.

## Memahami Subgraph dalam GraphQL (General)

> Hasura merupakan produk GraphQL, tetapi Produk GraphQL tidak hanya Hasura.

Pada GraphQL, Subgraph merupakan komponen yang digunakan untuk **memecah dan mengatur Data Kompleks menjadi bagian-bagian yang lebih kecil dan mudah dikelola**, yang bertujuan untuk memudahkan Query & memudahkan Data Retrieval (Pengambilan Data).

**Maksud dari Memecah dan Mengatur Data Kompleks:**

- **Memecah data kompleks**: Dalam aplikasi besar, data biasanya terdiri dari berbagai entitas (misalnya, pengguna, produk, pesanan) yang saling terkait. Subgraph membantu memisahkan data ini menjadi bagian-bagian kecil berdasarkan domain atau fungsionalitas.
- **Mengatur data**: Subgraph memungkinkan pengelolaan yang lebih terorganisir. Setiap Subgraph memiliki skema, resolvers, dan data sumbernya sendiri.
- contoh:
  - Subgraph `Users` hanya menangani data terkait pengguna (ID, nama, email).
  - Subgraph `Orders` hanya menangani data pesanan (ID pesanan, total, status).

**Mengapa Menggunakan Subgraph dalam GraphQL ?**

1. Modular structure

   Subgraph memungkinkan pemisahan data menjadi bagian-bagian yang lebih kecil berdasarkan domain atau fungsionalitas. Hal ini membantu dalam pengelolaan skema API yang lebih mudah, terutama untuk aplikasi besar yang memiliki banyak entitas.

   contoh kasus:

   | Entitas  | Fungsi                                                         |
   | -------- | -------------------------------------------------------------- |
   | Users    | Menangani data pengguna seperti nama, email, dan alamat.       |
   | Products | Menangani data produk seperti nama produk, harga, dan stok.3   |
   | Orders   | Menangani data pesanan seperti total harga dan status pesanan. |

   Query terhadap masing-masing subgraph adalah:

   ```graphQL

   # Users Subgraph
   query {
      user(id: "123") {
         name
         email
      }
   }

   # Products Subgraph
   query {
      product(id: "456") {
         name
         price
      }
   }

   # Orders Subgraph
   query {
      order(id: "789") {
         total
         status
      }
   }
   ```

2. Better Performance

   setiap subgraph hanya menangani bagian tertentu (specific part) dari System. hal ini dapat meningkatkan performance karena kita hanya **meng-query data yang di perlukan saja, tanpa harus membebani seluruh skema yang ada.**

   > **Untuk Informasi**
   >
   > bagaimana **Modularization** meningkatkan performance pada subgraph ?
   >
   > Modularization berarti membagi sesuatu menjadi bagian yang lebih kecil dan setiap bagian bersifat independent.
   >
   > Dalam konteks GraphQL, **Subgraph adalah bagian-bagian yang lebih kecil dari tersebut**,
   > yang mana masing-masing bagian ini bertanggung jawab untuk Area Fungsionalitas tertentu atau Data tertentu,
   > yaitu seperti Users, Products, atau Orders.
   >
   > **bagaimana Modularization meningkatkan performance ?**
   >
   > 1. Focused Queries
   >
   >    **contoh kasus:**
   >
   >    Saat Client (seperti WebApp) menginginkan Data. Client mengrimkan Request berupa Query, yang mana Query tersebut hanya berisi Relevant Subgraph (Subgraph yang berkaitan >> dengan Data yang kita minta). Misalnya jika Client meminta data "User Details", maka Query tersebut hanya berisi Subgraph User.
   >
   > 2. Optimized Data Fetching
   >
   >    Setiap Subgraph dapat Fetch Data (Mengambil Data) dengan cara yang paling efisien untuk Domain (area) tertentu. hal ini membuat fecth data menjadi lebih cepat karena sudah tau mau ambil data darimana.
   >
   >    **contoh kasus:**
   >
   >    misal saya mempunyai sebuah rak buku. Modularization akan mengatur dengan rapih penempatan kategori buku yang ada dirak tersebut.
   >
   >    - misal rak no 1, menyimpan buku dengan kategori programing.
   >    - rak no 2 menyimpan buku dengan kategori data science.
   >    - jika ingin mencari buku tentang programing saya sudah tau harus mencari di rak no 1. hal ini dapat mempercepat proses pencarian buku dan menghemat waktu karena tidak harus mencari di seluruh rak buku.
   >
   > 3. Independent Scalling
   >
   >    Secara umum, Scalling berarti meningkatkan jumlah Resources (seperti Server, Aplikasi, atau Database) yang digunakan System sehingga bisa menangani Workload (beban kerja) atau Traffic.
   >
   >    Setiap Subgraph dapat dilakukan Scalling secara Independen berdasarkan penggunaannya. misal **jika Area tertentu mendapatkan banyak Traffic, maka Subgraph yang dikhususkan untuk area tersebut tanpa ditingkatkan (Scale-Up) tanpa mempengaruhi yang lain**.
   >
   >    contohnya, jika `subgraph orders` memiliki jumlah traffic yang tinggi, maka subgraph order dapat di tingkatkan resourcenya tanpa mempengaruhi yang lain.
   >
   > 4. Paralel Processing
   >
   >    **pararel processing** adalah kondisi dimana saat clinet memerlukan data dari beberapa subgraph, beberapa subgraph tersebut dapat memproses request dalam waktu yang sama.
   >
   >    Paralel Processing = Beberapa Subgraph dapat memproses Request dalam waktu yang sama
   >
   > 5. Reduced Network Overhead
   >
   >    Karena Clients hanya Request Data dari Subgraph yang diperlukan, sehingga lebih sedikit data yang dikirim melalui Jaringan. yang mana hal ini, dapat menghasilkan Load Time yang lebih cepat, dan mengurangi Pemakaian Bandwith.

3. Easier Maintenance

   Subgraph memungkinkan Team untuk bekerja pada bagian tertentu dari suatu System secara mandiri.
   Misalnya, suatu Team mengelola "User Subgraph", sementara Team yang lainnya mengelola "Order Subgraph".

4. Federation

   Subgraph sangat berguna pada "Federated GraphQL Architecture".
   Pada Federated System, Multiple Subgraph (beberapa Subgraph) bekerja sama dibawah 'Unified Schema'.

## Bagaimana Subgraph bekerja pada GraphQL Federation

Federasi GraphQL adalah pendekatan arsitektur terdistribusi yang memungkinkan para pengembang untuk menggunakan satu API di beberapa layanan GraphQL (yaitu, layanan yang ditulis dalam bahasa kueri sumber terbuka, GraphQL).

[sumber bacaan](https://www.ibm.com/id-id/topics/graphql-federation)

> **Penjelasan Detail**
>
> GraphQL Federation adalah metode untuk membagi dan mengelola API GraphQL besar menjadi beberapa bagian lebih kecil yang disebut Subgraph. Setiap Subgraph bertanggung jawab atas bagian dari skema dan data aplikasi tertentu, tetapi mereka semua bekerja bersama di bawah satu API GraphQL terintegrasi.
>
> Federation memungkinkan beberapa tim atau layanan untuk mengelola bagian-bagian API mereka sendiri, sambil tetap dapat diakses melalui satu titik akhir (endpoint).

**Sudi kasus E-Commerce:**

**1. Subgraph Definition:**

ada 3 subgraph yaitu `Product Subgraph`, `Customer Subgraph`, `Order Subgraph`. yang masing-masing menangani data dari domain tertntu.

`Product Subgraph`

- Jenis (Type): Product, Category, Inventory
- Query: products, product(id: ID!), categories
- Mutasi: createProduct, updateProduct, deleteProduct

`Customer Subgraph`

- Jenis (Type): Customer, Address
- Query: customer(id: ID!), addresses
- Mutasi: createCustomer, updateAddress

`Order Subgraph`

- Jenis (Type): Order, OrderItem, OrderStatus
- Query: orders, order(id: ID!)
- Mutasi: createOrder, updateOrderStatus

> Dalam konteks GraphQL, **Jenis (Type)** merujuk pada struktur data yang digunakan untuk mendefinisikan objek atau entitas dalam skema GraphQL. Setiap Type mendefinisikan atribut atau field yang dimiliki oleh objek tersebut dan jenis data yang bisa diakses atau dimanipulasi melalui query dan mutasi.
>
> setiap object type misalnya product pada "Product Subgraph" mempunyai fieldnya sendiri misal (1d, name, price)

**2. Reference Between Subgraphs**

Setiap Subgraph dapat saling mereferensikan data dari Subgraph lain untuk menyelesaikan query yang lebih kompleks.

misalnya:

- `Order Subgraph`: Data pesanan akan merujuk ke `Product Subgraph` untuk mendapatkan detail produk yang ada dalam pesanan.

- Order memiliki relasi dengan `Product` dari `Product Subgraph` untuk menampilkan detail produk yang dipesan.

```GraphQL
query {
  order(id: "123") {
    id
    status
    items {
      product {
        name
        price
      }
      quantity
    }
  }
}
```

Dalam query ini, `Order Subgraph` akan mengembalikan informasi tentang pesanan, termasuk daftar item. Setiap item akan merujuk ke `Product Subgraph` untuk mendapatkan nama dan harga produk terkait.

**3. Gateway**

Gateway adalah komponen yang menggabungkan semua Subgraph dan menangani query dari klien. Ketika klien mengirimkan query, Gateway akan membagi query tersebut ke Subgraph yang sesuai, mengambil data, dan menggabungkannya menjadi satu respons terpadu.

misalnya :

- Ketika klien mengirimkan query untuk mendapatkan data tentang pelanggan dan pesanan mereka, Gateway akan mengirimkan permintaan ke `Customer Subgraph` untuk mendapatkan informasi pelanggan, dan ke `Order Subgraph` untuk mendapatkan informasi pesanan terkait.

```graphQL
query {
  customer(id: "456") {
    name
    orders {
      id
      status
      total
      items {
        product {
          name
          price
        }
      }
    }
  }
}
```

Proses:

- **Gateway** menerima query dari klien.
- **Gateway** mengirimkan permintaan ke Customer Subgraph untuk mendapatkan informasi pelanggan.
- **Gateway** mengirimkan permintaan ke Order Subgraph untuk mendapatkan informasi pesanan pelanggan.
- **Gateway** menggabungkan data dari kedua Subgraph (pelanggan dan pesanan), serta data produk terkait dalam pesanan (dari Product Subgraph).
- **Gateway** mengembalikan Single Response kepada klien yang berisi data pelanggan, pesanan, dan detail produk.

<br>

# Supergraph

[Link Dokumentasi Resmi](https://hasura.io/supergraph?utm_source=chatgpt.com)

**Supergraph** dalam konteks Hasura adalah arsitektur yang mengintegrasikan berbagai sumber data dan layanan menjadi satu lapisan akses data terpadu. Memungkinkan tim untuk mengelola domain data mereka secara independen sambil tetap mempertahankan kohesi tinggi dalam evolusi sistem secara keseluruhan.

## Supergraph dalam konteks GraphQL Secara Umum

Supergraph adalah konsep dalam GraphQL yang digunakan untuk **menggabungkan beberapa subgraph (subgraf) menjadi satu graph terpadu (unified graph)**. Supergraph memungkinkan integrasi berbagai sumber data, layanan, atau domain menjadi satu lapisan API yang terpusat dan mudah diakses oleh klien.

> Istilahnya, Supergraph sebagai 'Sebuah Payung Besar' yang menutupi 'Beberapa Payung Kecil', yang mana Payung Kecil tersebut adalah "Subgraph".

**Komponen Utama Supergraph**

1.  Subgraph

    **Subgraph** adalah bagian kecil dari keseluruhan supergraph yang mewakili domain atau layanan tertentu.
    Contoh:

    - **Subgraph Produk**: Mengelola data seperti produk, kategori, dan inventaris.
    - **Subgraph Pembayaran**: Mengelola data seperti saldo, metode pembayaran, dan riwayat transaksi.

2.  Schema Federation

    Dalam supergraph, beberapa subgraph diintegrasikan menggunakan schema federation. Federasi ini memungkinkan subgraph untuk saling berbagi dan mereferensikan data.

3.  Gateway

    **Gateway** adalah komponen yang bertugas menggabungkan semua subgraph menjadi satu supergraph. Gateway ini menerima query dari klien, membagi query ke subgraph yang relevan, dan menggabungkan hasilnya menjadi satu respons.

## Supergraph dalam konteks GraphQL di Hasura

Pada Hasura, Supergraph adalah Unified GraphQL API yang mengintegrasikan data dari berbagai sumber, seperti database, layanan GraphQL jarak jauh (Remote GraphQL Services), REST API, dan lainnya, menjadi satu API yang komprehensif. Konsep ini sangat berguna untuk aplikasi berskala besar, di mana data dikelola secara terpisah oleh berbagai layanan atau database, memungkinkan klien untuk berinteraksi dengan data tersebut secara lancar dan terpusat.

**Bagaimana Hasura Membangun Supergraph ?**

Hasura membangun Supergraph dengan menggunakan Features seperti `Remote Schemas` & `Actions`.

**Remote Schemas**

- Dalam GraphQL Remote Schema merupakan fitur yang berfungsi untuk menggabungkan beberapa "GraphQL API" menjadi "Satu Unified API".
- Meskipun data dan services tersebar di berbagai Server atau Database yang berbeda kita dapat menghubungkan dibawah 1 graphQL Endpoint.
- Dengan Remote Schemas, kita dapat menggunakan 'Satu Endpoint' untuk 'Multiple Services', sehingga Client tidak perlu tahu Data datang dari Service yang mana.

Cara Kerja **Remote Schemas:**

1. Menambahkan Remote Schemas dalam Hasura

   **Apa yang dilakukan**: Kita menghubungkan Hasura dengan API GraphQL lain.

   **Bagaimana caranya**:
   Masukkan URL API GraphQL eksternal ke Hasura.
   Tambahkan token atau header autentikasi jika API tersebut membutuhkan izin akses.

   Contoh:

   - API cuaca eksternal:
     - URL: `https://api.weather.com/graphql`
     - Header: `Authorization: Bearer <token>`

2. Menggabungkan Skema

   **Apa yang terjadi**: Hasura secara otomatis menggabungkan skema dari API eksternal dengan skema dari database lokal.

   **Hasilnya**: Semua data bisa diakses dalam satu GraphQL API.

   **contoh:**

   API Eksternal punya query:

   ```graphQL
   query {
      weather(location: "Jakarta") {
         temperature
         condition
      }
   }
   ```

   Database Lokal Hasura punya table `user`:

   ```graphQL
   query {
      user(id: 1) {
         name
         city
      }
   }
   ```

   Setelah digabung, klien bisa menjalankan query seperti ini:

   ```graphQL

   query {
      user(id: 1) {
         name
         city
      }
      weather(location: "Jakarta") {
         temperature
         condition
      }
   }
   ```

3. Apa yang dilakukan Hasura

   - Saat klien mengirimkan query, Hasura akan membagi query tersebut.
   - Bagian query yang berasal dari database akan dijalankan di Hasura.
   - Bagian query yang berasal dari API eksternal akan diteruskan ke Remote Schema.

4. Membuat Relasi Antar Data

   - **Apa yang bisa dilakukan**: Data dari API eksternal (Remote Schema) bisa dihubungkan dengan data dari database lokal.
   - **Hasilnya**: Query yang kompleks bisa dijalankan dengan mudah.

   Contoh:

   API eksternal punya data cuaca (Weather), dan database lokal punya data pengguna (User).

   ```graphQL
   query {
      user(id: 1) {
         name
         city
         weather {
            temperature
            condition
         }
      }
   }
   ```

   - Data `name` dan `city` diambil dari database lokal.
   - Data `weather` diambil dari API eksternal berdasarkan `city` pengguna.

**Actions**

**Actions** di Hasura adalah cara untuk menambahkan logika atau fungsionalitas kustom ke dalam GraphQL API yang disediakan oleh Hasura. Dengan menggunakan Actions, kita bisa membuat **mutasi atau query** yang tidak secara langsung berhubungan dengan database, tetapi bisa menghubungkan dengan **fungsi kustom** atau **API eksternal**.

**Langkah Kerja Action:**

1. Membuat Actions

   **Apa yang dilakukan**: Kita membuat sebuah **Action** untuk mendefinisikan query atau mutasi kustom. **Action ini akan menerima input, memprosesnya, dan memberikan output sesuai kebutuhan.**

   **Bagaimana caranya**:

   - Tentukan nama action, misalnya `createUser` atau `getWeather`.
   - **Tentukan input dan output** dari action tersebut (misalnya, parameter apa yang perlu diberikan dan apa yang akan dikembalikan).
   - Tentukan fungsi atau API eksternal yang akan dijalankan ketika action ini dipanggil.

   Contoh:

   Misalnya kita ingin membuat action untuk membuat pengguna baru dengan data yang lebih kompleks, yang tidak bisa langsung disimpan di database.

   Action `createUser`:

   - **Input**: Nama, email, password.
   - **Output**: ID pengguna yang baru dibuat.

2. Menentukan Handler untuk Action

   **Apa yang dilakukan**: Setelah Action dibuat, kita harus menambahkan handler untuk menjalankan logika kustom. **Handler ini bisa berupa fungsi yang dijalankan di server atau bisa juga mengarah ke API eksternal.**

   **Bagaimana caranya**:
   Buat endpoint untuk menangani Action, bisa berupa HTTP POST endpoint yang menerima data dan memprosesnya.
   Dalam handler, Anda bisa menambahkan logika bisnis, seperti memvalidasi data atau berinteraksi dengan layanan lain.

   Contoh:

   - Handler untuk `createUser` bisa mengarah ke fungsi backend yang membuat pengguna baru, lalu mengirim email konfirmasi, atau berinteraksi dengan API eksternal untuk memvalidasi email.

3. Menghubungkan Action dengan GraphQL

   **Apa yang dilakukan**: Setelah Action dan handler siap, kita bisa langsung menggunakannya di GraphQL API Hasura. Action ini akan muncul sebagai query atau mutasi baru yang bisa dipanggil oleh klien.

   **Bagaimana caranya**:
   Action yang sudah dibuat akan otomatis terdaftar dalam GraphQL API.
   Klien bisa memanggil Action ini seperti query atau mutasi biasa, menggunakan GraphQL.

   Contoh:

   Untuk Action createUser, klien bisa membuat query seperti ini:

   ```graphQL
   mutation {
   createUser(input: {name: "John", email: "john@example.com", password: "password123"}) {
      id
   }
   }
   ```

4. Keamanan Action

   **Apa yang dilakukan**: Anda bisa mengatur akses kontrol untuk Action, sehingga hanya pengguna tertentu yang bisa memanggil Action tersebut.

   **Bagaimana caranya**:

   - Gunakan Role-Based Access Control (RBAC) untuk membatasi siapa yang bisa mengakses Action.
   - Tentukan apakah Action bisa dipanggil oleh pengguna dengan peran tertentu atau apakah perlu autentikasi lebih lanjut.
