# Laporan Praktikum Jarkom IF

## Tujuan Praktikum
1. Memahami mekanisme dasar protokol HTTP melalui analisis paket di Wireshark.

2. Menganalisis interaksi GET/response, Conditional GET, pengambilan dokumen panjang, dan objek tersemat.

3. Memahami proses autentikasi HTTP dan encoding Base64.

## Langkah Pengerjaan
A. Basic HTTP GET/response interaction
1. Jalankan Wireshark dan terapkan filter http.

2. Buka browser, akses URL: http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html.

3. Hentikan capture, amati 2 paket HTTP (GET dari client dan 200 OK dari server).


B. HTTP Conditional GET/response interaction
1. Kosongkan cache browser dan cache DNS host.

2. Jalankan Wireshark, akses URL: http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file2.html.

3. Segera refresh/reload halaman yang sama (request kedua).

4. Hentikan capture, amati request kedua yang mengandung header If-Modified-Since dan response 304 Not Modified.

C. Retrieving Long Documents
1. Kosongkan cache browser.

2. Jalankan Wireshark, akses URL: http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file3.html.

3. Hentikan capture, amati bahwa response HTTP (file Bill of Rights ~4500 byte) dipecah menjadi beberapa segmen TCP (TCP segment of a reassembled PDU).

D. HTML Documents dengan Embedded Objects
1. Kosongkan cache browser.

2. Jalankan Wireshark, akses URL: http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html.

3. Hentikan capture, amati bahwa browser melakukan 3 request GET (1 HTML + 2 gambar logo) dan 3 response.

E. HTTP Authentication
1. Kosongkan cache browser.

2. Jalankan Wireshark, akses URL: http://gaia.cs.umass.edu/wireshark-labs/protected_pages/HTTP-wireshark-file5.html.

3. Masukkan username: wireshark-students dan password: network pada pop-up login.

4. Hentikan capture, amati 2 request GET (pertama 401 Unauthorized, kedua 200 OK dengan header Authorization: Basic berisi string Base64 d2lyZXNoYXJrLXN0dWRlbnRzOm5ldHdvcms=).



## Lampiran
Hasil Percobaan:
![Hasil Percobaan](...asset/week3.png)