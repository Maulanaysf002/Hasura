# Pengertian

Postman adalah aplikasi komputer yang digunakan untuk pengujian API. Postman mengirim permintaan API ke server web dan menerima respons, apa pun itu. Tidak ada pekerjaan tambahan atau pengaturan kerangka kerja yang diperlukan saat mengirim dan menerima permintaan di Postman.

# Menghubungkan Hasura dengan Postman untuk Graphql

1. Download dan Install terlebih dahulu aplikasi postman di browser

   Buka browser dan kunjungi situs resmi Postman di https://www.postman.com/downloads/. dan download postman tersebut. setelah terdownload buka file installer postman dan jalankan penginstallan.

2. Buka dan login ke dalam postman

   ![alt](/img/postman_dashboard.png)

3. Buat sebuah request baru, dengan method graphQL

   ![alt](/img/postman_new_request.png)

4. Tambahkan admin secret hasura

   ![alt](/img/postman_tambahkan_admin_secret.png)

5. Jika berhasil koneksinya, maka lakukan query dengan method post.

   ![alt](/img/postman_buat_query.png)

# Menghubungkan Hasura dengan Postman dengan GraphQL

1. Buka Aplikasi Postman, lalu buat request dengan pilih mode GraphQL.

   ![alt](/img/postman_koneksi_dengan_graphQL.png)

2. Lakukan konfigurasi url dan header pada hasura.

   ![alt](/img/postman_graphql_add_header.png)

3. Pada halaman query, pilih click pada bagian graphQL instropection.

   ![alt](/img/postman_graphql_intropection.png)

   Hasilnya adalah schema yang ada pada hasura bisa dimapping dengan postman:

   ![alt](/img/postman_hasil_instropeksi.png)

4. Testing query pada postman

   ![alt](/img/postman_query_mode_graphql.png)

   hasilnya adalah:

   ![alt](/img/postman_result_mode_graphql.png)
