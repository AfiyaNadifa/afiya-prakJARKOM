# Laporan Praktikum Jarkom IF

## Tujuan Praktikum
1. Memahami mekanisme connection establishment (three-way handshake) pada protokol TCP.

2. Menganalisis sequence number, acknowledgment number, dan flags (SYN, ACK) pada segmen TCP.

3. Menghitung Round-Trip Time (RTT) dari beberapa segmen TCP pertama dan memahami EstimatedRTT.

4. Memahami mekanisme congestion control TCP (slow start dan congestion avoidance) melalui Time-Sequence-Graph (Stevens).

5. Menganalisis jumlah data yang diakui dalam setiap ACK dan throughput koneksi TCP.

## Langkah Pengerjaan
A. Persiapan dan Upload File Alice.txt
1. Buka browser, akses http://gaia.cs.umass.edu/wireshark-labs/alice.txt dan unduh file teks alice.txt (berisi naskah Alice in Wonderland).

2. Buka halaman http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html.

3. Pada halaman tersebut, klik tombol Browse dan pilih file alice.txt yang sudah diunduh (jangan klik Upload dulu).

4. Jalankan Wireshark dan mulai capture.

5. Kembali ke browser, klik tombol "Upload alice.txt file" untuk mengunggah file ke server.

6. Tunggu hingga muncul pesan sukses di browser, lalu hentikan capture di Wireshark.

B. Tampilan Awal Captured Trace dan Filter TCP
1. Di Wireshark, terapkan filter tcp di display filter bar agar hanya menampilkan paket TCP.

2. Amati inisiasi koneksi TCP (three-way handshake): paket SYN, SYN-ACK, dan ACK.

3. Catat alamat IP dan nomor port TCP yang digunakan oleh komputer klien (sumber) dan server gaia.cs.umass.edu.

C. Menonaktifkan Protokol HTTP (Melihat Segmen TCP Murni)
1. Pilih menu Analyze -> Enabled Protocols.

2. Hapus centang pada kotak HTTP, lalu klik OK.

3. Jendela Wireshark sekarang hanya menampilkan segmen TCP murni (tanpa interpretasi HTTP). Cari segmen yang membawa data HTTP POST.

D. Analisis Dasar TCP (Three-way Handshake dan 6 Segmen Pertama)
1. Temukan paket SYN pertama dari client ke server. Catat nomor urut (Sequence Number) dan bukti bahwa paket tersebut adalah SYN (flag SYN=1).

2. Temukan paket SYN-ACK dari server. Catat nomor urut dan nomor acknowledgment dari segmen ini. Jelaskan bagaimana server menentukan nilai acknowledgment tersebut.

3. Temukan segmen TCP yang berisi perintah HTTP POST (cari di bagian data/payload yang mengandung string "POST").

4. Identifikasi 6 segmen TCP pertama yang dikirim dari client ke server (termasuk segmen yang berisi POST).

Catat nomor urut, waktu pengiriman, dan waktu diterimanya ACK untuk setiap segmen.

Hitung RTT untuk masing-masing segmen (selisih waktu kirim dan waktu ACK diterima).

Hitung EstimatedRTT setelah setiap ACK diterima (menggunakan rumus EstimatedRTT = 0.875 * EstimatedRTT + 0.125 * SampleRTT).

E. Analisis Length, Buffer, dan Retransmisi
1. Catat panjang (Length) dari masing-masing 6 segmen TCP pertama.

2. Cari tahu jumlah minimum ruang buffer (window size) yang disarankan oleh penerima sepanjang trace. Apakah kekurangan buffer pernah menghambat pengiriman?

3. Amati apakah ada segmen yang ditransmisikan ulang (retransmisi) dalam trace. Jelaskan bagaimana cara mengetahuinya di Wireshark.

4. Berapa banyak data yang biasanya diakui oleh penerima dalam satu ACK? Apakah ada kasus di mana penerima melakukan ACK untuk setiap segmen yang diterima?

F. Perhitungan Throughput
1. Hitung throughput (byte yang ditransfer per satuan waktu) untuk seluruh koneksi TCP. Jelaskan cara perhitungannya (total data dikirim dibagi total waktu koneksi).

G. Congestion Control (Time-Sequence-Graph Stevens)
1. Di Wireshark, pilih salah satu segmen TCP yang dikirim oleh client ke server.

2. Pilih menu Statistics -> TCP Stream Graph -> Time-Sequence-Graph(Stevens).

3. Amati grafik yang muncul (plot nomor urut vs waktu).

4. Identifikasi di mana fase slow start dimulai dan berakhir, serta di mana fase congestion avoidance mengambil alih.

5. grafik tersebut dan berikan komentar tentang perilaku yang teramati dibandingkan dengan teori ideal.

## Lampiran
Hasil Percobaan:
![Hasil Percobaan](...asset/week6.png)