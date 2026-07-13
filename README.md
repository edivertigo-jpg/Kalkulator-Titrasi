# Kalkulator Titrasi Syringe Pump (PWA)

Aplikasi web (PWA) untuk menghitung kecepatan syringe pump (mL/jam) dan konsentrasi obat drip ICU: Norepinefrin, Dopamin, Dobutamin, Adrenalin, Nitrogliserin, Nitroprusside, Fenilefrin, Isoproterenol, Milrinon, dan obat lain secara manual.

Bisa dipasang di HP (Android/iOS) seperti aplikasi biasa, dan tetap bisa dipakai offline setelah dibuka sekali.

## Isi folder

```
syringe-pump/
├─ index.html        -> aplikasi utama (semua logika ada di sini)
├─ manifest.json      -> konfigurasi PWA (nama, ikon, warna)
├─ sw.js               -> service worker (untuk mode offline)
└─ icons/
   ├─ icon-192.png
   ├─ icon-512.png
   └─ icon-512-maskable.png
```

## Cara Deploy ke GitHub Pages

1. Buat repository baru di GitHub, misal namanya `syringe-pump-calculator`.
2. Upload semua isi folder `syringe-pump/` ini ke repository tersebut (bisa lewat web GitHub: "Add file" → "Upload files", atau lewat `git push`).
   - Pastikan struktur foldernya tetap sama (file `index.html` ada di root repo, folder `icons/` ikut ter-upload).
3. Buka repo → **Settings** → **Pages** (di sidebar kiri).
4. Pada bagian **Build and deployment**, pilih:
   - Source: `Deploy from a branch`
   - Branch: `main` (atau `master`), folder `/ (root)`
5. Klik **Save**. Tunggu 1–2 menit, GitHub akan memberi link seperti:
   ```
   https://<username-github-anda>.github.io/syringe-pump-calculator/
   ```
6. Buka link tersebut di HP. Untuk memasang sebagai aplikasi:
   - **Android (Chrome):** akan muncul banner "Pasang" di aplikasi, atau menu ⋮ → "Tambahkan ke Layar Utama" / "Install app".
   - **iPhone (Safari):** tombol Share (kotak dengan panah) → "Add to Home Screen".

Setelah dipasang, aplikasi bisa dibuka tanpa internet (mode offline), karena `sw.js` menyimpan file aplikasinya di HP.

## Cara pakai (ringkas)

1. **Langkah 1 – Konsentrasi Obat**: pilih obat dari daftar (otomatis isi jumlah obat & volume), atau isi manual jumlah obat (mg/mcg) dan total volume pelarut (mL).
2. **Tab "Hitung Kecepatan"**: isi berat badan pasien dan dosis target (mcg/kg/menit, mcg/kg/jam, atau mg/jam) → hasil kecepatan pump (mL/jam) langsung muncul.
3. **Tab "Cek Dosis Berjalan"**: untuk cek ulang, isi berat badan dan kecepatan pump yang sedang berjalan → aplikasi menghitung dosis (mcg/kg/menit) yang sebenarnya sedang diterima pasien.

## Troubleshooting: logo patah / tombol "Pasang" tidak muncul

Kalau logo di header terlihat patah (ikon gambar rusak) dan banner "Pasang" tidak pernah muncul, hampir selalu penyebabnya **folder `icons/` tidak ikut ter-upload dengan benar** ke GitHub. Cara cek & benerin:

1. Buka `https://<username-anda>.github.io/<nama-repo>/icons/icon-192.png` langsung di browser.
   - Kalau muncul gambar ikon → folder icons aman, masalah di tempat lain.
   - Kalau muncul halaman 404 → folder `icons/` memang belum ke-upload atau strukturnya salah.
2. Cek juga di tab **Code** repo GitHub Anda: pastikan ada folder `icons` sejajar dengan `index.html`, `manifest.json`, dan `sw.js` (bukan malah `index.html` sendirian di root sementara `icons` ketinggalan, atau nyasar masuk subfolder lain).
3. Kalau belum ada, upload ulang: masuk ke repo → **Add file → Upload files** → **drag seluruh folder `icons`** (bukan file satu-satu) ke area upload, lalu commit.
4. Setelah folder `icons` benar, tunggu 1-2 menit lalu **hard refresh** (Ctrl+Shift+R / buka di tab incognito) karena browser sering nyimpen cache versi lama.

Catatan soal tombol install:
- Di **Android (Chrome)**, tombol "Pasang" baru muncul kalau: manifest + ikon + service worker semuanya valid, HTTPS aktif (GitHub Pages otomatis HTTPS), dan biasanya perlu sedikit interaksi/waktu di halaman dulu.
- Di **iPhone (Safari)**, tombol otomatis seperti ini **memang tidak akan pernah muncul** — itu bukan bug. Cara install di iPhone selalu manual: tombol Share (kotak dengan panah ke atas) → **Add to Home Screen**.

## Catatan penting

- Nilai default konsentrasi tiap obat pada dropdown adalah **contoh umum**, bukan standar baku — sesuaikan selalu dengan kebijakan/protokol farmasi rumah sakit masing-masing.
- Aplikasi ini alat bantu hitung, **bukan pengganti** penilaian klinis. Selalu lakukan double-check sebelum menyesuaikan titrasi obat vasoaktif.
- Ingin ganti nama aplikasi, warna, atau menambah daftar obat? Semua bisa diedit langsung di `index.html` (bagian array `DRUGS` di dalam tag `<script>`) dan `manifest.json`.
