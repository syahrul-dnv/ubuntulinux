# Langkah 1 — Menginstal Apache dan Memperbarui Firewall
Server web Apache adalah salah satu server web paling populer di dunia. Server web Apache terdokumentasi dengan baik, memiliki komunitas pengguna yang aktif, dan digunakan secara luas dalam sejarah web, yang membuatnya menjadi pilihan asali yang hebat untuk menjadi hos situs web.

Instal Apache menggunakan manajer paket Ubuntu, apt:
<pre>sudo apt update
sudo apt install apache2</pre>

Jika ini adalah kali pertama Anda menggunakan sudo dalam sesi ini, Anda akan diminta memberikan kata sandi pengguna Anda untuk memastikan Anda memiliki privilese yang benar untuk mengelola paket sistem dengan apt. Anda juga akan diminta mengonfirmasi instalasi Apache dengan menekan Y, lalu ENTER.
Setelah instalasi selesai, Anda akan perlu menyesuaikan pengaturan firewall Anda untuk memperbolehkan lalu lintas HTTP. UFW memiliki berbagai profil aplikasi berbeda yang dapat Anda manfaatkan untuk menyelesaikannya. Untuk mendapatkan daftar semua profil aplikasi UFW yang tersedia, Anda dapat menjalankan:

<pre>sudo ufw app list</pre>
Anda akan melihat keluaran seperti ini:
<pre>Output :
Available applications:
  Apache
  Apache Full
  Apache Secure
  OpenSSH</pre>
Berikut adalah makna dari setiap profil ini:

<li>Apache: Profil ini hanya membuka porta 80 (lalu lintas web normal dan tidak terenkripsi).</li>
<li>Apache Full: Profil ini membuka baik porta 80 (lalu lintas web normal dan tidak terenkripsi) dan porta 443 (lalu lintas terenkripsi TLS/SSL).</li>
<li>Apache Secure: Profile ini hanya membuka porta 443 (lalu lintas terenkripsi TLS/SSL).</li>
Untuk saat ini, sebaiknya izinkan hanya koneksi pada porta 80, karena ini adalah instalasi Apache yang baru dan Anda belum memiliki sertifikat TLS/SSL yang dikonfigurasi untuk mengizinkan lalu lintas HTTPS di server Anda.

Untuk hanya memperbolehkan lalu lintas pada porta 80, gunakan profil Apache:
<pre>sudo ufw allow in "Apache"</pre>

Anda dapat memverifikasi perubahan dengan:
<pre>Output:
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                                
Apache                     ALLOW       Anywhere                  
OpenSSH (v6)               ALLOW       Anywhere (v6)                    
Apache (v6)                ALLOW       Anywhere (v6)  </pre>

Lalu lintas pada porta 80 sekarang diperbolehkan melewati firewall.

Anda dapat melakukan pemeriksaan cepat untuk memastikan segalanya berjalan sesuai rencana dengan mengunjungi alamat IP publik server Anda di peramban web Anda (lihat catatan di bawah judul berikutnya untuk mengetahui alamat IP publik Anda jika Anda belum memiliki informasi ini):

http://your_server_ip ot ketikan "localhost" di navbar sear engine kalian.
Anda akan melihat laman web Apache Ubuntu 20.04 asali, yang tersedia dengan tujuan pengujian dan informasi.

## Cara Menemukan Alamat IP Publik Server Anda
Jika Anda tidak mengetahui alamat IP publik server Ada, ada sejumlah cara untuk mengetahuinya. Biasanya, ini adalah alamat yang digunakan untuk terhubung ke server Anda melalui SSH.

Ada beberapa cara untuk melakukannya dari baris perintah. Pertama, Anda dapat menggunakan alat iproute2 untuk mengetahui alamat IP dengan mengetik ini:
<pre>ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//' </pre>

Ini akan menampilkan dua atau tiga baris tanggapan. Semua adalah alamat yang benar, tetapi komputer Anda mungkin hanya dapat menggunakan salah satunya, jadi silakan mencoba masing-masing alamat itu.

Cara alternatifnya adalah menggunakan utilitas curl untuk menghubungi pihak luar supaya memberitahukan bagaimana pihak luar melihat server Anda. Hal ini dilakukan dengan menanyakan alamat IP Anda kepada server tertentu:
<pre>curl http://icanhazip.com</pre>
Terlepas dari cara yang digunakan untuk mengetahui alamat IP Anda, ketik alamat IP pada bilah alamat di peramban web Anda untuk melihat laman Apache asali.


# Langkah 2 — Menginstal MySQL
Setelah server web hidup dan berfungsi, Anda perlu menginstal sistem basis data agar dapat menyimpan dan mengelola data untuk situs Anda. MySQL adalah sistem manajemen basis data populer yang digunakan dalam lingkungan PHP.

Sekali lagi, gunakan apt untuk memperoleh dan menginstal perangkat lunak ini:

<pre>sudo apt install mysql-server</pre>
 
Ketika diminta, lakukan konfirmasi instalasi dengan mengetik Y, lalu ENTER.

Ketika instalasi selesai, Anda disarankan untuk menjalankan skrip keamanan yang sudah terinstal sebelumnya dengan MySQL. Skrip ini akan menghapus beberapa pengaturan asali yang tidak aman dan mengunci akses ke sistem basis data Anda. Mulai skrip interaktif dengan menjalankan:

<pre>sudo mysql_secure_installation</pre>
 
Anda akan ditanya apakah Anda ingin mengonfigurasi VALIDATE PASSWORD PLUGIN.

Catatan: Mengaktifkan fitur ini merupakan keputusan yang Anda pertimbangkan sendiri. Jika diaktifkan, kata sandi yang tidak cocok dengan kriteria yang ditentukan akan ditolak oleh MySQL dengan suatu kesalahan. Akan lebih aman jika Anda tetap menonaktifkan validasi, tetapi Anda harus selalu menggunakan kata sandi yang kuat dan unik untuk kredensial basis data.

Jawab Y untuk ya, atau jawaban lain untuk melanjutkan tanpa mengaktifkan.
<pre>
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:</pre>
Jika Anda menjawab “ya”, Anda akan diminta untuk memilih tingkat validasi kata sandi. Harap ingat bahwa jika Anda memasukkan 2 sebagai tingkat terkuat, Anda akan menjumpai kesalahan saat berusaha menentukan kata sandi yang tidak mengandung angka, huruf kapital dan huruf kecil, serta karakter khusus, atau kata sandi yang berdasarkan pada kata-kata kamus umum.
<pre>
There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary              file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1</pre>
Terlepas dari pilihan pengaturan VALIDATE PASSWORD PLUGIN, server Anda akan meminta Anda untuk memilih dan mengonfirmasi kata sandi untuk pengguna root MySQL. Ini tidak sama dengan root sistem. Pengguna root basis data adalah pengguna administratif dengan privilese penuh terhadap sistem basis data. Meskipun metode autentikasi asali untuk pengguna root MySQL mengecualikan penggunaan kata sandi, sekalipun kata kata sandi sudah dibuat, Anda tetap harus menentukan kata sandi yang kuat di sini sebagai langkah keamanan tambahan. Kita akan membahas hal ini sebentar lagi.

Jika Anda mengaktifkan validasi kata sandi, Anda akan diperlihatkan kekuatan kata sandi untuk kata sandi root yang baru saja Anda masukkan dan server Anda akan bertanya apakah Anda ingin melanjutkan dengan kata sandi itu. Jika Anda puas dengan kata sandi ini, tekan Y untuk “ya” di prompt:
<pre>
Estimated strength of the password: 100
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y</pre>
Untuk pertanyaan lainnya, tekan Y dan tombol ENTER pada setiap pertanyaan. Ini akan menghapus sebagian pengguna anonim dan basis data percobaan, menonaktifkan log masuk root dari jarak jauh, dan memuat aturan-aturan baru ini sehingga MySQL segera menerapkan perubahan yang Anda buat.

Setelah Anda selesai, lakukan percobaan apakah Anda dapat melakukan log masuk ke konsol MySQL dengan mengetik:

<pre>sudo mysql</pre>
 
Ini akan menghubungkan ke server MySQL sebagai root pengguna basis data administratif, yang ditentukan berdasarkan penggunaan sudo saat menjalankan perintah ini. Anda akan melihat keluaran seperti ini:
<pre>
Output :
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 22
Server version: 8.0.19-0ubuntu5 (Ubuntu)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

</pre>
Untuk keluar dari konsol MySQL, ketik:

<pre>mysql> exit</pre>

Perhatikan bahwa Anda tidak perlu memberikan kata sandi untuk terhubung sebagai pengguna root, meskipun Anda telah menentukannya saat menjalankan skrip mysql_secure_installation. Hal itu dikarenakan metode autentikasi asali untuk pengguna MySQL administratif adalah unix_socket alih-alih kata sandi. Meskipun awalnya ini mungkin terlihat seperti masalah keamanan, tetapi ini membuat server basis data menjadi lebih aman karena pengguna yang diizinkan melakukan log masuk sebagai pengguna MySQL root hanya pengguna sistem dengan privilese sudo yang terhubung dari konsol atau melalui aplikasi yang berjalan dengan privilese yang sama. Dalam praktiknya, itu berarti Anda tidak akan dapat menggunakan pengguna root basis data administratif untuk terhubung dari aplikasi PHP. Pengaturan kata sandi untuk akun MySQL root berfungsi sebagai perlindungan, apabila metode autentikasi asali diubah dari unix_socket menjadi kata sandi.

Untuk keamanan yang lebih baik, saran terbaiknya adalah memiliki akun pengguna khusus dengan pengaturan privilese yang lebih sempit untuk setiap basis data, terutama jika Anda berencana memiliki beberapa basis data di mana server Anda adalah hosnya.

Catatan: Saat menyusun tulisan ini, pustaka PHP MySQL asli mysqlnd tidak mendukung caching_sha2_authentication, metode autentikasi asali untuk MySQL 8. Karena itu, saat menciptakan pengguna basis data untuk aplikasi PHP di MySQL 8, Anda perlu memastikan pengguna telah dikonfigurasi untuk menggunakan mysql_native_password. Kami akan mendemonstrasikan caranya di Langkah 6.

Server MySQL Anda kini telah terinstal dan terlindungi. Selanjutnya, kita akan menginstal PHP, komponen terakhir dalam tumpukan LAMP.

# Langkah 3 — Menginstal PHP
Anda telah memiliki Apache terinstal untuk menyajikan konten dan MySQL terinstal untuk menyimpan dan mengelola data Anda. PHP adalah komponen persiapan kita yang akan memproses kode untuk menampilkan konten dinamis ke pengguna akhir. Selain paket 'php', Anda akan memerlukan 'php-mysql', suatu modul PHP yang memungkinkan PHP berkomunikasi dengan basis data yang berbasis MySQL. Anda juga akan memerlukan 'libapache2-mod-php' untuk memungkinkan Apache menangani berkas PHP. Paket PHP inti akan secara otomatis terinstal sebagai dependensi.

Untuk menginstal paket ini, jalankan:

<pre>sudo apt install php libapache2-mod-php php-mysql</pre>
 
Setelah instalasi selesai, Anda dapat menjalankan perintah berikut ini untuk mengonfirmasi versi PHP Anda:

<pre>php -v</pre>
<Pre> 
Output :
PHP 7.4.3 (cli) (built: Mar 26 2020 20:24:23) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
    with Zend OPcache v7.4.3, Copyright (c), by Zend Technologies</pre>
Di titik ini, tumpukan LAMP Anda sudah berfungsi sepenuhnya, tetapi sebelum Anda dapat menguji setelan Anda dengan skrip PHP, sebaiknya instal Apache Virtual Host yang tepat untuk menyimpan berkas dan folder situs web Anda. Kita akan melakukan itu di langkah selanjutnya.





















## Layanan pengaktifan / penonaktifan sementara

Untuk menghentikan dan memulai layanan sementara (Tidak mengaktifkan / menonaktifkannya untuk booting di masa mendatang), Anda dapat mengetik service SERVICE_NAME. Sebagai contoh:

<pre>sudo service apache2 stop</pre>(Akan BERHENTI layanan Apache sampai Reboot atau sampai Anda memulainya lagi).

<pre>sudo service apache2 start</pre>(Akan MULAI layanan Apache dengan asumsi itu dihentikan sebelumnya.)

<pre>service apache2 status</pre> (Akan memberitahu Anda STATUS layanan, jika diaktifkan / dijalankan dinonaktifkan / TIDAK berjalan.).

<pre>sudo service apache2 restart</pre>(Akan MEMULAI layanan. Ini paling umum digunakan ketika Anda telah mengubah, file konfigurasi. Dalam hal ini, jika Anda mengubah konfigurasi PHP atau konfigurasi Apache. Restart akan menyelamatkan Anda dari keharusan berhenti / mulai dengan 2 baris perintah) )

<pre>service apache2</pre>(Dalam hal ini, karena Anda tidak menyebutkan TINDAKAN untuk mengeksekusi untuk layanan, itu akan menunjukkan kepada Anda semua opsi yang tersedia untuk layanan tertentu.) Aspek ini bervariasi tergantung pada layanan, misalnya, dengan MySQL hanya akan menyebutkan bahwa itu tidak memiliki parameter. Untuk layanan lain seperti layanan jaringan, akan disebutkan daftar kecil dari semua opsi yang tersedia.
