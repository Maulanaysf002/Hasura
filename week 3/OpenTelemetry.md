# Pengertian OpenTelemetry (OTel)

**OpenTelemetry (OTel)** adalah proyek open-source yang menyediakan kerangka kerja untuk mengumpulkan, memproses, dan mengirimkan data observabilitas seperti traces, metrics, dan logs dari aplikasi. OTel mendukung berbagai bahasa pemrograman dan platform, memungkinkan pengembang untuk mengintegrasikan observabilitas ke dalam aplikasi mereka dengan mudah.

Fitur Utama OTel:

- Traces: Mencatat perjalanan dan waktu eksekusi fungsi dalam aplikasi.
- Metrics: Mengumpulkan data statistik tentang performa aplikasi, seperti latensi dan throughput.
- Logs: Menyediakan informasi terkait kejadian yang terjadi dalam aplikasi.

# Kegunaan OpenTelemetry pada Hasura

**Integrasi OpenTelemetry dalam Hasura memungkinkan pengembang untuk:**

- Memantau Performa: Mengidentifikasi bottleneck dan masalah kinerja dengan analisis trace dan metrics.
- Debugging: Melihat logs untuk mendiagnosis masalah saat menjalankan query atau mutasi.
- Optimasi: Menggunakan data yang dikumpulkan untuk mengoptimalkan performa aplikasi.

# OTel Exporter pada Hasura

![alt](/img/hasura_openTelemetri_exporter.png)

Exporter di Hasura berfungsi untuk mengirim data yang dikumpulkan ke sistem pemantauan eksternal seperti Jaeger atau Prometheus. Dengan mengkonfigurasi OTel exporter, dapat mengarahkan data observabilitas ke sistem yang lebih kompleks untuk analisis lebih lanjut.

# Endpoint Traces, Metrics, dan Logs

![alt](/img/hasura_opentelemetry_status.png)

untuk melakukan pengisian endpoint pada traces, metrics dan logs, dapat membukanya di halaman setting hasura yang ada simbol roda bergerigi, diklik lalu lihat tulisan atau pilihan opentelemetry exporter. kemudian isikan endpoint pada traces, metric dan logs. jika sudah isikan batch size, trace propagations, headers(optional), attribute(optional). Penjelasan dibawah ini:

1. Traces Endpoint

   Pengertian: Endpoint traces digunakan untuk mengumpulkan informasi tentang query yang dijalankan oleh Hasura. Traces Endpoint ini membantu dalam memahami performa query dan menemukan bottleneck.

   Pengisian: http://10.100.13.205:4318/v1/traces

   Perkiraan/Menduga/seharusnya: Endpoint ini dapat terhubung ke alat pemantauan seperti OpenTelemetry atau Jaeger.

2. Metrics Endpoint

   Pengertian: Endpoint metrics memberikan informasi statistik tentang penggunaan dan performa Hasura, seperti jumlah query yang dieksekusi, latensi, dan penggunaan resource.

   Pengisian: http://10.100.13.205:4318/v1/metrics

   Perkiraan/Menduga/seharusnya: Endpoint ini dapat dihubungkan dengan sistem monitoring seperti Prometheus untuk mengumpulkan dan menganalisis metrik.

3. Logs Endpoint

   Pengertian: Endpoint logs menangkap log dari Hasura, yang bisa membantu dalam debugging dan analisis kesalahan.

   Pengisian: http://10.100.13.205:4318/v1/logs

   Perkiraan/Menduga/seharusnya: mengarahkan logs ke sistem log management seperti Elasticsearch, Grafana Loki, atau sistem logging lainnya.

4. Batch Size

   Pengertian: digunakan untuk mengontrol berapa banyak data yang akan dikirimkan dalam satu batch.

   Pengisian: 512 (default)

   Perkiraan/Menduga/seharusnya: Semakin besar batch size, semakin banyak data yang dikirim sekaligus. Ini dapat mempengaruhi performa dan latensi pengiriman data observabilitas.

5. trace propagations

   Pengertian: Ini adalah format untuk menyebarkan trace antara layanan yang berbeda. Pilih salah satu dari B3 atau tracecontext.

   Pengisian:

   B3 sering digunakan dalam sistem observasi seperti Zipkin.
   tracecontext lebih umum digunakan dalam konteks distribusi trace antar layanan dalam OpenTelemetry.

6. Headers (optional)

   Pengertian: dapat menambahkan headers jika diperlukan, misalnya untuk otentikasi ke OpenTelemetry endpoint atau collector.

7. Attributes (Optional)

   Pengertian: dapat menambahkan atribut khusus untuk tracing, logs, atau metrics yang dikirimkan. Atribut ini biasanya berupa metadata yang relevan untuk operasi yang sedang dilakukan, seperti nama layanan atau informasi pengguna.

# Menghubungkan Hasura ke OpenTelemetry
