# Analisis & Rancangan Sistem Informasi E-Voting Tingkat Kelurahan

---

## 1. Definisi Sistem

**E-Voting Kelurahan** adalah sistem pemungutan suara elektronik berskala kelurahan/desa yang digunakan untuk pemilihan internal seperti **Ketua RT, Ketua RW, atau musyawarah kelurahan lainnya**. Sistem ini menggantikan proses coblos manual dengan aplikasi berbasis web yang dapat diakses melalui perangkat di TPS kelurahan.

### Ruang Lingkup

| Aspek               | Cakupan                                                     |
| ------------------- | ----------------------------------------------------------- |
| **Skala**           | 1 kelurahan (200–2.000 pemilih)                             |
| **Jenis Pemilihan** | Ketua RT, Ketua RW, Kepala Lingkungan, musyawarah kelurahan |
| **Infrastruktur**   | Server lokal / cloud sederhana, jaringan LAN/WiFi kelurahan |
| **Pengguna**        | Warga terdaftar di kelurahan bersangkutan                   |
| **Platform**        | Aplikasi web responsif, diakses via tablet/laptop di TPS    |

### Prinsip Dasar

| Prinsip          | Penerapan di Tingkat Kelurahan                                   |
| ---------------- | ---------------------------------------------------------------- |
| **Keabsahan**    | Hanya warga terdaftar (sesuai data kelurahan) yang bisa memilih  |
| **Satu Suara**   | Sistem mencegah pemilih memberikan suara lebih dari satu kali    |
| **Kerahasiaan**  | Pilihan tidak dapat dikaitkan ke identitas pemilih               |
| **Transparansi** | Hasil dapat diverifikasi oleh saksi dan panitia secara real-time |

---

## 2. Struktur Organisasi

```
                    ┌─────────────────┐
                    │  Lurah / Kades  │  ← Penanggung jawab utama
                    └────────┬────────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
     ┌────────────┐  ┌─────────────┐  ┌──────────┐
     │  Panitia   │  │  Operator   │  │  Saksi   │
     │  Pemilihan │  │  Sistem     │  │  (per    │
     │  Kelurahan │  │  (Admin IT) │  │  kandidat)│
     └─────┬──────┘  └─────────────┘  └──────────┘
           │
           ▼
  ┌──────────────────┐
  │  Petugas TPS     │  ← Verifikasi identitas warga
  │  (per RT/RW)     │
  └────────┬─────────┘
           │
           ▼
  ┌──────────────────┐
  │  Pemilih         │  ← Warga kelurahan terdaftar
  │  (Warga)         │
  └──────────────────┘
```

### Peran & Tanggung Jawab

| Peran                          | Tanggung Jawab                                                                 |
| ------------------------------ | ------------------------------------------------------------------------------ |
| **Lurah / Kepala Desa**        | Penanggung jawab kegiatan, mengesahkan hasil pemilihan                         |
| **Panitia Pemilihan**          | Menyusun DPT, menetapkan jadwal, mengkoordinasi TPS, mengumumkan hasil         |
| **Operator Sistem (Admin IT)** | Setup perangkat & jaringan, mengelola akun pemilih, troubleshoot teknis        |
| **Saksi Kandidat**             | Mengawasi jalannya pemilihan, memverifikasi hasil akhir                        |
| **Petugas TPS**                | Memverifikasi identitas pemilih (KTP/KK), memberikan akses ke perangkat voting |
| **Pemilih**                    | Warga terdaftar dalam DPT kelurahan, memberikan suara via perangkat            |

---

## 3. Alur Bisnis: Sistem Lama (Manual)

### Tahapan Proses Manual di Kelurahan

| No  | Tahap                     | Proses                                                          | Kelemahan                                                |
| --- | ------------------------- | --------------------------------------------------------------- | -------------------------------------------------------- |
| 1   | Pendataan pemilih         | RT/RW mengumpulkan data warga secara manual dari pintu ke pintu | Data tidak akurat, warga pindah tidak terdata, duplikasi |
| 2   | Pembuatan surat suara     | Panitia mencetak kertas suara sesuai jumlah DPT                 | Biaya cetak, risiko kelebihan/kekurangan surat           |
| 3   | Pelaksanaan di TPS        | Warga datang → cek KTP → terima surat → coblos di bilik         | Antrian panjang, proses lambat, warga malas datang       |
| 4   | Penghitungan suara        | Panitia buka kotak suara → hitung manual satu per satu          | Salah hitung, surat tidak sah diperdebatkan              |
| 5   | Rekapitulasi & pengumuman | Ditulis di papan, diumumkan lisan                               | Tidak ada rekam jejak digital, sulit diaudit ulang       |

### Masalah Utama Sistem Manual

- **Partisipasi rendah** — Warga malas antri, terutama usia muda
- **Waktu lama** — Proses 1 hari penuh untuk 1 RT/RW
- **Biaya operasional** — Cetak surat, konsumsi panitia, sewa tempat
- **Tidak ada audit trail** — Jika ada sengketa, harus hitung ulang fisik
- **Rentan kecurangan** — Surat suara bisa ditambah/dikurangi saat penghitungan

---

## 4. Pain Points & Justifikasi Adopsi E-Voting

### Perbandingan Sistem Lama vs E-Voting Kelurahan

| Aspek                   | 🔴 Sistem Lama (Manual)                          | ✅ E-Voting Kelurahan                                      |
| ----------------------- | ------------------------------------------------ | ---------------------------------------------------------- |
| **Pendataan**           | Kumpul data manual door-to-door, rawan duplikasi | Import dari data kependudukan kelurahan, validasi otomatis |
| **Pelaksanaan**         | Antri lama, coblos kertas, bilik fisik           | Akses tablet di TPS, voting digital 1–2 menit              |
| **Penghitungan**        | Hitung manual berjam-jam, rawan salah            | Otomatis real-time, hasil langsung tampil                  |
| **Rekam Jejak**         | Tidak ada — hanya catatan kertas                 | Log digital lengkap, bisa diaudit kapan saja               |
| **Biaya per Pemilihan** | Rp 2–5 juta (cetak, konsumsi, logistik)          | Rp 500rb–1 juta (listrik, internet) setelah setup awal     |
| **Partisipasi**         | Rendah (40–60%) karena antri & ribet             | Lebih tinggi karena proses cepat & modern                  |

### Asumsi Dasar Sebelum Adopsi

| Aspek                | Asumsi yang Harus Terpenuhi                                            |
| -------------------- | ---------------------------------------------------------------------- |
| **Infrastruktur**    | Kantor kelurahan memiliki akses listrik stabil & internet/WiFi minimal |
| **Perangkat**        | Tersedia minimal 2–3 tablet/laptop untuk TPS                           |
| **SDM**              | Ada 1 orang yang bisa mengoperasikan sistem (dilatih singkat)          |
| **Regulasi**         | Lurah/Kades menyetujui penggunaan e-voting untuk pemilihan internal    |
| **Penerimaan Warga** | Sosialisasi dilakukan agar warga percaya pada sistem digital           |

---

## 5. Alur Bisnis Sistem E-Voting Kelurahan (Usulan)

### Tahapan Proses E-Voting

| No  | Tahap                     | Proses                                                                           | Keterangan                                    |
| --- | ------------------------- | -------------------------------------------------------------------------------- | --------------------------------------------- |
| 1   | **Persiapan**             | Admin import data warga dari database kelurahan ke sistem → generate DPT digital | Dilakukan H-7 sebelum pemilihan               |
| 2   | **Registrasi kandidat**   | Panitia input data kandidat (nama, foto, visi-misi) ke sistem                    | Data ditampilkan di halaman voting            |
| 3   | **Verifikasi pemilih**    | Warga datang ke TPS → petugas scan/cek KTP → sistem validasi di DPT              | Warga yang sudah memilih otomatis ditandai    |
| 4   | **Pemberian suara**       | Pemilih akses halaman voting → pilih kandidat → konfirmasi → submit              | Token unik dicetak/ditampilkan sebagai bukti  |
| 5   | **Penghitungan otomatis** | Sistem hitung agregat suara secara real-time                                     | Hasil bisa dipantau live oleh panitia & saksi |
| 6   | **Pengumuman hasil**      | Setelah TPS tutup, hasil final ditampilkan di dashboard publik                   | Saksi memverifikasi, Lurah mengesahkan        |

### Diagram Alur

```
Warga datang ke TPS
       │
       ▼
┌──────────────┐     ┌─────────────────┐
│ Petugas cek  │────▶│ Sistem validasi │
│ KTP warga    │     │ di DPT digital  │
└──────────────┘     └───────┬─────────┘
                             │
                    ┌────────┴────────┐
                    │                 │
                 VALID            TIDAK VALID
                    │                 │
                    ▼                 ▼
           ┌──────────────┐   ┌──────────────┐
           │ Generate OTP │   │ Ditolak,     │
           │ + cetak slip │   │ data tidak   │
           │ ke pemilih   │   │ terdaftar    │
           └──────┬───────┘   └──────────────┘
                  │
                  ▼
           ┌──────────────┐
           │ Pemilih input│
           │ OTP di tablet│
           │ (autentikasi)│
           └──────┬───────┘
                  │
                  ▼
           ┌──────────────┐
           │ Pilih        │
           │ kandidat     │
           │ + konfirmasi │
           └──────┬───────┘
                  │
                  ▼
           ┌──────────────┐
           │ Suara masuk  │
           │ database     │
           │ + token bukti│
           └──────┬───────┘
                  │
                  ▼
           ┌──────────────┐
           │ Dashboard    │
           │ hasil        │
           │ real-time    │
           └──────────────┘
```

---

## 6. Rancangan Skema Database

Prinsip utama: **identitas pemilih dan isi suara tidak boleh bisa di-JOIN secara langsung**. Keduanya dihubungkan hanya melalui token anonim satu arah.

### Entitas & Relasi

```
┌─────────────────────────┐        ┌──────────────────────────┐
│ pemilih                 │        │ kandidat                 │
│─────────────────────────│        │──────────────────────────│
│ PK  id_pemilih (UUID)   │        │ PK  id_kandidat (UUID)   │
│     nik (VARCHAR, hash) │        │     nama (VARCHAR)       │
│     nama (VARCHAR)      │        │     foto_url (TEXT)      │
│     rt (VARCHAR)        │        │     visi_misi (TEXT)     │
│     rw (VARCHAR)        │        │     id_pemilihan (FK)    │
│     status_voting (BOOL)│        └──────────────────────────┘
│     id_pemilihan (FK)   │
│     created_at          │
└─────────┬───────────────┘
          │ saat verifikasi, generate token
          │ lalu putus relasi langsung
          ▼
┌─────────────────────────┐        ┌──────────────────────────┐
│ sesi_voting             │        │ suara                    │
│─────────────────────────│        │──────────────────────────│
│ PK  id_sesi (UUID)      │        │ PK  id_suara (UUID)      │
│     token_otp (VARCHAR) │        │     id_sesi (FK) ──────▶ │ id_sesi
│     id_pemilih (FK)     │        │     id_kandidat (FK)     │
│     expires_at          │        │     waktu_submit         │
│     used (BOOL)         │        │     token_bukti (VARCHAR)│
└─────────────────────────┘        └──────────────────────────┘

┌─────────────────────────┐        ┌──────────────────────────┐
│ pemilihan               │        │ audit_log                │
│─────────────────────────│        │──────────────────────────│
│ PK  id_pemilihan (UUID) │        │ PK  id_log (UUID)        │
│     nama_pemilihan      │        │     waktu (TIMESTAMP)    │
│     tanggal_mulai       │        │     aksi (VARCHAR)       │
│     tanggal_selesai     │        │     pelaku (VARCHAR)     │
│     status (ENUM)       │        │     detail (TEXT)        │
│     dibuat_oleh (FK)    │        │     ip_address           │
└─────────────────────────┘        └──────────────────────────┘
```

### Penjelasan Desain Privasi Database

| Keputusan Desain | Alasan |
|---|---|
| NIK disimpan dalam bentuk hash (bcrypt/SHA-256) | NIK asli tidak tersimpan di database — hanya hash untuk verifikasi |
| Tabel `suara` tidak menyimpan `id_pemilih` langsung | Suara hanya terhubung ke `id_sesi`, bukan ke identitas warga |
| `sesi_voting` dihapus/di-nullify setelah suara masuk | Memutus jalur JOIN antara pemilih ↔ suara setelah voting selesai |
| `token_bukti` di tabel `suara` bersifat satu arah | Pemilih bisa verifikasi suaranya tercatat, tanpa mengungkap pilihannya |

### Aturan Integritas Data

```sql
-- Pastikan satu pemilih hanya bisa submit satu suara per pemilihan
CREATE UNIQUE INDEX idx_satu_suara 
  ON sesi_voting(id_pemilih, id_pemilihan) WHERE used = TRUE;

-- Sesi voting kadaluarsa otomatis setelah 10 menit
-- (dikelola di application layer, bukan DB constraint)

-- Audit log tidak boleh di-UPDATE atau di-DELETE
-- (enforced via application role — akun DB audit hanya INSERT)
```

---

## 7. Rancangan Keamanan Sistem

### 7.1 Arsitektur Keamanan Berlapis

```
┌─────────────────────────────────────────────────────────┐
│  Lapisan 1 — Jaringan                                   │
│  HTTPS wajib (TLS 1.2+), sertifikat self-signed untuk   │
│  LAN atau Let's Encrypt untuk cloud                     │
└───────────────────────────┬─────────────────────────────┘
                            │
┌───────────────────────────▼─────────────────────────────┐
│  Lapisan 2 — Autentikasi                                │
│  OTP 6 digit, berlaku 10 menit, single-use              │
│  Role-based access: Admin / Petugas / Saksi / Publik    │
└───────────────────────────┬─────────────────────────────┘
                            │
┌───────────────────────────▼─────────────────────────────┐
│  Lapisan 3 — Aplikasi                                   │
│  Input validation & sanitasi (cegah SQL injection, XSS) │
│  CSRF token pada setiap form submission                 │
│  Rate limiting: maks. 5 request/menit per IP            │
└───────────────────────────┬─────────────────────────────┘
                            │
┌───────────────────────────▼─────────────────────────────┐
│  Lapisan 4 — Database                                   │
│  NIK di-hash sebelum disimpan                           │
│  Enkripsi kolom sensitif (AES-256)                      │
│  Akun DB terpisah per role (read-only, write, audit)    │
└─────────────────────────────────────────────────────────┘
```

### 7.2 Mekanisme Autentikasi Pemilih (OTP)

Menggantikan alur "petugas buka tablet langsung", autentikasi dua langkah ini memastikan hanya pemilih yang bersangkutan yang bisa submit suara:

```
Petugas TPS                  Sistem                    Pemilih
     │                          │                          │
     │── input NIK pemilih ────▶│                          │
     │                          │── validasi di DPT        │
     │                          │── generate OTP 6 digit   │
     │◀─ tampil OTP di layar ───│                          │
     │                          │                          │
     │── cetak/tunjuk OTP ─────────────────────────────▶  │
     │   ke pemilih             │                          │
     │                          │                          │
     │   (petugas mundur,       │◀── input OTP di tablet ──│
     │    tidak melihat layar)  │                          │
     │                          │── OTP valid? ────────────│
     │                          │── buka halaman voting ──▶│
     │                          │                          │
     │                          │◀── pilih & submit ───────│
     │                          │── suara tersimpan        │
     │                          │── OTP di-invalidate      │
```

### 7.3 Pembatasan Akses Admin (Role-Based Access Control)

| Role | Hak Akses | Tidak Bisa Mengakses |
|---|---|---|
| **Super Admin (Lurah)** | Buka/tutup pemilihan, export hasil resmi | Data suara individual, log OTP |
| **Admin IT** | Import DPT, kelola kandidat, pantau status sistem | Isi suara, token OTP pemilih |
| **Petugas TPS** | Generate OTP untuk pemilih yang terverifikasi | Dashboard hasil, data pemilih lain |
| **Saksi** | Pantau dashboard hasil real-time (read-only) | Data pemilih, log sistem |
| **Publik** | Verifikasi token bukti suara (hanya status: tercatat/tidak) | Semua data lain |

### 7.4 Checklist Keamanan Sebelum Pemilihan

- [ ] Sertifikat HTTPS aktif dan valid
- [ ] Backup database terakhir berhasil diverifikasi
- [ ] Semua akun admin sudah ganti password default
- [ ] Uji coba SQL injection pada form input (OWASP Top 10 dasar)
- [ ] Pastikan OTP expired setelah 10 menit (uji manual)
- [ ] Akun petugas TPS tidak bisa akses halaman hasil
- [ ] Log audit aktif dan mencatat semua aksi admin

---

## 8. Rancangan Kontingensi & Disaster Recovery

### 8.1 Skenario Risiko & Penanganan

| Skenario | Probabilitas | Dampak | Penanganan |
|---|---|---|---|
| WiFi/internet mati | Tinggi | Tinggi | Gunakan hotspot HP panitia sebagai backup; server lokal tetap jalan |
| Server crash / restart | Sedang | Tinggi | Data aman di DB; sistem otomatis reconnect; backup terakhir dimuat |
| Perangkat TPS rusak | Sedang | Sedang | Siapkan 1 perangkat cadangan; OTP bisa diinput dari perangkat lain |
| Pemilih lupa/tidak bisa baca OTP | Tinggi | Rendah | Petugas generate ulang OTP (invalidate yang lama otomatis) |
| Manipulasi data oleh orang dalam | Rendah | Sangat Tinggi | Audit log immutable + saksi bisa akses dashboard mandiri |
| Listrik padam | Sedang | Tinggi | UPS untuk server minimal 2 jam; jika padam total → prosedur penghentian darurat |

### 8.2 Prosedur Backup

```
Jadwal Backup Otomatis:
├── Setiap 30 menit selama pemilihan berlangsung
│     → Backup ke folder lokal + salinan ke USB/cloud
├── Setelah TPS tutup
│     → Full backup + export CSV hasil sebagai arsip offline
└── Sebelum pemilihan dibuka
      → Snapshot database awal (baseline untuk audit)

Lokasi Backup:
├── Primer  : Folder /backup di server lokal
├── Sekunder: USB flashdisk yang disegel oleh panitia & saksi
└── Tersier : Cloud storage (Google Drive kelurahan) jika tersedia
```

### 8.3 Prosedur Penghentian Darurat

Jika sistem tidak bisa dipulihkan dalam 30 menit:

1. Panitia umumkan penghentian sementara kepada warga
2. Admin export data suara yang sudah masuk (CSV) — ditandatangani saksi
3. Evaluasi bersama: lanjut setelah perbaikan, atau fallback ke manual
4. Jika fallback ke manual: suara digital yang sudah masuk **tetap sah** dan dihitung bersama hasil manual
5. Buat berita acara insiden yang ditandatangani semua pihak

---

## 9. Rancangan Antarmuka & Aksesibilitas

### 9.1 Prinsip Desain Antarmuka

Mengingat segmen pengguna utama adalah **warga 40–70 tahun** yang mungkin tidak terbiasa dengan teknologi:

| Prinsip | Implementasi |
|---|---|
| **Tampilan minimal** | Maksimal 1 aksi per layar — tidak ada menu atau tombol yang tidak relevan |
| **Font besar** | Ukuran teks minimal 18px, tombol aksi minimal 48px tinggi |
| **Kontras tinggi** | Rasio kontras warna ≥ 4.5:1 (standar WCAG AA) |
| **Instruksi verbal** | Setiap langkah disertai teks instruksi singkat dalam bahasa sehari-hari |
| **Konfirmasi sebelum submit** | Tampilkan ringkasan pilihan dan minta konfirmasi eksplisit sebelum suara dikirim |
| **Tidak ada timeout singkat** | Sesi voting tidak kedaluwarsa selama pemilih masih aktif di halaman |

### 9.2 Alur Layar (Screen Flow)

```
[Layar 1]              [Layar 2]              [Layar 3]
┌────────────┐         ┌────────────┐         ┌────────────┐
│ Masukkan   │  ──▶    │ Pilih satu │  ──▶    │ Konfirmasi │
│ Kode OTP   │         │ kandidat   │         │ pilihan    │
│            │         │            │         │ Anda:      │
│ [_ _ _ _ _ _]│        │ ○ Budi S.  │         │ BUDI S.    │
│            │         │ ○ Siti R.  │         │            │
│ [LANJUT]   │         │ ○ Ahmad W. │         │ [UBAH]     │
└────────────┘         │            │         │ [KIRIM ✓]  │
                       │ [LANJUT]   │         └────────────┘
                       └────────────┘
                                                     │
                                                     ▼
                                             [Layar 4]
                                             ┌────────────┐
                                             │ Suara Anda │
                                             │ BERHASIL   │
                                             │ tercatat ✓ │
                                             │            │
                                             │ Kode bukti:│
                                             │ #A7X-2931  │
                                             └────────────┘
```

### 9.3 Panduan untuk Petugas TPS

- Petugas **wajib** membalikkan badan atau mengalihkan pandangan saat pemilih menginput OTP dan memilih kandidat
- Jika pemilih meminta bantuan (lansia, disabilitas), satu petugas **dan** satu saksi mendampingi bersama — tidak boleh hanya petugas sendiri
- Setelah suara terkirim, minta pemilih mencatat atau difotokan kode bukti

---

## 10. Ringkasan Analisis Sistem

Sistem e-voting tingkat kelurahan yang ideal harus memenuhi tiga lapisan desain:

**Lapisan Identitas** — Verifikasi pemilih menggunakan NIK/KTP yang dicocokkan dengan DPT digital kelurahan. NIK tidak disimpan langsung melainkan dalam bentuk hash. Sistem memastikan setiap warga hanya bisa memilih satu kali melalui penandaan status di database, dan OTP single-use memastikan hanya pemilih yang bersangkutan yang bisa submit suara.

**Lapisan Suara** — Pilihan pemilih disimpan terpisah dari identitasnya di database. Relasi antara sesi voting dan identitas pemilih diputus setelah suara masuk. Setiap suara mendapat token bukti yang bisa digunakan pemilih untuk mengonfirmasi bahwa suaranya tercatat, tanpa mengungkap isi pilihannya kepada orang lain.

**Lapisan Audit** — Seluruh aktivitas tercatat dalam log sistem yang bersifat append-only (tidak bisa diedit). Saksi kandidat dan panitia dapat memantau dashboard hasil secara real-time dengan akses read-only yang terisolasi. Setelah pemilihan, rekap digital dapat dicetak sebagai dokumen resmi yang ditandatangani semua pihak.

### Kebutuhan Sistem

| Komponen          | Spesifikasi Minimum                                                |
| ----------------- | ------------------------------------------------------------------ |
| **Server**        | 1 unit laptop/PC sebagai server lokal atau cloud hosting sederhana |
| **Perangkat TPS** | 2–3 tablet/laptop dengan browser modern + 1 cadangan              |
| **Jaringan**      | WiFi lokal (LAN) atau koneksi internet + hotspot cadangan          |
| **Software**      | Aplikasi web (PHP/Node.js + MySQL/PostgreSQL)                      |
| **Backup**        | Backup database otomatis setiap 30 menit + USB tersegel + cloud   |
| **UPS**           | Minimal 2 jam untuk server agar tahan mati listrik                |

---

## 11. Rencana Pengujian (Testing Plan)

### 11.1 Jenis Pengujian

| Jenis Uji | Tujuan | Waktu Pelaksanaan |
|---|---|---|
| **Unit Testing** | Validasi fungsi kunci: hash NIK, generate OTP, hitung suara | Saat development |
| **Integration Testing** | Alur lengkap dari verifikasi KTP → submit suara → tampil di hasil | Saat development |
| **User Acceptance Testing (UAT)** | Panitia & petugas TPS mencoba sistem sesuai skenario nyata | H-3 sebelum pemilihan |
| **Simulasi Pemilihan** | Dry run penuh dengan data dummy, libatkan beberapa warga sukarela | H-1 sebelum pemilihan |
| **Penetration Test Dasar** | Coba akses halaman tanpa OTP, coba submit dua kali, coba SQL injection sederhana | H-3 sebelum pemilihan |

### 11.2 Skenario Uji Kritis

```
Skenario 1: Cegah Double Voting
  → Pemilih A selesai voting
  → Coba verifikasi NIK yang sama kembali
  → Ekspektasi: sistem menolak dengan pesan "sudah memilih"

Skenario 2: OTP Kadaluarsa
  → Generate OTP untuk pemilih B
  → Tunggu 11 menit tanpa digunakan
  → Coba input OTP tersebut
  → Ekspektasi: sistem menolak dengan pesan "kode tidak valid"

Skenario 3: Isolasi Peran
  → Login sebagai petugas TPS
  → Coba akses URL halaman hasil/dashboard admin
  → Ekspektasi: akses ditolak / redirect ke halaman tidak diizinkan

Skenario 4: Verifikasi Token Bukti
  → Pemilih C selesai voting, dapat token #B3K-5512
  → Masukkan token di halaman verifikasi publik
  → Ekspektasi: tampil status "Suara tercatat" tanpa info pilihan

Skenario 5: Simulasi Server Restart
  → Matikan dan nyalakan ulang server saat 50% pemilih sudah voting
  → Ekspektasi: semua data suara tetap ada, dashboard kembali normal
```

### 11.3 Kriteria Go/No-Go Sebelum Hari-H

Sistem **tidak boleh digunakan** jika salah satu kondisi berikut terjadi saat simulasi:

- [ ] Double voting berhasil dilakukan
- [ ] OTP bisa digunakan lebih dari satu kali
- [ ] Petugas TPS bisa mengakses halaman hasil
- [ ] Suara hilang setelah server restart
- [ ] Dashboard hasil tidak muncul setelah 5 detik

---

## 12. Jadwal Implementasi (Timeline)

| Fase | Kegiatan | Durasi Estimasi |
|---|---|---|
| **Fase 1 — Perancangan** | Finalisasi dokumen ANSI, desain database, wireframe UI | 2 minggu |
| **Fase 2 — Development** | Bangun aplikasi web, implementasi keamanan, unit testing | 4–6 minggu |
| **Fase 3 — Testing** | Integration test, UAT bersama panitia, penetration test | 2 minggu |
| **Fase 4 — Pelatihan** | Pelatihan petugas TPS, simulasi pemilihan, sosialisasi warga | 1 minggu |
| **Fase 5 — Pelaksanaan** | Hari pemilihan, monitoring real-time, backup berkala | 1 hari |
| **Fase 6 — Evaluasi** | Laporan hasil, evaluasi sistem, rekomendasi perbaikan | 3–5 hari |
