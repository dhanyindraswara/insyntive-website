# INSYNTIVE Website

Single-page website untuk INSYNTIVE.com. Dibangun dengan HTML/CSS/JS murni (tanpa framework), siap di-deploy ke GitHub Pages.

## 📁 Struktur File

```
insyntive-website/
├── index.html      ← File utama (semua kode di sini)
├── README.md       ← File ini
└── assets/         ← Folder buat gambar (dibuat nanti)
    └── images/
```

Saat ini semua CSS dan JS ada di dalam `index.html` biar gampang manage. Edit 1 file, deploy 1 file.

---

## 🚀 Deploy ke GitHub Pages

### Pertama Kali Setup

1. **Buat repository baru** di GitHub, kasih nama `insyntive-website` (atau apapun)
2. **Upload file `index.html`** ke repo
3. Buka **Settings → Pages**
4. Di "Source", pilih branch `main` dan folder `/ (root)`
5. Klik **Save**
6. Tunggu 1-2 menit, website akan live di `https://username.github.io/insyntive-website`

### Connect ke Domain insyntive.com

1. Di **Settings → Pages**, scroll ke "Custom domain"
2. Masukkan `insyntive.com`, klik Save
3. Di provider domain (Niagahoster/Cloudflare/dll), set DNS record:
   ```
   A     @    185.199.108.153
   A     @    185.199.109.153
   A     @    185.199.110.153
   A     @    185.199.111.153
   CNAME www  username.github.io
   ```
4. Tunggu DNS propagasi (max 24 jam, biasanya < 1 jam)
5. Centang "Enforce HTTPS" di GitHub Pages settings

### Update Konten

Setelah live, kalo mau update konten:
1. Edit `index.html` (langsung di GitHub web atau di laptop lo)
2. Commit perubahan
3. Tunggu ~1 menit, perubahan otomatis live di insyntive.com

---

## ✏️ Cara Edit Konten

### 1. Ganti Warna Brand

Buka `index.html`, cari `:root` di bagian `<style>` (sekitar baris 50). Semua warna ada di sini:

```css
:root {
  --color-primary: #02A0C1;       /* Cyan utama */
  --color-secondary: #3581E1;     /* Blue secondary */
  --color-accent: #D6FD91;        /* Lime green - CTA & highlight */
  --color-mint: #97D1C6;          /* Mint accent */
  --color-pale-blue: #D7E8FB;     /* Pale blue background */
  --color-light: #EDEDED;         /* Light gray */
  --color-dark: #1F1F1F;          /* Near black - text utama */
}
```

Ganti hex code di sini, otomatis semua section ikut berubah.

### 2. Ganti Teks / Headline

Setiap section di-comment dengan jelas. Cari bagian yang mau diedit:

```html
<!-- ============================================
     HERO SECTION
     Edit headline & subheadline di sini
     ============================================ -->
```

Section yang ada:
- **HEADER** — menu navigasi
- **HERO SECTION** — headline utama + tagline
- **INDUSTRY MARQUEE** — pills industri yang scroll otomatis
- **TRUSTED BY** — list klien & angka stats
- **LAYANAN / THREE PILLARS** — 3 layanan utama
- **PROCESS / HOW WE WORK** — 4 langkah cara kerja
- **INDUSTRIES** — 2 industri detail (Mining, Konstruksi)
- **DIGITAL PRODUCTS** — 4 produk digital
- **WHY INSYNTIVE** — stats counter
- **TESTIMONIALS** — testimoni klien (placeholder, ganti dengan real)
- **LATEST INSIGHT** — link ke Instagram
- **CONTACT / FORM** — form kontak
- **FOOTER**

### 3. Setup Form (PENTING)

Form-nya sekarang masih placeholder. Lo perlu setup Formspree (gratis):

**Step 1: Daftar Formspree**
1. Buka https://formspree.io
2. Sign up pake email lo (`halomas@dhanyindraswara.com` atau `dhanyindraswara@gmail.com`)
3. Klik "New Form"
4. Kasih nama form, contoh: "INSYNTIVE Contact"
5. Copy form endpoint, contoh: `https://formspree.io/f/abc123xyz`

**Step 2: Update di index.html**

Cari bagian ini di `index.html`:

```html
<form class="contact-form"
      id="contactForm"
      action="https://formspree.io/f/YOUR_FORM_ID"
      method="POST">
```

Ganti `YOUR_FORM_ID` dengan ID dari Formspree lo.

**Step 3: Verify Email**

Submit form sekali, Formspree akan kirim email konfirmasi. Klik confirm di email itu, baru form aktif.

**Free plan Formspree:** 50 submission/bulan. Cukup buat awal. Kalo udah ramai, upgrade ke paid plan.

### 4. Ganti Nomor WhatsApp

Cari semua occurence `6281805759025` di file (ada beberapa tempat: floating WA button, contact section, footer). Replace dengan nomor baru kalo perlu ganti.

Format WA:
- Nomor `081805759025` → tulis `6281805759025` (tanpa 0 depan, pake kode negara 62)
- Format link: `https://wa.me/6281805759025?text=PESAN%20DEFAULT`
- Spasi di pesan default pake `%20`

### 5. Ganti Gambar / Visual

Sekarang masih pake emoji icon sebagai placeholder. Mau ganti pake gambar real?

**Opsi A: Pake Google Drive (manage di GDrive)**

1. Upload gambar ke Google Drive
2. Klik kanan → Share → Anyone with the link → Copy link
3. Link biasanya: `https://drive.google.com/file/d/FILE_ID/view`
4. Convert ke direct image URL: `https://lh3.googleusercontent.com/d/FILE_ID`
5. Pake di HTML: `<img src="https://lh3.googleusercontent.com/d/FILE_ID" alt="...">`

⚠️ **Catatan:** Google Drive kadang rate-limit kalo traffic tinggi. Buat website production, opsi B lebih reliable.

**Untuk Trusted By logo strip (penting buat lo):**

Sekarang ada **3 cara setup logo perusahaan**. Pilih yang paling cocok:

---

#### 🚀 CARA 1: logo.dev (Paling Cepat, Recommended buat MVP)

logo.dev = pengganti resmi Clearbit Logo API. Gratis untuk traffic normal, butuh API token (sign up 2 menit).

**Setup:**

1. Buka https://www.logo.dev → Sign Up (pakai Google/email)
2. Dashboard → copy **publishable token** lo (formatnya: `pk_xxxxxxxxxxxxx`)
3. Buka `index.html`, tekan **Ctrl+F** → cari `pk_YOUR_TOKEN_HERE`
4. **Replace All** dengan token lo (ada 12 kemunculan total: 6 logo × 2 untuk loop animation)
5. Save, commit ke GitHub, selesai

**Cara kerjanya:** Setiap `<img>` panggil logo.dev dengan nama domain perusahaan, dapat balasan logo PNG resmi. Kalo logo gak ada di database, otomatis fallback ke text (handled by `onerror` attribute, udah built-in).

**Limitasi:**
- Coverage logo.dev bagus untuk perusahaan global, tapi **untuk perusahaan Indonesia hit-or-miss**. ITM, PAMA, AlamTri kemungkinan tidak tersedia (fallback ke text otomatis)
- Free tier: 5.000 requests/bulan. Untuk traffic normal website B2B, ini cukup banget

---

#### 🏆 CARA 2: Self-Host Logo (Recommended Long-term, Paling Pro)

Download logo resmi tiap perusahaan, host di repo lo. Paling reliable, kualitas terbaik, gak gantung sama service pihak ketiga.

**Step-by-step:**

1. Buat folder `assets/logos/` di repo GitHub lo
2. Download logo dari sumber resmi tiap perusahaan (link di bawah)
3. Save dengan nama yang konsisten: `xlsmart.svg`, `sicepat.svg`, `itm.svg`, dll. **Prefer SVG** (vector, sharp di semua resolusi). Kalo cuma ada PNG, pastiin background transparent dan minimum 200px tinggi
4. Buka `index.html`, ganti tiap baris `<img src="https://img.logo.dev/...">` jadi `<img src="assets/logos/nama.svg">`
5. Hapus attribute `onerror="..."` (gak perlu lagi)

**Sumber download logo resmi:**

| Perusahaan | Cara Download |
|---|---|
| **XLSmart** | Cari di Google Image "XLSmart logo PNG transparent" atau request ke tim mereka lewat website xlsmart.co.id |
| **SiCepat Ekspres** | https://www.sicepat.com → biasanya ada di footer Press Kit, atau cari "SiCepat logo SVG" di Wikipedia |
| **Markplus Institute** | https://markplusinstitute.com → footer atau About page |
| **ITM (Indo Tambangraya Megah)** | https://www.itmg.co.id → Media Center / Press → Download Logo |
| **AlamTri (ex-Adaro)** | https://www.alamtri.com → biasanya ada media kit. Kalo gak ada, screenshot logo dari header website mereka, hapus background pakai remove.bg |
| **PAMA (Pamapersada)** | https://www.pamapersada.com → About atau Media Center |

**Tools yang bantu:**
- **remove.bg** (gratis) — hapus background putih dari PNG biar jadi transparent
- **SVGOMG** — optimize SVG biar size kecil
- **Wikipedia** — banyak logo perusahaan public available di sini, biasanya quality bagus

⚠️ **Catatan legal:** Pakai logo perusahaan di "Trusted By" / "Our Clients" itu **OK secara legal** selama:
- Mereka beneran pernah jadi klien lo (Dhany ✅)
- Logo gak dimodifikasi (pakai original)
- Konteksnya jelas (gak nyiratkan endorsement)

Standard practice di semua B2B service company.

---

#### ✏️ CARA 3: Text Gede (Fallback, Paling Simple)

Kalo males urus logo, biarkan aja text gede. Sekarang udah lumayan kelihatan jelas dengan font Plus Jakarta Sans bold 32px.

**Caranya:** Hapus `<img>` tag, ganti jadi `<span>NAMA PERUSAHAAN</span>` di dalam tiap `<div class="logo-item">`.

Visual result: kayak yang lo lihat kalo logo.dev gagal load (fallback otomatis).

---

#### 💡 Rekomendasi Praktis dari Gw

Strategi mixed yang gw saranin:

1. **Sekarang:** Sign up logo.dev, masukin token, deploy. Beberapa logo bakal muncul otomatis (yang ada di database mereka), sisanya fallback text. Website lo udah live dan kelihatan keren.

2. **Minggu depan-an:** Sempetin download logo asli yang **gak muncul di logo.dev** (kemungkinan ITM, PAMA, AlamTri). Replace 1-by-1. 30 menit kerjaan.

Hasil akhir: campuran logo.dev (untuk yang available) + self-host (untuk yang Indonesia-spesifik). Paling pragmatis.

### 6. Ganti Testimonial

Cari section `TESTIMONIALS`. Setiap card ada placeholder `[Nama Klien]` dan `[Perusahaan]`. Ganti sesuai data real.

Avatar circle sekarang pake huruf (A, B, C). Bisa diganti pake foto:

```html
<div class="testimonial-avatar">
  <img src="assets/images/klien-1.jpg" alt="Nama Klien" style="width:100%;height:100%;border-radius:50%;object-fit:cover;">
</div>
```

### 7. SEO & Open Graph

Untuk preview yang cakep saat di-share di LinkedIn/WhatsApp/Facebook:

1. Bikin gambar OG image ukuran **1200x630px** (recommended)
2. Upload ke `assets/og-image.jpg` atau Google Drive
3. Update di `<head>`:

```html
<meta property="og:image" content="https://insyntive.com/assets/og-image.jpg">
<meta name="twitter:image" content="https://insyntive.com/assets/og-image.jpg">
```

### 8. Favicon

Sekarang masih pake favicon SVG inline (huruf "I" cyan). Bikin custom favicon?

1. Bikin logo ukuran 512x512 PNG di Canva/Figma
2. Convert ke favicon set di https://realfavicongenerator.net
3. Upload hasil ke folder `assets/`
4. Replace `<link rel="icon">` di `<head>` dengan kode dari favicon generator

---

## 🎨 Brand Guidelines (Auto-applied)

Sudah di-set sesuai brand kit INSYNTIVE:

| Element | Value |
|---------|-------|
| Font | Plus Jakarta Sans (Google Fonts) |
| Primary | `#02A0C1` (Cyan) |
| Secondary | `#3581E1` (Blue) |
| Accent (CTA) | `#D6FD91` (Lime) |
| Mint | `#97D1C6` |
| Pale Blue | `#D7E8FB` |
| Light Gray | `#EDEDED` |
| Dark | `#1F1F1F` |

Brand element yang dipake:
- ✅ **Glassmorphism** — di hero card & header saat scroll
- ✅ **Circle/blurred blue** — sebagai ambient blob di beberapa section
- ✅ **Plus Jakarta Sans** — semua typography

---

## 🧰 Fitur yang Sudah Built-in

- [x] Sticky header dengan glassmorphism saat scroll
- [x] Hero asymmetric dengan stats card
- [x] Marquee auto-scroll untuk industri
- [x] Counter animation untuk angka stats
- [x] Hover effect 3D di card services
- [x] Auto-scroll logo grid "Trusted By"
- [x] Floating WhatsApp button dengan pulse animation
- [x] Form contact dengan validation & status feedback
- [x] Scroll fade-in animation untuk semua section
- [x] Smooth scroll untuk anchor links
- [x] SEO meta tags (Open Graph + Twitter Card)
- [x] Mobile responsive (breakpoints di 900px & 600px)
- [x] Reduced motion support (accessibility)
- [x] Favicon SVG inline

---

## 🐛 Troubleshooting

**Form tidak terkirim setelah deploy?**
- Pastikan udah replace `YOUR_FORM_ID` dengan ID Formspree real
- Pastikan udah verify email Formspree dengan submit test 1x
- Cek browser console (F12) ada error gak

**Custom domain tidak bisa connect?**
- Tunggu DNS propagasi (max 24 jam)
- Cek dengan https://dnschecker.org apakah A record udah propagate
- Pastikan tidak ada conflict dengan record DNS lama

**Animation tidak jalan di mobile?**
- Beberapa user enable "reduce motion" di OS, ini intentional
- Cek di device lain untuk verify

**Gambar dari Google Drive broken?**
- GDrive sering ganti URL format. Pakai opsi B (commit ke repo)

---

## 📞 Kontak

Built for INSYNTIVE oleh Dhany Indraswara.

- WhatsApp: +62 818-0575-9025
- Email: halomas@dhanyindraswara.com / dhanyindraswara@gmail.com
- Instagram: @dhanyindraswara

---

## 📝 Changelog

- **v1.0** — Initial release. Single-page website dengan 13 section, form Formspree-ready, GitHub Pages compatible.
