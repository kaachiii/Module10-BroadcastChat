# Module 10 - Broadcast Chat

* Nama  : Ischika Afrilla
* NPM   : 2306227955

## Refleksi
### Experiment 2.1: Original code, and how it run
![Experiment 2.1: Original code, and how it run](images/Screenshot%20(1080).png)

Pada gambar di atas, kita menjalankan satu server dan tiga client secara bersamaan. Masing-masing client secara otomatis terhubung ke server, sehingga setiap pesan yang diketik di salah satu client akan dikirim ke server terlebih dahulu. Server kemudian akan meneruskan pesan tersebut ke semua client yang terhubung, termasuk pengirimnya. Hal ini memungkinkan setiap client untuk melihat pesan yang dikirim oleh client lain secara real-time. Terlihat bahwa ketika sebuah pesan diketik pada client 1, pesan tersebut juga muncul di client 2 dan client 3. Mekanisme ini berjalan karena server menggunakan format penandaan seperti `From server: message` untuk mendistribusikan pesan ke semua client yang aktif.