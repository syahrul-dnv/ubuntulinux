<p align="center"> <img src="https://drive.google.com/uc?export=view&id=1inSLG8n_FubP1YW6B1-M_Pkhi4ABy-aM"></p>

# Apa itu Docker?
Docker adalah platform terbuka untuk mengembangkan, mengirim, dan menjalankan aplikasi. Docker memungkinkan kita untuk memisahkan aplikasi dari infrastruktur sehingga dapat mengirimkan aplikasi dengan cepat. Dengan Docker, kita dapat mengelola infrastruktur dengan cara yang sama seperti mengelola aplikasi (infrastruktur dengan kode). Dengan memanfaatkan metodologi Docker untuk pengiriman, pengujian, dan penerapan kode dengan cepat, kita dapat secara signifikan mengurangi penundaan antara penulisan kode dan menjalankannya dalam produksi.

## Container
Docker termasuk salah satu Container. Container adalah unit standar perangkat lunak yang mengemas kode dan semua dependensinya sehingga aplikasi berjalan dengan cepat dan andal dari satu lingkungan komputasi ke lingkungan komputasi lainnya.

## Container vs Virtual Machine
Container dan virtual machine memiliki kemiripan dalam mengisolasi sumber daya. Perbedaannya container memvirtualisasikan sistem operasi sementara virtual machine memvirtualisasikan perangkat keras.

Container adalah abstraksi pada lapisan aplikasi yang mengemas kode dan dependensi bersama-sama. Beberapa container dapat berjalan pada mesin yang sama dan memakai kernel OS yang sama dengan host OS. Container membutuhkan lebih sedikit ruang daripada virtual machine.

Sementara virtual machine adalah abstraksi dari perangkat keras yang memungkinkan satu server fisik menjadi banyak server virtual. Hypervisor memungkinkan beberapa virtual machine berjalan pada satu mesin. Setiap virtual machine menyertakan salinan lengkap sistem operasi, aplikasi, binari, dan pustaka yang diperlukan, menghabiskan ruang sampai puluhan GB. Virtual machine juga bisa lambat pada proses boot.

<p align="center"> <img src="https://drive.google.com/uc?export=view&id=1inSLG8n_FubP1YW6B1-M_Pkhi4ABy-aM"></p>

## Docker Platform
Docker menyediakan kemampuan untuk mengemas dan menjalankan aplikasi di lingkungan yang terisolasi yang disebut container. Isolasi dan keamanannya memungkinkan kita untuk menjalankan container secara bersamaan. Container yang ringan dan berisi semua yang diperlukan untuk menjalankan aplikasi, jadi tidak bergantung pada pustaka yang ada di host OS.

Docker menyediakan alat dan platform untuk mengelola siklus hidup container.

Mengembangkan aplikasi dan kompenen pendukungnya menggunakan container.
Container menjadi unit untuk mendistribusikan dan menguji aplikasi.
Terapkan aplikasi ke lingkungan produksi sebagai container. Container berfungsi sama, baik itu di lingkungan lokal, lingkungan produksi, atau di cloud.

## Kapan Menggunakan Docker?
Docker merampingkan siklus hidup pengembangan dengan memungkinkan kita untuk bekerja di lingkungan standar menggunakan container lokal yang menyediakan aplikasi dan layanan. Container sangat bagus untuk alur kerja continuous integration dan continuous delivery (CI/CD).

Contoh skenario penggunaan Docker:

Developer mengembangkan aplikasi secara lokal dan membagikan hasil pekerjaannya menggunakan Docker.
Developer menggunakan Docker untuk mengirimnya ke lingkungan pengujian dan menjalankan pengujian baik secara otomatis.
Ketika developer menemukan bug, developer dapat memperbaikinya di lingkungan pengembangan dan mengirimnya kembali ke lingkungan pengujian untuk pengujian dan validasi.
Saat pengujian selesai, mengirimkan Docker image ke lingkungan produksi.

## Arsitektur Docker
Docker menggunakan arsitektur client-server. Docker client berkomunikasi dengan Docker daemon yang bertugas membangun, menjalankan, dan mendistribusikan Docker container. Docker client dan daemon dapat berjalan pada sistem yang sama, atau dapat menghubungkan Docker client ke Docker daemon secara remote. Docker client dan daemon berkomunikasi menggunakan REST API, melalui Unix socket atau antarmuka jaringan. Docker client lainnya adalah Docker compose yang memungkinkan bekerja dengan aplikasi yang terdiri dari sekumpulan container.


