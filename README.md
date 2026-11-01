# Portofolio & CV Muhammad Subeqi (`msubeqidev`)

Portofolio web interaktif personal yang dirancang dengan antarmuka bertema **IDE Dark Matte (PhpStorm/JetBrains Style)** dengan aksen warna hijau yang nyaman di mata (Terminal Emerald Green `#1bb55e`. Dilengkapi dengan dual-bahasa (ID/EN), timeline Gantt chart, interactive developer terminal, dan optimasi cetak PDF.

---

## Daftar Isi
1. [Cara Menjalankan Proyek](#1-cara-menjalankan-proyek)
2. [Kenapa Perubahan HTML Tidak Muncul di Browser?](#2-kenapa-perubahan-html-tidak-muncul-di-browser)
3. [Panduan Mengedit Konten (`assets/index.js`)](#3-panduan-mengedit-konten-assetsindexjs)
4. [Kapan Harus Mengedit `index.html`?](#4-kapan-harus-mengedit-indexhtml)
5. [Panduan Mengedit Warna & Desain (`assets/index.css`)](#5-panduan-mengedit-warna--desain-assetsindexcss)
6. [Fitur Interaktif](#6-fitur-interaktif)
7. [Struktur Direktori](#7-struktur-direktori)
8. [Tips Deployment](#8-tips-deployment)

---

## 1. Cara Menjalankan Proyek

Proyek ini tidak memerlukan proses build yang rumit (`npm run build`). File sudah siap dijalankan langsung melalui web server lokal.

### Opsi A: Menggunakan Laragon (Sangat Direkomendasikan)
Karena proyek berada di dalam folder `C:\laragon\www\msubeqidev`:
1. Buka aplikasi **Laragon**.
2. Klik tombol **Start All** untuk menyalakan Apache / Nginx.
3. Buka browser dan kunjungi salah satu URL berikut:
   - `http://msubeqidev.test` *(otomatis jika virtual host aktif)*
   - `http://localhost/msubeqidev/`

### Opsi B: Menggunakan Fitur Bawaan PhpStorm / WebStorm / VS Code
- **Di PhpStorm:**
  - Buka file `index.html`.
  - Di pojok kanan atas jendela editor, arahkan mouse ke ikon browser (**Chrome**, **Firefox**, atau **Edge**) lalu klik. PhpStorm akan langsung membuka server preview lokal.
- **Di VS Code:**
  - Pasang ekstensi **Live Server**, klik kanan pada `index.html`, lalu pilih **Open with Live Server**.

### Opsi C: Menggunakan PHP Built-in Server (Tanpa Setup)
Buka terminal di folder proyek (`C:\laragon\www\msubeqidev`) dan jalankan:
```bash
php -S localhost:8000
```
Buka browser di `http://localhost:8000`.

### Opsi D: Menggunakan Node.js
```bash
# Menggunakan npx serve
npx serve .

# Atau menggunakan http-server tanpa cache (agar perubahan langsung tampak)
npx http-server -c-1
```

### Opsi E: Menggunakan Python
```bash
python -m http.server 8000
```

---

## 2. Kenapa Perubahan HTML Tidak Muncul di Browser?

Jika Anda mengedit isi teks di dalam `<div id="root">` pada file `index.html`, teks tersebut **tidak akan muncul atau langsung tertimpa** saat halaman dibuka di browser.

### Penyebabnya:
1. **React Mengendalikan Konten `#root`**:
   Di baris paling akhir `index.html`, terdapat skrip:
   ```html
   <script type="module" src="./assets/index.js"></script>
   ```
   Saat halaman dimuat, file `assets/index.js` menginisialisasi React:
   ```javascript
   createRoot(document.getElementById('root')).render(...)
   ```
   React langsung me-render seluruh komponen interaktif (Hero, Karir, Skill, Pendidikan, Terminal, Bahasa) ke dalam `#root` dan menimpa isi HTML statis.
2. **Cache Browser**:
   Browser sering menyimpan file JavaScript (`assets/index.js`) dan CSS di dalam cache. Jika Anda baru saja mengedit kode, tekan kombinasi tombol berikut di browser:
   - **Hard Refresh:** `Ctrl + F5` atau `Ctrl + Shift + R`
   - Atau buka Inspect Element (`F12`) -> Buka tab **Network** -> Centang kotak **Disable cache** selama tab Inspect terbuka.

> **Kesimpulan:** 
> Untuk mengubah data profil, karier, skill, dan teks, editlah di **`assets/index.js`**. 
> Gunakan `index.html` khusus untuk pengaturan SEO, judul tab browser, dan meta preview media sosial.

---

## 3. Panduan Mengedit Konten (`assets/index.js`)

Semua data portofolio telah dirapikan dan dikelompokkan dengan komentar yang jelas di dalam file `assets/index.js` mulai **baris ~1354**.

Buka `assets/index.js` di PhpStorm / IDE Anda, lalu cari bagian berikut:

### [1] Data Profil & Kontak (Mulai Baris ~1354)
Variabel `d`:
```javascript
d = {
  "name": "Muhammad Subeqi",
  "email": "msubeqidev@gmail.com",
  "location": "Kabupaten Blitar, Jawa Timur",
  "careerStart": "2020-03",                 // Format YYYY-MM untuk hitung lama karier
  "github": "https://github.com/muhsubeqi",
  "linkedin": "https://id.linkedin.com/in/muhammadsubeqi",
  "phone": "08573561003",
  "typedRoles": [                           // Teks animasi mengetik di Hero section
    "Software Engineer",
    "Web Developer",
    "Mobile Developer",
    "Backend Developer",
    "Staff Programmer"
  ]
},
```

### [2] Label & Terjemahan UI (Mulai Baris ~1374)
Variabel `f` berisi kamus kata dua bahasa (ID = Indonesia, EN = English):
```javascript
f = {
  "navAbout": { "id": "Profil", "en": "About" },
  "navCareer": { "id": "Karier", "en": "Career" },
  "heroLead": {
    "id": "Lulusan Teknik Informatika yang berfokus pada...",
    "en": "Informatics Engineering graduate focused on..."
  },
  ...
}
```

### [3] Paragraf "Tentang Saya" (Mulai Baris ~1509)
Variabel `m` berisi teks paragraf di bagian Profil:
```javascript
m = e => [
  {
    id: `Saya merupakan lulusan Program Studi Teknik Informatika (S.Kom)...`,
    en: `Computer Science graduate (S.Kom)...`
  },
  {
    id: `Berpengalaman membangun dan memelihara sistem informasi perusahaan...`,
    en: `Experienced in developing and maintaining enterprise systems...`
  }
],
```

### [4] Riwayat Pengalaman Kerja (Mulai Baris ~1523)
Variabel `h` berisi daftar pekerjaan untuk **Gantt Timeline** dan **List Pengalaman**:
```javascript
h = [
  {
    "id": "santini",
    "title": { "id": "Staff Programmer", "en": "Staff Programmer" },
    "company": "PT Santinilestari Energi Indonesia",
    "place": "Kab. Pasuruan, Jawa Timur",
    "start": "2024-03",
    "end": null,                           // null berarti posisi aktif saat ini ("Sekarang")
    "bullets": [
      {
        "id": "Mengembangkan dan mengelola aplikasi web internal...",
        "en": "Developing and maintaining internal enterprise web apps..."
      }
    ],
    "stack": ["PHP", "Laravel", "Livewire", "Filament", "Flutter", "MySQL", "Jira"]
  },
  ...
]
```

### [5] Daftar Keahlian / Skill (Mulai Baris ~1643)
Variabel `g` berisi badge keahlian:
```javascript
g = [
  {
    "label": { "id": "Backend & Bahasa", "en": "Backend & Languages" },
    "items": ["PHP", "Laravel", "JavaScript", "Dart", "HTML5", "CSS3"]
  },
  {
    "label": { "id": "Mobile & Frontend", "en": "Mobile & Frontend" },
    "items": ["Flutter", "Livewire", "Filament", "Tailwind CSS", "Bootstrap", "React"]
  },
  ...
]
```

### [6] Riwayat Pendidikan (Mulai Baris ~1714)
Variabel `_`:
```javascript
_ = {
  "degree": { "id": "Strata 1 — Sarjana Komputer (S.Kom)", "en": "Bachelor’s — Computer Science (S.Kom)" },
  "major": { "id": "Teknik Informatika — Rekayasa Perangkat Lunak", "en": "Informatics Engineering — Software Engineering" },
  "school": "Universitas Islam Balitar",
  "year": "2021",
  "gpa": "Rekayasa Perangkat Lunak"
},
```

### [7] Pelatihan & Sertifikasi (Mulai Baris ~1731)
Variabel `v` berisi daftar sertifikat:
```javascript
v = [
  {
    "id": "Dicoding — Belajar Membuat Aplikasi Web dengan React",
    "en": "Dicoding — Building Web Applications with React"
  },
  ...
]
```

---

## 4. Kapan Harus Mengedit `index.html`?

Editlah file `index.html` ketika Anda ingin menyesuaikan:

1. **Judul Tab Browser (`<title>`)**:
   ```html
   <title>Muhammad Subeqi - Software Engineer | Web &amp; Mobile Developer</title>
   ```
2. **Deskripsi SEO Google Search**:
   ```html
   <meta name="description" content="CV Muhammad Subeqi (msubeqidev)..." />
   ```
3. **OpenGraph & Media Sharing Preview** (untuk tampilan thumbnail ketika link dikirim ke WhatsApp, Telegram, LinkedIn, Facebook):
   ```html
   <meta property="og:title" content="Muhammad Subeqi - Software Engineer" />
   <meta property="og:description" content="..." />
   <meta property="og:url" content="https://muhsubeqi.github.io/" />
   <meta property="og:image" content="https://muhsubeqi.github.io/og-image.png" />
   ```
4. **Data Terstruktur Schema.org (JSON-LD)**:
   Di baris ~50 terdapat `<script type="application/ld+json">` yang dibaca oleh mesin pencari Google untuk mengidentifikasi Anda sebagai entitas `Person`.

---

## 5. Panduan Mengedit Warna & Desain (`assets/index.css`)

Semua warna menggunakan sistem variabel CSS (**CSS Custom Properties**), sehingga Anda cukup mengubah variabel di bagian paling atas file `assets/index.css`:

### Tema Gelap (Dark Mode / Default IDE Style)
Terletak pada selektor `:root` (baris ~8):
```css
:root {
  --bg: #191a1c;         /* Warna background utama (PhpStorm matte dark charcoal) */
  --surface: #222428;    /* Warna kartu / card container */
  --surface-2: #282b30;  /* Warna kartu hover / layer kedua */
  --line: #2e3136;       /* Warna garis batas / border */
  --ink: #dfe1e5;        /* Warna teks utama */
  --muted: #868a91;      /* Warna teks sekunder / deskripsi redup */
  --accent: #1bb55e;     /* Warna aksen hijau terminal utama (Terminal Emerald Green) */
  --accent-ink: #0c1b11; /* Warna teks gelap tajam di atas tombol hijau */
  --pink: #38d97a;       /* Warna aksen hijau sekunder / hover (Mint Green) */
}
```

### Tema Terang (Light Mode)
Terletak pada selektor `:root[data-theme=light]` (baris ~65):
```css
:root[data-theme=light] {
  --bg: #f8fafc;
  --surface: #ffffff;
  --line: #e2e8f0;
  --ink: #0f172a;
  --muted: #64748b;
  --accent: #2563eb;
  ...
}
```

---

## 6. Fitur Interaktif

- **Tombol WhatsApp Mengambang (Floating Action Button)**:
  - Terletak di pojok kanan bawah dengan tautan langsung ke WhatsApp (`https://wa.me/628573561003`).
  - Dilengkapi efek animasi hover halus, transisi elevasi, dan tooltip interaktif.
- **Terminal Pengembang Interaktif**:
  - Dapat dibuka dengan menekan tombol **`** (backtick) pada keyboard atau mengklik trigger terminal.
  - Perintah yang didukung: `whoami`, `about`, `skills`, `exp`, `contact`, `theme`, `clear`, `help`, serta easter egg seperti `sudo hire msubeqidev`.
- **Gantt Chart Timeline Karier**:
  - Menghitung durasi kerja secara otomatis berdasarkan rentang tanggal.
  - Klik bar tertentu untuk melompat langsung ke detail pekerjaan terkait.
- **Peralihan Bahasa (ID / EN)**:
  - Tombol switch bahasa di pojok kanan atas mengubah seluruh teks secara instan tanpa reload halaman.
- **Peralihan Tema (Dark / Light)**:
  - Preferensi tema disimpan secara otomatis di `localStorage` browser pengguna.
- **Optimasi Cetak PDF / CV Fisik**:
  - Tekan `Ctrl + P` di browser untuk mencetak. CSS otomatis menyembunyikan navigasi, tombol, dan terminal, lalu memformat CV menjadi dokumen cetak yang bersih dan rapi.

---

## 7. Struktur Direktori

```text
msubeqidev/
├── assets/
│   ├── index.css            # Style CSS (unminified, rapi, variabel warna di atas)
│   ├── index.js             # Skrip React & seluruh data profil, karir, skill
│   └── *.woff2              # Font lokal JetBrains Mono
├── CV Muhammad Subeqi.pdf   # Dokumen CV asli
├── favicon.svg              # Ikon tab browser (bertema hijau IDE)
├── index.html               # File HTML utama (SEO & template mount React)
├── og-image.png             # Gambar pratinjau thumbnail media sosial
├── robots.txt               # Aturan crawler mesin pencari
├── sitemap.xml              # Peta situs untuk Google Search Console
├── .gitignore               # Menghindari commit folder cache (.idea/)
└── README.md                # Dokumentasi panduan lengkap
```

---

## 8. Tips Deployment

Jika ingin mempublikasikan portofolio ini secara online (misalnya ke **GitHub Pages**):
1. Buat repository baru di GitHub dengan nama `muhsubeqi.github.io` (atau nama repository pilihan Anda).
2. Lakukan push commit:
   ```bash
   git add .
   git commit -m "Initial portfolio setup msubeqidev"
   git push origin master
   ```
3. Di pengaturan repository GitHub:
   - Masuk ke **Settings** -> **Pages**.
   - Pilih sumber dari branch `master` (atau `main`) folder `/ (root)`.
   - Simpan. Website Anda akan aktif dalam 1-2 menit.
4. File `.nojekyll` sudah tersedia di dalam folder ini agar GitHub Pages tidak memfilter file aset yang diawali titik atau font.

