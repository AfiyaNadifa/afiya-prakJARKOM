# Laporan Praktikum Jarkom IF

## Tujuan Praktikum
1. Mahasiswa memahami struktur header IPv4, termasuk field Time-to-Live (TTL), Protocol, Source/Destination Address, dan Identification.

2. Mahasiswa memahami mekanisme fragmentasi IP pada datagram berukuran besar (3000 byte) melalui analisis field "More fragments" dan "Fragment offset".

3. Mahasiswa memahami perbedaan mendasar antara header IPv4 dan IPv6 serta cara kerja DNS query tipe AAAA untuk resolusi IPv6.

4. Mahasiswa mampu menggunakan Wireshark untuk menganalisis paket traceroute dan fragmentasi IP.

## Langkah Pengerjaan
A. Persiapan Awal (Menjalankan Traceroute)
1. Buka terminal (Linux/Mac) atau Command Prompt (Windows).

2. Siapkan Wireshark untuk mulai menangkap paket.

3. Catat alamat IP host Anda sendiri (misal: 192.168.1.100 atau 10.0.0.1) menggunakan perintah ipconfig (Windows) atau ifconfig/ip addr (Linux/Mac).

B. Bagian 1: IPv4 Dasar (Paket 56 Byte)

Untuk Windows:

1. Di Command Prompt, jalankan: tracert gaia.cs.umass.edu

2. Biarkan perintah selesai dijalankan.

3. Setelah perintah traceroute selesai, hentikan capture di Wireshark.

4. Di Wireshark, terapkan filter udp||icmp (atau icmp||udp) untuk menampilkan hanya paket UDP dan ICMP (seperti Figure 10.1).

5. Identifikasi paket UDP yang dikirim dari host Anda ke tujuan 128.119.245.12 (gaia.cs.umass.edu) dengan filter: ip.src == <your_IP> && ip.dst == 128.119.245.12 && udp && !icmp.

6. Pilih salah satu paket UDP, lalu expand bagian Internet Protocol Version 4 di packet details. Catat:

Field Time to Live (TTL) (nilai 1, 2, 3, dst.)

Field Protocol (harus UDP (17))

Field Source Address dan Destination Address.

7. Cari paket ICMP balasan dari router (Time-to-live exceeded) dengan filter ip.dst == <your_IP> && icmp.

8. Pilih salah satu paket ICMP, expand bagian Internet Control Message Protocol dan catat:

Type: 11 (Time-to-live exceeded)

Code: 0 (Time to live exceeded in transit).

C. Bagian 2: Fragmentasi IP (Paket 3000 Byte)

Untuk Windows (karena tracert tidak bisa mengatur ukuran):

1. Gunakan file trace alternatif: ip-wireshark-trace1-1.pcapng dari wireshark-traces.zip (unduh dari link modul).

2. Buka file tersebut di Wireshark.

3. Di Wireshark, terapkan filter: ip.src == <your_IP> && ip.dst == 128.119.245.12 && udp untuk melihat paket UDP 3000-byte.

4. Amati bahwa satu paket UDP besar dipecah menjadi beberapa fragmen IPv4.

5. Pilih fragmen pertama, expand bagian Internet Protocol Version 4 dan perhatikan:

Total Length (misal: 1500 byte)

Identification (nilai yang sama untuk semua fragmen)

Flags: 0x01 (More fragments) — pada fragmen pertama dan kedua, flag ini bernilai 1.

Fragment Offset (fragmen pertama = 0, fragmen kedua = 1480/8 = 185, dst.)

6. Pilih fragmen terakhir, perhatikan bahwa Flags: 0x00 (More fragments = 0).

7. Di Wireshark, coba gunakan filter ip.flags.mf == 1 untuk menampilkan hanya fragmen yang memiliki More Fragments flag aktif.


D. Bagian 3: IPv6
1. Buka file trace ip-wireshark-trace2-1.pcapng dari wireshark-traces.zip menggunakan Wireshark.

2. Di daftar paket, cari paket ke-20 (pada t=3.814489) yang merupakan DNS query untuk youtube.com.

3. Perhatikan kolom Source dan Destination — alamatnya menggunakan format IPv6 (bukan IPv4).

4. Pilih paket tersebut, expand bagian Internet Protocol Version 6 dan amati field-fieldnya (Traffic Class, Flow Label, Payload Length, Next Header, Source/Destination Address).

5. Expand bagian Domain Name System (query) dan perhatikan bahwa query type adalah AAAA (yang merupakan tipe DNS untuk IPv6 address), bukan type A (IPv4).

## Lampiran
Hasil Percobaan:
![Hasil Percobaan](...asset/week10.png)