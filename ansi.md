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

![Struktur Organisasi E-Voting Kelurahan](assets/struktur_organisasi_evoting.svg)

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

![Alur Sistem Lama Manual](assets/alur_sistem_lama_manual.svg)

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

![Alur Sistem E-Voting](assets/alur_sistem_evoting.svg)

### Tahapan Proses E-Voting

| No  | Tahap                     | Proses                                                                           | Keterangan                                    |
| --- | ------------------------- | -------------------------------------------------------------------------------- | --------------------------------------------- |
| 1   | **Persiapan**             | Admin import data warga dari database kelurahan ke sistem → generate DPT digital | Dilakukan H-7 sebelum pemilihan               |
| 2   | **Registrasi kandidat**   | Panitia input data kandidat (nama, foto, visi-misi) ke sistem                    | Data ditampilkan di halaman voting            |
| 3   | **Verifikasi pemilih**    | Warga datang ke TPS → petugas scan/cek KTP → sistem validasi di DPT              | Warga yang sudah memilih otomatis ditandai    |
| 4   | **Pemberian suara**       | Pemilih akses halaman voting → pilih kandidat → konfirmasi → submit              | Token unik dicetak/ditampilkan sebagai bukti  |
| 5   | **Penghitungan otomatis** | Sistem hitung agregat suara secara real-time                                     | Hasil bisa dipantau live oleh panitia & saksi |
| 6   | **Pengumuman hasil**      | Setelah TPS tutup, hasil final ditampilkan di dashboard publik                   | Saksi memverifikasi, Lurah mengesahkan        |

### Diagram Alur Sederhana

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
           │ Buka halaman │   │ Ditolak,     │
           │ voting di    │   │ data tidak   │
           │ tablet       │   │ terdaftar    │
           └──────┬───────┘   └──────────────┘
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

## 6. Ringkasan Analisis

Sistem e-voting tingkat kelurahan yang ideal harus memenuhi tiga lapisan desain:

**Lapisan Identitas** — Verifikasi pemilih menggunakan NIK/KTP yang dicocokkan dengan DPT digital kelurahan. Sistem memastikan setiap warga hanya bisa memilih satu kali melalui penandaan status di database.

**Lapisan Suara** — Pilihan pemilih disimpan terpisah dari identitasnya di database. Setiap suara mendapat token unik yang bisa digunakan pemilih untuk mengonfirmasi bahwa suaranya tercatat, tanpa mengungkap isi pilihannya kepada orang lain.

**Lapisan Audit** — Seluruh aktivitas tercatat dalam log sistem (waktu voting, jumlah pemilih, status DPT). Saksi kandidat dan panitia dapat memantau dashboard hasil secara real-time. Setelah pemilihan, rekap digital dapat dicetak sebagai dokumen resmi.

### Kebutuhan Sistem

| Komponen          | Spesifikasi Minimum                                                |
| ----------------- | ------------------------------------------------------------------ |
| **Server**        | 1 unit laptop/PC sebagai server lokal atau cloud hosting sederhana |
| **Perangkat TPS** | 2–3 tablet/laptop dengan browser modern                            |
| **Jaringan**      | WiFi lokal (LAN) atau koneksi internet                             |
| **Software**      | Aplikasi web (PHP/Node.js + MySQL/PostgreSQL)                      |
| **Backup**        | Backup database otomatis setiap 30 menit selama pemilihan          |
