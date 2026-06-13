# Data Flow Diagram (DFD)
## Sistem Informasi E-Voting Tingkat Kelurahan

---

## 1. Diagram Konteks (Context Diagram)

Diagram Konteks merupakan level tertinggi dalam hierarki DFD yang menggambarkan sistem informasi e-voting sebagai **satu proses tunggal** yang berinteraksi dengan seluruh entitas luar (*external entities*). Diagram ini menunjukkan batasan sistem (*system boundary*) serta aliran data utama yang masuk dan keluar dari sistem.

### Entitas Luar (*External Entities*)

| No | Entitas Luar | Peran dalam Sistem |
|:--:|--------------|--------------------|
| 1 | **Lurah / Kepala Desa** | Penanggung jawab tertinggi pemilihan; membuka/menutup sesi pemilihan dan mengesahkan hasil resmi |
| 2 | **Admin IT** | Operator teknis yang mengelola infrastruktur sistem, mengimpor data DPT, dan melakukan backup |
| 3 | **Panitia Pemilihan** | Penyelenggara yang mendaftarkan kandidat dan memantau progres partisipasi pemilih |
| 4 | **Petugas TPS** | Verifikator lapangan yang memvalidasi identitas pemilih dan menghasilkan OTP |
| 5 | **Pemilih (Warga)** | Warga terdaftar di DPT yang memberikan suara melalui sistem |
| 6 | **Saksi Kandidat** | Pengawas dari utusan kandidat yang memantau hasil pemilihan secara *read-only* |

### Visualisasi Diagram Konteks

```mermaid
flowchart TD
    %% Styling
    classDef entitas fill:#e0f2fe,stroke:#0284c7,stroke-width:2px,color:#0f172a,font-weight:bold;
    classDef sistem fill:#fef08a,stroke:#ca8a04,stroke-width:3px,color:#0f172a,font-weight:bold;

    %% Entitas Luar
    Lurah[Lurah / Kades]:::entitas
    Admin[Admin IT]:::entitas
    Panitia[Panitia Pemilihan]:::entitas
    Petugas[Petugas TPS]:::entitas
    Pemilih[Pemilih Warga]:::entitas
    Saksi[Saksi Kandidat]:::entitas

    %% Sistem Utama
    Sistem((Sistem E-Voting \nKelurahan)):::sistem

    %% Aliran Data
    Lurah -->|Buka/Tutup Sesi, Konfirmasi Pengesahan| Sistem
    Sistem -->|Hasil Final, Berita Acara| Lurah
    
    Admin -->|Data Warga, Data Kandidat, Perintah Backup| Sistem
    Sistem -->|Status Import, Log Audit, Status Backup| Admin

    Panitia -->|Registrasi Kandidat| Sistem
    Sistem -->|DPT, Statistik, Hasil Final| Panitia

    Petugas -->|NIK Pemilih| Sistem
    Sistem -->|Status NIK, OTP| Petugas

    Pemilih -->|OTP, Pilihan Kandidat| Sistem
    Sistem -->|Surat Suara, Token Bukti| Pemilih

    Sistem -->|Dashboard Real-time| Saksi
```

---

## 2. DFD Level 0

DFD Level 0 merupakan dekomposisi dari proses tunggal pada Diagram Konteks menjadi **tujuh proses utama** yang menggambarkan subsistem operasional di dalam Sistem Informasi E-Voting. Setiap proses dihubungkan oleh aliran data (*data flow*) dan berinteraksi dengan penyimpanan data (*data store*).

### Data Store (Tabel Database)

| ID | Data Store | Relasi ke ERD | Keterangan |
|:--:|------------|---------------|------------|
| D1 | DPT Digital | `DPT_DIGITAL` | Menyimpan data pemilih tetap (NIK, nama, status memilih) |
| D2 | Data Kandidat | `KANDIDAT` | Menyimpan profil pasangan calon (nomor urut, nama, foto) |
| D3 | Data Pengguna | `USERS` | Menyimpan akun seluruh aktor sistem dengan pembedaan role |
| D4 | Token OTP | `OTP_TOKENS` | Menyimpan hash OTP 6 digit beserta waktu kedaluwarsa |
| D5 | Suara Anonim | `SUARA_ANONIM` | Menyimpan hasil pilihan suara secara anonim |
| D6 | Berita Acara | `BERITA_ACARA` | Menyimpan dokumen hasil pemilihan yang telah disahkan |
| D7 | Backup Log | `BACKUP_LOG` | Menyimpan riwayat aktivitas pencadangan database |
| D8 | Audit Log | `AUDIT_LOG` | Menyimpan jejak seluruh aktivitas sensitif dalam sistem |

### Proses-Proses Utama

| ID | Nama Proses | Keterangan |
|:--:|-------------|------------|
| 1.0 | Manajemen DPT Digital | Pengimporan dan deduplikasi data pemilih dari CSV |
| 2.0 | Manajemen Kandidat | Pendaftaran dan pembaruan profil kandidat oleh Panitia |
| 3.0 | Verifikasi & Autentikasi | Validasi NIK dan pembuatan OTP hash |
| 4.0 | Pemungutan Suara | Autentikasi OTP, penyampaian e-ballot, dan pencatatan suara |
| 5.0 | Rekapitulasi & Hitung | Agregasi suara real-time untuk dashboard |
| 6.0 | Pengesahan & Laporan | Konfirmasi Lurah, penerbitan Berita Acara digital |
| 7.0 | Backup & Audit | Export log aktivitas dan pencadangan database |

### Visualisasi DFD Level 0

```mermaid
flowchart TD
    %% Styling
    classDef entitas fill:#e0f2fe,stroke:#0284c7,stroke-width:2px,color:#0f172a,font-weight:bold;
    classDef proses fill:#fef08a,stroke:#ca8a04,stroke-width:2px,color:#0f172a,font-weight:bold,shape:circle;
    classDef datastore fill:#f3f4f6,stroke:#4b5563,stroke-width:2px,color:#0f172a;

    %% Entitas Luar
    Lurah[Lurah / Kades]:::entitas
    Admin[Admin IT]:::entitas
    Panitia[Panitia]:::entitas
    Petugas[Petugas TPS]:::entitas
    Pemilih[Pemilih]:::entitas
    Saksi[Saksi]:::entitas

    %% Data Store
    D1[(D1 DPT_DIGITAL)]:::datastore
    D2[(D2 KANDIDAT)]:::datastore
    D4[(D4 OTP_TOKENS)]:::datastore
    D5[(D5 SUARA_ANONIM)]:::datastore
    D6[(D6 BERITA_ACARA)]:::datastore
    D7[(D7 BACKUP_LOG)]:::datastore
    D8[(D8 AUDIT_LOG)]:::datastore

    %% Proses
    P1((1.0\nManajemen\nDPT)):::proses
    P2((2.0\nManajemen\nKandidat)):::proses
    P3((3.0\nVerifikasi &\nAutentikasi)):::proses
    P4((4.0\nPemungutan\nSuara)):::proses
    P5((5.0\nRekapitulasi\nHasil)):::proses
    P6((6.0\nPengesahan &\nPelaporan)):::proses
    P7((7.0\nBackup &\nAudit)):::proses

    %% Aliran Proses 1 & 2
    Admin -->|Data Warga| P1
    P1 -->|Data Valid| D1
    P1 -->|Status| Admin
    P1 -->|DPT| Panitia

    Panitia -->|Registrasi| P2
    P2 -->|Profil| D2

    %% Aliran Proses 3
    Petugas -->|NIK| P3
    P3 -->|Cek NIK| D1
    P3 -->|Hash OTP| D4
    P3 -->|Status NIK & OTP| Petugas
    Pemilih -->|OTP| P3

    %% Aliran Proses 4
    P3 -->|Otorisasi Akses| P4
    D2 -->|Daftar Kandidat| P4
    Pemilih -->|Pilihan| P4
    P4 -->|Suara Terenkripsi| D5
    P4 -->|Token Bukti| Pemilih
    P4 -->|Update Status| D1

    %% Aliran Proses 5 & 6
    D5 -->|Data Suara| P5
    D1 -->|Total DPT| P5
    P5 -->|Dashboard| Saksi
    P5 -->|Statistik| Panitia
    P5 -->|Hasil Final| P6

    Lurah -->|Konfirmasi Pengesahan| P6
    P6 -->|Dokumen BA| D6
    P6 -->|Berita Acara| Lurah
    P6 -->|Hasil Publik| Panitia

    %% Aliran Proses 7
    Admin -->|Perintah Backup| P7
    P7 -->|Riwayat Backup| D7
    P7 -->|Log Aktivitas| D8
    P7 -->|Status & Audit CSV| Admin
```
