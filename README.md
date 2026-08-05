# 🌐 NetFlow — Simulasi Jaringan Interaktif

**NetFlow** adalah platform belajar jaringan komputer yang mengubah materi yang biasanya berat dan penuh istilah teknis jadi pengalaman visual, interaktif, dan bisa dicoba sendiri — bukan cuma dibaca. Dibangun sebagai **satu file HTML mandiri**, tanpa instalasi, tanpa server backend, tanpa build step.

🔗 **Live demo:** _tambahkan link GitHub Pages di sini setelah deploy_

---

## ✨ Fitur Utama

### 🖧 Kanvas Jaringan
Bangun topologi jaringan sendiri lewat drag & drop — tambah Laptop, Switch, Router, Server, atau **Firewall**, sambungkan kabelnya sendiri, lalu kirim data dan lihat animasi tiap lapisan OSI aktif secara real-time (dibungkus di pengirim, dibaca di tiap hop, dibongkar di penerima).

- **Mode Cepat** — muat topologi klasik (Bus, Star, Ring, Mesh, Tree) sekali klik
- **Firewall sungguhan** — klik untuk atur aturan blokir dari perangkat tertentu, lalu buktikan sendiri data dari sumber itu benar-benar ditolak, sementara sumber lain tetap lolos
- **Misi Kanvas** — 6 tantangan singkat yang otomatis tercentang begitu berhasil diselesaikan, dan tetap tersimpan sebagai pencapaian meski kanvas di-reset
- **🤖 Jelaskan ke AI** — setelah berhasil kirim data, coba jelasin dengan kata-kata sendiri kenapa itu bisa bekerja; Claude menilai apakah penjelasannya menunjukkan pemahaman asli atau cuma hafalan, lalu kasih masukan + pertanyaan lanjutan (lihat catatan penting di bagian [Fitur AI](#-tentang-fitur-jelaskan-ke-ai) di bawah)
- Error yang jujur — kalau dua perangkat belum tersambung, pengiriman data akan gagal beneran, bukan skenario yang di-skrip

### 🃏 Kartu Analogi
Istilah jaringan dipasangkan dengan analogi dunia nyata (Router = petugas pos, Switch = resepsionis kantor, DNS = buku telepon, dst) dalam **14 kartu** yang bisa dibalik. Tiga mode dalam satu tempat: **Jelajah Bebas**, **Tebak Konsep**, dan **Kuis Mini** — kuisnya menarik 5 soal acak dari bank berisi 10 soal setiap kali dicoba (urutan jawaban juga diacak), jadi tiap percobaan terasa beda.

### 📖 Glosarium
Kamus **30 istilah** jaringan, dikemas dalam widget folder yang bisa diklik untuk membuka pencarian instan — bukan grid panjang yang bikin capek scroll.

### 🧮 Kalkulator Subnet
Masukkan IP Address dan CIDR, langsung dapat Network Address, Broadcast Address, host range, dan visualisasi 32-bit yang menunjukkan pembagian bit jaringan vs host.

### 🎚️ 3 Tingkat Penjelasan
**Pemula**, **Menengah**, atau **Pro** — atur seberapa dalam detail teknis yang ditampilkan (analogi saja vs istilah teknis vs contoh protokol/CLI), berlaku di seluruh situs lewat satu sakelar.

### 📱 Responsif
Dioptimalkan untuk desktop, tablet, dan HP — termasuk penyesuaian khusus untuk orientasi landscape di ponsel.

---

## 🛠️ Teknologi

Tidak ada framework, tidak ada dependency untuk di-*install*:

- HTML5 + CSS3 (custom properties, Grid/Flexbox, animasi)
- JavaScript vanilla (ES6+, tanpa library)
- Google Fonts (Plus Jakarta Sans, Inter, JetBrains Mono) via CDN

Seluruh situs — struktur, gaya, dan logika — ada di **satu file**: `index.html`.

---

## 🤖 Tentang Fitur "Jelaskan ke AI"

Fitur ini memanggil Claude API langsung dari browser (`fetch` ke `api.anthropic.com`) untuk menilai penjelasan siswa. Ini penting untuk dipahami sebelum deploy:

- **Dibuka sebagai artifact di Claude.ai** → langsung jalan, tidak perlu setup apa pun.
- **Di-deploy mandiri** (GitHub Pages, hosting lain, dibuka langsung dari file) → panggilan API-nya **akan gagal**, dan situs akan menampilkan pesan yang jelas ke pengguna (bukan diam-diam error). Ini bukan bug — API key tidak boleh ditaruh di file publik karena siapa pun bisa mengambil dan memakainya.

**Supaya fitur ini live di GitHub Pages**, kamu perlu backend kecil (proxy) yang menyimpan API key dengan aman dan meneruskan permintaan dari situs ke Anthropic. Cara paling sederhana dan gratis:

1. Buat [Cloudflare Worker](https://workers.cloudflare.com/) atau [Vercel Serverless Function](https://vercel.com/docs/functions) baru.
2. Simpan API key Anthropic-mu sebagai *environment variable* di sana (bukan di kode).
3. Worker/function itu menerima request dari situsmu, menempelkan API key di header `x-api-key`, lalu meneruskannya ke `https://api.anthropic.com/v1/messages`.
4. Di `index.html`, ganti URL fetch pada fungsi `submitAiExplanation()` dari `https://api.anthropic.com/v1/messages` menjadi URL Worker/function kamu sendiri.

Kalau langkah ini belum dilakukan, fitur lain di situs tetap berjalan normal — hanya "Jelaskan ke AI" yang menampilkan pesan info, bukan mengganggu bagian lain.

---

## 🚀 Cara Pakai

### Jalankan secara lokal
Unduh `index.html`, buka langsung di browser mana saja. Tidak perlu `npm install`, tidak perlu server.

### Deploy ke GitHub Pages
1. Push repo ini ke GitHub.
2. Buka **Settings → Pages**.
3. Di bagian **Source**, pilih branch `main` dan folder `/ (root)`.
4. Klik **Save** — situs akan tersedia beberapa menit kemudian di:
   `https://<username-kamu>.github.io/<nama-repo>/`

---

## 📂 Struktur Proyek

```
.
├── index.html   # Seluruh situs — HTML, CSS, dan JS dalam satu file
└── README.md    # Berkas ini
```

---

## 🗺️ Rencana Selanjutnya

Beberapa ide yang sedang dipertimbangkan untuk pengembangan lanjutan:

- Catatan kelebihan/kekurangan tiap topologi saat dimuat lewat Mode Cepat
- Halaman ringkasan/"sertifikat" kecil saat semua modul di bagian Progres selesai 6/6

---

## 📄 Lisensi

Belum ditentukan. Tambahkan berkas `LICENSE` (mis. [MIT](https://choosealicense.com/licenses/mit/)) kalau proyek ini ingin dibuka untuk dipakai atau dimodifikasi orang lain.
