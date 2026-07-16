# 📝 Naskah Presentasi — E-Voting Kelurahan
### Kelompok 11 Barbarabar

---

## SLIDE 1 — Hero / Pembuka

> **Judul:** *Mendigitalisasi Demokrasi Kelurahan.*

**Naskah:**

Assalamualaikum warahmatullahi wabarakatuh. Selamat pagi/siang Bapak/Ibu dosen dan teman-teman sekalian.

Perkenalkan, kami dari **Kelompok 11 — Barbarabar**. Hari ini kami akan mempresentasikan proyek kami yang berjudul **"Sistem Informasi E-Voting Kelurahan"**.

Sistem ini dirancang untuk mendigitalisasi proses demokrasi di tingkat kelurahan — menggantikan proses pemilihan manual yang selama ini masih rentan dengan berbagai masalah, menjadi sebuah sistem yang **aman, transparan, dan aksesibel** dengan arsitektur keamanan berlapis serta akurasi matematis absolut.

Mari kita mulai eksplorasinya.

---

## SLIDE 2 — Definisi & Identitas Kelompok

> **Judul:** *Meredefinisi Pilkades.*

**Naskah:**

Jadi, apa sebenarnya E-Voting Kelurahan ini?

E-Voting Kelurahan adalah sistem yang **mentransformasi pemilihan konvensional menjadi sepenuhnya digital**. Sistem ini hadir untuk menjawab tiga masalah utama yang sering terjadi dalam pemilihan manual di tingkat kelurahan:

1. **Rekapitulasi yang lambat** — bisa memakan waktu berhari-hari.
2. **Inefisiensi logistik** — percetakan surat suara, distribusi, dan perlengkapan bilik.
3. **Rentannya manipulasi suara** — karena proses hitung manual yang terbuka peluang human error maupun kecurangan.

Sistem kami menjawab ini semua dengan DPT digital yang tervalidasi, proses paperless, hasil real-time, dan keamanan berlapis.

Dan untuk memperkenalkan tim kami — **Kelompok 11 Barbarabar** terdiri dari:

| Nama | NIM |
|------|-----|
| Yudistira Azfa Dani Wibowo | 24.12.3274 |
| Muhammad Adam Siswantoro | 24.12.3281 |
| Wasima Juhaina | 24.12.3282 |
| Sherly Meisya Maharani | 24.12.3301 |
| Evan Aubin Wibowo | 24.12.3319 |

---

## SLIDE 3 — Problem vs Solusi (Paradigma Baru)

> **Judul:** *Paradigma Baru.*

**Naskah:**

Sekarang, mari kita bicara angka supaya lebih konkret.

Dalam pemilihan manual konvensional, proses rekapitulasi suara bisa memakan waktu **hingga 5 hari**. Lima hari yang penuh risiko — mulai dari kesalahan hitung, kelelahan petugas, hingga potensi manipulasi data. Dengan E-Voting, proses ini berubah menjadi **hitungan detik secara real-time**. Begitu pemilih selesai mencoblos, suara langsung tercatat dan terakumulasi di sistem.

Selain itu, setiap periode pemilihan biasanya menghabiskan **lebih dari 1.200 lembar** kertas suara. Dengan E-Voting, logistik kertas ini sepenuhnya dieliminasi — **100% digital, 100% paperless**.

Dan yang tidak kalah penting, sistem kami menyediakan **dashboard real-time** yang di-update otomatis setiap 5 detik. Saksi-saksi dapat memantau secara langsung — live — bagaimana suara masuk dan terakumulasi. Transparansi total.

---

## SLIDE 4 — Workflow Sistem (3 Fase)

> **Judul:** *Workflow Sistem.*

**Naskah:**

Bagaimana alur kerja sistem ini? Kami membaginya ke dalam **tiga fase utama**:

### Fase 1: Persiapan (H-7 sampai H-1)
Sebelum hari pemilihan, panitia melakukan persiapan:
- **Import DPT Digital** — data pemilih tetap diimpor ke sistem dalam format CSV yang sudah tervalidasi.
- **Registrasi Kandidat** — visi misi setiap calon didaftarkan ke dalam sistem.
- **Setup Infrastruktur** — Mini PC server lokal disiapkan sebagai pusat data di TPS.

### Fase 2: Pelaksanaan (Hari H)
Pada hari pemilihan, alurnya adalah:
- **Verifikasi identitas** — pemilih datang dengan KTP, petugasverifikasi NIK-nya terhadap DPT.
- **Generate OTP** — sistem menghasilkan kode OTP 6 digit yang di-hash dengan Bcrypt sebagai kunci masuk pencoblosan.
- **Pencoblosan** — pemilih melakukan pemilihan di tablet, lalu mencetak token bukti.
- **Monitoring** — dashboard real-time menampilkan progress suara masuk secara langsung.

### Fase 3: Penutupan (Pasca Acara)
Setelah pemungutan selesai:
- **Lurah mengunci sesi** — tidak ada lagi suara yang bisa masuk.
- **Persetujuan digital saksi** — saksi-saksi menyetujui hasil rekapitulasi secara digital.
- **Cetak Berita Acara** — laporan resmi di-generate dalam format PDF.
- **Backup database** — data di-backup ke USB dan cloud untuk keamanan jangka panjang.

---

## SLIDE 5 — Analisis PIECES

> **Judul:** *Analisis PIECES.*

**Naskah:**

Untuk membuktikan kelayakan sistem ini, kami menggunakan **framework analisis PIECES** — yang mengevaluasi enam aspek utama:

1. **Performance** — Seluruh proses, dari verifikasi NIK, cetak OTP, hingga cetak token bukti, selesai dalam **kurang lebih 2 menit per pemilih**. Jauh lebih cepat dibanding antrian manual.

2. **Information** — Sistem menjamin **transparansi penuh**. Saksi bisa memantau rekapitulasi data secara live dengan polling setiap 5 detik. Tidak ada lagi "ruang gelap" dalam penghitungan.

3. **Economy** — Terjadi **penghematan masif** karena biaya logistik cetak surat suara dan perlengkapan bilik yang berulang setiap periode dihilangkan sepenuhnya.

4. **Control** — Keamanan dikelola dengan **RBAC 5 level** — Role-Based Access Control. Setiap aksi admin dicatat dalam audit log yang bersifat *append-only*, artinya catatan tidak bisa diubah atau dihapus.

5. **Efficiency** — Rekapitulasi yang tadinya memakan **waktu berhari-hari** kini dikerjakan oleh komputer secara instan. Akurasi komputasi menggantikan hitung manual.

6. **Service** — UI E-Voting didesain dengan **kontras tinggi** yang elderly-friendly, sehingga mudah digunakan bahkan oleh pemilih lansia.

---

## SLIDE 6 — Keamanan Berlapis

> **Judul:** *Empat Lapis Pertahanan.*

**Naskah:**

Keamanan adalah aspek paling krusial dalam sistem pemilihan. Sistem kami mengimplementasikan **empat lapis pertahanan**:

**Lapis 1 — Infrastruktur Terisolasi.**
Selama pemungutan suara berlangsung, sistem berjalan di **jaringan LAN tertutup**. Tidak ada koneksi ke internet. Ini artinya mustahil diserang dari luar — tidak ada DDoS, tidak ada remote hacking.

**Lapis 2 — Otentikasi Berlapis.**
Setiap pemilih melewati tiga tahap verifikasi:
- Pertama, pemeriksaan **KTP fisik** oleh petugas.
- Kedua, **validasi NIK** terhadap database DPT digital.
- Ketiga, **OTP 6 digit** yang di-hash menggunakan Bcrypt — hanya berlaku sekali pakai.

**Lapis 3 — Anonimitas Identitas.**
Ini yang membedakan sistem kami — setelah pemilih memilih, **relasi antara suara dan identitas pemilih diputus total**. Ditambah dengan jeda waktu acak saat penyimpanan data, sehingga tidak mungkin melacak siapa memilih siapa, bahkan melalui timing attack sekalipun.

Jadi keamanan kami bukan hanya di level software, tapi dimulai dari **arsitektur fisik jaringan** hingga **algoritma kriptografi**.

---

## SLIDE 7 — Struktur Database & DFD

> **Judul:** *Struktur Database.*

**Naskah:**

Dari sisi teknis, sistem E-Voting kami menggunakan **arsitektur 8 tabel utama** dalam database-nya:

`USERS`, `DPT_DIGITAL`, `KANDIDAT`, `OTP_TOKENS`, `SUARA_ANONIM`, `BERITA_ACARA`, `BACKUP_LOG`, dan `AUDIT_LOG`.

Yang paling penting untuk diperhatikan adalah tabel **`SUARA_ANONIM`**. Tabel ini **sengaja tidak memiliki Foreign Key** ke tabel identitas pemilih. Artinya, secara struktural di level database, tidak ada cara untuk menghubungkan suara dengan siapa yang memilih.

Selain itu, timestamp penyimpanan suara **dibulatkan ke menit** dan ditambahkan **delay acak antara 2 hingga 10 detik**. Ini secara efektif mematikan potensi **timing attack** — di mana seseorang mencoba mencocokan waktu pemilihan dengan waktu penyimpanan suara.

Untuk alur data, kami merancang **DFD Level 0 dengan 7 proses utama**:
1. Manajemen DPT
2. Manajemen Kandidat
3. Verifikasi & OTP
4. Pemungutan Suara
5. Rekapitulasi
6. Pengesahan Berita Acara
7. Backup & Audit

Semuanya terdokumentasi dan saling terhubung secara sistematis.

---

## SLIDE 8 — Kelayakan Finansial

> **Judul:** *Kelayakan Finansial.*

**Naskah:**

Salah satu pertanyaan kritis yang pasti muncul adalah: **apakah ini layak secara finansial?**

Memang, di awal ada biaya pengembangan atau CAPEX yang harus dikeluarkan — untuk perangkat keras, perangkat lunak, dan setup infrastruktur. Namun, di sisi lain, E-Voting **menihilkan biaya logistik** yang selama ini berulang di setiap periode pemilihan — cetak surat suara, distribusi, perlengkapan bilik, dan sebagainya.

Kami telah melakukan analisis kelayakan finansial dengan tiga metrik utama:

- **Payback Period: 1,83 tahun** — artinya investasi awal sudah kembali dalam waktu kurang dari 2 tahun.

- **NPV (Net Present Value): Rp 1,55 juta positif** — nilai ini lebih besar dari nol, yang berarti proyek ini **sangat layak** dari perspektif investasi.

- **ROI (Return on Investment): 18,5%** — keuntungan bersih yang dihasilkan cukup signifikan untuk skala kelurahan.

Ketiga indikator ini membuktikan bahwa E-Voting bukan hanya unggul secara teknis, tapi juga **masuk akal secara ekonomi**.

---

## SLIDE 9 — Arsitektur Teknologi (Tech Stack)

> **Judul:** *Tech Stack Modern.*

**Naskah:**

Untuk implementasi teknis, kami memilih tech stack yang sudah mature dan terbukti andal:

| Komponen | Teknologi |
|----------|-----------|
| **Framework Backend** | Laravel 10 dengan PHP 8.2 — framework yang robust, memiliki ekosistem keamanan yang kuat, dan komunitas besar. |
| **Database Inti** | MySQL 8.0 — relational database yang stabil untuk mengelola data pemilih, kandidat, dan transaksi suara. |
| **Frontend UI** | Bootstrap 5 + Vanilla JavaScript — ringan, responsif, dan cukup untuk kebutuhan interface di tablet kiosk. |
| **Web Server TPS** | Nginx yang di-deploy di Mini PC NUC — server lokal di setiap TPS yang beroperasi dalam jaringan tertutup. |
| **Terminal Klien** | Tablet Android dalam mode Kiosk — pemilih hanya bisa mengakses aplikasi E-Voting, tidak bisa membuka aplikasi lain. |

Arsitektur ini dipilih karena **keseimbangan antara performa, keamanan, dan kemudahan deployment** di lingkungan kelurahan yang mungkin memiliki keterbatasan infrastruktur IT.

---

## SLIDE 10 — Penutup / Call to Action

> **Judul:** *Siap Mengubah Demokrasi Anda?*

**Naskah:**

Demikianlah presentasi kami mengenai **Sistem Informasi E-Voting Kelurahan**.

Kami telah menunjukkan bahwa sistem ini:
- ✅ Mempercepat proses pemilihan dari berhari-hari menjadi real-time.
- ✅ Menghilangkan biaya logistik berulang.
- ✅ Mengamankan suara dengan empat lapis pertahanan.
- ✅ Menjamin anonimitas pemilih secara teknis.
- ✅ Layak secara finansial dengan payback period kurang dari 2 tahun.

Sistem ini siap untuk dieksekusi dan diimplementasikan sebagai solusi nyata bagi modernisasi demokrasi di tingkat kelurahan.

Terima kasih atas perhatiannya. Kami dari **Kelompok 11 — Barbarabar**, terbuka untuk pertanyaan dan diskusi.

Wassalamualaikum warahmatullahi wabarakatuh.

---

> *© 2026 Kelompok Barbarabar — Yudistira, M. Adam, Wasima, Sherly, Evan*
