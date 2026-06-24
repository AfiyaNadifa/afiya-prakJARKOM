# Laporan Praktikum Jarkom IF

## Tujuan Praktikum
1. Mahasiswa mampu membuat program web server sederhana berbasis TCP socket programming menggunakan Python.

2. Mahasiswa memahami cara menangani permintaan HTTP GET dari browser dan mengirimkan response (200 OK atau 404 Not Found).

3. Mahasiswa memahami format dasar HTTP request dan response header.

4. Mahasiswa mampu mengimplementasikan server multi-threaded (opsional tambahan) dan membuat custom HTTP client.

## Langkah Pengerjaan
A. Persiapan Awal
1. Pastikan Python sudah terinstal di komputer.

2. Siapkan editor teks atau IDE untuk menulis kode Python.

3. Buat file HTML sederhana bernama HelloWorld.html dengan isi misalnya:

html
<html>
<body>
<h1>Hello World!</h1>
</body>
</html>
4. Simpan file HelloWorld.html di direktori yang sama dengan tempat file server akan dibuat.

B. Membuat Program Web Server (Skeleton Code)
1. Buat file baru bernama webserver.py.

2. Tulis kode skeleton seperti di modul (halaman 50–51) dengan bagian #Fill in start dan #Fill in end yang harus diisi.

3. Isi bagian-bagian kosong dengan ketentuan:

Mempersiapkan server socket: serverSocket.bind(('', 6789)) dan serverSocket.listen(1).

Menerima koneksi: connectionSocket, addr = serverSocket.accept().

Menerima pesan dari client: message = connectionSocket.recv(1024).decode().

Membuka file yang diminta: f = open(filename[1:]) dan baca seluruh isinya ke outputdata.

Mengirim response header 200 OK: connectionSocket.send("HTTP/1.1 200 OK\r\n\r\n".encode()).

Mengirim konten file: Looping outputdata dan kirim setiap baris dengan connectionSocket.send(outputdata[i].encode()).

Menangani file tidak ditemukan (IOError): Kirim response "HTTP/1.1 404 Not Found\r\n\r\n" dan "<html><body><h1>404 Not Found</h1></body></html>" ke client.

Menutup socket koneksi: connectionSocket.close().

4. Simpan file webserver.py.

C. Menjalankan Server dan Menguji dengan Browser
1. Buka Command Prompt/Terminal, navigasi ke direktori tempat webserver.py dan HelloWorld.html berada.

2. Jalankan server dengan perintah: python webserver.py.

3. Pastikan muncul pesan "Ready to serve..." di terminal.

4. Buka browser (Chrome/Firefox/Edge).

5. Ketik URL: http://127.0.0.1:6789/HelloWorld.html (atau http://localhost:6789/HelloWorld.html).

6. Amati browser menampilkan isi file HelloWorld.html (misal: "Hello World!").


D. Menguji File Tidak Ditemukan (404 Not Found)
1. Di browser, ketik URL: http://127.0.0.1:6789/FileTidakAda.html (atau nama file lain yang tidak ada di direktori).

2. Amati browser menampilkan pesan "404 Not Found".


## Lampiran
Hasil Percobaan:
![Hasil Percobaan](...asset/week9.png)