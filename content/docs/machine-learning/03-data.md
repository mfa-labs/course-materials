---
title: "Data"
date: 2026-05-02
draft: false
weight: 3
---
# Jenis Data dalam Machine Learning

## Pendahuluan

Dalam Machine Learning, memahami jenis data adalah langkah fundamental.

Pemilihan algoritma, metode preprocessing, hingga evaluasi model sangat dipengaruhi oleh tipe data yang digunakan.

## Analogi

Bayangkan data seperti bahan bangunan.

* Kayu cocok untuk furnitur
* Besi cocok untuk jembatan
* Kaca cocok untuk jendela

Jika salah menggunakan material, hasil bangunan bisa gagal.

Begitu juga dalam Machine Learning.

Jenis data menentukan bagaimana data diproses dan model apa yang cocok digunakan.

---

# Mengapa Memahami Jenis Data Penting?

Karena setiap jenis data memiliki:

* Karakteristik berbeda
* Cara pengolahan berbeda
* Teknik visualisasi berbeda
* Algoritma yang berbeda

Kesalahan memahami tipe data dapat menyebabkan:

* Analisis salah
* Visualisasi tidak tepat
* Model tidak optimal
* Bias hasil prediksi

---

# Kategori Utama Jenis Data

Secara umum data dibagi menjadi:

```text
Data
├── Kualitatif (Categorical)
│   ├── Nominal
│   └── Ordinal
│
└── Kuantitatif (Numerical)
    ├── Interval
    └── Rasio
```

---

# 1. Data Nominal

Data nominal adalah data kategori tanpa urutan.

## Karakteristik

* Tidak memiliki tingkatan
* Tidak bisa dibandingkan lebih besar/kecil
* Hanya sebagai label

## Contoh

| Data          | Contoh                        |
| ------------- | ----------------------------- |
| Jenis kelamin | Laki-laki, Perempuan          |
| Warna         | Merah, Biru, Hijau            |
| Agama         | Islam, Kristen, Hindu         |
| Jurusan       | Informatika, Sistem Informasi |

## Analogi

Data nominal seperti nama pemain sepak bola.

Tidak ada nama yang “lebih besar” dibanding nama lain.

---

# 2. Data Ordinal

Data ordinal adalah data kategori yang memiliki urutan.

## Karakteristik

* Ada tingkatan
* Jarak antar kategori belum tentu sama
* Bisa dibandingkan secara ranking

## Contoh

| Data             | Contoh                   |
| ---------------- | ------------------------ |
| Tingkat kepuasan | Sangat puas, puas, cukup |
| Pendidikan       | SMA, S1, S2              |
| Ranking          | Juara 1, 2, 3            |

## Analogi

Ordinal mirip peringkat lomba.

Kita tahu juara 1 lebih tinggi dari juara 2, tetapi tidak tahu “selisih kemampuan” secara pasti.

---

# 3. Data Interval

Data interval adalah data numerik dengan jarak yang sama tetapi tidak memiliki nol absolut.

## Karakteristik

* Selisih antar nilai bermakna
* Tidak memiliki nol mutlak
* Tidak bisa dibandingkan dalam bentuk rasio

## Contoh

| Data         | Contoh     |
| ------------ | ---------- |
| Suhu Celsius | 20°C, 30°C |
| Tahun        | 1990, 2025 |
| Skor IQ      | 100, 120   |

## Penjelasan

Suhu 40°C bukan berarti dua kali lebih panas dari 20°C.

Karena nol pada Celsius bukan nol absolut.

## Analogi

Data interval seperti posisi lantai gedung.

Lantai 10 memang lebih tinggi dari lantai 5, tetapi bukan berarti dua kali lebih tinggi secara fisik.

---

# 4. Data Rasio

Data rasio adalah data numerik yang memiliki nol absolut.

## Karakteristik

* Memiliki nol mutlak
* Bisa dilakukan operasi matematika penuh
* Bisa dibandingkan dalam bentuk rasio

## Contoh

| Data         | Contoh      |
| ------------ | ----------- |
| Berat badan  | 50 kg       |
| Tinggi badan | 170 cm      |
| Umur         | 20 tahun    |
| Pendapatan   | Rp5.000.000 |

## Penjelasan

Berat 60 kg memang dua kali lebih berat dari 30 kg.

Karena terdapat nol absolut.

## Analogi

Data rasio seperti uang di dompet.

Rp200.000 benar-benar dua kali lebih banyak dibanding Rp100.000.

---

# Data dalam Machine Learning

Dalam praktik ML modern, data sering dikategorikan menjadi:

| Jenis            | Contoh           |
| ---------------- | ---------------- |
| Numerical Data   | Umur, pendapatan |
| Categorical Data | Gender, jurusan  |
| Time Series      | Harga saham      |
| Text Data        | Tweet, artikel   |
| Image Data       | Foto, X-ray      |
| Audio Data       | Voice recording  |
| Video Data       | CCTV             |

---

# 1. Numerical Data

Data berbentuk angka.

## Contoh

* Tinggi badan
* Nilai ujian
* Harga rumah

## Algoritma Cocok

* Linear Regression
* Random Forest
* XGBoost

---

# 2. Categorical Data

Data berbentuk kategori.

## Contoh

* Jenis kendaraan
* Kota asal
* Status mahasiswa

## Tantangan

Model ML tidak memahami teks secara langsung.

Karena itu categorical data perlu diubah menjadi angka menggunakan:

* Label Encoding
* One Hot Encoding

---

# 3. Time Series Data

Data berdasarkan urutan waktu.

## Contoh

* Harga saham
* Suhu harian
* Jumlah pengunjung website

## Karakteristik

* Memiliki pola waktu
* Memiliki trend
* Memiliki seasonality

## Algoritma

* ARIMA
* LSTM
* Prophet

---

# 4. Text Data

Data berbentuk teks.

## Contoh

* Tweet
* Review produk
* Artikel berita

## Tantangan

Komputer tidak memahami bahasa manusia secara langsung.

Karena itu teks perlu diubah menjadi representasi numerik.

## Teknik Umum

* Bag of Words
* TF-IDF
* Word Embedding
* Transformer Embedding

---

# 5. Image Data

Data berupa gambar.

## Contoh

* Foto wajah
* Citra satelit
* Hasil CT Scan

## Algoritma Umum

* CNN
* Vision Transformer

## Analogi

Image processing mirip manusia mengenali objek dari pola visual.

---

# 6. Audio Data

Data berbentuk suara.

## Contoh

* Voice assistant
* Musik
* Rekaman percakapan

## Tantangan

Audio perlu diubah menjadi representasi sinyal atau spectrogram.

---

# Structured vs Unstructured Data

## Structured Data

Data dengan format terstruktur.

Contoh:

| Nama | Umur | IPK |
| ---- | ---- | --- |
| Andi | 20   | 3.7 |

Biasanya disimpan dalam:

* Database SQL
* Spreadsheet

## Unstructured Data

Data tanpa struktur tetap.

Contoh:

* Foto
* Video
* Audio
* Teks bebas

---

# Tantangan Pengolahan Data

## Missing Value

Data kosong yang perlu ditangani.

## Imbalanced Data

Jumlah kelas tidak seimbang.

## Noise

Data mengandung kesalahan.

## Data Drift

Distribusi data berubah seiring waktu.

---

# Studi Kasus

## Kasus: Prediksi Kelulusan Mahasiswa

| Fitur          | Jenis Data |
| -------------- | ---------- |
| Nama           | Nominal    |
| Jenis kelamin  | Nominal    |
| Semester       | Ordinal    |
| IPK            | Rasio      |
| Kehadiran      | Rasio      |
| Komentar dosen | Text       |

---

# Best Practice

## Pahami Data Sebelum Modeling

Banyak kegagalan proyek ML terjadi karena kurang memahami karakteristik data.

## Gunakan Visualisasi

Visualisasi membantu memahami pola dan anomaly.

## Dokumentasikan Data

Catat:

* Sumber data
* Tipe data
* Missing value
* Distribusi data

---

# Kesimpulan

Memahami jenis data adalah dasar penting dalam Machine Learning.

Jenis data menentukan:

* Teknik preprocessing
* Algoritma yang cocok
* Teknik evaluasi
* Kualitas model

Semakin baik pemahaman terhadap data, semakin baik kemungkinan menghasilkan model Machine Learning yang akurat.

---

# Latihan Mahasiswa

## Latihan 1

Kelompokkan data berikut:

* Tinggi badan
* Jurusan
* Ranking kelas
* Suhu ruangan

## Latihan 2

Cari contoh:

* Structured data
* Unstructured data
* Time series data

## Latihan 3

Identifikasi tipe data pada dataset Kaggle sederhana.

---

# Referensi

1. Aurélien Géron — Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow
2. Ian Goodfellow — Deep Learning
3. Scikit-Learn Documentation
4. TensorFlow Documentation
5. Kaggle Learn
