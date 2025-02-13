# 1. Jalankan VM di virtualbox dan akses dengan ssh

![alt](/img/server_hostnamectl.png)

Saya menggunakan vm dengan hostname server 2, didalam vm virtualbox, dengan os ubuntu versi Ubuntu 24.04.1 LTS.

# 2. Installasi Docker

Jika Belum Menginstall docker dapat mengikuti langkah-langkah dibawah ini

[Installasi Docker](https://github.com/Maulanaysf002/Hasura/blob/main/week%201/practice%20docker.md)

# 3. Install DDN CLI

perintah untuk installasi DDN CLI adalah:

`curl -L https://graphql-engine-cdn.hasura.io/ddn/cli/v4/get.sh | bash`

[Sumber Link](https://hasura.io/docs/3.0/quickstart)

![alt](/img/installasi_ddn_cli.png)

Dari gambar diatas, terlihat beberapa hal harus dipersiapkan untuk menjalankan hasura DDN. maka kita harus pastikan hal tersebut dijalankan.

# 4. Install Docker-Compose

untuk installasi docker-compose bisa dilihat di [Installasi docker-compose]([Installasi Docker](https://github.com/Maulanaysf002/Hasura/blob/main/week%201/practice%20docker.md))

docker-compose yang digunakan adalh versi v2.27.1 or later.

hasilnya adalah

![alt](/img/installasi_docker_compose.png)

# 5. Jika sudah di install reset VM

# 6. Cek Hasura DDN

perintah yang digunakan adalah `ddn doctor`.
hasilnya adalah:

![alt](/img/ddn_doctor.png)

jika docker sudah jalan dan docker-compose sudah di install tapi masih no ketika di verivikasi dengan ddn doctor, tidak masalah coba langsung ke tahap berikutnya.

# 7. Log in via the CLI

login ke dalam hasura ddn dengan perintah

`ddn auth login`

![alt](/img/ddn_auth_login.png)

Kita akan diminta untuk masuk ke dalam browser dan login dengan email. jika berhasil maka hasilnya adalah:

![alt](/img/hasura_ddn_login.png)

perhatikan ip diatas, ip yang saya gunakan adalah ip dinamis pemberian dari dhcp server yang bisa dicek menggunakan perintah `ip addr`. dan jika kita kembali kedalam terminal maka akan ada pemberitahuan login sukses.

![alt](/img/hasura_ddn_login_sukses.png)

Ini menunjukkan bahwa Anda sekarang telah terautentikasi dan dapat mulai menggunakan perintah DDN CLI untuk mengelola proyek Hasura DDN Anda.

# 8. Inisialisasi Supergraf Baru di Direktori Baru

## Prasyarat

1. **DDN CLI** harus sudah terinstal di sistem Anda.
2. Pastikan Anda berada di dalam direktori tempat Anda ingin membuat proyek supergraph baru.

## Langkah Langkah

1.  Buat direktori baru untuk proyek supergraph Anda, dan masuk ke dalam direktori tersebut. Anda bisa mengganti nama direktori dengan nama proyek Anda.

    ```
    mkdir mkdir hasura_ddn_project && cd hasura_ddn_project
    ```

    disini saya menamakan project saya yaitu hasura_ddn_project.

2.  Inisiasi Supergraph dengan menggunakan perintah

    ```
    ddn supergraph init <path directory>
    ```

    saya menggunakan perintah

    `ddn supergraph init .`

    artinya adalah saya menginisiasi supergraph didalam directory saat ini.

    ![alt](/img/ddn_init_supergraph.png)

    berikut ini adalah struktur folder setelah supergraph di init.

    ![alt](/img/hasura_ddn_struktur_folder_init_supergraph.png)

    penjelasan singkat folder diatas:

    - **app/**: Berisi metadata dan konfigurasi untuk subgraph.
    - **compose.yaml**: Konfigurasi Docker Compose untuk menjalankan aplikasi.
    - **engine/**: Berisi konfigurasi build dan file terkait untuk Hasura engine.
    - **globals/**: Berisi metadata dan konfigurasi global untuk supergraph.
    - **hasura.yaml**: Konfigurasi utama untuk Hasura.
      otel-collector-config.yaml: Konfigurasi untuk OpenTelemetry.
    - **supergraph.yaml**: File konfigurasi utama untuk supergraph, menghubungkan subgraph.

# 9. Menghubungkan ke data (connect to data)

Untuk memulai, inisialisasi konektor dengan perintah berikut:

`ddn connector init my_connector -i`

Penjelasan:

- `ddn connector init` adalah perintah untuk menginisialisasi konektor baru.
- `my_connector` adalah nama konektor yang akan Anda buat. Gantilah dengan nama yang sesuai dengan kebutuhan Anda.
- `-i` adalah opsi interaktif yang memungkinkan Anda untuk memasukkan informasi konfigurasi selama proses inisialisasi.

setelah dijalankan akan ada dropdown seperti dibawah ini:

![alt](/img/hasura_ddn_init_connector.png)

saya akan memilih `hasura/postgres` sesuai dengan langkah di [website resmi](https://hasura.io/docs/3.0/quickstart) untuk pembelajaran.

lalu menggunakan koneksi `postgresql://read_only_user:readonlyuser@35.236.11.122:5432/v3-docs-sample-app`

hasilnya seperti gambar dibawah ini. bagian optional bisa di enter atau dibiarkan kosong.

![alt](/img/hasura_ddn_init_connector_2.png)

Berikut adalah penjelasan setiap bagian dari output tersebut:

1. **Hub Connector**: Sistem mengidentifikasi bahwa konektor yang akan diinisialisasi adalah konektor PostgreSQL yang terhubung ke `hasura/postgres`.

2. **Connector Port 9064**: Port default untuk koneksi konektor adalah 9064. Port ini biasanya digunakan oleh konektor untuk berkomunikasi dengan database.

3. **Environment Variables**:

   - **CONNECTION_URI**: URI koneksi PostgreSQL yang digunakan untuk menghubungkan ke database. Dalam contoh ini, URI yang digunakan adalah:
     ```
     postgresql://read_only_user:readonlyuser@35.236.11.122:5432/v3-docs-sample-app
     ```
     URI ini berisi nama pengguna, kata sandi, alamat IP, port, dan nama database.
   - **CLIENT_CERT, CLIENT_KEY, ROOT_CERT**: Opsi untuk memasukkan sertifikat SSL klien dan sertifikat root jika diperlukan. Dalam output ini, nilai-nilai ini opsional dan tidak diisi (dilewatkan).

4. **INFO Messages**:
   - Sistem membuat berbagai file dan direktori yang terkait dengan konektor di direktori `app/connector/my_connector`, antara lain:
     - `connector.yaml`: Konfigurasi utama untuk konektor.
     - `compose.yaml`: File untuk Docker Compose jika konektor perlu dijalankan dalam container.
     - `.ddnignore`: File ignore untuk mengabaikan file tertentu.
     - `Dockerfile.my_connector`: Dockerfile khusus untuk konektor ini.
     - `my_connector.html`: File metadata untuk konektor.
   - **Environment Variables**: Koneksi URI dan variabel lainnya ditambahkan ke file `.env`.
   - **Konektor Inisialisasi**: Konektor dengan nama `my_connector` berhasil diinisialisasi dalam subgraf yang disebut "app".

# 10. Introspect your data source

perintah yang digunakan adalah

`sudo ddn connector introspect my_connector`

penjelasan perintah diatas:

1. `ddn`
   Ini adalah CLI tool atau perintah yang digunakan untuk berinteraksi dengan Hasura Data Delivery Network (DDN). Ini digunakan untuk mengelola dan mengonfigurasi berbagai aspek terkait dengan pengelolaan supergraph dan subgraph dalam DDN.

2. `connector`
   Bagian ini menunjukkan bahwa Anda ingin bekerja dengan connector. Connector dalam konteks Hasura DDN merujuk pada komponen yang menghubungkan sumber data eksternal (seperti database, API, atau sumber data lainnya) ke dalam Hasura. Connector digunakan untuk membawa data dari berbagai sumber eksternal ke dalam DDN.

3. `introspect`
   Perintah ini merujuk pada introspeksi atau proses otomatis untuk menganalisis struktur skema dan metadata dari connector yang Anda tentukan. Introspeksi adalah langkah pertama untuk memahami bagaimana struktur data dan API bekerja, mengidentifikasi tabel, kolom, dan tipe data yang tersedia dari sumber data yang terhubung.

   Dalam konteks GraphQL, introspeksi digunakan untuk memeriksa skema GraphQL untuk mendapatkan informasi tentang query, mutation, tipe data, dan lainnya yang tersedia.

4. `my_connector`
   Ini adalah nama dari connector yang ingin Anda introspeksi. Nama ini merujuk pada connector yang sudah dikonfigurasi sebelumnya di proyek DDN Anda. Misalnya, ini bisa jadi sebuah koneksi ke database PostgreSQL, API GraphQL, atau layanan lainnya.

# Note Perbaikan

1. perbarui versi docker: [tutorial](https://www.geeksforgeeks.org/update-docker/#why-you-should-update-docker)
