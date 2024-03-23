## Tutorial 6
### Commit 1
Saya membuat Single-Threaded Web Server,

Saya menggunakan library `std::io::prelude` dan `std::io::BufReader` untuk membaca dan menulis ke stream. 
Saya membuat metode handle_connection untuk menangani koneksi masuk, 
di mana metode tersebut membuat instance BufReader yang memproses stream tersebut. 
BufReader mengadopsi trait BufRead yang menyediakan fungsi lines untuk mendapatkan setiap baris permintaan HTTP dari browser. Kemudian, baris-baris permintaan tersebut dicetak dalam format yang dapat dibaca. Saat program dijalankan dan permintaan dikirim melalui browser, output akan menampilkan baris-baris permintaan HTTP yang telah dikirim oleh browser.
### Commit 2

![commit2.png](assets%2Fimg%2Fcommit2.png)
Saya menggunakan modul sistem berkas Rust untuk membaca isi berkas dan mengirimkannya sebagai respons HTTP dari server.

Langkah awal adalah mengimpor modul fs untuk mengakses fungsi-fungsi berkas. 

Kemudian, berkas hello.html dibaca dan diubah menjadi string menggunakan fungsi fs::read_to_string("hello.html").unwrap();. 

Setelah itu, isi berkas diformat menjadi respons HTTP yang sesuai dengan penambahan header Content-Length yang berisi panjang konten. 

Terakhir, respons tersebut dikirim ke klien melalui objek stream menggunakan metode write_all.
### Commit 3
Saya telah menambahkan validasi pada kode untuk menangani permintaan HTTP yang masuk. Ini dilakukan dengan menggunakan `next` untuk membaca hanya baris pertama dari permintaan HTTP dan menyimpannya dalam variabel `request_line`.
```rust
let request_line = match request_lines.next() {
    Some(line) => line,
    None => {
        return;
    }
};
```
Jika `request_line` berisi permintaan GET ke `/`, maka akan dikirimkan respons yang berisi isi berkas `hello.html`. Namun, jika permintaan tidak sesuai, kode akan mengeksekusi blok `else` untuk menangani permintaan yang tidak valid dengan mengirimkan berkas `404.html`.

Saya melakukan refactoring pada kode karena langkah ini mirip dengan langkah sebelumnya. Namun, ada perbedaan pada bagian penanganan respons dan berkas yang dikirim, seperti `status_line` dan `filename`.
![commit3.png](assets%2Fimg%2Fcommit3.png)
### Commit 4
Untuk mencapai simulasi slow response, saya telah menambahkan penundaan selama 10 detik pada server sebelum memberikan respons. Ini dilakukan dengan menggunakan fungsi `std::thread::sleep` dan menentukan durasi penundaan sebelum memberikan respons.

Milestone ini mengubah struktur `if-else` menjadi penggunaan `match` untuk menangani tiga jenis permintaan HTTP: `GET /`, `GET /sleep`, dan permintaan lainnya. Ketika permintaan adalah `GET /sleep`, server akan melakukan penundaan selama 10 detik sebelum mengirimkan respons. Ketika server dijalankan dan permintaan `/sleep` diterima, permintaan lain seperti `/` akan tertunda sampai waktu penundaan (10 detik) selesai sebelum menerima respons. Hal ini memastikan bahwa respons untuk permintaan lain akan tertunda hingga selesai menangani permintaan `GET /sleep`.

### Commit 5
Saya telah mengimplementasikan multi-threaded web server dengan menggunakan thread pool.

Thread pool adalah kumpulan thread yang telah dibuat sebelumnya dan siap untuk menangani tugas. Ketika ada tugas baru yang harus dilakukan, salah satu thread dari pool akan diambil untuk menyelesaikan tugas tersebut. Sementara itu, thread lain dalam pool tetap tersedia untuk menangani tugas-tugas berikutnya. Setelah menyelesaikan tugasnya, thread akan kembali ke dalam pool untuk menangani tugas selanjutnya. Konsep thread pool ini memungkinkan server untuk memproses banyak koneksi secara bersamaan, yang pada akhirnya meningkatkan throughput atau kinerja server.

Jumlah thread dalam pool biasanya dibatasi untuk mencegah serangan Denial of Service (DoS) yang dapat menghabiskan semua sumber daya server. Dengan batasan ini, server hanya dapat memproses hingga N permintaan secara bersamaan, di mana N adalah jumlah thread dalam pool. Ini membantu menjaga stabilitas dan ketersediaan server saat menghadapi beban tinggi.