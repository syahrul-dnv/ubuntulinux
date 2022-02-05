# Cara Install Docker di Ubuntu 20.04
Docker adalah platform container yang digunakan oleh developer dalam pengembangan, pengiriman, dan pengujian aplikasi. Docker memungkinkan developer untuk mengisolasi aplikasi dari infrastruktur dan memudahkan dalam distribusi dan deploy.

## Install Docker
Update package index dan install dependensi.
<pre>sudo apt update
sudo apt install apt-transport-https ca-certificates curl gnupg lsb-release</pre>

Downlod GPG key untuk Docker.
<pre>curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg</pre>

Pasang Docker Repository
<pre>echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null	</pre>
  
Update kembali dan install docker-ce.

<pre>sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io</pre>
  
Supaya dapat menjalankan docker tanpa sudo, buat group dengan nama docker dan masukkan user yang digunakan ke dalam group docker.
<pre>sudo groupadd docker
sudo usermod -aG docker $USER</pre>

Logout dan login kembali.

Uji coba menjalankan docker dan menampilkan versinya.
<pre>docker version</pre>
nanti akan muncul keterangan dibawah ini
<pre>Client: Docker Engine - Community
 Version:           20.10.8
 API version:       1.41
 Go version:        go1.16.6
 Git commit:        3967b7d
 Built:             Fri Jul 30 19:54:27 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.8
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.6
  Git commit:       75249d8
  Built:            Fri Jul 30 19:52:33 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.9
  GitCommit:        e25210fe30a0a703442421b0f60afac609f950a3
 runc:
  Version:          1.0.1
  GitCommit:        v1.0.1-0-g4144b63
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0</pre>
  
  
## Docker image
Untuk membuat container kita membutuhkan image yang tersedia di hub.docker.com (Docker registry).

Mencari image, misal nginx image. dan nanti akan muncul daftar image 
<pre>docker search nginx </pre>
<pre>NAME                              DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
nginx                             Official build of Nginx.                        15317     [OK]       
jwilder/nginx-proxy               Automated Nginx reverse proxy for docker con…   2059                 [OK]
richarvey/nginx-php-fpm           Container running Nginx + PHP-FPM capable of…   815                  [OK]
jc21/nginx-proxy-manager          Docker container for managing Nginx proxy ho…   233                  
linuxserver/nginx                 An Nginx container, brought to you by LinuxS…   151         
Download (pull) nginx image.</pre>

sekarang kita download imagenya
<pre>docker pull nginx </pre>
contoh peritah di atas
<pre>Using default tag: latest
latest: Pulling from library/nginx
33847f680f63: Downloading [============>                                      ]  6.695MB/27.15MB
dbb907d5159d: Downloading [================>                                  ]  8.608MB/26.6MB
8a268f30c42a: Download complete 
b10cf527a02d: Download complete  </pre>

nginx image sudah tersedia.
<pre>
Using default tag: latest
latest: Pulling from library/nginx
33847f680f63: Pull complete 
dbb907d5159d: Pull complete 
8a268f30c42a: Pull complete 
b10cf527a02d: Pull complete 
c90b090c213b: Pull complete 
1f41b2f2bf94: Pull complete 
Digest: sha256:8f335768880da6baf72b70c701002b45f4932acae8d574dedfddaf967fc3ac90
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest  
</pre>

Menampilkan semua image yang tersedia di local.
<pre>docker image ls</pre>
Contoh hasil perintah di atas.
<pre>REPOSITORY                 TAG       IMAGE ID       CREATED         SIZE
nginx                      latest    08b152afcfae   3 weeks ago     133MB  
</pre>

Menampilkan informasi detail image nginx.
<pre>docker inspect nginx
docker image inspect nginx
</pre>
