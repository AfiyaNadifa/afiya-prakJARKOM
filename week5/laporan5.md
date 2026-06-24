# Laporan Praktikum Jarkom IF

## Tujuan Praktikum
1. Memahami struktur header protokol UDP (Source Port, Destination Port, Length, Checksum).

2. Menganalisis nilai-nilai field pada header UDP dan memahami arti dari masing-masing field.

3. Memahami hubungan antara port sumber dan port tujuan pada pasangan request-response UDP.

4. Mengetahui nomor protokol UDP (dalam desimal dan heksadesimal) pada datagram IP.

## Langkah Pengerjaan
1. Jalankan Wireshark dan mulai capture paket (tanpa melakukan aktivitas khusus, karena trafik UDP seperti SNMP atau DNS sering muncul secara pasif).

2. (Opsional) Jika tidak ada trafik UDP, buka browser dan akses situs web apa pun untuk memicu query DNS (yang menggunakan UDP port 53), atau gunakan file trace http-ethereal-trace-5 dari wireshark-traces.zip.

3. Hentikan capture, lalu terapkan filter udp di display filter bar untuk menampilkan hanya paket UDP.

4. Pilih salah satu paket UDP dari daftar, lalu di bagian packet-header details, expand bagian User Datagram Protocol sehingga terlihat 4 field:
Source Port
Destination Port
Length
Checksum

5. Amati dan catat nilai dari keempat field tersebut.

6. Catat nilai Length dan verifikasi bahwa nilainya = 8 byte (header) + panjang payload.

7. Pada paket UDP yang sama, expand bagian Internet Protocol Version 4 dan cari field Protocol. Catat nilainya (harus UDP (17) dalam desimal dan 0x11 dalam heksadesimal).

8. Cari dua paket UDP yang berpasangan (request dan response) dengan cara:

 Cari paket UDP pertama dari host Anda ke suatu server (misal: ke port 53 DNS atau port 123 NTP).

Cari paket UDP kedua sebagai balasan dari server ke host Anda.

Amati bahwa port sumber pada paket pertama sama dengan port tujuan pada paket kedua, dan port tujuan pada paket pertama sama dengan port sumber pada paket kedua (port saling bertukar/swap).

9. Wireshark yang menunjukkan:

Satu paket UDP dengan header UDP di-expand penuh.

Field Protocol: UDP (17) di header IP (desimal dan heksadesimal).

Dua paket UDP yang berpasangan (request-response) dengan port yang saling bertukar.

## Lampiran
Hasil Percobaan:
![Hasil Percobaan](...asset/week5.png)