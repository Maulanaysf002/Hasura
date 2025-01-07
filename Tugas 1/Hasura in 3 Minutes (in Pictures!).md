- link ppt :
- link video : https://www.youtube.com/watch?v=9QZL8YNNgvc

## 4 Keunggulan Hasura

![keunggulan hasura](/img/4_keunggulan%20hasura.png)

- Declaratively configured (Dikonfigurasi secara deklaratif)

  **Hasura** menggunakan pendekatan deklaratif untuk konfigurasi. cukup mendeklarasikan apa yang diinginkan (seperti **schema GraphQL**, **relasi**, atau **aturan otorisasi**) melalui antarmuka Hasura Console atau file metadata. Tidak perlu menulis kode boilerplate untuk membuat resolver atau endpoint.

  Manfaat:

  1. Mengurangi kompleksitas pengaturan API.
  2. Perubahan konfigurasi mudah dilacak karena disimpan sebagai metadata.
  3. Mempermudah kolaborasi dalam tim, terutama jika menggunakan version control.

- Fully authorized (Sepenuhnya diotorisasi)

  **Hasura** menyediakan sistem otorisasi yang kuat dan fleksibel berbasis aturan (rule-based). hasura dapat mendefinisikan aturan otorisasi granular menggunakan role, kondisi akses berbasis kolom, atau bahkan fungsi SQL.

  Manfaat:

  1. Keamanan untuk melindungi data dari akses yang tidak sah.
  2. Kemampuan untuk mendukung berbagai skenario otorisasi, seperti user-specific access atau multi-tenancy.
  3. Otorisasi langsung terintegrasi dengan query GraphQL tanpa perlu menulis kode tambahan.

- Easily extensible (Mudah diperluas
  )

  **Hasura** mendukung extensibility dengan mengintegrasikan custom resolvers, remote schemas, dan action handlers. Anda bisa menghubungkan Hasura dengan API eksternal atau menambahkan logika bisnis kustom.

  Manfaat:

  1. Kemudahan menggabungkan data dari berbagai sumber tanpa mengorbankan performa.
  2. Mendukung berbagai kebutuhan bisnis tanpa membatasi fleksibilitas pengembangan.
  3. Mempermudah integrasi dengan teknologi modern seperti serverless functions atau microservices.

- High performance (Performa tinggi)

  **Hasura** dirancang untuk performa tinggi dengan optimasi query SQL otomatis. Ia mampu menangani beban kerja yang besar karena menggunakan PostgreSQL sebagai backend, yang dikenal dengan kemampuan skalabilitasnya.

  Manfaat:

  1. Latency rendah dalam eksekusi query GraphQL, bahkan untuk data yang kompleks.
  2. Dukungan caching bawaan untuk mempercepat respons.
  3. Dapat digunakan untuk aplikasi dengan skala besar tanpa kehilangan efisiensi.

## Cara Kerja Hasura

1. Deklarasikan Dimana Data Berada
2. dan bagaimana model bisa terhubung

## Query Dalam Hasura

![query dalam hasura](/img/query_dalam_hasura.png)

**Query** adalah salah satu jenis operasi GraphQL yang digunakan untuk membaca atau mengambil data dari database. Hasura menyediakan query bawaan secara otomatis berdasarkan struktur database yang dihubungkan dengannya.

**Contoh query:**

```graphQL
query {
  users {
    id
    name
    email
  }
}
```

**Hasil query:**

```graphQL
{
  "data": {
    "users": [
      {
        "id": 1,
        "name": "John Doe",
        "email": "john@example.com"
      },
      {
        "id": 2,
        "name": "Jane Smith",
        "email": "jane@example.com"
      }
    ]
  }
}
```

**Relasi Dalam Query**

Contohnya, jika ada tabel `orders` yang terkait dengan `users`, bisa membuat query seperti ini:

```graphQL
query {
  users {
    name
    orders {
      id
      product_name
    }
  }
}
```

## Mutation Dalam Hasura

Mutation dalam Hasura adalah jenis operasi GraphQL yang digunakan untuk mengubah data dalam database, seperti **menambahkan** (insert), **memperbarui** (update), atau **menghapus** (delete) data. Mutation memungkinkan klien untuk melakukan operasi perubahan data dengan fleksibilitas tinggi.

**Contoh Mutation Insert Data:**

menambah data dari table `users` yang memiliki kolom `id`, `name`, `email`.

```graphQL
mutation {
  insert_users(objects: {name: "John Doe", email: "john@example.com"}) {
    returning {
      id
      name
      email
    }
  }
}

```

Penjelasan:

1. `insert_users`: Operasi untuk menambahkan data ke tabel users.
2. `objects`: Objek data yang ingin dimasukkan.
3. `returning`: Data yang ingin dikembalikan setelah operasi selesai.

hasil:

```graphQL
{
  "data": {
    "insert_users": {
      "returning": [
        {
          "id": 1,
          "name": "John Doe",
          "email": "john@example.com"
        }
      ]
    }
  }
}

```

**Contoh Mutation Update Data:**
Untuk memperbarui data `users` berdasarkan `id`

```graphQL
mutation {
  update_users(where: {id: {_eq: 1}}, _set: {email: "newemail@example.com"}) {
    returning {
      id
      name
      email
    }
  }
}
```

Penjelasan:

1. `update_users`: Operasi untuk memperbarui data di tabel users.
2. `where`: Kondisi untuk menentukan data mana yang akan diperbarui.
3. `_set`: Data baru yang ingin diubah.
4. `returning`: Data yang dikembalikan setelah pembaruan.

Hasil:

```graphQL
{
  "data": {
    "update_users": {
      "returning": [
        {
          "id": 1,
          "name": "John Doe",
          "email": "newemail@example.com"
        }
      ]
    }
  }
}

```

**Contoh Mutation Delete Data:**
Untuk menghapus pengguna berdasarkan `id`.

```graphQL
mutation {
  delete_users(where: {id: {_eq: 1}}) {
    returning {
      id
      name
    }
  }
}
```

Penjelasan:

1. `delete_users`: Operasi untuk menghapus data di tabel users.
2. `where`: Kondisi untuk menentukan data mana yang akan dihapus.
3. `returning`: Data yang dikembalikan setelah penghapusan.

Hasil:

```graphQL
{
  "data": {
    "delete_users": {
      "returning": [
        {
          "id": 1,
          "name": "John Doe"
        }
      ]
    }
  }
}
```

## Subscription Dalam Hasura

![Subscription Hasura](/img/subscription_hasura.png)

**Subscription** dalam Hasura adalah salah satu jenis operasi GraphQL yang memungkinkan klien untuk menerima pembaruan real-time dari database setiap kali data berubah. Dengan subscription, tidak hanya membaca data tetapi juga **mendapatkan notifikasi secara langsung jika ada perubahan**, seperti penambahan, penghapusan, atau pembaruan data.

**Cara Kerja Subscription di Hasura**

1. WebSocket Protocol
   **Subscription** di Hasura menggunakan protokol WebSocket untuk menjaga koneksi terbuka antara klien dan server. Ketika data berubah, **server secara otomatis mengirimkan pembaruan ke klien yang sudah berlangganan**.

2. Sintax yang mirip seperti Query Biasa
   Syntax untuk subscription sangat mirip dengan query. **Perbedaannya hanya pada kata kunci subscription yang menggantikan query**.

contoh subscription di Hasura:

Misalkan kita memiliki table `users`, dengan kolom `id`, `name`

**Mendapatkan data users denangan subscription:**

```graphQL
subscription {
  users {
    id
    name
  }
}
```

Hasil: Klien akan mendapatkan data awal dari tabel messages. Jika ada perubahan (seperti penambahan pesan baru), data yang diperbarui akan langsung dikirimkan ke klien.

**Subscription Dengan Filter**

```graphQL
subscription {
  messages(where: {sender: {_eq: "John"}}) {
    id
    content
  }
}
```

Hasil:
Klien hanya akan menerima pembaruan untuk pesan yang dikirim oleh "John".

**Subscription Dengan Sorting**

```graphQL
subscription {
  messages(order_by: {created_at: desc}) {
    id
    content
    sender
  }
}
```

Hasil:
Data akan disortir berdasarkan waktu pembuatan (created_at), dan klien akan menerima pembaruan dengan urutan yang sesuai.

> Subscription di Hasura adalah fitur powerful untuk mendukung aplikasi real-time. Dengan memanfaatkan subscription, pengembang dapat membangun aplikasi yang responsif terhadap perubahan data tanpa perlu menulis kode tambahan untuk sinkronisasi. Hal ini membuat Hasura menjadi pilihan ideal untuk aplikasi modern yang membutuhkan pembaruan data secara instan.

## Menghubungkan Hasura ke Database

![Macam Macam Koneksi Database](/img/macam_macam_koneksi_database.png)

Hasura memungkinkan Anda untuk **menggabungkan data antar model di berbagai penyimpanan data** (data store), sehingga menciptakan grafik data yang terhubung secara banyak. Proses ini bekerja secara transparan dengan kemampuan bawaan Hasura. Selain itu, Hasura juga mendukung federasi, yaitu kemampuan untuk mengintegrasikan beberapa instance Hasura menjadi satu sistem terpadu.

## Perbedaan Antara API Tradisional dan Hasura

![cara_kerja_rest_API](/img/cara_kerja_rest_API.png)

Dalam pengembangan API tradisional, setiap kali membuat endpoint baru untuk mengakses data tertentu, perlu menulis ulang logika untuk otorisasi, untuk memastikan bahwa data hanya dapat diakses oleh pengguna yang berhak. **Masalahnya, meskipun data yang sama diakses melalui berbagai jalur (endpoint)**, logika otorisasi tersebut biasanya:

- Ditulis secara terpisah untuk setiap endpoint.

  **contoh :**

  - Endpoint `GET /users/:id` untuk mengambil data pengguna tertentu.

  - Endpoint `POST /users/:id/update` untuk memperbarui data pengguna.

  > Pada kedua endpoint ini, meskipun data pengguna sama, tetap harus menulis logika otorisasi/autentikasi dua kali untuk memastikan hanya pengguna yang berwenang yang dapat mengakses atau memperbarui data tersebut.

- Inkonstistensi dalam Implementasi.
- Meningkatkan Kompleksitas dan Risiko Kesalahan.
- Waktu dan Upaya yang Boros.

![otentikasi dalam hasura](/img/otentikasi_dalam_hasura.png)

Di Hasura, izin (permissions) didefinisikan secara deklaratif langsung pada model data. Artinya, aturan akses ke data ditentukan langsung di tingkat model (misalnya tabel atau kolom), bukan di setiap jalur akses (endpoint) seperti dalam pendekatan tradisional.

**Manfaat Pendekatan Ini**

1. Menghilangkan Duplikasi

   Anda tidak perlu menulis logika otorisasi secara manual di setiap endpoint atau fungsi, karena aturan sudah ditentukan di model data.

2. Mengurangi Bug

   Karena logika otorisasi dikelola secara terpusat dan otomatis diterapkan oleh Hasura, risiko kesalahan implementasi atau inkonsistensi menjadi jauh lebih kecil.

3. Kinerja yang Optimal

   Query yang dikirim ke database sudah dioptimalkan dengan predikat otorisasi. Ini mengurangi beban kerja server backend dan meningkatkan performa aplikasi.

4. Keamanan yang Konsisten

   Tidak ada celah keamanan karena aturan otorisasi selalu diterapkan dengan cara yang sama, di mana pun data diakses.

> **Kesimpulan**:
> Dengan pendekatan deklaratif ini, Hasura memastikan bahwa setiap akses ke model data sudah secara otomatis dilindungi oleh aturan otorisasi yang telah ditentukan. Hal ini tidak hanya menyederhanakan pengembangan aplikasi tetapi juga memastikan keamanan, mengurangi bug, dan meningkatkan performa aplikasi.

## Performa Hasura

![Performa Hasura](/img/performa_hasura.png)

Hasura dirancang untuk memberikan performa tinggi secara default. Artinya, Hasura tidak hanya fokus pada fungsionalitas, tetapi juga pada kecepatan dan efisiensi dalam menangani permintaan (requests) dari aplikasi.

Hasura jauh **lebih efisien dalam menangani jumlah permintaan** dari aplikasi dibandingkan dengan framework API kustom yang dibangun dari awal. Misalnya:

- API kustom: Pengembang perlu menulis kode untuk menangani query, logika bisnis, dan aturan otorisasi secara manual.Hal ini bisa memakan waktu lebih lama dan menghasilkan kode yang kurang efisien.
- Hasura: Hasura **mengotomatisasi** banyak hal, termasuk **otorisasi** dan **query ke database**, sehingga aplikasi bisa melayani lebih banyak permintaan dalam waktu yang lebih singkat. **Hasura bisa menangani 10 kali lebih banyak permintaan dibandingkan solusi API kustom yang serupa**, bahkan jika aplikasi memiliki logika bisnis yang kompleks.

> Jadi, meskipun aplikasi yang dibuat memiliki query yang rumit atau aturan otorisasi yang ketat, Hasura dapat tetap menangani beban yang lebih besar tanpa mengurangi performa.

**Mengelola Jutaan Subscription**

Hasura dapat mengelola jutaaan subscription (misalnya, pengguna yang berlangganan pembaruan data secara real-time) dengan sangat efisien. Subscription ini digunakan dalam aplikasi yang memerlukan pembaruan data secara langsung atau real-time.

- **Hasura + Postgres**: Hasura menggunakan PostgreSQL sebagai database, yang sangat kuat dan dapat menangani data dalam jumlah besar. Kombinasi ini memungkinkan Hasura untuk **mendukung jutaan koneksi atau subscription secara bersamaan**.
- **Perangkat Keras Murah**: Keunggulan lainnya adalah bahwa kombinasi Hasura dan PostgreSQL ini bisa berjalan di perangkat keras yang murah (komoditas), tanpa memerlukan server mahal atau infrastruktur yang rumit.

> Dengan kata lain,kita bisa memiliki aplikasi yang mendukung banyak pengguna dan banyak koneksi real-time (seperti aplikasi chat, atau aplikasi yang memerlukan data yang terus diperbarui), bahkan jika menggunakan server dengan biaya rendah.

## Memanfaatkan Hasura

![Memanfaatkan Hasura](/img/memanfaatkan_hasura.png)

Hasura dapat digunakan sebagai lapisan data utama (native data layer) dalam aplikasi, menggantikan peran database langsung. Artinya, **tidak perlu menulis query SQL manual atau membangun API untuk berinteraksi dengan database**.

Hasura mendukung subscriptions, yang memungkinkan aplikasi untuk mendengarkan perubahan data secara real-time. Misalnya, **jika ada data yang ditulis atau diperbarui langsung ke database (misalnya pengguna baru ditambahkan), aplikasi yang berlangganan (subscribe) akan menerima pembaruan ini secara langsung.**

Hasura memungkinkan Anda untuk mengintegrasikan dengan layanan lain atau stack teknologi yang sudah ada melalui **event triggers** dan **scheduled triggers**.

- **Event triggers** memungkinkan Hasura untuk mendengarkan peristiwa (events) yang terjadi di database, seperti insert, update, atau delete pada data tertentu, dan kemudian melakukan aksi tertentu (misalnya, mengirim data ke API lain, memicu alur kerja lain).

- **Scheduled triggers** memungkinkan Anda untuk mengatur tugas terjadwal (misalnya, menjalankan proses tertentu pada waktu yang telah ditentukan, seperti memperbarui data atau mengirim laporan).

> Anda dapat membuat Hasura sebagai lapisan data utama untuk aplikasi Anda, memungkinkan **interaksi data yang lebih mudah dan efisien**. Anda juga dapat memanfaatkan fitur-fitur seperti **subscriptions** untuk pembaruan data real-time, **event triggers dan scheduled triggers** untuk mengintegrasikan dengan sistem lain, serta **mempublikasikan query GraphQL** yang parametrik sebagai endpoint HTTP. **Semua fitur ini memungkinkan Anda untuk membangun aplikasi yang lebih terintegrasi, otomatis, dan efisien.**
