# Laporan Praktikum Jarkom IF

## Tujuan Praktikum
1. Mahasiswa mampu membuat program client-server sederhana berbasis socket UDP menggunakan Python.

2. Mahasiswa mampu membuat program client-server sederhana berbasis socket TCP menggunakan Python.

3. Mahasiswa memahami perbedaan mendasar komunikasi connectionless (UDP) dan connection-oriented (TCP) melalui implementasi kode dan eksekusi program.

## Langkah Pengerjaan
A. Persiapan Awal
1. Pastikan Python sudah terinstal di komputer (cek dengan perintah python --version di Command Prompt/Terminal).

2. Siapkan editor teks atau IDE (Notepad, VS Code, PyCharm, atau IDLE) untuk menulis kode Python.

3. Buka dua jendela Command Prompt/Terminal (satu untuk menjalankan server, satu untuk menjalankan client).

B. Program Socket dengan UDP
1. Membuat dan Menjalankan UDPServer.py

Buat file baru bernama UDPServer.py.

Tulis kode server UDP seperti di modul (halaman 42), dengan ketentuan:

Import from socket import *

Tentukan serverPort = 12000

Buat socket UDP: socket(AF_INET, SOCK_DGRAM)

Bind ke port: serverSocket.bind(('', serverPort))

Tampilkan "The server is ready to receive"

Gunakan loop while True untuk menerima pesan dengan recvfrom(2048)

Ubah pesan menjadi huruf kapital dengan .upper()

Kirim balik dengan sendto(modifiedMessage.encode(), clientAddress)

Simpan file, lalu jalankan di terminal pertama: python UDPServer.py

Pastikan muncul pesan "The server is ready to receive" (server berjalan dan menunggu).

2. Membuat dan Menjalankan UDPClient.py

Buat file baru bernama UDPClient.py.

Tulis kode client UDP seperti di modul (halaman 40), dengan ketentuan:

Import from socket import *

Tentukan serverName = '127.0.0.1' (atau 'localhost') dan serverPort = 12000

Buat socket UDP: socket(AF_INET, SOCK_DGRAM)

Minta input dari pengguna: input('Input lowercase sentence:')

Kirim pesan dengan sendto(message.encode(), (serverName, serverPort))

Terima balasan dengan recvfrom(2048)

Tampilkan hasil dengan print(modifiedMessage.decode())

Tutup socket dengan close()

Simpan file, lalu jalankan di terminal kedua: python UDPClient.py

Ketik kalimat huruf kecil (misal: "hello world"), amati output di client yang berubah menjadi huruf kapital ("HELLO WORLD").

Screenshot kode UDPServer.py, kode UDPClient.py, dan tampilan kedua terminal (server dan client berjalan).

C. Program Socket dengan TCP
1. Membuat dan Menjalankan TCPServer.py

Buat file baru bernama TCPServer.py.

Tulis kode server TCP seperti di modul (halaman 47), dengan ketentuan:

Import from socket import *

Tentukan serverPort = 12000

Buat socket TCP: socket(AF_INET, SOCK_STREAM)

Bind ke port: serverSocket.bind(('', serverPort))

Listen untuk koneksi: serverSocket.listen(1)

Tampilkan "The server is ready to receive"

Gunakan loop while True untuk menerima koneksi dengan accept()

Terima data dengan recv(1024).decode()

Ubah menjadi huruf kapital dengan .upper()

Kirim balik dengan send(capitalizedSentence.encode())

Tutup socket koneksi dengan close()

Simpan file, lalu jalankan di terminal pertama: python TCPServer.py

Pastikan muncul pesan "The server is ready to receive".

2. Membuat dan Menjalankan TCPClient.py

Buat file baru bernama TCPClient.py.

Tulis kode client TCP seperti di modul (halaman 45), dengan ketentuan:

Import from socket import *

Tentukan serverName = '127.0.0.1' dan serverPort = 12000

Buat socket TCP: socket(AF_INET, SOCK_STREAM)

Connect ke server: clientSocket.connect((serverName, serverPort))

Minta input dari pengguna: input('Input lowercase sentence:')

Kirim data dengan send(sentence.encode())

Terima balasan dengan recv(1024)

Tampilkan hasil dengan print('From Server: ', modifiedSentence.decode())

Tutup socket dengan close()

Simpan file, lalu jalankan di terminal kedua: python TCPClient.py

Ketik kalimat huruf kecil, amati output di client yang menjadi huruf kapital.

Screenshot kode TCPServer.py, kode TCPClient.py, dan tampilan kedua terminal.


## Lampiran
Hasil Percobaan:
![Hasil Percobaan](...asset/week7.png)