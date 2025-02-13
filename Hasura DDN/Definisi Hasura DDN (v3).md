# Apa itu Hasura DDN

Hasura DDN merupakan versi ke 3 atau yang terbaru dari hasura.

Hasura DDN bekerja seperti Content Delivery Network (CDN) untuk data, dengan tujuan utama meningkatkan performa aplikasi, mengurangi latensi, dan memberikan pengalaman pengguna yang lebih responsif, terutama untuk aplikasi yang melayani pengguna di berbagai lokasi geografis.

# Fitur Utama Hasura DDN

1. **Caching Data**:

   Query GraphQL yang sering digunakan dapat di-cache di edge nodes (server yang berada lebih dekat dengan pengguna). Ini mengurangi latensi dan beban pada server utama.

2. **Global Edge Network**:

   Data disajikan dari edge nodes (server yang berada lebih dekat dengan pengguna) yang tersebar di seluruh dunia, memastikan data diterima lebih cepat oleh pengguna terlepas dari lokasi geografis mereka.

3. **Real-time Support**:

   DDN juga mendukung data real-time, memungkinkan perubahan data di backend segera dipush ke klien melalui jaringan edge.

4. **Secure Delivery**:

   Keamanan terjamin melalui mekanisme seperti HTTPS, kontrol akses berbasis token, dan kebijakan keamanan Hasura.

5. **Optimisasi API**:

   Dengan memanfaatkan DDN, pengembang dapat mengurangi biaya infrastruktur karena query tidak selalu harus mencapai server Hasura utama.

# Kapan Menggunakan Hasura DDN

- Aplikasi dengan banyak pengguna global.
- Aplikasi yang membutuhkan waktu respon rendah (low latency) untuk GraphQL API.
- Aplikasi dengan query yang sering diulang atau permintaan data yang sama oleh banyak pengguna.
- Proyek yang memerlukan pengurangan beban server utama untuk skala besar.

# Perbedaan Hasura v2 dan Hasura DDN

## Hasura v2

Hasura v2 merupakan Versi utama dari platform Hasura yang menyediakan kemampuan untuk membangun aplikasi berbasis **GraphQL** dengan cepat.

**berfokus pada** Pengelolaan GraphQL API, real-time data, dan integrasi database.

**Fitur Utama**:

- Auto-generate GraphQL API dari database PostgreSQL, SQL Server, BigQuery, dan lainnya.
- Role-based Access Control (RBAC) untuk mengamankan data.
- Event Triggers untuk integrasi backend (misalnya, memicu webhook pada perubahan data).
- Remote Schemas untuk menggabungkan beberapa API GraphQL.
- Action untuk menjalankan logika custom menggunakan REST atau GraphQL.
- Real-time subscriptions untuk pembaruan data langsung.

## Hasura DDN (Data Delivery Network)

Hasura DDN merupakan Fitur tambahan atau layanan dari Hasura yang dirancang untuk mengoptimalkan pengiriman data GraphQL melalui caching, edge delivery, dan pengurangan latensi.

**fokus utama** dari Hasura DDN adalah Pengiriman data GraphQL yang lebih cepat dengan memanfaatkan edge nodes dan caching.

**Fitur Utama**:

- **Global Edge Caching**: Data sering di-cache di edge nodes untuk mengurangi permintaan ke server backend.
- **Latency Reduction**: Menggunakan jaringan global untuk menyajikan data dari lokasi terdekat pengguna.
- **Data Freshness**: Caching dinamis yang dapat diatur untuk mempertahankan data yang mutakhir.
- **Real-time Optimization**: Mendukung real-time query dengan optimalisasi dari edge.
- **Built-in Security**: Penyampaian data aman melalui HTTPS dan kontrol akses Hasura.
