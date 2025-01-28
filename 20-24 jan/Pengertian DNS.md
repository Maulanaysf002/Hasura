# Pengertian

Domain Name System atau DNS adalah sistem yang menerjemahkan nama domain seperti www.google.com menjadi IP address (contoh: 192.0.0.1) agar bisa dipahami oleh komputer saat Anda mengakses sebuah website menggunakan nama domain.

# Cara Kerja

DNS bekerja dalam beberapa langkah menggunakan proses yang disebut DNS lookup atau resolution.

Misalnya saya ingin membuka website tokopedia . Anda kemudian mengetikkan nama domain www.tokopedia.com ke kolom alamat web browser. Nah, di sini saya sedang melakukan proses yang disebut **DNS Request (Permintaan DNS)**.

Komputer saya lalu akan mengecek penyimpanan lokalnya untuk mencari apakah ada record (data) untuk domain tersebut. DNS record adalah IP address yang terkait dengan **FQDN**.

> FQDN adalah nama domain lengkap yang menentukan lokasi komputer atau host dalam jaringan, termasuk di internet maupun jaringan lokal. Struktur FQDN terdiri dari hostname dan nama domain.
>
> ![fqdn](/img/fqdn.webp)
>
> - Hostname. Label yang ditetapkan pada perangkat atau layanan di jaringan. Hostname merupakan bagian dari nama domain yang membuat alamat IP jadi mudah diingat. Contohnya, “www” adalah hostname untuk www.hostinger.co.id, dan “en” adalah hostname untuk en.wikipedia.org.
>
> - Subdomain. Bagian ini terletak di sisi kiri domain utama, dan terkadang menunjukkan bagian dari domain yang lebih besar. Misalnya, support.hostinger.com memiliki subdomain “support” yang merupakan bagian dari hostinger.com. Namun, tidak semua domain memiliki elemen ini.
>
> - Nama domain. Terdiri dari domain tingkat kedua dan top-level domain (TLD). Misalnya, di hostinger.co.id, “hostinger” adalah domain tingkat kedua, dan “.co.id” adalah TLD.

Selanjutnya komputer akan mencari dalam file host dan cache. File host adalah file teks biasa yang mengarahkan hostname ke IP address dalam sistem operasi, sedangkan cache adalah data sementara yang disimpan oleh hardware atau software.

begini gambaran kerja dns dalam mengakses website:

![alt](/img/cara-kerja-dns.jpg)

1. DNS Resolver

   perantara utama antara komputer Anda dan DNS server lainnya. Fungsinya adalah untuk meneruskan permintaan ke DNS server lainnya lalu mengirimkannya kembali setelah dipenuhi.

2. Root Nameserver

   Root nameserver atau root DNS server adalah server yang paling tinggi dalam alur kerja DNS. Fungsinya bisa diibaratkan seperti ruang arsip. Setelah menerima permintaan dari recursive DNS resolver, root nameserver akan memeriksa TLD milik domain yang Anda buka. Kemudian, recursive resolver akan diarahkan olehnya ke namaserver TLD yang tepat.

3. TLD Nameserver

   DNS server yang bertugas untuk menyimpan dan mengelola informasi domain yang menggunakan TLD tertentu. Top-level Domain atau TLD adalah bagian akhir domain, seperti .com, .org, .online, dan .net.

4. Authoritative Nameserver

   Authoritative name server atau authoritative DNS server adalah server terakhir dalam proses resolusi DNS. Server ini menyimpan semua informasi yang terkait dengan domain yang Anda kunjungi, termasuk alamat IP.

   Recursiver resolver kemudian akan memperoleh IP address milik domain yang Anda kunjungi, lalu mengirimkannya kembali ke komputer Anda sehingga website yang Anda akses akan terbuka.

   Terakhir, resolver akan melakukan DNS caching, yaitu menyimpan IP address yang berhasil diperolehnya dari authoritative name server sebagai data cache. Jadi, ketika Anda kembali website yang sama, prosesnya bisa lebih singkat karena record bisa langsung diambil dari cache.

# DNS dalam kubernetes

DNS (Domain Name System) dalam Kubernetes adalah fitur yang digunakan untuk memberikan resolusi nama kepada layanan dan pod dalam kluster Kubernetes.

DNS membuat aplikasi dalam kluster saling berkomunikasi menggunakan **nama yang mudah diingat**, bukan alamat IP yang bersifat dinamis.

## Fungsi DNS dalam kubernetes

1. sebagai Resolusi service name

   DNS Kubernetes memungkinkan layanan diakses melalui nama domain seperti my-service.my-namespace.svc.cluster.local, tanpa perlu mengetahui IP address-nya. Nama domain ini mempermudah komunikasi antar-layanan dalam kluster.

2. Resolusi Nama Pod

   Kubernetes DNS juga dapat digunakan untuk mengakses pod secara langsung, terutama jika pod memiliki hostname atau subdomain yang telah dikonfigurasi.

3. Komunikasi Antar-Namespace

   Dengan DNS, Anda dapat mengakses layanan di namespace yang berbeda menggunakan format:

   ```bash
   <service-name>.<namespace>.svc.cluster.local
   ```
