- judul video: From Monolith to Supergraph: How to Tame Microservice Complexity and Chaos
- link video: https://www.youtube.com/watch?v=bTbkdUdsUUE
<br>
<hr>

# Introduction To Hasura

![intro to hasura](/img/video3_introduction_to_hasura.png)

> menit 00:00 - 01:59

- Perusahaaan hasura beranggotakan sekitar 180 orang di seluruh dunia.
- Kantor pusat di San Francisco, Amerika Serikat.
- Salah satu hal yang menjadi perhatian utama tim hasura adalah **bagaimana cara berpikir untuk membuat beberapa tim menjadi produktif, yang tentu saja merupakan topik pembicaraan yang sama yang muncul ketika kita berpikir tentang monolit hingga layanan mikro.**

# Monolith To Microservices

![monolith to microservices](/img/monolith_to_microservices.png)

> menit 01:59 - 06:33

**Kondisi Menggunakan Monolith API:**

- Sistem awalnya mungkin menggunakan **monolith API**, seperti yang dibangun dengan framework seperti Rails, Django, atau Spring Boot. API ini dirancang untuk melayani domain tertentu dengan mengintegrasikan satu atau lebih sumber data.
- API ini digunakan oleh berbagai konsumen, seperti aplikasi internal, pengembang, aplikasi eksternal, atau bahkan API mitra.

**Kebutuhan Skalabilitas**

- Seiring waktu, kebutuhan bisnis dan teknis berkembang:

  - **Penambahan fitur baru**: Sistem harus mendukung lebih banyak fitur untuk memenuhi kebutuhan bisnis.
  - **Peningkatan penggunaan infrastruktur**: Volume permintaan meningkat secara drastis, dari ratusan permintaan per detik menjadi jutaan permintaan per detik.

**Tantangan Pada Monolith**

- Sistem monolith menghadapi kesulitan untuk mengimbangi pertumbuhan ini karena:
  - **Kompleksitas**: Menambah fitur baru atau memperluas fungsionalitas menjadi lebih sulit karena keterkaitan antar bagian dalam sistem.
  - **Keterbatasan skalabilitas**: Sistem monolith sering kali tidak dapat menangani lonjakan beban atau kebutuhan arsitektur yang lebih fleksibel.

**Transisi Ke Microservices**

Untuk mengatasi tantangan tersebut, banyak tim memilih beralih ke microservices.
Microservices memungkinkan:

- Pemecahan sistem besar menjadi layanan-layanan kecil yang independen.
- Setiap layanan dapat dikembangkan, diuji, dan di-deploy secara terpisah.
- Skalabilitas lebih baik karena setiap layanan dapat dioptimalkan secara terpisah sesuai kebutuhan.

**Debat Monolith vs Microservices**

Ada diskusi luas di komunitas teknologi tentang kapan harus menggunakan microservices:

- **Overengineering dengan microservices**: Menggunakan microservices sejak awal tanpa alasan yang jelas dapat meningkatkan kompleksitas.
- **Kekuatan monolith**: Untuk sistem yang lebih sederhana atau saat skalabilitas bukan masalah utama, monolith sering kali menjadi pilihan yang lebih efisien.

**Keuntungan Microservices untuk Tim dan Inovasi**

- **Decoupling Tim**: Microservices memungkinkan pemisahan tim yang mengerjakan berbagai bagian sistem, yang memungkinkan mereka untuk berinovasi lebih cepat. Setiap tim dapat bekerja pada layanan yang terpisah tanpa khawatir bahwa pekerjaan mereka akan mempengaruhi tim lain.

  > **Misalnya**, jika tim A mengubah fitur di microservice A, tim B yang mengerjakan microservice B tidak akan terpengaruh, baik dari segi bug, fitur baru, maupun performa.

- **Masalah pada Monolith**: Dalam arsitektur monolith, satu perubahan di bagian tertentu bisa mempengaruhi bagian lain, baik dari sisi bug maupun penggunaan infrastruktur. Dengan microservices, setiap tim bisa lebih terpisah dan bertanggung jawab atas bagiannya sendiri, memungkinkan mereka untuk bekerja lebih cepat dan lebih aman.

**Pemecahan Beban Kerja dan Penggunaan Microservices**

Dengan microservices, setiap tim dapat memilih jenis data layer yang paling sesuai dengan kebutuhan mereka. Sebagai contoh:

- Satu tim mungkin menggunakan database SQL untuk transaksi, sementara tim lain menggunakan data lake untuk analitik realtime atau streaming data.

Pemisahan beban kerja ini memungkinkan tim untuk mengelola dan mengembangkan bagian mereka secara lebih efisien, mengurangi ketergantungan satu sama lain, dan mengatasi masalah skalabilitas dengan lebih mudah.

**Tantangan pada API Konsumen**

- **API Konsumen Tidak Peduli**: Meskipun tim internal dapat mengelola microservices dengan lebih efisien, konsumen API (seperti aplikasi atau produk yang menggunakan API tersebut) tidak peduli dengan bagaimana API dibangun atau dipisah-pisahkan menjadi beberapa microservices. Mereka hanya peduli pada pengalaman terintegrasi.
- **Permintaan untuk Web Scale**: Konsumen ingin produk atau aplikasi yang mereka bangun terintegrasi dengan lancar. Misalnya, jika aplikasi menampilkan data pengguna, mereka juga mungkin membutuhkan data terkait seperti alamat atau transaksi yang berasal dari microservices lain.
  Jika API terbagi dalam beberapa domain, konsumen harus bisa mengakses dan mengintegrasikan data dari berbagai sumber secara transparan.

<hr>

![monolith to microservices 2](/img/video3_monolith_to_microservices_2.png)

> menit 07:07 - 10:19

**Pengalaman Terintegrasi untuk Pengguna dan API**

Meskipun microservices memungkinkan pemisahan domain dan tim, para konsumen API (baik pengembang atau aplikasi) tetap menginginkan pengalaman yang terintegrasi.

- Sebagai contoh, ketika menampilkan data pengguna, kita mungkin juga perlu menampilkan data alamat atau transaksi yang berasal dari microservices yang berbeda.
- Begitu juga dengan data inventaris yang mungkin terhubung dengan sistem katalog merek yang berbeda, bukan hanya sistem inventaris transaksi.

API konsumen menginginkan API yang konsisten, dengan ekspektasi yang jelas mengenai cara API bekerja:

- **Latency rendah.**
- **Error handling** yang konsisten.
- **Pagination** yang standar di seluruh API.
- **Keteraturan** dalam cara data diakses, tidak peduli dari domain mana data itu berasal.

**Tantangan dalam Memenuhi Ekspektasi API di Microservices**

Dengan memecah sistem menjadi banyak microservices, tantangan muncul dalam memenuhi ekspektasi tersebut.

- Setiap microservice bisa memiliki pola dan standar API yang berbeda, sehingga akan sulit untuk memberikan garansi konsistensi yang diinginkan oleh konsumen API.

**Strategi yang Ditemui di Organisasi Besar (Enterprise)**

Dalam organisasi besar yang sedang menjalani transformasi ke microservices, ada beberapa inisiatif strategis yang biasanya terkait dengan masalah ini:

- **Microservices Foundation**: Perusahaan sedang menyusun dasar microservices, mengatur lapisan-lapisan microservices yang akan ada, seperti domain APIs, process APIs, capability APIs, dan experience APIs.
- **Data Mesh**: Di sisi data, ada upaya untuk mengelola data di berbagai tempat dan menyatukannya menjadi produk data yang konsisten, meskipun data tersebut disimpan terpisah-pisah.
- **Dilo dan Silo**: Seringkali perusahaan menyilo data terlebih dahulu untuk alasan pengelolaan, namun kemudian mereka ingin mengintegrasikan atau mengdilo data untuk menghasilkan pandangan yang lebih terkoordinasi.

**Tensi antara Decoupling dan Desiloing**

Tensi utama yang muncul adalah bagaimana memisahkan berbagai bagian untuk mempercepat pengembangan (decoupling), namun tetap mempertahankan integrasi dan visibilitas yang memudahkan konsumen API untuk bekerja dengan berbagai data dan layanan secara mulus.

**Decoupling** membuat pengembangan lebih cepat karena tim dapat bekerja secara terpisah, tetapi desiloing diperlukan untuk menjaga kesatuan pengalaman pengguna.
Cognitive overload dapat terjadi jika pengguna harus mengelola banyak API dan domain yang berbeda, sehingga penting untuk menjaga standar yang konsisten.

**Masalah Integrasi antara Domain dan API**

Ketika kita memecah sistem menjadi beberapa microservices, kita harus menghindari masalah seperti **spaghetti crisscross** (kerumitan integrasi) yang muncul ketika data dan API dari berbagai domain harus dihubungkan satu sama lain.

Standardisasi API sangat penting. Setiap domain harus membangun API dengan pola yang konsisten untuk memastikan bahwa penggabungan data dari berbagai layanan bisa berjalan lancar.

<hr>

![monolith to microservices 3](/img/video3_monolith_to_microservices_3.png)

> menit 10:52 - 11:21

**Pengalaman Pengembang dalam Menggunakan API yang Terpisah**

Pengembang atau aplikasi client yang mengkonsumsi berbagai microservices dan API yang terpisah mungkin akan merasa kesulitan dan frustasi jika standar API tidak konsisten.

> Sebagai contoh, jika dua layanan berbeda mengimplementasikan pagination dengan cara yang berbeda, hal ini bisa membingungkan dan menyulitkan pengembang yang mencoba mengintegrasikan API-API tersebut.

Konsistensi dalam cara API beroperasi, seperti bagaimana menangani pagination atau error, sangat penting agar pengembang tidak merasa "terbebani" oleh pengalaman integrasi yang buruk.

**Tantangan untuk Pemilik Domain dalam Menjaga Konsistensi**

Pemilik domain yang menyediakan API untuk layanan mereka harus memastikan bahwa API mereka tetap sinkron dengan **implementasi, dokumentasi, dan sumber data yang mendasarinya.**

Seiring berjalannya waktu, layanan dan domain API akan terus berkembang. Jika pemilik domain tidak berhati-hati, API, dokumentasi, dan sumber data bisa terpisah atau out of sync satu sama lain.
Drift ini bisa terjadi, di mana implementasi API tidak lagi sesuai dengan dokumentasi atau data yang ada, dan ini bisa menciptakan masalah besar dalam pemeliharaan dan penggunaan API.

**Masalah Integrasi dan Orkestrasi Data**

**Data Integration** dan **Orkestrasi** adalah tantangan besar ketika menggabungkan berbagai microservices yang memiliki API yang berbeda. Semua API ini harus berinteraksi satu sama lain, dan memastikan bahwa data dari berbagai sumber bisa digabungkan secara lancar menjadi satu pengalaman pengguna yang koheren.

- Hal ini membutuhkan **registry terpusat** untuk mencatat dan mengelola informasi tentang layanan dan API yang ada.
- Tanpa registry yang terpusat dan cara yang jelas untuk mengelola interaksi antar API, integrasi antar layanan bisa menjadi sangat rumit dan penuh masalah.

<hr>

![monolith to microservices 4](/img/video3_monolith_to_microservices_4.png)

> menit: 11:55 - 14:34

**Tantangan Pengintegrasian Data di Microservices**

Dalam konteks **microservices**, banyak tim atau aplikasi yang perlu mengakses data dari berbagai sumber dan melakukan data integration yang serupa, berulang kali.

- Proses ini memakan waktu dan rawan kesalahan. Jika terjadi masalah atau bug, misalnya saat mencoba menggabungkan dua data dan mendapatkan hasil null, sulit untuk mengetahui penyebabnya.
- Apakah **null** tersebut disebabkan oleh kesalahan antar sistem? Apakah data tersebut memang **null** secara alami? Atau apakah data tersebut tidak dapat diakses? Semua tim mungkin mengimplementasikan logika yang berbeda untuk menangani hal ini.

**Dokumentasi dan Pemeliharaan API**

Semua API microservices harus didokumentasikan secara terpusat agar mudah ditemukan dan dikelola.

Hal ini adalah tantangan besar karena setiap tim atau domain mungkin memiliki pendekatan yang berbeda dalam menangani integrasi data dan API, dan mereka harus menjaga standarisasi untuk mencegah masalah seperti drift antara implementasi API dan dokumentasi.

**Peningkatan Kerumitan dengan Microservices**

**Microservices** dapat membantu dalam memisahkan dan mengelola domain yang berbeda, tetapi juga memperkenalkan tantangan baru.

- Kerja yang sebelumnya dilakukan dalam monolitik kini perlu diperbanyak dan dikelola secara terpisah di setiap microservice. Misalnya, upaya untuk mencegah drift, memelihara skema API, dan standarisasi harus dilakukan oleh setiap tim secara terpisah, yang dapat menambah kerumitan.

<br>
<hr>

# Introducing the Supergraph

![introduction to supergraph](/img/introduction_to_supergraph.png)

> menit 15:09 - 17:27

**Pengenalan Supergraph**

Supergraph adalah pendekatan yang terinspirasi oleh konsep **GraphQL** untuk menyelesaikan masalah integrasi data antar **microservices**.

- Dalam pendekatan ini, setiap **domain** atau **microservice** dianggap sebagai **subgraph**. Semua subgraph ini kemudian digabungkan secara otomatis menjadi sebuah super graph yang memungkinkan integrasi dan komunikasi antar layanan yang lebih mudah dan konsisten.
- Dengan supergraph, tantangan-tantangan terkait integrasi data, orkestrasi, dan dokumentasi dapat lebih mudah dikelola karena data dari berbagai domain disatukan dalam satu graf terpusat.

**Evolusi dari ESB dan iPass ke Microservices dan GraphQL**

Sebelum munculnya microservices, masalah integrasi data antar silo juga sudah ada, dan digunakan teknologi seperti **ESB (Enterprise Service Bus)** dan **iPaaS (Integration Platform as a Service)**.

- Dalam konteks **microservices**, masalah yang sama ditangani dengan **API gateways**, dan dalam konteks GraphQL, solusi yang lebih terstruktur adalah dengan menggunakan graph gateway yang menghubungkan berbagai GraphQL servers.
- Supergraph merupakan evolusi lebih lanjut dari pendekatan ini, dengan menyatukan subgraph-subgraph dari berbagai domain menjadi satu kesatuan yang lebih mudah diakses.

**Tantangan Crisscross di Microservices**

- Masalah utama dalam microservices adalah adanya tantangan dalam integrasi data antara berbagai domain atau subgraph, yang sering kali membutuhkan banyak pekerjaan manual dan intervensi manusia untuk memastikan semuanya bekerja dengan baik.
- Proses ini memerlukan banyak upaya ekstra, dan ini menjadi sumber rasa sakit baik di level subgraph maupun level integrasi antar microservices.

**Konsep Subgraph Semantik**

Setiap domain dalam organisasi dapat dianggap sebagai subgraph semantik.

- Meskipun **domain-domain** ini mungkin tidak berhubungan secara langsung di level atas, mereka tetap membentuk graf entitas yang berisi node dan model yang terhubung dalam cara tertentu.
- **Subgraph** ini memungkinkan kita untuk memahami dan mengakses data dalam domain tertentu dengan cara yang lebih mudah dan terstruktur. Ini memudahkan pemahaman dan penggunaan API dalam domain tersebut.

**Membangun Supergraph secara Otomatis**

- Jika kita menganggap setiap domain sebagai subgraph, maka ketika beberapa subgraph digabungkan, mereka membentuk sebuah supergraph yang terintegrasi.
- **Supergraph** ini memungkinkan kita untuk mengotomatisasi proses integrasi dan orkestrasi data antar domain tanpa perlu banyak intervensi manual atau pekerjaan ekstra dari tim pengembang.

  - Ini memungkinkan kita untuk mendapatkan registri API organisasi secara otomatis, sehingga kita tidak perlu lagi mengelola registri API secara manual.
  - Ketika subgraph berkembang, supergraph akan terus memperbarui dan menyediakan informasi yang diperlukan untuk mengakses data dari berbagai domain.

**Freeness dalam Pengintegrasian dan Orkestrasi Data**

Salah satu keuntungan besar dari pendekatan **supergraph** adalah bahwa proses integrasi dan orkestrasi data yang sebelumnya memerlukan banyak pekerjaan manual, sekarang dapat diperoleh secara otomatis atau "gratis" ketika subgraph digabungkan menjadi supergraph.

Artinya, kita dapat mengakses data yang saling terkait di tingkat subgraph dan supergraph tanpa perlu mengulang pekerjaan yang sama di setiap tim atau domain.
Ini mengurangi duplikasi usaha dan memungkinkan pemeliharaan dan pembaruan API yang lebih mudah dan lebih efisien.

**Contoh Kasus E-commerce dengan Subgraph**

Sebagai contoh, jika kita memiliki domain e-commerce dengan tiga subgraph:

- **Subgraph Pengguna** dan Alamat (user information and addresses)
- **Subgraph Pesanan** (order information)
- **Subgraph Katalog** Produk dan Inventaris (product catalog and inventory)
  Ketiga subgraph ini dapat digabungkan menjadi satu supergraph yang terintegrasi, memungkinkan akses dan pengelolaan data dari berbagai domain dengan lebih efisien dan terstruktur.

<hr>

![alt](/img/Introducing_the_Supergraph_2.png)

> menit: 17:59

**Fleksibilitas Akses Data untuk Konsumen API**

Dengan menggunakan **GraphQL**, kita memberikan kebebasan kepada konsumen API (misalnya, aplikasi atau tim lain) untuk mengakses data yang mereka butuhkan dengan lebih fleksibel.
Alih-alih mengelola banyak endpoint API yang berbeda untuk setiap jenis data di berbagai domain (seperti pengguna, alamat, pesanan, dll.), GraphQL memungkinkan konsumen API untuk melakukan satu query untuk mendapatkan data dari berbagai domain secara bersamaan.

**Pengambilan Data dalam Satu Panggilan API**

Dengan **GraphQL**, konsumen API dapat meminta data dalam satu panggilan API (satu fetch) dan menentukan sendiri bagian data apa yang ingin mereka ambil, misalnya hanya informasi pengguna dan alamat, tanpa harus membuat banyak permintaan terpisah ke berbagai endpoint.
Ini memungkinkan efisiensi dalam pengambilan data dan mengurangi overhead yang biasanya terjadi dengan pendekatan endpoint tradisional.

**Pengurangan Kompleksitas Pengelolaan Endpoint**

Pendekatan ini mengurangi kebutuhan untuk memelihara banyak endpoint untuk setiap bentuk data yang berbeda di berbagai domain. Sebaliknya, dengan GraphQL, kita bisa memiliki satu API yang bisa mengakses berbagai sumber data yang tersebar di berbagai domain melalui query yang lebih dinamis dan fleksibel.

<hr>

![alt](/img/Introducing_the_Supergraph_3.png)

> menit: 18:34

**Skalabilitas Query Lintas Subgraph**

Dengan menggunakan Supergraph, kita dapat memperluas kemampuan query tidak hanya dalam satu subgraph tetapi juga melintasi berbagai subgraph.
Contohnya, kita dapat melakukan satu query untuk mendapatkan informasi pengguna, alamat, pesanan terbaru, dan detail produk dari pesanan tersebut, semuanya dalam satu panggilan API.
Ini memberikan kemudahan dan efisiensi karena integrasi data antar domain terjadi secara otomatis.

**Integrasi Data yang Didapatkan "Secara Gratis"**

Dengan Supergraph, proses integrasi data yang biasanya membutuhkan usaha manual dan kompleksitas tambahan kini dilakukan secara otomatis.
Konsumen API tidak perlu mengelola logika integrasi di sisi mereka; mereka hanya perlu menentukan query GraphQL, dan sistem akan mengurus penggabungan data dari berbagai domain.

**Pengurangan Overhead Dokumentasi**

Karena Supergraph menggabungkan semua subgraph dalam satu entitas terintegrasi, ini secara otomatis menciptakan dokumentasi terpadu untuk semua domain.
Dokumentasi ini membantu pengembang memahami jumlah domain yang tersedia, hubungan antar data, dan bagaimana cara mengakses informasi tersebut tanpa perlu memelihara dokumentasi terpisah untuk setiap domain.

<hr>

![alt](/img/Introducing_the_Supergraph_4.png)

> menit: 19:07 - 20:06

**Perubahan Paradigma: Endpoint vs. Entitas yang Terhubung**

- **Pendekatan API Tradisional**:
  Dalam pendekatan berbasis endpoint, pengembang harus memahami daftar endpoint API yang terpisah-pisah. Setiap endpoint memiliki fungsi spesifik, dan dokumentasinya harus dipelajari untuk mengetahui cara penggunaannya.
- **Pendekatan Supergraph**:
  Supergraph mengubah cara pandang dari sekumpulan endpoint menjadi graf entitas yang saling terhubung. Setiap entitas memiliki hubungan yang jelas, sehingga lebih mudah dipahami.

**Kemudahan Konsumsi API dengan GraphQL**

- Keterbacaan dan Intuisi:
  Dengan Supergraph, pengembang dapat dengan cepat membangun intuisi tentang cara membaca dan mengakses data yang terhubung. Contoh:

  - Query seperti `user.orders` untuk mendapatkan pesanan pengguna.
  - Query tambahan seperti `order.topFiveProducts` atau `order.mostExpensiveProducts` untuk mendapatkan detail produk tertentu.

- Tanpa Membaca Dokumentasi Endpoint yang Rumit:
  Karena Supergraph menyatukan semua subgraph menjadi satu sumber data yang terorganisir, pengembang tidak perlu mempelajari dokumentasi terpisah untuk setiap endpoint.

**Tantangan dan Solusi**

- **Tantangan dalam API Tradisional**:
  Memahami, membaca, dan mengintegrasikan berbagai endpoint secara manual adalah pekerjaan yang melelahkan dan rentan terhadap kesalahan.
- **Solusi dalam Supergraph**:
  Supergraph menyediakan cara untuk membaca data dengan pendekatan semantik yang terstandarisasi, menjadikan integrasi data lintas domain lebih mudah dan lebih intuitif.

Supergraph memperkenalkan pendekatan berbasis entitas yang terhubung dalam bentuk graf semantik. Hal ini mempermudah pengembang dalam mengakses data, mengurangi beban dokumentasi manual, dan mengatasi kompleksitas integrasi API tradisional berbasis endpoint. Dengan demikian, Supergraph menjadi solusi yang lebih efisien untuk kebutuhan API modern.

<hr>

![alt](/img/Introducing%20the%20Supergraph%20burden.png)

> menit: 20:45 - 24:45

**Membangun Subgraph**

- Definisi Subgraph:
  Setiap domain dalam sistem perlu dikonversi menjadi subgraph, yang menyediakan cara untuk mengakses informasi domain tersebut melalui API GraphQL.
- Tantangan:
  - Apakah subgraph ini akan menjadi layanan baru atau hanya lapisan tambahan di atas layanan atau database yang sudah ada?
  - Penambahan lapisan ini berarti kerja ekstra dalam pengembangan dan operasional.

**Supergraph: Risiko dan Tantangan**

- **Single Point of Failure**:
  Meskipun Supergraph menyatukan API menjadi satu antarmuka terpadu, ia juga dapat menjadi titik kegagalan tunggal (single point of failure) dan bottleneck kinerja.
- **Operasional yang Kompleks**:
  Supergraph memerlukan pengelolaan tambahan, seperti pemantauan dan debugging. Ini meningkatkan beban kerja tim pengembang dan operasi (DevOps).
- **Ketergantungan pada Protokol GraphQL**:
  - Jika seluruh sistem didasarkan pada GraphQL, ini menciptakan keterbatasan karena protokol ini mungkin tidak selalu cocok untuk semua kebutuhan.
  - Contoh:
    - **Real-time data**: Beberapa tim mungkin menginginkan data real-time yang dikirim melalui webhooks alih-alih websockets.
    - **Efisiensi**: Protokol seperti gRPC dengan HTTP/2 atau HTTP/3 dianggap lebih cepat daripada GraphQL karena menggunakan protokol biner.

**Kritik terhadap GraphQL**

Tidak semua organisasi atau tim merasa GraphQL adalah solusi terbaik, terutama dalam hal efisiensi protokol dan real-time data delivery.
Ketergantungan penuh pada GraphQL menciptakan risiko "lock-in" (keterikatan pada teknologi tertentu).

**Solusi: Data Delivery Network (DDN)**

- **Pendekatan Baru**:
  DDN adalah infrastruktur seperti Content Delivery Network (CDN), yang dirancang untuk mengatasi tantangan Supergraph tanpa menciptakan lock-in atau single point of failure.
- **Keunggulan DDN**:
  - Dapat dijalankan di lingkungan perusahaan atau solusi yang di-host oleh penyedia layanan.
  - Dibangun di atas mesin generasi terbaru (H V3 engine).
- **Filosofi Baru**:
  Alih-alih melihat Supergraph sebagai solusi tunggal untuk API, DDN memperluas konsep dengan fokus pada distribusi data yang efisien dan fleksibel.

<br>
<hr>

# Hasura DDN - Data Supergraph made easy

![alt](/img/Hasura%20DDN%20-%20Data%20Supergraph%20made%20easy.png)

> Menit 25:25 - 26:34

<hr>

![alt](/img/Hasura%20DDN%20-%20Data%20Supergraph%20made%20easy_2.png)

> Menit 26:34 - 32:30

<hr>

# Domain-driven

![alt](/img/domain-driven.png)

> Menit 33:06 - 37:35

<hr>

# Federated CI/CD

![alt](/img/Federated%20CICD.png)

> Menit 38:07 - 42:46

<hr>

# Composable & Performant

![alt](/img/Composable%20&%20Performant.png)

> Menit 43:23 - 44:23

![alt](/img/Composable%20&%20Performant_2.png)

> Menit 45:00 - 47:13

<br>
<hr>

# Sumary

![alt](/img/video3_sumary.png)

> Menit 48:21 - 49:29
