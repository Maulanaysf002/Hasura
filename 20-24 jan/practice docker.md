# Installasi

## Install Docker

Update Apt:

`sudo apt update`

Install Dependency Untuk Docker:

`sudo apt install -y apt-transport-https ca-certificates curl software-properties-common`

Tambahkan GPG Key:

`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg`

Tambahkan Repository Docker:

`echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`

Update Daftar Paket:

`sudo apt update`

Instal Docker Engine:

`sudo apt install -y docker-ce docker-ce-cli containerd.io`

Verivikasi Installasi:

`docker --version`

Hasilnya:

![alt](/img/docker_version.png)

## Install Docker Compose

Update Apt

`sudo apt update`

Install Docker Compose dengan CURL

`sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`

Berikan Izin Eksekusi pada file tempat menyimpan docker compose

`sudo chmod +x /usr/local/bin/docker-compose`

Tambahkan ke Path

`sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose`

Verivikasi Installasi

`docker-compose --version`

Hasilnya:

![alt](/img/docker_compose_version.png)
