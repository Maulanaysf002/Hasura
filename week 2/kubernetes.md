# Pengertian

![alt](/img/logo_kubernetes.png)

Kubernetes adalah platform open-source yang dirancang untuk mengelola container aplikasi.

Container sendiri adalah unit kecil dari perangkat lunak yang mengemas kode beserta dependensi agar aplikasi dapat berjalan konsisten di berbagai lingkungan (operating system).

Adanya Kubernetes berkaitan dengan munculnya Docker atau aplikasi yang dikontainerisasi, seperti yang sudah dijelaskan pada artikel (Backlink Docker) sebelumnya, bahwa docker berfungsi untuk mengemas aplikasi menjadi sebuah kontainer.

**Fungsi Dari Kubernetes :**

1. **Manajemen Container**: Kubernetes mengatur dan mengelola container dalam suatu lingkungan cluster, sehingga pengembang tidak perlu repot mengelola server satu per satu.
2. **Penskalaan Otomatis**: Jika ada lonjakan lalu lintas pengguna, Kubernetes dapat secara otomatis menambah atau mengurangi sumber daya untuk aplikasi.
3. **Ketersediaan Tinggi (High Availability)**: Dengan fitur seperti load balancing, Kubernetes memastikan aplikasi tetap berjalan meskipun ada gangguan pada server tertentu.
4. **Orkestrasi Kompleks**: Dalam aplikasi modern, satu layanan biasanya terdiri dari banyak komponen. Kubernetes menyederhanakan pengelolaan komponen-komponen ini.

## Perbedaan Kubernetes Dengan Docker

Docker adalah teknologi untuk membuat dan menjalankan container.

Kubernetes bertugas mengelola container-container tersebut.

# Bagian-Bagian dalam Kubernetes

![alt](/img/komponen_kubernetes.png)

1. **Cluster**

   Kluster adalah server gabungan dari beberapa **VPS** untuk menjalankan sebuah Kubernetes, pada cluster terdapat master node dan worker node.

2. **Master node**

   Master node adalah server utama yang berfungsi untuk mengatur semua operasi cluster seperti, mekanisme schedule, didalamya terdapat beberapa komponen yaitu kube-controller-manager, kube-apiserver, kube-schejuler, dan ectd.

   - **Kube-controller-manager**

     Melakukan konfigurasi dan monitoring yang dibuat pada node untuk memastikan sesuai dengan Deployment. bertanggung jawab melakukan tracking apa yang terjadi dalam **cluster**.

   - **Kube-apiserver**

     Sistem central k8s, sebagai planning konfigurasi dari k8s, sistem dirancang untuk dapat validasi data untuk objek API, yaitu pod, services, volume, dan lainnya.

     digunakan sebagai penghubung dari cli, dashboard, API. semua interaksi akan terhubung dengan API-Server sebelum masuk ke kubernetes.

   - **Kube-scheduler**

     Sebagai program eksekusi Kubernetes, melakukan deploy ke node dan menginstall ke node tertentu.

     bertugas untuk melakukan manajemen pada **pod**.

   - **Ectd**

     Digunakan untuk menyimpan storage key value Kubernetes. bisa dibilang sebagai jantungnya kubernetes karena menyimpan konfigurasi2 dari kubernetes itu sendiri.

3. **Worker Node**
   Worker node menjalankan proses dari master node, dengan menggunakan kubelet dan kube-proxy.

   - **Kubelet**

     Sebuah komponen yang berfungsi untuk memastikan agar service berjalan didalam pod.

   - **Kube-proxy**

     Mengatur rule network dan akan melakukan forward ke kontainer yang sesuai.

   - **Container Runtime**

     Software yang bertanggung jawab untuk menjalankan kontainer, seperti Docker, containerd, atau CRI-O.

   - **Docker Image**

     File konfigurasi dari docker yang akan dibuat menjadi container.

## POD

![alt](/img/kubernetes_pod.png)

pod merupakan unit terkecil dari kubernetes. didalam pod bisa terdapat lebih dari 1 container.

setiap pod pasti akan memiliki 1 IP address.

# Cara Kerja

Pada dasarnya, Kubernetes bekerja dengan membagi aplikasi ke dalam beberapa bagian kecil yang disebut **pod**.

Setiap pod ini berisi satu atau lebih container yang saling bekerja sama. **Pod-pod** ini kemudian dijalankan di dalam sebuah **cluster**, yang terdiri dari banyak **node**.

# Installasi

1.  Buat sebuah virtual machine di virtualbox.

2.  Install Docker dan kubectl.

3.  Lakukan installasi minikube.

    `curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64`

    `sudo install minikube-linux-amd64 /usr/local/bin/minikube`

    ![alt](/img/install%20minikube.png)

4.  tambahkan user ke dalam group docker.

    `sudo usermod -aG docker $USER & newgrp docker`

5.  jalankan minikube dengan driver docker

    `minikube start --driver=docker --force`

    ![alt](/img/run_minikube_docker.png)

    untuk menghemat ram:

    `minikube start --memory=1967mb`

6.  pastikan cluster berjalan

    `kubectl get nodes`

# Sumber Belajar

1. [PPT Tentang Kubernetes](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbXA3aTVCTGhneUlIc1hKSTNXemNBTGlndF9Gd3xBQ3Jtc0tuempiSjZYZnRtSG10b083RXZBVmg2M1Z3TmV6MEhyVDdIQ0NUWkNac0xINE9iWHZCb0FDZVM0ZW1DaGlONkdOUXNfLWhkUTI4WlZoRkNRcDhyNFhCU1c0S3V5dHVmTFMzUy00YVhaU3FOSEZ2VnRQRQ&q=https%3A%2F%2Fdocs.google.com%2Fpresentation%2Fd%2F15cPaGS_nRWF1iK2RRfrvudlN7mYQJBL5eX0g8CI45iM%2Fedit%3Fusp%3Dsharing&v=7zInpQfPRqo)

2. [link video youtube](https://www.youtube.com/watch?v=7zInpQfPRqo&t=11s)
