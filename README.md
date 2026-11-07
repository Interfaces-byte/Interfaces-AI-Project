# Sodium AI

AI open source dengan sistem **BYOK** (Bring Your Own Key). Satu file HTML, tanpa server, tanpa build. Masukkan API key-mu, semua model yang tersedia terdeteksi otomatis, lalu ngobrol, kirim file, dan buat gambar.

Dibuat oleh **Interfaces**, perusahaan yang dipimpin oleh **Dimas Fairuz Manulang**.

> Misi: menjadi AI *less filtered* untuk chat dan *semi uncensored* untuk gambar, supaya orang bebas mengeluarkan imajinasi dan kreativitas mereka.

---

## Daftar isi

- [Fitur](#fitur)
- [Penyedia API](#penyedia-api)
- [Mulai cepat](#mulai-cepat)
- [Deploy ke GitHub Pages](#deploy-ke-github-pages)
- [Konfigurasi](#konfigurasi)
- [Batas harian dan kode akses](#batas-harian-dan-kode-akses)
- [Privasi dan keamanan](#privasi-dan-keamanan)
- [Dijadikan APK](#dijadikan-apk)
- [Struktur file](#struktur-file)
- [Keterbatasan yang perlu diketahui](#keterbatasan-yang-perlu-diketahui)
- [Dukung proyek ini](#dukung-proyek-ini)
- [Lisensi](#lisensi)

---

## Fitur

**Chat**
- Jawaban mengalir bertahap (streaming), dengan tombol Stop.
- Riwayat obrolan tersimpan di sidebar: cari, ganti nama, hapus, dan lanjutkan kapan saja.
- Salin jawaban, Ulangi jawaban, dan gulir otomatis (bisa dimatikan).
- Bubble pesan bergerak dengan animasi liquid seperti Telegram.

**Model**
- Daftar model dibaca langsung dari penyedia, bukan dari daftar tetap.
- Tombol **Muat ulang** di jendela pilih model, plus pembaruan otomatis saat jendela dibuka dan tiap 5 menit.
- Filter: Gratis/Berbayar, provider, konteks minimal (32K, 128K, 1M), kemampuan (Buat gambar, Baca gambar, Video, Audio, Tools, Reasoning), dan urutan (terbaru, termurah, konteks terbesar, nama).
- Di OpenRouter, model berbayar terbuka otomatis kalau saldo ada.

**Lampiran**
- Gambar, PDF, audio, video, dan file teks atau kode (txt, md, csv, json, py, js, html, dan sekitar 20 format lain).
- Jumlah lampiran per pesan tidak dibatasi. Batas ukuran per file bisa diatur (5 sampai 100 MB).
- Tempel dari clipboard, seret ke chat, atau pilih lewat tombol Lampirkan.

**Buat gambar**
- Mode Buat gambar lewat model pembuat gambar OpenRouter, atau endpoint gambar standar OpenAI di penyedia yang mendukungnya.
- Lampiran gambar bisa dipakai sebagai bahan edit (OpenRouter).
- Hasil tersimpan di riwayat dan bisa diunduh.

**Web**
- **Web Search:** Tavily, Brave, atau Serper (butuh API key masing-masing).
- **Web Reading:** link di pesan dibaca otomatis lewat Jina Reader (key opsional) atau Tavily Extract.
- Jawaban yang memakai web menampilkan chip sumber.

**Personalisasi dan tampilan**
- Nama panggilan, tentang kamu, gaya jawaban, bahasa, instruksi khusus, dan kreativitas.
- Desain **Novel You**: kertas krem dengan font buku (Literata). Tema Otomatis, Kertas, Malam, dan Hitam.
- 8 warna aksen plus pemilih warna bebas, 4 jenis huruf, ukuran teks, jarak baris, bentuk sudut, kepadatan, lebar obrolan, lebar sidebar, gaya jawaban AI (Polos atau Bubble), dan banyak pengaturan kecil lainnya.
- Animasi latar liquid dengan tiga mode: **Liquid**, **Hemat**, **Mati**. Perangkat lemah otomatis memakai Hemat.

**Identitas**
- Sodium AI tahu siapa penciptanya dan menjawab jujur soal model yang sedang menjalankannya.
- Gaya *less filtered* bisa dimatikan di Pengaturan > Personalisasi.

---

## Penyedia API

| Penyedia | Catatan |
| --- | --- |
| OpenRouter | Dukungan paling lengkap: daftar model kaya, saldo, harga, gambar, video, audio |
| OpenAI | Chat dan gambar lewat endpoint standar |
| Google Gemini | Lewat endpoint kompatibel OpenAI |
| Groq, DeepSeek, Mistral, xAI, Together AI | Lewat endpoint kompatibel OpenAI |
| Kustom | Alamat (Base URL) dan key sendiri untuk API apa pun yang kompatibel dengan OpenAI |

Kamu bisa menyimpan key beberapa penyedia sekaligus dan berpindah dari pemilih model atau **Pengaturan > API**.

Untuk penyedia selain OpenRouter, kemampuan tiap model (gambar, audio, video) hanya ditebak dari namanya, jadi bisa meleset.

---

## Mulai cepat

1. Buka `index.html` di browser, atau pasang di hosting statis mana pun.
2. Pilih penyedia dan tempel API key.
   - OpenRouter: <https://openrouter.ai/keys>
   - OpenAI: <https://platform.openai.com/api-keys>
   - Google Gemini: <https://aistudio.google.com/apikey>
3. Klik **Hubungkan**, pilih model, lalu mulai ngobrol.

Tambahkan `?lite` di URL untuk memaksa mode animasi hemat.

---

## Deploy ke GitHub Pages

1. Buat repository di GitHub dan unggah `index.html` (dan `README.md`).
2. Buka **Settings > Pages**, pilih branch `main` dan folder `/ (root)`, lalu simpan.
3. Tunggu sebentar, situsmu aktif di `https://<username>.github.io/<nama-repo>/`.

GitHub Pages hanya menyajikan file statis, jadi tidak ada server milikmu yang bisa jebol karena banyak pengunjung. Semua panggilan AI dikirim langsung dari browser pengguna ke penyedia API.

> **Jangan unggah file rahasia.** Lihat bagian [Struktur file](#struktur-file) untuk file yang harus tetap di komputermu.

---

## Konfigurasi

Semua pengaturan pengembang ada sebagai konstanta di bagian atas `<script>` di `index.html`:

| Konstanta | Fungsi |
| --- | --- |
| `APP_NAME` | Nama AI yang tampil dan dipakai di prompt |
| `BRAND` | Nama perusahaan dan pendiri yang diketahui AI |
| `DONATE` | Tautan Saweria, nominal minimal, dan teks ajakan donasi |
| `CONTACT_URL` | Tautan WhatsApp, Instagram, atau email untuk menerima bukti donasi (kosong = tombol disembunyikan) |
| `FREE` | Batas bawaan sebelum donasi: chat per hari, gambar per hari, panjang jawaban, dan riwayat |
| `PUBKEY` | Kunci publik untuk memverifikasi kode akses |
| `PROVS` | Daftar penyedia API dan Base URL bawaannya |

Prompt identitas dan misi ada di fungsi `sysPrompt`.

---

## Batas harian dan kode akses

Pengguna biasa dibatasi **20 chat** dan **5 gambar** per hari. Pengaturan batas (chat, gambar, panjang jawaban, riwayat) terkunci. Donatur dengan donasi minimal **Rp30.000 per bulan** mendapat **kode akses** yang membuka dan memungkinkan mereka mengatur batas sendiri. Developer memakai kode akses khusus tanpa batas.

**Alur untuk donatur**
1. Donasi lewat Saweria dan kirim bukti ke pengembang.
2. Terima kode akses, lalu tempel di **Pengaturan > Batas & Token** (atau di jendela batas yang muncul saat batas tercapai).

**Alur untuk pengembang**
1. Buka `lisensi-dev.html` langsung dari komputermu (jangan di-hosting).
2. Muat kunci rahasia dari `kunci-rahasia-developer.json`.
3. Pilih jenis (Donatur bulanan atau Developer), isi nama dan durasi, lalu klik **Buat kode**.
4. Kirim kode ke donatur.

**Mengganti pasangan kunci** (disarankan sebelum rilis publik)
1. Di `lisensi-dev.html`, klik **Buat pasangan kunci baru**.
2. Simpan kunci rahasia yang muncul di tempat aman.
3. Salin kunci publik ke konstanta `PUBKEY` di `index.html`.
4. Buat ulang kode akses developer dan donatur, karena kode lama tidak lagi valid.

Kode akses ditandatangani dengan ECDSA P-256 dan diverifikasi di browser. Kode palsu, kode yang diubah isinya, dan kode kedaluwarsa ditolak.

---

## Privasi dan keamanan

- API key disimpan hanya di browser pengguna (localStorage) dan dikirim langsung ke penyedia yang dipilih. Pengguna bisa mematikan opsi "Ingat di perangkat ini".
- Riwayat chat disimpan di browser. Teks dan metadata di localStorage, gambar di IndexedDB. Tidak ada yang dikirim ke server pengembang.
- Menghapus data situs di browser menghapus riwayat dan key. Obrolan tidak ikut pindah antar perangkat.
- Jangan pakai di komputer bersama tanpa mematikan penyimpanan key.

**Soal batas harian:** hitungan dan batas disimpan di browser, jadi siapa pun yang membersihkan data situs atau mengubah kode (proyek ini open source) bisa menembusnya. Ini penghalang ringan, bukan penguncian sungguhan. Untuk penguncian yang kuat, dibutuhkan backend yang menghitung pemakaian dan memverifikasi donasi otomatis.

**Soal "less filtered":** prompt Sodium hanya mengatur sikap AI. Model dan penyedia tetap punya filter keamanan sendiri yang tidak bisa ditimpa dari sini, dan prompt ini sengaja menyisakan beberapa batas tegas (tidak membantu tindakan nyata yang mencelakai orang, tidak ada konten seksual yang melibatkan anak atau remaja, tidak memfitnah orang nyata).

---

## Dijadikan APK

Cara tercepat adalah membungkus `index.html` dengan [Capacitor](https://capacitorjs.com/):

```bash
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap init "Sodium AI" com.namakamu.sodiumai --web-dir=www
mkdir www && cp index.html www/index.html
npx cap add android
npx cap sync android
npx cap open android
```

Lalu bangun dari Android Studio (Build > Build APK, atau Build App Bundle untuk Play Store). Hal yang perlu diperhatikan:

- Tombol **Unduh** gambar mungkin butuh plugin `@capacitor/filesystem` atau `@capacitor/share`.
- Tautan Saweria sebaiknya dibuka di browser luar lewat plugin Browser.
- Simpan keystore dan passwordnya baik-baik. Kalau hilang, aplikasi di Play Store tidak bisa diperbarui.

---

## Struktur file

| File | Fungsi | Boleh di-hosting? |
| --- | --- | --- |
| `index.html` | Aplikasi utama | Ya |
| `README.md` | Dokumentasi ini | Ya |
| `iklan-sodium-ai.html` | Video iklan berbasis kode (opsional) | Ya |
| `lisensi-dev.html` | Generator kode akses | **Tidak**, jalankan lokal saja |
| `kunci-rahasia-developer.json` | Kunci rahasia penanda-tangan kode akses | **Tidak, jangan pernah di-upload** |
| `token-developer.txt` | Kode akses developer | **Tidak** |

Tambahkan ini ke `.gitignore` supaya tidak ikut terunggah:

```
kunci-rahasia-developer.json
token-developer.txt
lisensi-dev.html
```

Kalau kunci rahasia sempat terunggah, anggap sudah bocor: buat pasangan kunci baru dan ganti `PUBKEY`.

---

## Keterbatasan yang perlu diketahui

- **CORS:** sebagian penyedia memblokir panggilan langsung dari browser. Kalau begitu, isi Base URL di Pengaturan > API dengan proxy milikmu sendiri. Untuk Web Search, Tavily dan Jina paling aman dipakai langsung dari browser. Brave dan Serper sering butuh proxy.
- **Ukuran lampiran:** penyedia bisa menolak permintaan yang terlalu besar, terutama video, meski jumlah lampiran tidak dibatasi aplikasi.
- **Lampiran di pertanyaan lanjutan:** hanya isi file teks yang dikirim ulang. Gambar, PDF, audio, dan video perlu dilampirkan lagi kalau mau dibahas lebih jauh.
- **Format file:** Word, Excel, dan ZIP belum bisa dibaca di browser.
- **Edit gambar lewat lampiran** hanya tersedia di OpenRouter.
- **Kemampuan model** di penyedia selain OpenRouter ditebak dari nama model.

---

## Dukung proyek ini

Sodium AI gratis dan open source. Kalau terbantu, dukung pengembangannya lewat Saweria:
**<https://saweria.co/BugDawg>**

---

## Lisensi

Belum ditentukan. Pilih lisensi (misalnya MIT) dan tambahkan file `LICENSE` ke repository sebelum dipublikasikan.

---

Dibuat oleh **Interfaces** · dipimpin oleh **Dimas Fairuz Manulang**
