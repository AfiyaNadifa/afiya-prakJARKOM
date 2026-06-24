# Laporan Praktikum Jarkom IF

## Tujuan Praktikum
1. Memahami cara kerja Domain Name System (DNS) dalam menerjemahkan nama host ke alamat IP.

2. Menggunakan perintah nslookup untuk query DNS secara manual dan menganalisis hasilnya.

3. Menggunakan perintah ipconfig untuk melihat dan mengelola cache DNS di host.

4. Menganalisis trafik DNS (query dan response) menggunakan Wireshark.

## Langkah Pengerjaan
A. Penggunaan Nslookup (Command Line)
1. Buka Command Prompt / Terminal.

2. Jalankan perintah nslookup www.mit.edu dan amati output (nama server DNS lokal, alamat IP tujuan, dan jawaban non-otoritatif).

3. Jalankan perintah nslookup -type=NS mit.edu dan amati output (server DNS otoritatif untuk domain mit.edu).

4. Jalankan perintah nslookup www.aiit.or.kr bitsy.mit.edu dan amati output (query dikirim langsung ke server DNS bitsy.mit.edu, bukan ke DNS lokal).


B. Penggunaan Ipconfig (Cache DNS)
1. Di Command Prompt, jalankan ipconfig /displaydns untuk melihat isi cache DNS yang tersimpan di host.

2. Jalankan ipconfig /flushdns untuk menghapus seluruh cache DNS.


C. Tracing DNS dengan Wireshark (Akses www.ietf.org)
1. Jalankan ipconfig /flushdns untuk mengosongkan cache DNS.

2. Kosongkan cache browser.

3. Jalankan Wireshark, terapkan filter ip.addr == <your_IP_address> (ganti <your_IP_address> dengan alamat IP host Anda dari ipconfig).

4. Mulai capture, lalu buka browser dan akses http://www.ietf.org.

5. Hentikan capture, amati paket DNS (query dan response) via UDP port 53 sebelum paket TCP SYN dikirim.

6. Wireshark yang menunjukkan detail query DNS (type A) dan response (berisi 1 atau lebih answers).

D. Tracing Nslookup dengan Wireshark (3 Skenario)
1. Mulai capture di Wireshark (tanpa filter atau dengan filter khusus).

2. Jalankan nslookup www.mit.edu di Command Prompt. Amati di Wireshark query dikirim ke DNS lokal dan response berisi alamat IP MIT.

3. Jalankan nslookup -type=NS mit.edu. Amati query type NS dan response berisi nama server DNS otoritatif MIT.

4. Jalankan nslookup www.aait.or.kr bitsy.mit.edu. Amati query dikirim ke bitsy.mit.edu (bukan ke DNS lokal) dan response dari server tersebut.

5. Wireshark untuk masing-masing skenario yang menunjukkan alamat tujuan query, type query, dan jumlah answers.

## Lampiran
Hasil Percobaan:
![Hasil Percobaan](...asset/week4.png)