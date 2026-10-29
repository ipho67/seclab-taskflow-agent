# Android Security Helper — pemeriksaan koneksi luar

Panduan ini ditujukan untuk memeriksa keamanan Android secara **read-only**. Ini bukan firewall, tidak bisa mengubah konfigurasi HP dari GitHub, dan tidak membuktikan bahwa perangkat aman hanya dari satu hasil pemeriksaan.

## Langkah cepat pada HP
1. Buka **Setelan → Jaringan & internet / Koneksi**. Matikan Wi‑Fi, hotspot, atau Bluetooth saat tidak digunakan.
2. Buka **Setelan → Keamanan & privasi → Pembaruan** dan pasang pembaruan Android/Google Play yang tersedia.
3. Buka **Setelan → Aplikasi → Akses aplikasi khusus**. Tinjau aplikasi dengan akses **Aksesibilitas**, **Admin perangkat**, **Tampilkan di atas aplikasi lain**, **Akses notifikasi**, **Instal aplikasi tidak dikenal**, **VPN**, dan **Akses penggunaan**. Cabut akses hanya untuk aplikasi yang dikenali dan tidak membutuhkannya.
4. Periksa **Opsi developer → Debugging USB**. Matikan jika tidak digunakan. Jika ADB pernah dipakai, tinjau perangkat/otorisasi debugging dan cabut otorisasi yang tidak dikenal.
5. Buka **Play Store → Play Protect → Pindai**.
6. Periksa perangkat yang masuk ke akun Google dan sesi WhatsApp yang tertaut. Keluar dari sesi yang tidak dikenali dan ganti kata sandi akun jika ada tanda akses yang tidak sah.
7. Pada router, ubah kata sandi admin dan Wi‑Fi bila masih memakai kredensial bawaan; gunakan WPA2-AES/WPA3 dan matikan pengelolaan jarak jauh jika tidak diperlukan.

## Pemeriksaan ADB (hanya membaca)
Jalankan dari komputer tepercaya setelah menyambungkan HP dan menyetujui prompt USB debugging:

```sh
adb devices
adb shell getprop ro.build.version.release
adb shell getprop ro.build.version.security_patch
adb shell settings get global adb_enabled
adb shell settings get secure enabled_accessibility_services
adb shell settings get secure always_on_vpn_app
adb shell dumpsys device_policy
adb shell pm list packages -3
```

Perintah di atas menampilkan status dan daftar untuk ditinjau; hasilnya perlu ditafsirkan sesuai perangkat. Jangan membagikan keluaran yang mengandung data pribadi secara publik. Jangan menjalankan perintah penghapusan paket sistem, mengubah partisi system, atau menonaktifkan komponen sistem hanya berdasarkan nama paket.

## Jika ingin memeriksa koneksi jaringan
ADB standar tidak selalu menyediakan daftar koneksi lengkap untuk aplikasi biasa. Jangan menganggap alamat IP atau koneksi yang tidak dikenal sebagai bukti penyusupan tanpa verifikasi. Catat waktu, aplikasi yang aktif, dan gejala; periksa penggunaan data per aplikasi pada Setelan.

## Batasan
GitHub hanya menyimpan panduan ini. File ini **tidak terpasang di HP**, tidak memutus koneksi secara otomatis, dan tidak dapat mengonfirmasi kondisi perangkat. Mulailah dengan pemeriksaan baca-saja, kemudian tinjau setiap perubahan sebelum dilakukan.
