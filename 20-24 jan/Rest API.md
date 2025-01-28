# Pengertian Rest API

## Pengertian API

**API** singkatan dari Application Programming Interface adalah kumpulan aturan / code yang membuat 2 program atau lebih dapat berkomunikasi. API menjadi jembatan antar sistem yang menghubungkan client (program yang membutuhkan data) dengan server (database).

Dengan kata lain, **API** adalah penghubung / perantara antar berbagai aplikasi, baik dalam satu platform atau lintas platform.

**API** membantu developer untuk mengkoneksikan fitur dengan aplikasi yang sudah ada. Hal ini membuat pekerjaan tim developer menjadi lebih efisien, tanpa harus mengembangkan fitur dari nol. Developer cukup mengambil data dari platform / aplikasi lain melalui API.

## Cara Kerja API

![alt](/img/cara_kerja_api.jpeg)

- Aplikasi mengakses API

  Bagian pertama dari cara kerja API adalah ketika pengguna mengakses sebuah aplikasi. Untuk memudahkan penjelasan saya menggunakan contoh Traveloka.

  Ketika saya ingin memesan tiket pesawat untuk tujuan tertentu, Traveloka akan mengakses API maskapai penerbangan yang sudah dihubungkan.

- API Melakukan Request ke Server

  setelah aplikasi melakukan hit pada API (mengakses API). request akan diteruskan ke dalam server.

  API yang di akses oleh user dalam Traveloka akan meneruskan permintaan ke server maskapai penerbangan.

- Server Memberi Respon ke API

  Ketika menemukan data yang sesuai permintaan, server kembali menghubungi API. Data tersebut berupa informasi seperti ketersediaan tempat duduk, jam keberangkatan dan lainnya.

- API Menyampaikan Respon ke Aplikasi
  setelah respons didapat, API akan menerukan respons tersebut kembali ke aplikasi Traveloka.

## Macam-macam arsitektur API

1. REST API

   REST merupakan salah satu gaya arsitektur API yang paling populer dan banyak digunakan. REST menggunakan konsep sederhana berbasis HTTP seperti GET, POST, PUT, dan DELETE untuk mengakses dan memanipulasi data. API RESTful berfokus pada sumber daya (resources) yang direpresentasikan dalam format yang dapat dibaca oleh mesin, seperti JSON atau XML.

2. SOAP (Simple Object Access Protocol)

   SOAP adalah gaya arsitektur API yang lebih kompleks dan formal. SOAP menggunakan protokol XML untuk pertukaran pesan antara klien dan server. Dalam SOAP, pesan dikirim dalam format XML dan mendefinisikan protokol yang ketat untuk komunikasi antara aplikasi.

3. GraphQL

   **GraphQL** adalah gaya arsitektur API yang dikembangkan oleh Facebook. GraphQL memungkinkan klien untuk mengirim permintaan yang spesifik terkait data yang diperlukan, sehingga mengurangi jumlah permintaan yang harus dikirim ke server. Dengan GraphQL, klien memiliki kontrol penuh terhadap data yang diterima dari server.

4. JSON-RPC (Remote Procedure Call)

   **JSON-RPC** adalah protokol yang memungkinkan pemanggilan prosedur jarak jauh melalui HTTP atau protokol transport lainnya. Pesan JSON-RPC dikirim menggunakan format JSON dan berisi informasi tentang metode yang akan dipanggil dan parameter yang diterima.

5. XML-RPC (Remote Procedure Call)

   XML-RPC merupakan protokol yang serupa dengan JSON-RPC, namun menggunakan format XML untuk pertukaran pesan. XML-RPC memungkinkan pemanggilan prosedur jarak jauh melalui HTTP atau protokol transport lainnya.

6. WebSocket

   WebSocket adalah protokol komunikasi dua arah antara klien dan server yang memungkinkan pertukaran data real-time. WebSocket memungkinkan pengiriman pesan secara langsung antara klien dan server tanpa perlu melakukan permintaan ulang.

7. gRPC

   gRPC adalah kerangka kerja remote procedure call (RPC) yang dikembangkan oleh Google. gRPC menggunakan Protocol Buffers sebagai format pesan dan HTTP/2 sebagai protokol transport. gRPC memungkinkan komunikasi efisien antara klien dan server dengan dukungan untuk berbagai bahasa pemrograman.

8. OData (Open Data Protocol)

   OData adalah protokol standar yang memungkinkan akses data melalui API web. OData memungkinkan klien untuk melakukan operasi CRUD (Create, Read, Update, Delete) pada sumber daya melalui URL yang konsisten dan dapat diprediksi.

[Sumber Bacaan](https://www.codepolitan.com/blog/8-macam-gaya-arsitektur-api-dalam-web/)

## Apa itu RestAPI

Rest API (Representational State Transfer Application Programming Interface) adalah API layanan website menggunakan permintaan HTTP untuk melakukan operasi CRUD (Create, Read, Update, Delete) pada data.

Rest API dirancang agar sederhana dan fleksibel sehingga, memungkinkan pengembang membangun aplikasi yang dapat bekerja di berbagai bahasa dan kerangka kerja pemrograman. Salah satu fitur utama Rest API adalah penggunaan metode HTTP untuk melakukan operasi CRUD. Empat metode HTTP utama yang digunakan dalam Rest API adalah GET, POST, PUT, dan DELETE.

GET digunakan untuk mengambil data dari server, POST digunakan untuk membuat data baru di server, PUT digunakan untuk memperbarui data yang ada di server, dan DELETE digunakan untuk menghapus data dari server. Rest API adalah menggunakan serangkaian batasan dan prinsip arsitektural untuk memastikannya andal, dan mudah digunakan.

# Pengertian GraphQl

**GraphQL** adalah **bahasa kueri** untuk API dan **runtime** untuk menjalankan kueri tersebut dengan data yang ada. GraphQL memungkinkan klien untuk meminta data yang tepat yang mereka butuhkan, tidak lebih dan tidak kurang. berbeda dengan REST, di mana klien sering kali harus membuat beberapa permintaan (mengakses endpoint) untuk mendapatkan semua data yang diperlukan.

GraphQL muncul pada tahun 2012 sebagai respons terhadap kebutuhan akan kecepatan dalam platform-platform media sosial yang bermunculan.

kapan harus menggunakan graphQL:

- **Aplikasi mobile**: GraphQL sangat cocok untuk aplikasi mobile yang memiliki batasan bandwidth dan memerlukan data yang sangat spesifik.
- **Aplikasi dengan antarmuka yang kompleks**: GraphQL memungkinkan Anda membangun antarmuka yang dinamis dan responsif dengan mudah.
- **Tim pengembangan yang besar**: GraphQL dapat membantu meningkatkan efisiensi pengembangan dengan menyediakan satu sumber kebenaran untuk data.

# persamaan antara GraphQL dan REST API

Baik GraphQL dan REST adalah gaya arsitektur API populer yang memungkinkan pertukaran data antara berbagai layanan atau aplikasi dalam model klien-server.

REST dan GraphQL dapat membuat, memodifikasi, memperbarui, dan menghapus data pada aplikasi, layanan, atau modul yang terpisah melalui API.

Tim frontend dan backend menggunakan arsitektur API ini untuk membuat aplikasi yang modular dan mudah diakses. Menggunakan arsitektur API membantu menjaga sistem tetap aman, modular, dan dapat diskalakan. Hal ini juga membuat sistem memiliki performa yang lebih baik dan menjadi lebih mudah berintegrasi dengan sistem lain.

[Sumber Bacaan](https://aws.amazon.com/id/compare/the-difference-between-graphql-and-rest/)

# Perbedaan Rest API dan GraphQL
