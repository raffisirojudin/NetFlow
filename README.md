# 🌐 NetFlow — Simulasi Jaringan Interaktif

**NetFlow** adalah platform belajar jaringan komputer yang mengubah materi yang biasanya berat dan penuh istilah teknis jadi pengalaman visual, interaktif, dan bisa dicoba sendiri — bukan cuma dibaca. Dibangun sebagai **satu file HTML mandiri**, tanpa instalasi, tanpa server backend, tanpa build step.

---

## ✨ Fitur Utama

### 🖧 Kanvas Jaringan
Bangun topologi jaringan sendiri lewat drag & drop — tambah Laptop, Switch, Router, atau Server, sambungkan kabelnya sendiri, lalu kirim data dan lihat animasi tiap lapisan OSI aktif secara real-time (dibungkus di pengirim, dibaca di tiap hop, dibongkar di penerima).

- **Mode Cepat** — muat topologi klasik (Bus, Star, Ring, Mesh, Tree) sekali klik
- **Misi Kanvas** — 5 tantangan singkat yang otomatis tercentang begitu berhasil diselesaikan, dan tetap tersimpan sebagai pencapaian meski kanvas di-reset
- Error yang jujur — kalau dua perangkat belum tersambung, pengiriman data akan gagal beneran, bukan skenario yang di-skrip

### 🃏 Kartu Analogi
Istilah jaringan dipasangkan dengan analogi dunia nyata (Router = petugas pos, Switch = resepsionis kantor, DNS = buku telepon, dst) dalam kartu yang bisa dibalik. Tiga mode dalam satu tempat: **Jelajah Bebas**, **Tebak Konsep**, dan **Kuis Mini**.

### 📖 Glosarium
Kamus 20 istilah jaringan, dikemas dalam widget folder yang bisa diklik untuk membuka pencarian instan — bukan grid panjang yang bikin capek scroll.

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

- Perangkat **Firewall** yang bisa benar-benar ditaruh di Kanvas dan menolak data dari sumber tertentu
- Catatan kelebihan/kekurangan tiap topologi saat dimuat lewat Mode Cepat
- Halaman ringkasan/"sertifikat" kecil saat semua modul di bagian Progres selesai 6/6

---

## 📄 Lisensi

Belum ditentukan. Tambahkan berkas `LICENSE` (mis. [MIT](https://choosealicense.com/licenses/mit/)) kalau proyek ini ingin dibuka untuk dipakai atau dimodifikasi orang lain.
