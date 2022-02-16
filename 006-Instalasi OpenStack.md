# Cara Menginstal OpenStack di Ubuntu dengan DevStack [Metode mudah]

OpenStack adalah infrastruktur komputasi awan (IaaS) yang membantu mengendalikan kumpulan besar daya komputasi, penyimpanan, dan sumber daya jaringan di seluruh pusat data. Ia melakukannya dengan bantuan API. Singkatnya, OpenStack membantu dalam membangun dan mengelola Cloud Publik dan Pribadi, dengan menggunakan sumber daya virtual yang dikumpulkan.

Devstack adalah serangkaian skrip yang dapat diperluas, yang digunakan untuk mengatur lingkungan OpenStack dengan mudah. Ini banyak digunakan, karena memberikan lingkungan interaktif untuk pengembangan dengan OpenStack.

Pada artikel ini, kita akan belajar cara mengatur OpenStack di sistem Ubuntu kita dengan bantuan Devstack.

## Prasyarat untuk menggunakan OpenStack
Ada beberapa prasyarat dasar yang perlu Anda penuhi, sebelum menyiapkan OpenStack di sistem Anda.

<ul>
  <li>OS Ubuntu</li>
  <li>RAM minimal 4 GB</li>
  <li>Prosesor berkemampuan multi-core</li>
  <li>Setidaknya 10GB ruang hard disk kosong</li>
  <li>Koneksi internet yang bagus</li>
</ul>
  
Ada beberapa persyaratan perangkat lunak tambahan juga, yang harus Anda penuhi.

<li>Git</li>
<li>Peramban web(chrome,firefox, dll)</li>

## Langkah-langkah untuk Menginstal Openstack di Ubuntu dengan Devstack
Menginstal OpenStack di Ubuntu adalah proses yang agak rumit. Tapi itu dipermudah oleh Devstack. Langkah-langkah untuk menginstalnya, cukup mudah bahkan jika Anda tidak terlalu mahir dengan baris perintah, cukup ikuti langkah-langkahnya dan jalankan.

### Langkah 1: Mempersiapkan sistem
Sebelum kita memulai, kita perlu memastikan bahwa sistem kita diperbarui , untuk itu jalankan perintah berikut:

<pre>sudo apt-get update && sudo apt-get upgrade -y</pre>

Perintah akan meminta hak akses root . Masukkan kata sandi pengguna Anda dan tunggu hingga sistem Anda ditingkatkan. Setelah pemutakhiran selesai, pastikan untuk me- reboot sistem Anda . Ini akan menginisialisasi dan mengatur upgrade Anda di reboot berikutnya.
