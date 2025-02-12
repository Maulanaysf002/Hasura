# Use Case Aplikasi Management Produk

Sistem memungkinkan pengguna (admin gudang atau manajer toko) untuk mencatat, mengelola, dan memonitor data produk serta stok di gudang/toko. Sistem ini mendukung penambahan produk baru, pembaruan informasi produk, dan pencatatan keluar/masuk stok.

# Alur Sistem

1. Tambah Produk Baru (mutation):

   - Admin memasukkan data produk baru seperti nama produk, kategori, harga, dan stok awal.
   - Sistem menyimpan data produk ke dalam database.

2. Perbarui Informasi Produk (mutation):

   - Admin memilih produk yang ada dan memperbarui informasi, seperti harga jual, deskripsi, atau kategori.
   - Sistem menyimpan pembaruan ke dalam database.

3. Keluar/Masuk Stok (mutation):

   - Admin mencatat stok yang keluar (penjualan/pengiriman) atau masuk (restock).
   - Sistem memperbarui jumlah stok di database berdasarkan transaksi.

4. Cek Daftar dan Stok Produk (query):

   - Admin dapat melihat daftar semua produk, termasuk - - jumlah stok saat ini, dan melakukan pencarian/filter berdasarkan kategori.

5. Peringatan Stok Rendah (subscription):

   - Sistem memberikan notifikasi jika stok produk tertentu berada di bawah ambang batas yang ditentukan.

# Membuat Database dan Tabel

Masuk kedalam console hasura pada bagian data.

![alt](/img/hasura_dashboard_data.png)

Klik Database yang sudah dibuat sebelumnya.

![alt](/img/hasura_pilih_database.png)

Klik view untuk melihat schemas yang ada pada database.

![alt](/img/hasura_database_klik_view.png)

Buat Schema baru dengan klik Create New Schemas.

![alt](/img/hasura_create_new_schemas.png)

Tambahkan Schema baru

![alt](/img/hasura_tambahkan_schema_baru.png)

Selanjutkan Buat Table baru dengan klik tomboh create table. bisa juga menggunakan sql.

![alt](/img/hasura_create_new_table.png)

jika menggunakan sql untuk membuat tabel

![alt](/img/hasura_buat_table_produk_dengan_schema.png)

Jika sudah semua tabel dibuat dengan sql, jalankan track All agar relasi antara tabel bisa terbentuk.

![alt](/img/hasura_daftar_tabel.png)

# Alur Sistem

## 1. Tambah Produk Baru (mutation)

mutation untuk menambah barang:

```graphql
mutation MyMutation {
  DB_Maulana {
    insert_management_product_product(objects: { nama_produk: "botol minuman", kategori: "barang", harga: "30000", deskripsi: "menyimpan minuman panas & dingin", stok: 50, ambang_batas_stok: 5 }) {
      returning {
        id
        nama_produk
        kategori
        deskripsi
        harga
        stok
        ambang_batas_stok
        created_at
      }
    }
  }
}
```

hasilnya adalah:

```graphql
{
  "data": {
    "DB_Maulana": {
      "insert_management_product_product": {
        "returning": [
          {
            "id": 1,
            "nama_produk": "botol minuman",
            "kategori": "barang",
            "deskripsi": "menyimpan minuman panas & dingin",
            "harga": 30000,
            "stok": 50,
            "ambang_batas_stok": 5,
            "created_at": "2025-02-12T03:46:21.86366"
          }
        ]
      }
    }
  }
}
```

gambarnya:

![alt](/img/mutation_menambah_produk_baru.png)

## 2. Perbarui Informasi Produk (mutation):

data yang sudah masuk ke database:

![alt](/img/hasura_produk_botol_minuman.png)

data yang ingin dirubah adalah harga, dan jumlah stok. maka mutationnya adalah:

```graphql
mutation MyMutation {
  DB_Maulana {
    update_management_product_product(where: { id: { _eq: 1 } }, _set: { stok: 60, harga: "40000" }) {
      returning {
        id
        nama_produk
        harga
        stok
      }
    }
  }
}
```

hasilnya adalah:

```graphql
{
  "data": {
    "DB_Maulana": {
      "update_management_product_product": {
        "returning": [
          {
            "id": 1,
            "nama_produk": "botol minuman",
            "harga": 40000,
            "stok": 60
          }
        ]
      }
    }
  }
}
```

![alt](/img/hasura_update_product.png)

![alt](/img/hasura_data_terupdate.png)

# 3. Cek Daftar dan Stok Produk (query)

Cek Daftar Produk menggunakan query

```
query MyQuery {
  DB_Maulana {
    management_product_product {
      id
      nama_produk
      kategori
      harga
      deskripsi
      stok
      ambang_batas_stok
      created_at
      updated_at
    }
  }
}

```

hasilnya adalah:

```
{
  "data": {
    "DB_Maulana": {
      "management_product_product": [
        {
          "id": 1,
          "nama_produk": "botol minuman",
          "kategori": "barang",
          "harga": 40000,
          "deskripsi": "menyimpan minuman panas & dingin",
          "stok": 60,
          "ambang_batas_stok": 5,
          "created_at": "2025-02-12T03:46:21.86366",
          "updated_at": "2025-02-12T03:46:21.86366"
        }
      ]
    }
  }
}
```

![alt](/img/hasura_query_graphql.png)
