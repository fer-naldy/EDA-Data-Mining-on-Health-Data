# Analisis Data Kesehatan Masyarakat — Data Mining & Business Intelligence

Proyek Tugas Akhir mata kuliah **Data Mining** yang melakukan proses *data mining* menyeluruh terhadap data survei kesehatan (SRQ 2023) untuk menggali *insight* seputar **kesehatan mental**, **obesitas**, dan **pola penyakit kronis/infeksi** di masyarakat.

## Tentang Proyek

Tugas ini terdiri dari tiga bagian utama:

- **A.** Melakukan proses *mining* pada data yang diberikan (preprocessing, pembersihan data, dan analisis).
- **B.** Menggali informasi dan *insight* dari hasil proses tersebut.
- **C.** Menyusun laporan/presentasi dari hasil analisis.

## Anggota Kelompok

| Nama | NPM |
|---|---|
| Chatlea Shakira Haq | 2106725116 |
| Fernaldy | 2106706464 |
| Jihan Sandrina Halim | 2106708160 |
| Niken Salsabila Helmelia | 2106724933 |
| Zahrah Mahfuzah | 2106704004 |

## Dataset

Data yang digunakan adalah **Data Kesehatan Mental (SRQ) 2023 – Filtered**, berisi data survei kesehatan masyarakat mencakup data demografis (usia, jenis kelamin, wilayah, pendidikan, status perkawinan), data antropometri (tinggi badan, berat badan, IMT), riwayat penyakit (jantung, stroke, diabetes, kanker, dll.), gaya hidup (pola makan, olahraga, merokok), dan indikator kesehatan mental (skala SRQ).

## Alur Kerja (Workflow)

### 1. Import & Setup
Import library (`pandas`, `numpy`, `matplotlib`, `seaborn`, `sklearn`, `statsmodels`) dan pengambilan dataset dari Google Drive menggunakan `gdown`.

### 2. Data Preprocessing
- **Pengecekan tipe data** — perbaikan tipe data kolom `TINGGI BADAN` yang seharusnya numerik.
- **Penanganan noise & outlier** — koreksi nilai tidak wajar pada `USIA`, `TINGGI BADAN`, dan `BERAT BADAN` (mis. usia tertulis sebagai tanggal lahir, tinggi badan dalam satuan yang tidak konsisten) menggunakan aturan kondisional bertingkat.
- **Rekalkulasi turunan** — perhitungan ulang `Kelompok Umur`, `NILAI IMT`, dan kategori `IMT` setelah outlier dibersihkan.
- **Missing value** — imputasi nilai kosong berdasarkan konteks pertanyaan (mis. tidak merokok → 0 batang/hari).
- **Pengecekan duplikasi** dan **analisis korelasi** antar variabel numerik.

### 3. Pembuatan Subset Data
Data dipecah menjadi beberapa dataframe tematik: `data_mental`, `data_obesitas`, `data_gagal_ginjal`, dan `data_penyakit`.

### 4. Analisis & Pemodelan
- **Penyakit paling umum** — visualisasi frekuensi dan proporsi penyakit yang diderita responden.
- **Kesehatan Mental**
  - Kategorisasi kondisi mental (Normal vs Perlu Perhatian Khusus) berdasarkan skor SRQ (standar Riskesdas).
  - Validasi kategorisasi menggunakan klasifikasi **SVM**, **Decision Tree**, dan **K-NN** (akurasi > 99%).
  - Eksplorasi demografis: sebaran berdasarkan wilayah, kelompok umur, jenis kelamin, dan status pernikahan.
- **Obesitas**
  - Distribusi kategori IMT dan demografi penderita obesitas.
  - Hubungan pola konsumsi (junk food, gula, sayur-buah) dan aktivitas fisik dengan obesitas.
- **Distribusi umur per penyakit** — analisis kepadatan (KDE plot) untuk kelompok penyakit infeksi vs kronis, serta korelasi antar-penyakit kronis.
- **Hubungan antar variabel** menggunakan **regresi logistik**:
  - Obesitas terhadap risiko gangguan kesehatan mental.
  - Status pernikahan terhadap risiko gangguan kesehatan mental.

## Temuan Utama

- Sebagian besar responden memiliki kesehatan mental normal, namun kelompok umur **35–44 tahun** dan individu yang **sudah menikah** menunjukkan proporsi gangguan mental lebih tinggi.
- **28,4%** responden termasuk kategori obesitas, terbanyak berada di wilayah **Jawa Timur, Jawa Barat, dan Jawa Tengah**, didominasi laki-laki dan kelompok umur 35–44 tahun.
- Penderita obesitas cenderung memiliki pola makan kurang sehat (konsumsi sayur-buah rendah, aktivitas fisik minim).
- **Obesitas** meningkatkan peluang gangguan kesehatan mental sebesar ±1,42 kali (regresi logistik).
- **Status menikah** dikaitkan dengan peluang gangguan kesehatan mental yang lebih tinggi (±1,55 kali) dibanding belum menikah.
- Penyakit kronis (Jantung, Stroke, Hipertensi) banyak muncul bersamaan pada kelompok usia 35–45 dan 55–65 tahun.

## Tools/Library yang Digunakan

- **Python 3**
- `pandas`, `numpy` — manipulasi data
- `matplotlib`, `seaborn` — visualisasi data
- `scikit-learn` — klasifikasi (SVM, Decision Tree, K-NN)
- `statsmodels` — regresi logistik
- `gdown` — pengambilan dataset dari Google Drive

## Struktur Notebook

```
1. Import Module
2. Import Dataset
3. Preprocessing
   ├── Tipe Data
   ├── Noise & Outlier
   ├── Missing Value
   ├── Duplikasi Data
   └── Korelasi
4. Pembuatan Dataframe Tematik (Mental, Obesitas, Gagal Ginjal, Penyakit)
5. Analisis Data
   ├── Penyakit Paling Umum
   ├── Kesehatan Mental
   ├── Obesitas
   ├── Distribusi Umur per Penyakit
   └── Hubungan Antar Variabel (Regresi Logistik)
