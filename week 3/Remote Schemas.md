# Pengertian

**Remote schemas** dalam Hasura adalah fitur yang memungkinkan integrasi API GraphQL dari sumber lain ke dalam skema GraphQL Hasura. Dengan menggunakan remote schemas, Hasura dapat menggabungkan beberapa API GraphQL menjadi satu endpoint GraphQL tunggal.

**Remote schemas** sangat berguna jika kamu ingin mengakses data dari berbagai layanan atau microservices yang menyediakan API GraphQL, tetapi ingin mengonsolidasikan akses ke dalam satu GraphQL endpoint untuk aplikasi klien.

Cara Kerja Remote Schemas:

1. **Integrasi API GraphQL Eksternal**: Kamu bisa menambahkan API GraphQL eksternal (misalnya API GraphQL dari layanan lain) ke dalam skema Hasura.
2. **Penggabungan Skema**: Hasura akan menggabungkan skema API eksternal dengan skema internal-nya, memungkinkan query dan mutation yang dijalankan melalui Hasura untuk mengakses kedua sumber tersebut.
3. **Forwarding Request**: Ketika klien membuat query atau mutation yang membutuhkan data dari API remote, Hasura akan meneruskan permintaan tersebut ke remote schema dan menggabungkan hasilnya dengan data lokal (jika ada).
4. **Fitur Authorization**: Remote schemas juga bisa dilindungi oleh otorisasi, seperti JWT atau header API keys, yang memastikan bahwa hanya permintaan yang sah yang diteruskan ke remote A

Keuntungan Menggunakan Remote Schemas:

- Penggabungan Data: Menggabungkan beberapa API GraphQL ke dalam satu endpoint.
- Modularitas: Memungkinkan untuk mengintegrasikan layanan microservices dengan lebih mudah.
- Mengurangi Overhead Klien: Klien hanya perlu berinteraksi dengan satu endpoint GraphQL tanpa harus mengelola beberapa API secara terpisah.

Implementasi Remote Schema:

- Tambahkan remote schema melalui Hasura Console atau dengan API Admin Hasura.
- Tentukan URL dan autentikasi (misalnya JWT) untuk remote schema.
- Query ke remote schema dapat dilakukan dengan syntax GraphQL yang sama seperti query biasa, hanya dengan menambahkan nama remote schema di query.

# Langkah Integrasi dengan Remote Schemas

1. Siapkan API Graphql untuk integrasi

   saya menggunakan link API https://countries.trevorblades.com/ untuk contoh dibawah ini. api ini adalah data negara-negara didunia beserta detailnya.

2. Buka console Hasura

   ![alt](/img/console_hasura_remote_schemas.png)

3. Klik add untuk menambah remote schemas baru

4. Isi data mulai dari nama, deskripsi, dan url apinya.

   ![alt](/img/remote_schema_isi_data.png)

5. Coba lakukan query pada remote schemas yang sudah ter-mapping

   ![alt](/img/remote_schema_query.png)
