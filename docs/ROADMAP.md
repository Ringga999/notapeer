# 🗺️ NotaPeer Roadmap — Dari Warung ke Notaris Global

> *"Setiap warung memiliki cerita. Setiap cerita layak dipercaya."*

Dokumen ini adalah peta hidup NotaPeer. Ia menjelaskan **apa** yang kami bangun, **mengapa** dalam urutan ini, dan **bagaimana** setiap fitur memperkuat identitas berdaulat di ekosistem ZCP2O.

Peta ini hidup — ia akan tumbuh bersama kami, ditinjau ulang setiap kuartal, dan dipertahankan secara publik agar siapa pun (merchant, investor, grant committee, kontributor) dapat mengikuti perjalanan kami.

---

## 📜 Enam Hukum NotaPeer

Setiap fitur, di gelombang mana pun, tunduk pada enam prinsip yang tidak bisa ditawar:

### Hukum 1 — Witness Wajib, Login Opsional
Identitas berdaulat (`zid`) melalui **Witness Gate** adalah satu-satunya pintu masuk wajib. Login Google/Supabase hanya membuka sinkronisasi & cadangan — **bukan syarat pakai**. Warung tanpa akun Google tetap berhak penuh atas NotaPeer.

### Hukum 2 — Offline-First, Online-Nanti
Setiap fitur harus bekerja tanpa internet. Integrasi blockchain, sync cloud, AI cerdas adalah **lapisan tambahan**, bukan fondasi. Merchant di pelosok dengan sinyal lemah sama berhaknya dengan merchant di pusat kota.

### Hukum 3 — Privasi Lebih Dulu dari Fitur
Data warung tidak pernah keluar dari perangkat tanpa persetujuan eksplisit. Setiap anchor on-chain hanya membawa **Merkle root** — bukan transaksi mentah. Auditabilitas tanpa pengintaian.

### Hukum 4 — Setiap Fitur Memperkuat ZCP2O
Tidak ada fitur yang berdiri sendiri. Kasir, absensi, donasi — semua menghasilkan **attestation proof-of-human** yang memperkuat jaringan identitas ZCP2O. Sebuah HR feature adalah sebuah identity feature.

### Hukum 5 — Dokumen Sebelum Kode
Tidak ada fitur dibangun sebelum spesifikasi + acceptance criteria tertulis. Repo ini dibangun di atas doktrin, bukan di atas terburu-buru. Kami menulis dulu, baru kami bangun.

### Hukum 6 — Satu Fitur, Satu Fokus
Tidak ada PR berisi 3 fitur sekaligus. Build fokus, review jelas, commit bersih. Kompleksitas adalah musuh kepercayaan.

---

## 🌊 Lima Gelombang Pengembangan

### 🌊 GELOMBANG 1 — Kerangka & Wajah
**Filosofi:** *Produk harus terlihat seperti produk, bukan demo.*

Fitur yang dibangun di gelombang ini menjadi rumah bagi semua gelombang berikutnya:

| Fitur | Tujuan | Doktrin yang Dipenuhi |
|---|---|---|
| **AppShell** | Sidebar/topbar + logo + chip zid + status jaringan | Hukum 2 (offline indicator) |
| **Dashboard Pro** | Kartu ringkasan upgrade + tabel transaksi rapi | Hukum 4 (data = kekuatan) |
| **Grafik Estetik** | Area chart arus kas 30 hari + donut kategori (recharts) | Hukum 4 (visualisasi data) |
| **Footer Sosmed** | Tautan X/GitHub/Email + logo kecil | Hukum 5 (transparansi) |

**Kriteria Selesai:** Screenshot aplikasi dapat masuk pitch deck tanpa perlu penjelasan "ini masih MVP".
**Status Gelombang 1: ✅ SELESAI (23 September 2026)** — kerangka, i18n, ikon, grafik, profil, dan footer sosial telah berdiri di `notapeer-app`.
---

### 🌊 GELOMBANG 2 — Operasional Warung
**Filosofi:** *Alasan merchant membuka aplikasi setiap hari.*

| Fitur | Tujuan | Doktrin yang Dipenuhi |
|---|---|---|
| **Menu Kasir** | Input penjualan sekali-tap (kategori & nominal cepat) | Hukum 2 (offline-first) |
| **Absensi Pekerja** | Check-in via HOLD Witness — proof-of-presence | Hukum 4 (setiap check-in = attestation baru) |


**Status: ✅ SELESAI (26 September 2026)** — Mode Kasir shift-based, shift log (F6), halaman Absensi (G2), dan kanonisasi kategori (F5) berdiri.

**Catatan Strategis:** Fitur absensi adalah kemenangan doktrin tersembunyi — ia mengubah "HR feature" menjadi "identity network feature". Investor akan menyukai bahwa fitur operasional ternyata memperkuat jaringan ZCP2O.

---

### 🌊 GELOMBANG IDENTITAS (2.5) — Sovereign Identity
**Filosofi:** *Buku tanpa pemilik adalah daun tanpa pohon.*

| Fitur | Tujuan | Doktrin |
|---|---|---|
| Root + faces | Identitas persisten, unlinkable antar-konteks | Hukum 3 |
| Register + captcha | Kemanusiaan sebagai pintu masuk | Hukum 1 |
| PIN + trust token | Login tanpa email/phone/KYC | Hukum 1 |
| Attestation queue | Offline-first menuju WitnessRegistry | Hukum 2 |
| WitnessRegistry.sol | Validator on-chain wajah pseudonim | Hukum 4 |

**Kriteria Selesai:** zid yang sama selamat dari reload, restart, dan ganti hari; badge ⏳/✅ jujur terhadap chain.

### 🌊 GELOMBANG 3 — Kepercayaan & Edukasi
**Filosofi:** *Mengubah pengguna menjadi percaya, dan percaya menjadi setia.*

| Fitur | Tujuan | Doktrin yang Dipenuhi |
|---|---|---|
| **Riwayat Anchor** | Baca LANGSUNG dari kontrak (on-chain, read-only) | Hukum 3 (no central database) |
| **Tutorial** | Wizard 4 langkah bahasa warung | Hukum 5 (doktrin diteruskan) |
| **FAQ** | Akordeon, diisi dari GLOSSARY.md | Hukum 5 (pengetahuan terbuka) |
| **Menu Donasi** | Address dompet donasi + doktrin 30% + QR | Hukum 3 (transparansi radikal) |

**Kriteria Selesai:** Seorang merchant baru dapat onboarding sendiri dalam <10 menit tanpa bantuan CS.

---

### 🌊 GELOMBANG 4 — Identitas & Fitur Unggulan
**Filosofi:** *Panggung utama ekosistem ZCP2O.*

| Fitur | Tujuan | Doktrin yang Dipenuhi |
|---|---|---|
| **Pengaturan** | Profil warung, ekspor CSV, zona bahaya (hapus data) | Hukum 3 (kontrol pengguna) |
| **Login Google** | OPSIONAL via Supabase — hanya sync antar-perangkat | Hukum 1 (Google bukan syarat) |
| **WALLET ZCP2O** | Panggung utama: zid, jejak attestation, saldo $ZPRO | Hukum 4 (fitur unggulan ekosistem) |

**Kriteria Selesai:** Seorang merchant dapat melihat, memiliki, dan mengontrol identitas berdaulatnya secara penuh.

**Catatan Strategis:** Wallet ZCP2O tampil terakhir bukan karena remeh — karena ia **mahkota**. Ia membutuhkan keputusan desain keamanan (kunci di mana? recovery bagaimana?) yang hanya matang setelah semua lapisan lain terbukti.

---

### 🌊 GELOMBANG 5 — Kecerdasan & Publikasi
**Filosofi:** *Dari produk yang bekerja, ke ekosistem yang berbicara.*

| Fitur | Tujuan | Doktrin yang Dipenuhi |
|---|---|---|
| **AI Helper** | Penasihat bahasa warung, offline-first, aturan lokal | Hukum 2 (tidak butuh sinyal) |
| **Hosting Publik** | Vercel (rumah asli Next.js) | Hukum 5 (transparansi) |
| **Demo Video** | 2 menit: HOLD → catat → anchor → explorer | Hukum 5 (cerita terbuka) |
| **Grant & Hackathon** | DoraHacks, ETHGlobal, Polygon Village | Hukum 4 (ekosistem tumbuh) |

**Kriteria Selesai:** NotaPeer dikenal di minimal 3 platform Web3 global.

---

## 🔗 Hubungan dengan ZCP2O Protocol

NotaPeer adalah **tonggak pertama** ekosistem ZCP2O. Setiap merchant yang onboarding = 1 node ZCP2O aktif. Setiap anchor bulanan = data nyata yang memperkuat Merkle tree ZCP2O. Setiap credit score yang dibaca lender = proof bahwa ZCP2O identity punya nilai ekonomi.

Semua milestone di roadmap ini akan selalu menyebut dua repo:
- [`notapeer`](https://github.com/Ringga999/notapeer) — doktrin, visi, janji publik
- [`zcp2o-protocol`](https://github.com/Ringga999/zcp2o-protocol) — infrastruktur protokol

Lihat [Section 9: Foundation Economics & Ethics](WHITEPAPER.md#9-foundation-economics--ethics) untuk detail komitmen ekosistem.

---

## 🏁 Kriteria Kesiapan

### Siap Pilot (10 warung pertama)
- ✅ Gelombang 1 selesai (kerangka + dashboard)
- ✅ Gelombang 2 selesai (kasir + absensi)
- ✅ Tutorial + FAQ tersedia
- ✅ Minimal 1 anchor genesis on-chain (✅ SUDAH TERCAPAI 23 Sep 2026)

### Siap Produksi (mainnet)
- ✅ Gelombang 1–3 selesai penuh
- ✅ Wallet ZCP2O minimal mode baca (Gelombang 4)
- ✅ Security audit internal selesai
- ✅ Dana operasional minimal 6 bulan (grant/revenue)

### Siap Skala (1000+ warung)
- ✅ Gelombang 1–5 selesai
- ✅ AI Helper aktif
- ✅ B2B API Licensing berjalan
- ✅ Mainnet ZCP2O live

---

## 📅 Revisi & Transparansi

Roadmap ini ditinjau ulang setiap **kuartal** (Januari, April, Juli, Oktober). Setiap perubahan akan didokumentasikan di file ini dengan timestamp, agar publik dapat melihat evolusi pemikiran kami.

**Versi saat ini:**
- Tanggal: 23 September 2026
- Status: Post-Genesis Anchor, pre-Gelombang 1
- Next review: 1 Oktober 2026

---

*Dibangun di muka publik. Solo founder. Rp 0 modal. Verifiable books for the world's unbanked businesses.*

[← Kembali ke README](../README.md) · [Whitepaper](WHITEPAPER.md) · [Glossary](GLOSSARY.md) · [Flowchart](FLOWCHART.md)