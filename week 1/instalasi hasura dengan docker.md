Mengunduh file docker-compose.yaml dari repository resmi Hasura v2

`wget https://raw.githubusercontent.com/hasura/graphql-engine/stable/install-manifests/docker-compose/docker-compose.yaml`

hasilnya:
![alt text](/img/unduh_docker_compose_hasura.png)

periksa file docker-compose.yaml

`nano docker-compose.yaml`

ganti HASURA_GRAPHQL_ADMIN_SECRET menjadi apa yang kita inginkan, misal saya menggantinya menjadi `kuncirahasia`

![alt text](/img/nano_docker_version_hasura.png)

jalankan docker-compose

`sudo docker-compose up -d` atau `docker compose up -d`

hasilnya:
![alt text](/img/docker_compose_hasura_up.png)

tambah license untuk hasura dalam file yaml

![alt](/img/hasura_add_license.png)

## Mengakses Hasura

buat rule untuk https dengan host port `8080` dan guest port `8080` di virtualbox

akses console hasura dengan link

`127.0.0.1:8080/console/`

maka anda sudah bisa login ke dalam hasura

![alt text](/img/dashboard_hasura.png)

## Koneksi Ke Database

buat inisiasi database dengan docker-compose

- buat file docker-compose.yaml
- isikan dengan script:

```
services:
  mariadb:
    image: mariadb:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: maulanaysf
      MYSQL_USER: maulanaysf
      MYSQL_PASSWORD: password
      MYSQL_AUTHENTICATION_PLUGIN: mysql_native_password
    ports:
      - "3307:3306"

  mysql:
    image: mysql:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: maulanaysf
      MYSQL_USER: maulanaysf
      MYSQL_PASSWORD: password
      MYSQL_AUTHENTICATION_PLUGIN: mysql_native_password
    ports:
      - "3306:3306"
```

hasilnya:
![alt text](/img/docker_compose_mysql.png)

> periksa container yang berjalan

`sudo docker ps -a`

hasilnya:

![alt text](/img/docker_ps.png)

lakukan restart image docker graphql engine

`sudo docker restart maulanaysf-graphql-engine-1`

Kemudian masuk kedalam hasura console, untuk mengconnect database mysql dan mariadb, dengan langkah :

1. Dalam console hasura, klik data tab
2. Connect postgres,
3. Connect database mysql dan mariadb terlebih dahulu
4. Kemudian masukkan nama tampilan untuk database dan 5. atur URL Koneksi JDBC untuk MySQL
5. Untuk dasar JDBC Mysql: jdbc:mysql://:/?user=&password=
6. Untuk Dasar JDBC Mariadb: jdbc:mariadb://:/?user=&password=
7. Masukkan JDBC Mariadb: jdbc:mariadb://dutar-mysql-1:3306/maulanaysf?user=maulanaysf&password=password
8. Masukkan JDBC MySql: jdbc:mysql://instalasi_mysql-mysql-1:3306/maulanaysf?user=maulanaysf&password=password
9. Kemudian Submit Connect
   Tampilan Database di hasura sudah terlihat

connet database postgres via database url

`postgres://postgres:postgrespassword@postgres:5432/postgres` (bisa dilihat di docker-compose.yaml)

## Note

- jika menggunakan ip static di vm, yang diambil adalah ip dinamicnya yang muncul dalam vm.

![alt](/img/ip_a_command.png)

pada contoh diatas yang diambil adalah `10.50.220.249`
