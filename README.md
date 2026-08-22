# Nusa Chat

Aplikasi chat realtime berbasis Firebase Realtime Database.

Autentikasi memakai Firebase Authentication dan akses data dibatasi berdasarkan UID,
membership room, serta role admin di Realtime Database Security Rules.

Pengguna dapat mendaftar mandiri untuk menunggu persetujuan. Admin juga dapat membuat
akun Firebase Auth langsung dari panel menggunakan sesi autentikasi sekunder, sehingga
sesi admin utama tidak terputus.

## Struktur project

```text
.
├── assets/
│   ├── css/styles.css       # Tampilan dan layout aplikasi
│   ├── images/favicon.png   # Aset gambar
│   └── js/
│       ├── ambient.js       # Efek visual ambient
│       └── app.js           # Logika aplikasi dan integrasi Firebase
├── database.rules.json      # Aturan Firebase Realtime Database
├── firebase.json            # Konfigurasi Firebase CLI
├── SECURITY.md              # Aktivasi Auth, bootstrap admin, dan deployment aman
└── index.html               # Struktur halaman dan pemuatan aset
```

## Menjalankan secara lokal

Project ini tidak memerlukan proses build. Jalankan server statis dari root project,
misalnya dengan Python:

```sh
python -m http.server 8080
```

Lalu buka `http://localhost:8080` di browser.

Jangan membuka `index.html` langsung melalui protokol `file://`, karena beberapa fitur
browser dan Firebase memerlukan halaman yang dilayani melalui HTTP.

Sebelum deployment pertama versi aman, ikuti [SECURITY.md](SECURITY.md). Akun dari sistem
login lama harus didaftarkan ulang karena password tidak disimpan dalam format yang dapat
dimigrasikan ke Firebase Authentication.
