<p align="center"> <img src="https://drive.google.com/uc?export=view&id=1inSLG8n_FubP1YW6B1-M_Pkhi4ABy-aM"></p>

# Apa itu Docker?
Docker adalah platform terbuka untuk mengembangkan, mengirim, dan menjalankan aplikasi. Docker memungkinkan kita untuk memisahkan aplikasi dari infrastruktur sehingga dapat mengirimkan aplikasi dengan cepat. Dengan Docker, kita dapat mengelola infrastruktur dengan cara yang sama seperti mengelola aplikasi (infrastruktur dengan kode). Dengan memanfaatkan metodologi Docker untuk pengiriman, pengujian, dan penerapan kode dengan cepat, kita dapat secara signifikan mengurangi penundaan antara penulisan kode dan menjalankannya dalam produksi.

## Container
Docker termasuk salah satu Container. Container adalah unit standar perangkat lunak yang mengemas kode dan semua dependensinya sehingga aplikasi berjalan dengan cepat dan andal dari satu lingkungan komputasi ke lingkungan komputasi lainnya.

## Container vs Virtual Machine
Container dan virtual machine memiliki kemiripan dalam mengisolasi sumber daya. Perbedaannya container memvirtualisasikan sistem operasi sementara virtual machine memvirtualisasikan perangkat keras.

Container adalah abstraksi pada lapisan aplikasi yang mengemas kode dan dependensi bersama-sama. Beberapa container dapat berjalan pada mesin yang sama dan memakai kernel OS yang sama dengan host OS. Container membutuhkan lebih sedikit ruang daripada virtual machine.

Sementara virtual machine adalah abstraksi dari perangkat keras yang memungkinkan satu server fisik menjadi banyak server virtual. Hypervisor memungkinkan beberapa virtual machine berjalan pada satu mesin. Setiap virtual machine menyertakan salinan lengkap sistem operasi, aplikasi, binari, dan pustaka yang diperlukan, menghabiskan ruang sampai puluhan GB. Virtual machine juga bisa lambat pada proses boot.
