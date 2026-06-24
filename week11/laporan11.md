# Laporan Praktikum Jarkom IF

## Tujuan Praktikum
1. Mahasiswa memahami mekanisme kerja DHCP dalam menetapkan alamat IP secara dinamis kepada host.

2. Mahasiswa mampu menangkap dan menganalisis 4 pesan DHCP (DORA): Discover, Offer, Request, ACK.

3. Mahasiswa memahami isi field-field penting dalam paket DHCP, seperti Client IP, Your IP, Subnet Mask, Router/Gateway, dan Lease Time.

4. Mahasiswa mampu menggunakan perintah ipconfig /release dan /renew (Windows) atau perintah serupa di Linux/Mac untuk memicu trafik DHCP.

## Langkah Pengerjaan
A. Persiapan Awal
1. Buka Command Prompt / Terminal dengan hak akses administrator (Windows) atau sudo (Linux/Mac).

2. Catat antarmuka jaringan yang aktif (misal: Ethernet, Wi-Fi, atau en0 di Mac) melalui Wireshark (Capture -> Options).

3. Jalankan Wireshark dan siapkan untuk memulai capture.

B. Mengumpulkan Jejak Paket DHCP
Untuk Windows:

1. Di Command Prompt (admin), jalankan perintah: ipconfig /release

Perintah ini akan melepas alamat IP yang sedang digunakan.

2. Segera mulai capture di Wireshark (jika belum dimulai).

3. Di Command Prompt, jalankan perintah: ipconfig /renew

Perintah ini akan meminta alamat IP baru dari server DHCP.

4. Tunggu beberapa detik hingga proses selesai, lalu hentikan capture di Wireshark.

C. Analisis Paket DHCP di Wireshark
1. Di Wireshark, terapkan filter dhcp di display filter bar.

2. Amati daftar paket yang muncul — seharusnya ada 4 paket DHCP berurutan (seperti Figure 11.1):

DHCP Discover — dari client (0.0.0.0) ke broadcast (255.255.255.255), client mencari server DHCP.

DHCP Offer — dari server DHCP ke client, server menawarkan alamat IP.

DHCP Request — dari client ke server (atau broadcast), client meminta alamat yang ditawarkan.

DHCP ACK — dari server ke client, server mengonfirmasi dan memberikan alamat IP beserta konfigurasi lainnya.

3. Perhatikan bahwa keempat paket memiliki Transaction ID yang sama (menandakan satu sesi DHCP).

4. Pilih paket DHCP Offer atau DHCP ACK, lalu di packet-header details:

5. Expand bagian Bootstrap Protocol (DHCP).

Amati field-field penting:

Message Type (Discover = 1, Offer = 2, Request = 3, ACK = 5).

Client IP Address (biasanya 0.0.0.0 pada Discover/Request).

Your (client) IP Address (alamat IP yang ditawarkan/diberikan).

Server IP Address (alamat IP server DHCP).

Client MAC Address (alamat hardware client).

Expand bagian Options dan cari:

Option (53) DHCP Message Type.

Option (1) Subnet Mask (misal: 255.255.255.0).

Option (3) Router (default gateway, misal: 192.168.1.1).

Option (51) IP Address Lease Time (lama waktu sewa, misal: 86400 detik = 1 hari).

Option (54) Server Identifier (alamat IP server DHCP).

Option (50) Requested IP Address (pada paket Request).


## Lampiran
Hasil Percobaan:
![Hasil Percobaan](...asset/week11.png)