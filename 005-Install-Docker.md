# Cara Install Docker di Ubuntu 20.04
Docker adalah platform container yang digunakan oleh developer dalam pengembangan, pengiriman, dan pengujian aplikasi. Docker memungkinkan developer untuk mengisolasi aplikasi dari infrastruktur dan memudahkan dalam distribusi dan deploy.

## Install Docker
Update package index dan install dependensi.
<pre>sudo apt update
sudo apt install apt-transport-https ca-certificates curl gnupg lsb-release</pre>

Downlod GPG key untuk Docker.
<pre>curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg</pre>
