# Laporan Praktikum Jarkom IF

## Tujuan Praktikum
1. Mahasiswa memahami struktur frame Ethernet (Destination MAC, Source MAC, Type/Length, Data, CRC).

2. Mahasiswa mampu menganalisis frame Ethernet murni dengan menonaktifkan protokol IP di Wireshark (Analyze -> Enabled Protocols -> uncheck IP).

3. Mahasiswa memahami mekanisme kerja protokol ARP dalam menerjemahkan alamat IP ke alamat MAC.

4. Mahasiswa mampu mengamati proses ARP Request (broadcast) dan ARP Reply (unicast) setelah membersihkan cache ARP.

5. Mahasiswa mampu menggunakan perintah arp -a untuk melihat cache ARP dan arp -d * untuk menghapusnya.

## Langkah Pengerjaan
A. Persiapan Awal
1. Buka Command Prompt / Terminal.

2. Jalankan Wireshark dan siapkan untuk mulai capture.

3. Kosongkan cache browser.

B. Menangkap dan Menganalisis Frame Ethernet (Bagian 13.2)
Menjalankan Capture:

1. Mulai capture di Wireshark.

2. Buka browser, akses URL: http://gaia.cs.umass.edu/wireshark-labs/HTTP-ethereal-lab-file3.html (file Bill of Rights AS).

3. Tunggu hingga halaman tampil, lalu hentikan capture.

Menonaktifkan Protokol IP di Wireshark:

1. Di Wireshark, pilih menu Analyze -> Enabled Protocols.

2. Pada dialog yang muncul, cari dan hapus centang (uncheck) pada kotak IP (dan juga IPv6 jika ada).

3. Klik OK.

4. Sekarang jendela Wireshark hanya akan menampilkan frame-frame Ethernet (tanpa interpretasi lapisan IP/Transport). Kolom Protocol mungkin tetap menunjukkan HTTP atau TCP, tetapi yang penting adalah detail frame Ethernet di bagian bawah.

Analisis Frame Ethernet (Figure 13.1 & 13.2):

1. Cari paket yang berisi HTTP GET (biasanya ada di daftar paket, dengan Info GET /wireshark-labs/HTTP-ethereal-lab-file3.html).

2. Pilih paket tersebut. Di packet-header details, expand bagian Ethernet II.

3. Amati field-field berikut:

Destination (MAC address tujuan, biasanya MAC address gateway atau server).

Source (MAC address host Anda).

Type (0x0800 = IPv4, atau 0x0806 = ARP, atau 0x86DD = IPv6).

Data (payload, bisa berupa IP datagram atau ARP message).

C. Address Resolution Protocol (ARP) — Bagian 13.3
Melihat Cache ARP Sebelum Dihapus (Figure di teks 13.3):

1. Di Command Prompt, jalankan perintah: arp -a

2. Amati output yang menampilkan daftar alamat IP dan alamat MAC yang tersimpan di cache ARP.

3. output arp -a.

Menghapus Cache ARP:

1. Di Command Prompt (admin/root), jalankan perintah:

Windows: arp -d * (untuk menghapus semua entri).

Linux/Mac: sudo arp -d * atau sudo ip neigh flush all.

2. Jalankan kembali arp -a untuk memastikan cache sudah kosong (atau hampir kosong).

Mengamati Aksi ARP (Figure 13.4):

1. Mulai capture baru di Wireshark.

2. Buka browser, akses URL: http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-lab-file3.html (perhatikan nama filenya berbeda dengan bagian B!).

3. Tunggu hingga halaman tampil, hentikan capture.

4. Di Wireshark, terapkan filter arp untuk menampilkan hanya paket ARP.

5. Amati daftar paket ARP — seharusnya ada:

ARP Request (broadcast) dari host Anda yang bertanya: "Who has 192.168.x.x? Tell 192.168.x.x". Ciri-ciri:

Destination MAC: ff:ff:ff:ff:ff:ff (broadcast).

Opcode: request (1).

Target MAC: 00:00:00:00:00:00 (kosong).

ARP Reply (unicast) dari pemilik IP tujuan yang menjawab: "192.168.x.x is-at 00:11:22:33:44:55". Ciri-ciri:

Destination MAC: MAC address host Anda (unicast).

Opcode: reply (2).

Target MAC: terisi dengan MAC address yang dicari.

6. Pilih paket ARP Request, di packet-header details:

Expand bagian Ethernet II — tunjukkan Destination MAC = ff:ff:ff:ff:ff:ff.

Expand bagian Address Resolution Protocol — tunjukkan:

Opcode: request (1)

Sender MAC address: ...

Sender IP address: ...

Target MAC address: 00:00:00:00:00:00

Target IP address: ...

7. Pilih paket ARP Reply (jika ada), tunjukkan:

Opcode: reply (2)

Sender MAC address: ... (MAC address tujuan yang dicari)

Sender IP address: ... (IP address tujuan)

Target MAC address: ... (MAC address host Anda)

## Lampiran
Hasil Percobaan:
![Hasil Percobaan](...asset/week13.png)