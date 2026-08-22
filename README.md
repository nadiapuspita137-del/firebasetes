# Nusa Chat

Aplikasi chat realtime berbasis Firebase Realtime Database.

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
