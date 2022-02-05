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

## Docker image
Untuk membuat container kita membutuhkan image yang tersedia di hub.docker.com (Docker registry).

Mencari image, misal nginx image.
<pre>docker search nginx </pre>
