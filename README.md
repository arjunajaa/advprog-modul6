## Tutorial 6
### Commit 1
```
Saya membuat Single-Threaded Web Server, 
Saya menggunakan library std::io::prelude dan std::io::BufReader untuk membaca dan menulis ke stream. Saya membuat metode handle_connection untuk menangani koneksi masuk, 
di mana metode tersebut membuat instance BufReader yang memproses stream tersebut. 
BufReader mengadopsi trait BufRead yang menyediakan fungsi lines untuk mendapatkan setiap baris permintaan HTTP dari browser. Kemudian, baris-baris permintaan tersebut dicetak dalam format yang dapat dibaca. Saat program dijalankan dan permintaan dikirim melalui browser, output akan menampilkan baris-baris permintaan HTTP yang telah dikirim oleh browser.
```
### Commit 2

![commit2.png](assets%2Fimg%2Fcommit2.png)
```
Saya menggunakan modul sistem berkas Rust untuk membaca isi berkas dan mengirimkannya sebagai respons HTTP dari server.

Langkah awal adalah mengimpor modul fs untuk mengakses fungsi-fungsi berkas. 
Kemudian, berkas hello.html dibaca dan diubah menjadi string menggunakan fungsi fs::read_to_string("hello.html").unwrap();. 
Setelah itu, isi berkas diformat menjadi respons HTTP yang sesuai dengan penambahan header Content-Length yang berisi panjang konten. 
Terakhir, respons tersebut dikirim ke klien melalui objek stream menggunakan metode write_all.
```
