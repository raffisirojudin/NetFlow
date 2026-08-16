# 🌐 NetFlow — Simulasi Jaringan Interaktif

**NetFlow** adalah platform belajar jaringan komputer yang mengubah materi yang biasanya berat dan penuh istilah teknis jadi pengalaman visual, interaktif, dan bisa dicoba sendiri — bukan cuma dibaca. Dibangun sebagai **satu file HTML mandiri**, tanpa instalasi, tanpa server backend, tanpa build step.

🔗 **Live demo:** _tambahkan link GitHub Pages di sini setelah deploy_

---

## ✨ Fitur Utama

### 🖧 Kanvas Jaringan
Bangun topologi jaringan sendiri lewat drag & drop — pilih dari **11 jenis perangkat** lewat dropdown "+ Tambah Perangkat" (Laptop, Switch, Router, Server, Firewall, Hub, Access Point, Modem, Internet, DNS Server, DHCP Server), sambungkan kabelnya sendiri, lalu kirim data dan lihat animasi tiap lapisan OSI aktif secara real-time. Tiap jenis perangkat punya perilaku simulasi sendiri saat dilewati data — Switch & Access Point membaca Layer 2, Router & Internet membaca Layer 3, Firewall memeriksa Layer 4, Hub & Modem cuma beroperasi di Layer 1 (dan Hub secara sengaja "kurang pintar" — dia menyiarkan ke semua yang tersambung, bukan cuma tujuan, buat menunjukkan kenapa Switch lebih unggul). Koneksi ke Access Point digambar putus-putus untuk membedakan sambungan nirkabel dari kabel.

- **Mode Cepat** — muat topologi klasik (Bus, Star, Ring, Mesh, Tree) sekali klik
- **Firewall sungguhan** — klik untuk atur aturan blokir dari perangkat tertentu, lalu buktikan sendiri data dari sumber itu benar-benar ditolak, sementara sumber lain tetap lolos
- **Misi Kanvas** — 7 tantangan singkat yang otomatis tercentang begitu berhasil diselesaikan, dan tetap tersimpan sebagai pencapaian meski kanvas di-reset
- **🤖 Jelaskan ke AI** — setelah berhasil kirim data, coba jelasin dengan kata-kata sendiri kenapa itu bisa bekerja; AI (Llama 3.3 lewat Groq, gratis) menilai apakah penjelasannya menunjukkan pemahaman asli atau cuma hafalan, lalu kasih masukan + pertanyaan lanjutan (lihat catatan penting di bagian [Fitur AI](#-tentang-fitur-jelaskan-ke-ai) di bawah)
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

Fitur ini memanggil **Groq API** (menjalankan model **Llama 3.3 70B**) untuk menilai penjelasan siswa — dipilih karena Groq punya tingkat gratis beneran, tanpa kartu kredit, cukup kuat untuk kebutuhan ini. Yang perlu dipahami:

- Fitur ini **butuh proxy sendiri untuk aktif** — beda dari fitur lain di situs yang langsung jalan begitu file dibuka, "Jelaskan ke AI" perlu backend kecil dulu (langkah di bawah) karena API key tidak boleh ditaruh langsung di file publik.
- Sebelum di-setup, tombolnya tetap bisa diklik tapi akan menampilkan pesan "belum dikonfigurasi" yang jelas — bukan diam-diam error, dan fitur lain di situs tetap jalan normal.

### Cara mengaktifkannya (gratis, ±10 menit)

Kamu butuh backend kecil (*proxy*) yang menyimpan API key Groq dengan aman lalu meneruskan permintaan dari situsmu. File `ai-proxy-worker.js` di repo ini sudah berisi kodenya — tinggal ikuti langkah berikut pakai [Cloudflare Workers](https://workers.cloudflare.com/) (gratis, cukup lewat browser, tidak perlu install apa pun di komputer):

1. **Siapkan API key Groq (gratis).**
   Buka [console.groq.com](https://console.groq.com/), daftar (tanpa kartu kredit), lalu buat API key baru di menu **API Keys**. Key-nya diawali `gsk_`. Simpan, jangan dibagikan ke siapa pun.

2. **Buat akun Cloudflare** (gratis) di [dash.cloudflare.com](https://dash.cloudflare.com/) kalau belum punya.

3. **Buat Worker baru.**
   Di dashboard, buka menu **Workers & Pages** di sidebar kiri → klik **Create application** → pilih **Create Worker** → klik **Deploy** (pakai kode contoh dulu, nanti diganti).

4. **Ganti kode Worker-nya.**
   Setelah ter-deploy, klik **Edit code**. Hapus semua isi editornya, lalu paste seluruh isi file **`ai-proxy-worker.js`** dari repo ini. Klik **Save and Deploy**.

5. **Tambahkan API key sebagai Secret** (bukan teks biasa, supaya tidak terlihat siapa pun termasuk kamu sendiri setelah disimpan).
   Balik ke halaman Worker → tab **Settings** → bagian **Variables and Secrets** → klik **Add**.
   - Type: pilih **Secret**
   - Variable name: `GROQ_API_KEY`
   - Value: paste API key dari langkah 1

   Klik **Deploy** untuk menyimpan.

6. **Salin URL Worker-mu.** Bentuknya seperti:
   `https://nama-worker-kamu.username-kamu.workers.dev`

7. **Sambungkan ke NetFlow.** Buka `index.html`, cari baris ini di paling atas bagian `<script>`:
   ```js
   const AI_PROXY_URL = '';
   ```
   Isi tanda kutip kosong itu dengan URL Worker-mu dari langkah 6. Simpan, lalu push ke GitHub seperti biasa.

Selesai — fitur "Jelaskan ke AI" sekarang aktif penuh dan gratis, dan API key-nya tetap aman tersimpan di Cloudflare, tidak pernah terlihat di kode publik.

> 💡 Groq punya *rate limit* di tingkat gratisnya (dibatasi jumlah request per menit, bukan tagihan). Cukup untuk pemakaian kelas/demo. Kalau butuh model lain, cek daftar model terbaru di [console.groq.com/docs/models](https://console.groq.com/docs/models) dan ubah nilai `model` di `ai-proxy-worker.js` maupun `submitAiExplanation()` dalam `index.html`.

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
├── index.html            # Seluruh situs — HTML, CSS, dan JS dalam satu file
├── ai-proxy-worker.js    # (Opsional) kode proxy untuk mengaktifkan "Jelaskan ke AI" di GitHub Pages
└── README.md             # Berkas ini
```

---

## 🗺️ Rencana Selanjutnya

Beberapa ide yang sedang dipertimbangkan untuk pengembangan lanjutan:

- Catatan kelebihan/kekurangan tiap topologi saat dimuat lewat Mode Cepat
- Halaman ringkasan/"sertifikat" kecil saat semua modul di bagian Progres selesai 6/6

---

## 📄 Lisensi

Belum ditentukan. Tambahkan berkas `LICENSE` (mis. [MIT](https://choosealicense.com/licenses/mit/)) kalau proyek ini ingin dibuka untuk dipakai atau dimodifikasi orang lain.
