# Laporan Praktikum Jarkom IF

## Tujuan Praktikum
1. Mahasiswa memahami struktur frame 802.11 Wireless LAN, termasuk perbedaan dengan frame Ethernet kabel.

2. Mahasiswa mampu menganalisis Beacon Frames yang digunakan oleh Access Point (AP) untuk mengiklankan keberadaan dan parameter jaringan (SSID, Supported Rates, Channel, Beacon Interval).

3. Mahasiswa memahami mekanisme Data Transfer melalui frame 802.11 Data, termasuk field To DS/From DS dan 4 address fields.

4. Mahasiswa memahami proses Association dan Disassociation antara host nirkabel dan Access Point, termasuk status code keberhasilan/kegagalan.

5. Mahasiswa mampu membedakan berbagai subtype frame 802.11 (Beacon, Association Request, Association Response, Disassociation, Data).

## Langkah Pengerjaan
A. Persiapan dan Membuka File Trace
Catatan: Karena capture 802.11 membutuhkan driver khusus (AirPcap) yang jarang tersedia di komputer lab, modul ini disediakan file trace yang sudah dikumpulkan. Praktikan tidak perlu melakukan capture sendiri, cukup menganalisis file yang diberikan.

1. Unduh file wireshark-traces.zip dari link yang diberikan di modul (http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip).

2. Ekstrak file zip, cari file bernama Wireshark_802_11.pcap.

3. Buka file tersebut di Wireshark (File -> Open).

4. Tampilan Wireshark akan terlihat seperti Figure 14.1, dengan daftar paket 802.11 yang berisi berbagai jenis frame.

B. Analisis Beacon Frames (Bagian 14.3)
Beacon frame digunakan oleh AP untuk mengiklankan keberadaan secara periodik (sekitar 10-100 kali per detik).

1. Di Wireshark, terapkan filter untuk menampilkan hanya Beacon frames:

Gunakan filter: wlan.fc.type == 0 && wlan.fc.subtype == 8

Atau filter yang lebih sederhana: wlan.fc.type_subtype == 0x08

2. Pilih salah satu Beacon frame dari AP 30 Munroe St (biasanya SSID terlihat di kolom Info).

3. Di packet-header details, expand bagian IEEE 802.11 kemudian expand bagian Tagged parameters.

4. Amati dan catat field-field berikut:

SSID (Service Set Identifier) — nama jaringan, yaitu 30 Munroe St.

Supported Rates — kecepatan data yang didukung (misal: 1.0, 2.0, 5.5, 11.0 Mbps).

DS Parameter Set — menunjukkan channel yang digunakan (Channel 6).

Beacon Interval — interval pengiriman beacon (biasanya 0.1024 detik = 102.4 ms).

TIM (Traffic Indication Map) — untuk indikasi traffic yang tertunda.

5. Beacon frame yang dipilih dengan bagian IEEE 802.11 dan Tagged parameters (SSID, Supported Rates, Channel) di-expand penuh.

C. Analisis Data Transfer (Bagian 14.4)
Dalam trace ini, host nirkabel melakukan 2 permintaan HTTP via frame Data 802.11:

Permintaan 1 (t = 24.82):

1. Di Wireshark, cari frame Data yang membawa HTTP GET ke gaia.cs.umass.edu (IP 128.119.245.12) untuk file alice.txt.

Cari di kolom Info yang mengandung GET /wireshark-labs/alice.txt atau gunakan filter: http.request.uri contains "alice.txt".

2. Pilih frame Data tersebut. Di packet-header details:

Expand bagian IEEE 802.11 dan amati Frame Control:

Type: Data (2)

Subtype: 0

Amati 4 Address fields:

Address 1 (Receiver Address / RA) — biasanya MAC address AP.

Address 2 (Transmitter Address / TA) — MAC address host nirkabel.

Address 3 (Destination Address / DA) — alamat IP tujuan (dalam bentuk MAC, biasanya MAC router/gateway).

Address 4 — jarang digunakan (untuk WDS).

Amati To DS dan From DS flags:

Untuk frame dari client ke AP: To DS = 1, From DS = 0.

Untuk frame dari AP ke client: To DS = 0, From DS = 1.

3. frame Data dengan 802.11 header di-expand, menunjukkan Type/Subtype, Address fields, dan To DS/From DS flags.

Permintaan 2 (t = 32.82):

1. Ulangi langkah di atas untuk permintaan HTTP ke www.cs.umass.edu (IP 128.119.240.19).

2. frame Data tersebut.

D. Analisis Association dan Disassociation (Bagian 14.5)
Timeline di trace:

Host sudah terasosiasi dengan 30 Munroe St di awal trace.

t = 49.58 : Host melakukan Disassociation dari 30 Munroe St.

t = 49.58 – 63.0 : Host mencoba Association ke AP linksys_ses_24086 (tetapi gagal karena AP tidak terbuka / terproteksi).

t = 63.0 : Host menyerah dan melakukan Reassociation kembali ke 30 Munroe St (berhasil).

Menganalisis Disassociation (t = 49.58):

1. Gunakan filter: wlan.fc.type == 0 && wlan.fc.subtype == 3 (Disassociation frame).

2. Pilih frame Disassociation pada waktu t=49.58.

3. Expand bagian IEEE 802.11 dan catat:

Type: Management (0)

Subtype: Disassociation (3)

Reason Code (misal: 1 = Unspecified, atau 3 = Deauthenticated because sending station is leaving).

4. Disassociation frame.

Menganalisis Association yang Gagal ke linksys_ses_24086:

1. Gunakan filter: wlan.fc.type == 0 && wlan.fc.subtype == 0 (Association Request).

2. Cari Association Request yang ditujukan ke SSID linksys_ses_24086 (biasanya di kolom Info ada tulisan Association Request to linksys_ses_24086).

3. Pilih request tersebut, lalu cari pasangan Association Response (subtype 1) yang merupakan balasan dari AP.

4. Di Association Response, perhatikan Status Code — karena gagal, Status Code bukan 0 (Successful). Status code bisa 15 (Authentication failure) atau lainnya.

5. Association Request dan Association Response yang menunjukkan kegagalan.

Menganalisis Reassociation ke 30 Munroe St (t = 63.0):

1. Cari Association Request / Reassociation Request ke 30 Munroe St pada waktu sekitar t=63.0.

2. Cari Association Response yang menunjukkan Status Code = 0 (Successful).

3. Reassociation yang berhasil dengan Status Code 0.

E. Kesimpulan
Tampilan awal Wireshark setelah membuka Wireshark_802_11.pcap (Figure 14.1).

Beacon frame dengan SSID 30 Munroe St, Supported Rates, Channel, dan Beacon Interval di-expand.

Frame Data HTTP GET ke alice.txt dengan 802.11 header (Type/Subtype, Address fields, To DS/From DS) di-expand.

Frame Data HTTP GET ke www.cs.umass.edu (sama seperti di atas).

Frame Disassociation dari 30 Munroe St (t=49.58) dengan Reason Code.

Association Request ke linksys_ses_24086 dan Association Response dengan Status Code gagal (bukan 0).

Reassociation Request ke 30 Munroe St (t=63.0) dan Association Response dengan Status Code = 0 (Successful).

## Lampiran
Hasil Percobaan:
![Hasil Percobaan](...asset/week14.png)