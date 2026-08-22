# Panduan aktivasi keamanan Nusa Chat

Project menggunakan Firebase Authentication dan Realtime Database Rules. Ikuti
urutan ini agar administrator pertama tidak terkunci saat rules baru diterapkan.

## 1. Aktifkan Firebase Authentication

Di Firebase Console untuk project `chatroom-app-34746`:

1. Buka **Authentication > Sign-in method**.
2. Aktifkan provider **Email/Password**.
3. Buat satu akun administrator dari tab **Users**.
4. Salin UID akun administrator tersebut.

## 2. Bootstrap administrator pertama

Sebelum menerbitkan rules baru, buka **Realtime Database > Data** dan buat data:

```text
admins/
  UID_ADMIN: true
```

Ganti `UID_ADMIN` dengan UID dari Firebase Authentication. Jangan memakai email,
username, atau password sebagai key. Setelah rules baru aktif, browser tidak dapat
menambah administrator baru karena penulisan path `admins` ditolak oleh rules.

## 3. Terbitkan aplikasi dan rules secara bersamaan

```sh
firebase deploy --only hosting,database
```

Lakukan deployment segera setelah bootstrap administrator. Rules lama memberi akses
publik dan tidak boleh dibiarkan aktif lebih lama dari yang diperlukan.

## 4. Bersihkan data autentikasi lama

Setelah login admin baru berhasil, hapus melalui Firebase Console:

- `appConfig/adminCodeHash`
- akun lama pada `appConfig/accounts` yang masih mempunyai `passwordHash` atau `salt`

Password lama tidak dapat dimigrasikan ke Firebase Authentication. Pengguna lama harus
mendaftar ulang dengan email, kemudian disetujui admin. Saat admin menyetujui akun,
aplikasi membuat `roomMembers/{roomId}/{uid}: true` secara otomatis.

## Model keamanan

- Identitas pengguna berasal dari token Firebase Authentication (`auth.uid`).
- Pengguna hanya dapat membaca room tempat UID-nya terdaftar sebagai anggota.
- Pesan baru wajib memakai UID pengirim yang sama dengan `auth.uid`.
- Pesan hanya dapat diubah atau dihapus pemiliknya; admin dapat melakukan moderasi.
- Thread japri hanya dapat dibaca UID yang tercatat pada `participants`.
- Pengaturan, approval, ban, room, dan pembersihan data hanya dapat ditulis admin.
- Mengetahui `firebaseConfig` tidak memberikan hak akses tanpa token dan rules yang sesuai.

## Langkah tambahan yang direkomendasikan

Aktifkan Firebase App Check untuk aplikasi Web menggunakan reCAPTCHA Enterprise. Mulai
dengan mode monitoring, periksa metrik request, lalu aktifkan enforcement untuk Realtime
Database. App Check adalah lapisan anti-abuse tambahan dan bukan pengganti Authentication
atau Security Rules.
