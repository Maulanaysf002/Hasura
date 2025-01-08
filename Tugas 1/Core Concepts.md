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

      [Sumber Bacaan perbedaan traditional HTTP dengan Websocket](https://appmaster.io/id/blog/soket-web-vs-http-tradisional)

    - sumary cara kerja Subscription

      1. Client menjaga agar "WebSocket Connection" tetap aktif agar bisa menerima Update Perubahan Data secara Real-Time

      2. Client mengirimkan "Subscription Query" untuk melakukan Subscribes ke Perubahan Data tertentu.

      3. Hasura Server "Listens" (mendengarkan) setiap perubahan pada Data yang di-subscribes.

      4. Hasura Server mendeteksi adanya perubahan pada Data.

      5. Hasura Server mengirim perubahan data ke semua Client yang terhubung (Connected Clients) yang melakukan Subscribes ke Data tersebut.

      6. Setiap Client menerima Update Perubahan Data melalui WebSocket Connection mereka masing-masing
