## Tutorial 6
### Commit 1
```
Saya membuat Single-Threaded Web Server, 
Saya menggunakan library std::io::prelude dan std::io::BufReader untuk membaca dan menulis ke stream. Saya membuat metode handle_connection untuk menangani koneksi masuk, 
di mana metode tersebut membuat instance BufReader yang memproses stream tersebut. 
BufReader mengadopsi trait BufRead yang menyediakan fungsi lines untuk mendapatkan setiap baris permintaan HTTP dari browser. Kemudian, baris-baris permintaan tersebut dicetak dalam format yang dapat dibaca. Saat program dijalankan dan permintaan dikirim melalui browser, output akan menampilkan baris-baris permintaan HTTP yang telah dikirim oleh browser.
```
