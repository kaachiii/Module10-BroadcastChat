# Module 10 - Broadcast Chat

* Nama  : Ischika Afrilla
* NPM   : 2306227955

## Refleksi
### Experiment 2.1: Original code, and how it run
![Experiment 2.1: Original code, and how it run](images/Screenshot%20(1080).png)

Pada gambar di atas, kita menjalankan satu server dan tiga client secara bersamaan. Masing-masing client secara otomatis terhubung ke server, sehingga setiap pesan yang diketik di salah satu client akan dikirim ke server terlebih dahulu. Server kemudian akan meneruskan pesan tersebut ke semua client yang terhubung, termasuk pengirimnya. Hal ini memungkinkan setiap client untuk melihat pesan yang dikirim oleh client lain secara real-time. Terlihat bahwa ketika sebuah pesan diketik pada client 1, pesan tersebut juga muncul di client 2 dan client 3. Mekanisme ini berjalan karena server menggunakan format penandaan `From server: message` untuk mendistribusikan pesan ke semua client yang aktif.

### Experiment 2.2: Modifying port
Port client dan server sesuai
![Port client dan server sesuai](images/Screenshot%20(1081).png)

Port client dan server tidak sesuai
![Port client dan server tidak sesuai](images/Screenshot%20(1082).png)

Jika kita ingin memodifikasi port komunikasi antara server dan client, maka perubahan harus dilakukan pada kedua sisi koneksi. Pada file `client.rs`, kita perlu memodifikasi baris `ClientBuilder::from_uri(Uri::from_static("ws://127.0.0.1:2000"))` untuk menyesuaikan alamat dan port tujuan client. Sementara itu, pada file `server.rs`, bagian `let listener = TcpListener::bind("127.0.0.1:8080").await?;` juga harus disesuaikan agar server dapat mendengarkan pada port yang sama dengan yang digunakan oleh client. Keduanya menggunakan protokol WebSocket, yang terlihat dari penggunaan URI dengan skema `ws://` pada sisi client. Protokol ini didefinisikan secara eksplisit di sisi client melalui `ClientBuilder`, dan di sisi server melalui `ServerBuilder`, yang secara khusus membungkus `TcpListener` untuk menerima dan mengelola koneksi WebSocket. Jika port pada kedua sisi sudah disamakan, maka koneksi akan berhasil dibangun dan komunikasi dapat berjalan dengan baik. Namun, jika hanya salah satu sisi yang diubah dan terjadi ketidaksesuaian port, maka client tidak akan bisa terhubung ke server karena alamat tujuan yang dituju tidak sesuai dengan yang disediakan oleh server.

### Experiment 2.3: Small changes, add IP and Port
![Experiment 2.3: Small changes, add IP and Port](images/Screenshot%20(1083).png)

Terlihat pada gambar di atas, saya melakukan beberapa modifikasi pada kode untuk meningkatkan visibilitas alur komunikasi antara server dan client. Pada file `client.rs`, saya menambahkan baris `println!("Chika's computer - From server: {}", text);` untuk memudahkan proses debugging maupun pemantauan pesan yang masuk. Sementara itu, pada file `server.rs`, saya menambahkan `bcast_tx.send(format!("{addr} : {text}"))?;` agar pesan dari client disertai dengan alamat pengirim saat disiarkan ke client lain, sehingga lebih informatif. Saya juga menambahkan `println!("New connection from Chika's computer {addr:?}");` untuk mencatat setiap koneksi baru yang masuk ke server sehingga mempermudah pemantauan aktivitas koneksi.