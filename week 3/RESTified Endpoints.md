# RESTified Endpoints

## 1. Masuk ke Menu API pada Console Hasura

Pertama, masuk ke menu API di Hasura Console. Setelah itu, buatlah query GraphQL yang ingin diubah menjadi RESTful endpoint (RESTified). Anda dapat melihat query yang tersedia dengan mengeklik tombol **Explorer** yang terdapat di bagian atas field query GraphQL.

![alt](/img/hasura_console_menu_API.png)

## 2. Membuat REST Endpoint

Setelah menentukan query yang akan diubah, klik tombol **REST** di bagian atas field query GraphQL.

![alt](/img/hasura_klik_tombol_rest.png)

lalu akan diarahkan ke halaman **Rest**.

![alt](/img/hasura_halaman_rest.png)

## 3. Konfigurasi REST Endpoint

- Masukkan nama untuk REST endpoint.
- Berikan deskripsi mengenai query (opsional).
- Centang box method yang ingin diubah menjadi REST endpoint (RESTified). Misalnya, pilih method GET untuk mempermudah developer dalam mengakses query.
- Setelah konfigurasi selesai, klik tombol Create untuk membuat REST endpoint.

![alt](/img/hasura_create_rest.png)

Jika berhasil, REST endpoint yang telah Anda buat akan muncul pada daftar REST endpoint seperti gambar berikut.

![alt](/img/hasura_hasil_create_rest.png)

## 4. Menggunakan REST Endpoint di Postman

- Buka Postman dan masukkan link REST endpoint yang telah dibuat.
- Pilih method yang sesuai dengan REST endpoint tersebut (misalnya GET).
- Jangan lupa untuk menambahkan header x-hasura-admin-secret beserta valuenya.
- Klik tombol Send untuk menjalankan REST endpoint dan melihat hasilnya pada kolom Response.

![alt](/img/hasura_testing_rest_nasabah.png)

# REST API Metode: GET dengan Parameter

Pada metode **GET**, parameter biasanya dikirim melalui URL sebagai query parameters. Ketika menggunakan GraphQL, Anda dapat mengimplementasikan query GraphQL dalam REST API.

## 1. REST API GET Request dengan Parameter

Susun GraphQL yang ingin dijadikan **Rest** dengan GraphiQL. misalnya untuk mendapatkan data nasabah berdasarkan id yang dikirim dengan parameter.

![alt](/img/hasura_rest_dengan_parameter.png)

setelah selesai klik rest untuk membuat endpoint.

isikan nama, deskripsi, metode, yang diinginkan.

## 2. Testing di Postman

1. Buka Postman
2. Buat Request Baru
3. Isikan Header Secret Hasura
4. masukan url endpoint yang telah dibuat ke dalam request yang sudah dibuat, lalu send request tersebut.

![alt](/img/hasura_getnasabahbyid_testing.png)
