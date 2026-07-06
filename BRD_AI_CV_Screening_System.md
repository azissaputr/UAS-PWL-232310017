# BUSINESS REQUIREMENTS DOCUMENT (BRD)
## Sistem Seleksi CV Berbasis Kecerdasan Buatan (AI CV Screening System)

---

| Atribut          | Keterangan                                      |
|------------------|-------------------------------------------------|
| Nama Project     | AI CV Screening System                          |
| Kode Project     | UAS-PWL-232310017                               |
| Disusun oleh     | Egi Abdul Azis Saputra                          |
| NIM              | 232310017                                       |
| Mata Kuliah      | Pemrograman Web Lanjut (PWL)                    |
| Platform         | n8n Workflow Automation                         |
| Versi Dokumen    | 3.0                                             |
| Tanggal          | Juli 2026                                       |
| Status           | Final                                           |

---

## DAFTAR ISI

1. Pendahuluan
2. Tujuan Bisnis
3. Ruang Lingkup
4. Pemangku Kepentingan (Stakeholder)
5. Kebutuhan Bisnis
6. Kebutuhan Fungsional
7. Kebutuhan Non-Fungsional
8. Arsitektur Sistem dan Alur Kerja
9. Komponen Sistem
10. Aturan Bisnis (Business Rules)
11. Sistem Penilaian (Scoring System)
12. Integrasi Layanan Eksternal
13. Kebutuhan Data
14. Asumsi dan Batasan
15. Risiko dan Mitigasi
16. Kriteria Keberhasilan

---

## 1. PENDAHULUAN

### 1.1 Latar Belakang

Proses seleksi kandidat secara manual memerlukan waktu yang panjang, tenaga yang besar, dan rentan terhadap bias subjektif dari rekruter. Setiap lamaran pekerjaan memerlukan waktu rata-rata 15-30 menit untuk ditelaah, sehingga jika terdapat ratusan pelamar, proses ini menjadi tidak efisien dan tidak skalabel.

Project ini dirancang sebagai solusi otomasi proses penerimaan dan penilaian lamaran kerja menggunakan kecerdasan buatan (AI). Sistem ini memanfaatkan platform n8n sebagai orkestrator workflow, dikombinasikan dengan model bahasa besar (Large Language Model) untuk menganalisis dan menilai CV pelamar secara objektif, konsisten, dan terstandarisasi.

### 1.2 Permasalahan yang Diselesaikan

- Proses seleksi CV yang memakan waktu lama jika dilakukan secara manual.
- Ketidakkonsistenan penilaian antar rekruter yang berbeda.
- Sulitnya mengelola dan menyimpan data pelamar dalam jumlah besar.
- Tidak adanya standar penilaian yang terukur dan dapat dipertanggungjawabkan.
- Keterlambatan dalam memberikan respons kepada pelamar.

### 1.3 Solusi yang Diusulkan

Membangun sistem otomasi end-to-end yang mampu:
1. Menerima lamaran kerja melalui formulir web yang terstruktur.
2. Mengekstrak isi teks dari dokumen CV (PDF) menggunakan AI.
3. Mengevaluasi kualifikasi kandidat menggunakan rubrik penilaian berbasis AI.
4. Menyimpan hasil evaluasi secara otomatis ke Google Sheets.
5. Menyimpan file CV secara terorganisasi di Google Drive.

---

## 2. TUJUAN BISNIS

### 2.1 Tujuan Utama

1. Mengotomasi proses seleksi awal CV sehingga tim HR dapat fokus pada kandidat yang benar-benar memenuhi kualifikasi.
2. Mengurangi waktu seleksi awal dari rata-rata 20 menit per CV menjadi kurang dari 1 menit per CV.
3. Memberikan penilaian yang konsisten, objektif, dan dapat diaudit untuk setiap pelamar.
4. Membangun sistem penyimpanan data pelamar yang terpusat dan mudah diakses.

### 2.2 Tujuan Jangka Panjang

1. Menjadi fondasi sistem rekrutmen berbasis data yang dapat dikembangkan lebih lanjut.
2. Mendukung pengambilan keputusan rekrutmen berdasarkan data yang terstandarisasi.
3. Mengurangi potensi bias manusia dalam proses seleksi awal.

---

## 3. RUANG LINGKUP

### 3.1 Dalam Ruang Lingkup (In Scope)

- Formulir lamaran kerja berbasis web dengan antarmuka modern.
- Ekstraksi teks otomatis dari dokumen CV berformat PDF.
- Evaluasi dan penilaian CV menggunakan AI (Google Gemini 2.0 Flash).
- Klasifikasi kandidat ke dalam tiga kategori: QUALIFIED, REVIEW, NOT_QUALIFIED.
- Penyimpanan data hasil evaluasi ke Google Sheets.
- Penyimpanan file CV ke Google Drive.
- Dukungan untuk tiga posisi: Fullstack Developer, Frontend Developer, Backend Developer.

### 3.2 Di Luar Ruang Lingkup (Out of Scope)

- Proses wawancara dan seleksi lanjutan.
- Pengiriman notifikasi email otomatis kepada pelamar.
- Integrasi dengan sistem HRIS (Human Resource Information System).
- Evaluasi untuk posisi selain posisi developer yang telah ditentukan.
- Pengelolaan data karyawan yang sudah diterima.

---

## 4. PEMANGKU KEPENTINGAN (STAKEHOLDER)

| Pemangku Kepentingan | Peran                          | Kepentingan                                               |
|----------------------|--------------------------------|-----------------------------------------------------------|
| Tim HR / Rekruter    | Pengguna utama sistem          | Mendapatkan daftar kandidat yang sudah terseleksi         |
| Manajer Rekrutmen    | Pengambil keputusan akhir      | Akses laporan dan rekapitulasi hasil seleksi              |
| Pelamar Kerja        | Pengguna formulir lamaran      | Proses pengajuan lamaran yang mudah dan cepat             |
| Tim IT               | Administrator sistem           | Pemeliharaan dan monitoring workflow n8n                  |
| Developer (Pembuat)  | Pembuat dan pemelihara sistem  | Implementasi dan pengembangan fitur sistem                |

---

## 5. KEBUTUHAN BISNIS

### BR-01: Penerimaan Lamaran Kerja Digital
Sistem harus menyediakan formulir lamaran kerja yang dapat diakses melalui web browser tanpa memerlukan instalasi perangkat lunak tambahan.

### BR-02: Validasi Dokumen CV
Sistem harus memastikan bahwa dokumen CV yang diunggah hanya dalam format PDF untuk menjamin kompatibilitas dengan proses ekstraksi teks AI.

### BR-03: Evaluasi Otomatis Berbasis AI
Sistem harus mampu mengevaluasi setiap CV secara otomatis menggunakan model AI tanpa memerlukan intervensi manusia pada tahap seleksi awal.

### BR-04: Penilaian Terstandarisasi
Sistem harus menerapkan rubrik penilaian yang sama untuk setiap pelamar pada posisi yang sama, sehingga hasil evaluasi dapat dibandingkan secara objektif.

### BR-05: Penyimpanan Data Terpusat
Seluruh data hasil seleksi harus tersimpan secara otomatis dalam sistem yang dapat diakses oleh tim HR kapan saja.

### BR-06: Pengelolaan File CV
File CV yang diunggah pelamar harus tersimpan secara terorganisasi di penyimpanan cloud dengan penamaan yang sistematis.

---

## 6. KEBUTUHAN FUNGSIONAL

### 6.1 Modul Formulir Lamaran

| Kode  | Kebutuhan                                                                                             | Prioritas |
|-------|-------------------------------------------------------------------------------------------------------|-----------|
| FR-01 | Sistem menampilkan formulir lamaran kerja dengan judul "Submit Your Application"                      | Tinggi    |
| FR-02 | Formulir mewajibkan pengisian: Nama Lengkap, Email, Tanggal Lahir, Posisi yang Dilamar, dan Upload CV | Tinggi    |
| FR-03 | Dropdown posisi mencakup: Fullstack Developer, Frontend Developer, Backend Developer                  | Tinggi    |
| FR-04 | Field upload CV hanya menerima file berformat .pdf                                                    | Tinggi    |
| FR-05 | Formulir memiliki antarmuka visual modern dengan tema gelap (dark mode)                               | Sedang    |
| FR-06 | Tombol submit berlabel "Submit Application"                                                           | Sedang    |

### 6.2 Modul Ekstraksi Teks CV

| Kode  | Kebutuhan                                                                           | Prioritas |
|-------|-------------------------------------------------------------------------------------|-----------|
| FR-07 | Sistem mengekstrak teks dari file PDF CV yang diunggah menggunakan Mistral AI       | Tinggi    |
| FR-08 | Sistem menormalisasi output teks dari berbagai format respons AI                    | Tinggi    |
| FR-09 | Sistem memvalidasi bahwa teks CV yang diekstrak memiliki panjang minimal 50 karakter| Tinggi    |
| FR-10 | Sistem menyertakan informasi posisi yang dilamar bersama teks CV untuk evaluasi     | Tinggi    |

### 6.3 Modul Evaluasi AI

| Kode  | Kebutuhan                                                                                        | Prioritas |
|-------|--------------------------------------------------------------------------------------------------|-----------|
| FR-11 | Sistem mengirimkan teks CV dan posisi yang dilamar ke model AI untuk dievaluasi                  | Tinggi    |
| FR-12 | AI mengklasifikasikan relevansi bidang kandidat: RELEVANT_DIRECT, RELEVANT_ADJACENT, IRRELEVANT  | Tinggi    |
| FR-13 | AI mendeteksi tingkat pengalaman kandidat: JUNIOR, SENIOR, INSUFFICIENT                          | Tinggi    |
| FR-14 | AI menerapkan rubrik penilaian spesifik sesuai posisi yang dilamar                               | Tinggi    |
| FR-15 | AI menghitung skor akhir dalam skala 0-10                                                        | Tinggi    |
| FR-16 | AI mengkategorikan kandidat: QUALIFIED (>=7), REVIEW (4-6), NOT_QUALIFIED (<=3)                  | Tinggi    |
| FR-17 | AI menghasilkan penjelasan detail per kriteria penilaian                                          | Tinggi    |
| FR-18 | AI menghasilkan ringkasan temuan utama (keyFindings)                                              | Tinggi    |
| FR-19 | Sistem melakukan retry otomatis hingga 3 kali jika evaluasi AI gagal                             | Sedang    |

### 6.4 Modul Penyimpanan Data

| Kode  | Kebutuhan                                                                                        | Prioritas |
|-------|--------------------------------------------------------------------------------------------------|-----------|
| FR-20 | Sistem menyimpan hasil evaluasi ke Google Sheets pada sheet "Applications"                       | Tinggi    |
| FR-21 | Data yang disimpan mencakup: Nama, Email, Tanggal Lahir, Posisi, Level Pengalaman, Tahun Pengalaman, Waktu Submit, Skor, Rating, Kategori, Penjelasan, Temuan Utama | Tinggi |
| FR-22 | Sistem mencari folder "data cv" di Google Drive secara otomatis                                  | Tinggi    |
| FR-23 | Sistem membuat folder "data cv" secara otomatis jika belum ada                                   | Tinggi    |
| FR-24 | Sistem mengunggah file CV ke Google Drive dengan format penamaan: "[Nama] - CV - [Tanggal].pdf"  | Tinggi    |

---

## 7. KEBUTUHAN NON-FUNGSIONAL

### 7.1 Ketersediaan (Availability)
- Sistem harus tersedia selama jam operasional normal (minimal 99% uptime).
- Formulir lamaran harus dapat diakses 24 jam sehari, 7 hari seminggu.

### 7.2 Kinerja (Performance)
- Proses evaluasi CV harus diselesaikan dalam waktu maksimal 60 detik per pengajuan.
- Formulir lamaran harus memuat dalam waktu kurang dari 3 detik pada koneksi standar.

### 7.3 Keamanan (Security)
- File CV yang diunggah hanya dapat diakses oleh pihak yang memiliki otorisasi Google Drive.
- Data pelamar yang tersimpan di Google Sheets harus dibatasi aksesnya sesuai kebijakan organisasi.
- Token API dan kredensial layanan eksternal harus dikelola melalui sistem manajemen kredensial n8n.

### 7.4 Skalabilitas (Scalability)
- Sistem harus mampu memproses minimal 100 lamaran per hari tanpa penurunan performa yang signifikan.
- Arsitektur workflow harus mendukung penambahan posisi baru tanpa mengubah alur utama.

### 7.5 Ketepatan (Accuracy)
- Sistem penilaian AI harus konsisten dalam menerapkan rubrik yang telah ditetapkan.
- Nilai akhir yang dihasilkan harus selalu berada dalam rentang 0-10.
- Klasifikasi kategori kandidat harus sesuai dengan ambang batas yang telah ditentukan.

---

## 8. ARSITEKTUR SISTEM DAN ALUR KERJA

### 8.1 Gambaran Umum Arsitektur

Sistem terdiri dari dua alur paralel yang berjalan secara bersamaan setelah formulir disubmit:

```
[Pelamar]
    |
    v
[Formulir Lamaran Web (n8n Form Trigger)]
    |
    |--> [ALUR 1: Evaluasi CV] -----> [Ekstraksi Teks CV (Mistral AI)]
    |                                          |
    |                                  [Normalisasi Data CV]
    |                                          |
    |                                  [Evaluasi AI (Gemini 2.0 Flash)]
    |                                          |
    |                                  [Pengolahan Data Akhir]
    |                                          |
    |                                  [Simpan ke Google Sheets]
    |
    |--> [ALUR 2: Simpan File CV] --> [Cari Folder "data cv" di Drive]
                                               |
                                   [Folder Ada?]---[Tidak]--> [Buat Folder Baru]
                                       |                            |
                                      [Ya]                         |
                                       |<--------------------------+
                                       |
                                  [Persiapkan Upload]
                                       |
                                  [Upload CV ke Google Drive]
```

### 8.2 Alur Data Lengkap

1. Pelamar mengisi dan mengirimkan formulir lamaran.
2. Sistem secara paralel memulai dua proses:
   - Proses A: Ekstraksi dan evaluasi teks CV.
   - Proses B: Penyimpanan file CV ke Google Drive.
3. Pada Proses A:
   - Mistral AI mengekstrak teks dari file PDF CV.
   - Node normalisasi membersihkan dan memvalidasi teks yang diekstrak.
   - Gemini 2.0 Flash mengevaluasi CV berdasarkan rubrik penilaian.
   - Parser output mengonversi respons AI ke format JSON terstruktur.
   - Node pengolahan akhir menerapkan batas skor dan normalisasi data.
   - Data hasil evaluasi disimpan ke Google Sheets.
4. Pada Proses B:
   - Sistem mencari folder "data cv" di Google Drive.
   - Jika folder belum ada, folder dibuat secara otomatis.
   - File CV diunggah dengan nama terformat ke folder tersebut.

---

## 9. KOMPONEN SISTEM

### 9.1 Node n8n yang Digunakan

| Nama Node              | Tipe                               | Fungsi                                                           |
|------------------------|------------------------------------|------------------------------------------------------------------|
| Application Form3      | n8n Form Trigger                   | Menampilkan formulir lamaran dan menerima input pelamar          |
| Extract CV Text2       | Mistral AI                         | Mengekstrak teks dari dokumen PDF CV yang diunggah               |
| Normalize CV Data      | Code (JavaScript)                  | Menormalisasi output teks dari berbagai format respons AI        |
| Gemini 2.0 Flash2      | LangChain Google Gemini LLM        | Model bahasa untuk evaluasi konten CV                            |
| AI Qualification2      | LangChain Chain LLM                | Mengeksekusi rantai evaluasi AI dengan prompt dan parser         |
| JSON Output Parser2    | LangChain Structured Output Parser | Memaksa output AI dalam format JSON yang terstruktur             |
| Prepare Final Data2    | Code (JavaScript)                  | Memproses, memvalidasi, dan menormalisasi data hasil evaluasi AI |
| Save to Applications2  | Google Sheets                      | Menyimpan data evaluasi ke spreadsheet Google Sheets             |
| Find data cv Folder2   | HTTP Request (Google Drive API)    | Mencari folder penyimpanan CV di Google Drive                    |
| Folder Exists?2        | IF (Kondisional)                   | Menentukan apakah folder sudah ada atau perlu dibuat             |
| Create data cv Folder2 | HTTP Request (Google Drive API)    | Membuat folder baru di Google Drive jika belum ada               |
| Prepare Upload2        | Code (JavaScript)                  | Menyiapkan data biner CV dan metadata untuk proses upload        |
| Upload CV to Drive3    | Google Drive                       | Mengunggah file CV ke folder yang telah ditentukan               |

---

## 10. ATURAN BISNIS (BUSINESS RULES)

### BR-001: Validasi Format File
Hanya file berformat PDF yang diterima oleh sistem. File dalam format lain (DOCX, JPEG, PNG, dll.) akan ditolak oleh formulir sebelum diproses.

### BR-002: Validasi Panjang Teks CV
Teks CV yang berhasil diekstrak harus memiliki panjang minimal 50 karakter. Jika teks terlalu pendek, CV dianggap tidak valid untuk dievaluasi.

### BR-003: Posisi yang Didukung
Sistem hanya mendukung evaluasi untuk tiga posisi berikut:
- Fullstack Developer
- Frontend Developer
- Backend Developer

### BR-004: Penentuan Relevansi Bidang
AI mengklasifikasikan relevansi bidang kandidat terhadap posisi yang dilamar ke dalam tiga kategori:
- RELEVANT_DIRECT: Kandidat memiliki latar belakang langsung sesuai posisi.
- RELEVANT_ADJACENT: Kandidat memiliki latar belakang yang berdekatan dengan posisi.
- IRRELEVANT: Kandidat tidak memiliki latar belakang yang relevan dengan posisi.

### BR-005: Penentuan Tingkat Pengalaman
Tingkat pengalaman profesional kandidat diklasifikasikan berdasarkan jumlah tahun kerja relevan:
- INSUFFICIENT: Kurang dari 1 tahun pengalaman profesional relevan.
- JUNIOR: Antara 1 hingga 2 tahun pengalaman profesional relevan (inklusif).
- SENIOR: Lebih dari 2 tahun pengalaman profesional relevan.

Catatan: Pengalaman akademis dan magang dihitung dengan bobot 0.5x dari pengalaman kerja penuh.

### BR-006: Batas Skor Berdasarkan Relevansi Bidang (Field Relevance Ceiling)
- RELEVANT_DIRECT: Skor maksimum 10/10.
- RELEVANT_ADJACENT: Skor maksimum 6/10.
- IRRELEVANT: Skor maksimum 2/10.

### BR-007: Batas Skor Berdasarkan Tingkat Pengalaman (Experience Level Cap)
- INSUFFICIENT: Skor maksimum 3/10.
- JUNIOR: Skor maksimum 6/10.
- SENIOR: Tidak ada batas tambahan dari sisi pengalaman.

### BR-008: Kategori Kelulusan Akhir
Berdasarkan skor akhir (0-10), kandidat dikategorikan sebagai:
- QUALIFIED: Skor >= 7 (Disarankan untuk diproses ke tahap selanjutnya).
- REVIEW: Skor antara 4 dan 6 (Perlu pertimbangan lebih lanjut oleh tim HR).
- NOT_QUALIFIED: Skor <= 3 (Tidak memenuhi kualifikasi minimum).

### BR-009: Pencatatan Penyesuaian Skor
Jika sistem melakukan penyesuaian pada skor yang diberikan AI (karena penerapan batas), catatan penyesuaian akan ditambahkan secara otomatis pada kolom explanation di Google Sheets.

### BR-010: Penamaan File CV
File CV yang disimpan di Google Drive mengikuti format penamaan:
[Nama Lengkap Pelamar] - CV - [YYYY-MM-DD].pdf

---

## 11. SISTEM PENILAIAN (SCORING SYSTEM)

### 11.1 Rubrik Penilaian - Frontend Developer

| Nomor | Kriteria                              | Bobot | STRONG_MET | PARTIAL | MISSING |
|-------|---------------------------------------|-------|------------|---------|---------|
| R1    | Pengalaman Frontend dengan Tanggal    | 2.5   | 2.5        | 1.25    | 0       |
| R2    | Kemampuan JavaScript / TypeScript     | 2.0   | 2.0        | 1.0     | 0       |
| R3    | Framework Frontend (React, Vue, dll.) | 2.0   | 2.0        | 1.0     | 0       |
| R4    | CSS / Styling (Tailwind, SASS, dll.)  | 1.0   | 1.0        | 0.5     | 0       |
| R5    | Integrasi API (REST, GraphQL)         | 0.75  | 0.75       | 0.375   | 0       |
| R6    | State Management                      | 0.5   | 0.5        | 0.25    | 0       |
| R7    | Version Control / Git                 | 0.5   | 0.5        | 0.25    | 0       |
| R8    | Portofolio / Kualitas Proyek          | 0.75  | 0.75       | 0.375   | 0       |
|       | Total                                 | 10.0  |            |         |         |

### 11.2 Rubrik Penilaian - Backend Developer

| Nomor | Kriteria                                  | Bobot | STRONG_MET | PARTIAL | MISSING |
|-------|-------------------------------------------|-------|------------|---------|---------|
| R1    | Pengalaman Backend dengan Tanggal         | 2.5   | 2.5        | 1.25    | 0       |
| R2    | Bahasa Pemrograman Backend                | 2.0   | 2.0        | 1.0     | 0       |
| R3    | Framework Backend (Express, Django, dll.) | 2.0   | 2.0        | 1.0     | 0       |
| R4    | Database (MySQL, PostgreSQL, dll.)        | 1.0   | 1.0        | 0.5     | 0       |
| R5    | Desain API (REST, GraphQL, gRPC)          | 0.75  | 0.75       | 0.375   | 0       |
| R6    | Autentikasi / Keamanan (JWT, OAuth)       | 0.5   | 0.5        | 0.25    | 0       |
| R7    | Version Control / Git                     | 0.5   | 0.5        | 0.25    | 0       |
| R8    | Portofolio / Kualitas Proyek              | 0.75  | 0.75       | 0.375   | 0       |
|       | Total                                     | 10.0  |            |         |         |

### 11.3 Rubrik Penilaian - Fullstack Developer

| Nomor | Kriteria                                       | Bobot | STRONG_MET | PARTIAL | MISSING |
|-------|------------------------------------------------|-------|------------|---------|---------|
| R1    | Pengalaman Web/Fullstack dengan Tanggal        | 2.0   | 2.0        | 1.0     | 0       |
| R2    | Kemampuan Frontend (HTML, CSS, JS + Framework) | 1.5   | 1.5        | 0.75    | 0       |
| R3    | Kemampuan Backend (Bahasa + Framework + DB)    | 1.5   | 1.5        | 0.75    | 0       |
| R4    | Bukti Proyek Fullstack (Frontend + Backend)    | 1.25  | 1.25       | 0.625   | 0       |
| R5    | Database dan Pengelolaan Data                  | 1.0   | 1.0        | 0.5     | 0       |
| R6    | Integrasi / Desain API                         | 0.75  | 0.75       | 0.375   | 0       |
| R7    | Version Control / Git                          | 0.5   | 0.5        | 0.25    | 0       |
| R8    | Portofolio / Kualitas Proyek                   | 0.5   | 0.5        | 0.25    | 0       |
|       | Total                                          | 10.0  |            |         |         |

### 11.4 Prinsip Penilaian

Sistem penilaian menerapkan prinsip konservatif, yaitu:
- Nilai awal dimulai dari 0, bukan dari nilai tertinggi.
- Poin hanya ditambahkan jika ditemukan bukti konkret dalam CV.
- Sekadar mencantumkan nama teknologi tanpa konteks proyek hanya mendapat nilai PARTIAL.
- Kandidat dengan STRONG_MET pada suatu kriteria harus menunjukkan di mana dan bagaimana mereka menggunakan teknologi tersebut (nama proyek, nama perusahaan, atau periode waktu).

---

## 12. INTEGRASI LAYANAN EKSTERNAL

| Layanan Eksternal       | Tujuan Integrasi                              | Metode Autentikasi          |
|-------------------------|-----------------------------------------------|-----------------------------|
| Mistral AI (Cloud)      | Ekstraksi teks dari file PDF CV               | API Key (Mistral Cloud API) |
| Google Gemini 2.0 Flash | Model AI untuk evaluasi dan penilaian CV      | API Key (Google PaLM API)   |
| Google Sheets           | Penyimpanan data hasil evaluasi pelamar       | OAuth2                      |
| Google Drive            | Penyimpanan file CV yang diunggah pelamar     | OAuth2                      |

---

## 13. KEBUTUHAN DATA

### 13.1 Data Input dari Pelamar

| Field            | Tipe Data | Wajib | Validasi                  |
|------------------|-----------|-------|---------------------------|
| Full Name        | String    | Ya    | Tidak boleh kosong        |
| Email            | String    | Ya    | Format email valid        |
| Date of Birth    | Date      | Ya    | Format tanggal valid      |
| Position Applied | Enum      | Ya    | Salah satu dari 3 pilihan |
| Upload CV        | File      | Ya    | Hanya format .pdf         |

### 13.2 Data Output yang Disimpan ke Google Sheets

| Kolom             | Tipe Data | Sumber                           |
|-------------------|-----------|----------------------------------|
| Full Name         | String    | Form input                       |
| Email             | String    | Form input                       |
| Date of Birth     | Date      | Form input                       |
| Position Applied  | String    | Form input / AI output           |
| experienceLevel   | Enum      | AI evaluation                    |
| yearsOfExperience | Number    | AI evaluation                    |
| submittedAt       | DateTime  | System timestamp                 |
| qualificationRate | Integer   | AI evaluation (0-10)             |
| ratingDisplay     | String    | System generated (contoh: 7/10)  |
| category          | Enum      | System generated                 |
| fieldRelevance    | Enum      | AI evaluation                    |
| scoreCeiling      | Integer   | System calculated                |
| rawScore          | Number    | AI evaluation                    |
| explanation       | Text      | AI evaluation                    |
| keyFindings       | Text      | AI evaluation                    |

---

## 14. ASUMSI DAN BATASAN

### 14.1 Asumsi

- Pelamar memiliki akses internet yang stabil untuk mengisi dan mengirimkan formulir.
- File CV yang diunggah dalam format PDF memiliki konten teks yang dapat diekstrak (bukan PDF hasil scan gambar tanpa OCR).
- Layanan Mistral AI, Google Gemini, Google Sheets, dan Google Drive tersedia dan dapat diakses selama sistem beroperasi.
- Kredensial API untuk semua layanan eksternal telah dikonfigurasi dengan benar di n8n.
- Pelamar memahami bahwa formulir hanya menerima file PDF.

### 14.2 Batasan

- Sistem tidak dapat mengevaluasi CV dalam format gambar (JPEG, PNG) atau dokumen yang diproteksi password.
- Akurasi evaluasi AI bergantung pada kualitas teks yang terekstrak dari PDF.
- Sistem tidak mengirimkan notifikasi atau umpan balik otomatis kepada pelamar.
- Sistem hanya mendukung bahasa Inggris untuk konten CV (bahasa Indonesia pada teks CV dapat mempengaruhi akurasi evaluasi).
- Tidak ada mekanisme untuk pelamar melihat hasil evaluasi mereka secara langsung.

---

## 15. RISIKO DAN MITIGASI

| Kode Risiko | Deskripsi Risiko                                          | Tingkat | Strategi Mitigasi                                                                       |
|-------------|-----------------------------------------------------------|---------|-----------------------------------------------------------------------------------------|
| R-01        | Gagalnya ekstraksi teks dari CV (PDF gambar atau rusak)   | Tinggi  | Validasi panjang teks minimal; menampilkan pesan error yang informatif                  |
| R-02        | Respons AI tidak sesuai format JSON yang diharapkan       | Sedang  | Mekanisme retry otomatis 3 kali; fallback parsing dari berbagai format                  |
| R-03        | Batas kuota API layanan eksternal terlampaui              | Sedang  | Monitoring penggunaan API; penerapan rate limiting jika diperlukan                      |
| R-04        | Ketidakakuratan evaluasi AI terhadap CV                   | Sedang  | Implementasi rubrik penilaian yang ketat; mekanisme review manual untuk kategori REVIEW |
| R-05        | Gangguan layanan Google Drive atau Google Sheets          | Rendah  | Retry mechanism; notifikasi error ke administrator                                      |
| R-06        | Upload file CV gagal karena ukuran file terlalu besar     | Rendah  | Pembatasan ukuran file pada formulir; validasi sebelum upload                           |

---

## 16. KRITERIA KEBERHASILAN

Sistem dianggap berhasil jika memenuhi kriteria berikut:

1. Formulir lamaran dapat diakses dan berfungsi melalui web browser standar.
2. Sistem berhasil mengekstrak teks dari file PDF CV yang valid.
3. Evaluasi AI menghasilkan skor dalam rentang 0-10 dan kategori yang sesuai (QUALIFIED / REVIEW / NOT_QUALIFIED).
4. Data hasil evaluasi tersimpan secara otomatis ke Google Sheets tanpa intervensi manual.
5. File CV tersimpan secara terorganisasi di Google Drive dengan penamaan yang benar.
6. Seluruh proses (dari submit formulir hingga data tersimpan) selesai dalam waktu kurang dari 60 detik.
7. Sistem berhasil memproses minimal 10 lamaran berturut-turut tanpa error.

---

Dokumen ini merupakan bagian dari proyek UAS Pemrograman Web Lanjut.
Disusun oleh: Egi Abdul Azis Saputra - NIM 232310017
