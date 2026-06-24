# Laporan Praktikum Jarkom IF

## Tujuan Praktikum
1. Mahasiswa memahami format dan isi pesan ICMP, khususnya Echo Request (Type 8) dan Echo Reply (Type 0) pada program Ping.

2. Mahasiswa memahami pesan ICMP Time-to-live exceeded (Type 11) yang dihasilkan oleh program Traceroute.

3. Mahasiswa mampu menganalisis field-field penting ICMP (Type, Code, Checksum, Identifier, Sequence Number) menggunakan Wireshark.

4. Mahasiswa memahami perbedaan implementasi Traceroute di Windows (menggunakan ICMP) dan Linux/Mac (menggunakan UDP).

5. Mahasiswa melaporkan progress pengerjaan tugas besar dan melakukan asistensi.

## Langkah Pengerjaan
A. Persiapan Awal
1. Buka Command Prompt / Terminal.

2. Jalankan Wireshark dan siapkan untuk mulai capture.

3. Pastikan host target dapat dijangkau (gunakan ping terlebih dahulu untuk cek konektivitas).

B. ICMP dan Ping (10 Paket)
Menjalankan Ping:

1. Di Command Prompt (Windows), jalankan perintah: ping -n 10 www.ust.hk (atau host lain di benua lain, misal: www.inria.fr).

Argumen -n 10 berarti mengirim 10 paket ICMP Echo Request.

2. Tunggu hingga perintah selesai (muncul 10 baris Reply from ... dan statistik RTT).

3. Hentikan capture di Wireshark (setelah Ping selesai).

Analisis di Wireshark:

1. Di Wireshark, terapkan filter icmp untuk menampilkan hanya paket ICMP.

2. Amati daftar paket — seharusnya terdapat 20 paket ICMP (10 Echo Request dari client + 10 Echo Reply dari server) seperti Figure 12.2.

3. Pilih satu paket Echo Request (dari client ke server). Di packet-header details:

Expand bagian Internet Protocol Version 4 dan catat bahwa field Protocol bernilai ICMP (1).

Expand bagian Internet Control Message Protocol dan amati:

Type: 8 (Echo (ping) request)

Code: 0

Checksum: 0x...

Identifier (BE): ... (nilai identifier)

Sequence Number (BE): ... (nomor urut, mulai dari 0 atau 1)

Data (32 bytes) atau payload (biasanya berisi alfabet).

4. Pilih satu paket Echo Reply (dari server ke client). Amati bahwa:

Type: 0 (Echo (ping) reply)

Code: 0

Identifier dan Sequence Number sama dengan paket Request yang bersesuaian.

5. Catat Round-Trip Time (RTT) dari setiap paket (bisa dilihat dari selisih waktu antara Request dan Reply, atau dari output Command Prompt).


C. ICMP dan Traceroute (Windows tracert)
Menjalankan Traceroute:

1. Di Command Prompt (Windows), jalankan perintah: tracert www.inria.fr (atau host lain di Eropa).

2. Tunggu hingga perintah selesai (menampilkan daftar hop/router yang dilalui).

3. Hentikan capture di Wireshark (jika belum dihentikan).

Analisis di Wireshark:

1. Di Wireshark, terapkan filter icmp (atau icmp.type == 11 untuk memfilter hanya TTL-exceeded).

2. Amati paket-paket ICMP yang dikembalikan oleh router perantara.

3. Pilih satu paket ICMP Time-to-live exceeded (biasanya dari router pertama, kedua, dst.). Di packet-header details:

Expand bagian Internet Control Message Protocol dan amati:

Type: 11 (Time-to-live exceeded)

Code: 0 (Time to live exceeded in transit)

Checksum: 0x...

Perhatikan bagian bawah dari detail ICMP — terdapat Internet Header (salinan header IP dari paket asli yang menyebabkan error) dan 8 bytes of original datagram (8 byte pertama dari payload asli). Ini adalah ciri khas pesan ICMP error.

4. Bandingkan dengan output Command Prompt tracert — setiap hop yang muncul di CMD bersesuaian dengan satu paket ICMP TTL-exceeded dari router tersebut.

## Lampiran
Hasil Percobaan:
![Hasil Percobaan](...asset/week12.png)