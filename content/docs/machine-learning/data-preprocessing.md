---
title: "Data Preprocessing"
date: 2026-04-13
draft: false
weight: 2
---

# Data Preprocessing

## Deskripsi Modul
Modul ini membahas teknik persiapan data yang merupakan langkah krusial dalam pipeline machine learning. Data preprocessing memastikan data siap digunakan untuk pelatihan model yang efektif.

### Mengapa Data Preprocessing Penting?

**Analogi: Memasak Bahan Mentah**

- **Bahan mentah kotor** = Data mentah dari dunia nyata (ada yang hilang, kotor, tidak seragam)
- **Data preprocessing** = Mencuci, memotong, dan menyiapkan bahan sebelum dimasak
- **Model ML** = Chef yang memasak bahan yang sudah siap

**Fakta Menarik**: 80% waktu dalam proyek ML dihabiskan untuk data preprocessing!

## Learning Outcomes Modul
Setelah menyelesaikan modul ini, mahasiswa akan mampu:
- Melakukan eksplorasi data awal (EDA)
- Menangani missing values dan outliers
- Melakukan normalisasi dan standardisasi data
- Mengimplementasikan feature engineering
- Menangani data kategorikal dan imbalance

---

## 1. Exploratory Data Analysis (EDA)

### Penjelasan Sederhana
EDA adalah proses "mengenal" data sebelum digunakan, seperti dokter memeriksa pasien sebelum memberikan diagnosis.

**Analogi: Bertemu Orang Baru**
- Lihat penampilan umum (info dasar)
- Tanyakan latar belakang (describe statistics)
- Perhatikan perilaku unik (distribusi data)
- Cari tahu kekurangan (missing values)

### Tujuan EDA:
1. **Memahami struktur data** - Berapa kolom? Tipe data apa?
2. **Menemukan pola** - Data seperti apa distribusinya?
3. **Deteksi masalah** - Ada data hilang? Ada outlier?
4. **Generate hipotesis** - Apa insight awal dari data?

### 1.1 Memahami Dataset
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
df = pd.read_csv('data.csv')

# Basic info - seperti melihat kartu nama orang baru
print(df.info())  # Tipe data, jumlah non-null
print(df.describe())  # Statistik dasar: mean, std, min, max

# Visualisasi distribusi - seperti melihat bagaimana orang tersebut
df.hist(figsize=(10, 8))
plt.show()
```

### 1.2 Deteksi Missing Values
```python
# Cek missing values - seperti mencari tahu apa yang belum diketahui
print(df.isnull().sum())

# Visualisasi missing values - heatmap seperti peta harta karun yang hilang
sns.heatmap(df.isnull(), cbar=False)
plt.show()
```

## 2. Penanganan Missing Values

### Penjelasan Sederhana
Missing values seperti "lubang" dalam data yang perlu diisi agar model bisa belajar dengan baik.

**Analogi: Puzzle yang Kurang Potongan**
- **Deletion** = Buang potongan puzzle yang hilang (berisiko kehilangan info)
- **Imputation** = Buat potongan baru berdasarkan potongan sekitar
- **Prediction** = Tebak seperti apa potongan yang hilang berdasarkan pola

### Kapan Menggunakan Teknik Mana?

| Teknik | Kapan Digunakan | Kelebihan | Kekurangan |
|--------|----------------|-----------|------------|
| **Deletion** | < 5% data hilang | Sederhana | Kehilangan informasi |
| **Mean/Median** | Data numerik normal | Cepat | Mengurangi variasi |
| **Mode** | Data kategorikal | Sederhana | Bias terhadap kategori mayoritas |
| **KNN** | Data kompleks | Akurat | Lambat untuk data besar |

### 2.2 Implementasi
```python
from sklearn.impute import SimpleImputer, KNNImputer

# Mean imputation untuk numerical - seperti mengisi rata-rata nilai ujian
imputer = SimpleImputer(strategy='mean')
df['numerical_col'] = imputer.fit_transform(df[['numerical_col']])

# KNN imputation - seperti mengisi berdasarkan teman terdekat
knn_imputer = KNNImputer(n_neighbors=5)
df = pd.DataFrame(knn_imputer.fit_transform(df), columns=df.columns)
```

## 3. Deteksi dan Penanganan Outliers

### Penjelasan Sederhana
Outliers adalah data yang "aneh" atau berbeda drastis dari data lainnya, seperti orang yang tinggi 3 meter di antara orang normal.

**Analogi: Pemain Gila dalam Tim**
- **Outlier baik**: Pemain super jago (bisa dianggap sebagai data valid)
- **Outlier buruk**: Pemain yang tidak ikut aturan (perlu dihapus atau diperbaiki)

### Mengapa Outliers Berbahaya?
- Membuat model "bingung" dan belajar pola yang salah
- Menurunkan akurasi prediksi
- Bisa menunjukkan kesalahan pengukuran data

### 3.1 Metode Deteksi

#### Box Plot Method
**Analogi: Kotak mainan dengan garis luar**
- Kotak = 50% data tengah
- Garis = batas normal
- Titik di luar = outliers

#### Z-Score Method  
**Analogi: Berapa standar deviasi dari rata-rata**
- Z-score > 3 = outlier (jarang banget)
- Z-score > 2 = perlu diperhatikan

#### IQR Method
**Analogi: Rentang antar kuartil**
- Q1 = 25% data terendah
- Q3 = 75% data tertinggi  
- IQR = Q3 - Q1
- Outlier = di luar 1.5 * IQR dari Q1/Q3

### 3.2 Implementasi
```python
# IQR method - seperti mengukur jangkauan normal
Q1 = df['column'].quantile(0.25)  # 25% data
Q3 = df['column'].quantile(0.75)  # 75% data
IQR = Q3 - Q1  # Rentang tengah

lower_bound = Q1 - 1.5 * IQR  # Batas bawah normal
upper_bound = Q3 + 1.5 * IQR  # Batas atas normal

outliers = df[(df['column'] < lower_bound) | (df['column'] > upper_bound)]
print(f"Jumlah outliers: {len(outliers)}")
```

## 4. Feature Scaling

### Penjelasan Sederhana
Feature scaling membuat semua fitur memiliki skala yang sama, seperti menyamaratakan ukuran pemain dalam tim agar permainan adil.

**Analogi: Lomba Lari Estafet**
- **Tanpa scaling**: Ada yang lari 100m, ada yang lari 1000m
- **Dengan scaling**: Semua lari dalam jarak yang sama

### Mengapa Perlu Feature Scaling?
- Algoritma seperti KNN, SVM sensitif terhadap skala
- Gradient descent konvergen lebih cepat
- Membantu interpretasi fitur

### 4.1 Standardization vs Normalization

#### Standardization (Z-score Scaling)
**Analogi: Nilai Standar Ujian**
- Mengubah menjadi distribusi normal: mean=0, std=1
- Cocok untuk data yang terdistribusi normal
- **Rumus**: (X - mean) / std

#### Normalization (Min-Max Scaling)  
**Analogi: Skor 0-100**
- Mengubah ke range [0,1] atau [-1,1]
- Cocok untuk data dengan range terbatas
- **Rumus**: (X - min) / (max - min)

### Kapan Menggunakan Yang Mana?

| Teknik | Kapan Digunakan | Contoh Algoritma |
|--------|----------------|------------------|
| **Standardization** | Data normal, outliers banyak | Linear Regression, Logistic Regression, KNN |
| **Normalization** | Data range terbatas, neural networks | Neural Networks, Image Processing |

### 4.2 Implementasi
```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler

# Standardization - seperti mengubah nilai ke skala standar
scaler = StandardScaler()
df_scaled = pd.DataFrame(scaler.fit_transform(df), columns=df.columns)
print("Mean setelah scaling:", df_scaled.mean().round(2))
print("Std setelah scaling:", df_scaled.std().round(2))

# Normalization - seperti mengubah ke skala 0-1
minmax = MinMaxScaler()
df_normalized = pd.DataFrame(minmax.fit_transform(df), columns=df.columns)
print("Range setelah normalization:", df_normalized.min().round(2), "to", df_normalized.max().round(2))
```

## 5. Encoding Categorical Variables

### Penjelasan Sederhana
Data kategorikal seperti "merah", "biru", "hijau" perlu diubah ke angka agar komputer bisa mengerti.

**Analogi: Menerjemahkan Bahasa**
- **Data asli**: "Jakarta", "Surabaya", "Bandung"
- **Label Encoding**: 0, 1, 2 (seperti kode bahasa)
- **One-Hot Encoding**: [1,0,0], [0,1,0], [0,0,1] (seperti bendera negara)

### Mengapa Perlu Encoding?
- Algoritma ML hanya mengerti angka
- Encoding yang salah bisa membuat model bias

### 5.1 Teknik Encoding

#### Label Encoding
**Analogi: Memberi Nomor Urut**
- "Merah" = 0, "Biru" = 1, "Hijau" = 2
- **Kelebihan**: Sederhana, hemat memory
- **Kekurangan**: Algoritma mengira ada urutan (2 > 1 > 0)

#### One-Hot Encoding
**Analogi: Bendera untuk Setiap Kategori**
- "Merah" = [1,0,0], "Biru" = [0,1,0], "Hijau" = [0,0,1]
- **Kelebihan**: Tidak ada asumsi urutan
- **Kekurangan**: Banyak kolom baru (curse of dimensionality)

#### Ordinal Encoding
**Analogi: Rating Bintang**
- "Buruk" = 1, "Sedang" = 2, "Baik" = 3
- **Kapan digunakan**: Kategori memiliki urutan natural

### 5.2 Implementasi
```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder

# Label Encoding - cocok untuk ordinal data
le = LabelEncoder()
df['size_encoded'] = le.fit_transform(df['size'])  # S, M, L, XL -> 0, 1, 2, 3
print("Mapping:", dict(zip(le.classes_, le.transform(le.classes_))))

# One-Hot Encoding - cocok untuk nominal data
ohe = OneHotEncoder(sparse=False)
encoded = ohe.fit_transform(df[['color']])  # Red, Blue, Green
df_encoded = pd.DataFrame(encoded, columns=ohe.get_feature_names_out(['color']))
print("One-hot columns:", df_encoded.columns.tolist())
```

## 6. Feature Engineering

### Penjelasan Sederhana
Feature engineering adalah seni menciptakan fitur baru dari data yang ada untuk membantu model belajar lebih baik.

**Analogi: Memasak Kreatif**
- **Bahan dasar**: Bawang, cabai, tomat
- **Feature engineering**: Membuat sambal, tumis, atau pasta
- **Hasil**: Fitur baru yang lebih bermakna

### Mengapa Feature Engineering Penting?
- Model sederhana dengan fitur bagus > Model kompleks dengan fitur buruk
- Domain knowledge bisa diubah jadi fitur matematis
- Mengurangi dimensionalitas sambil mempertahankan informasi

### 6.1 Teknik Feature Engineering

#### Polynomial Features
**Analogi: Kombinasi Bahan**
- Dari fitur A dan B, buat A², B², A×B
- Menangkap hubungan non-linear

#### Binning (Grouping)
**Analogi: Mengelompokkan Umur**
- Umur 0-12 = Anak, 13-19 = Remaja, 20-59 = Dewasa
- Mengubah numerik jadi kategorikal

#### Feature Interaction
**Analogi: Efek Gabungan**
- Pendapatan × Pengalaman = Kekayaan pengalaman
- Menangkap efek sinergi antar fitur

#### Domain Knowledge Features
**Analogi: Rahasia Resep Keluarga**
- BMI = Berat / (Tinggi)²
- Rasio debt-to-income

### 6.2 Implementasi
```python
from sklearn.preprocessing import PolynomialFeatures

# Polynomial features - seperti membuat kombinasi bahan
poly = PolynomialFeatures(degree=2, include_bias=False)
poly_features = poly.fit_transform(df[['height', 'weight']])
feature_names = poly.get_feature_names_out(['height', 'weight'])
print("Fitur baru:", feature_names)
# Output: ['height', 'weight', 'height^2', 'height weight', 'weight^2']

# Domain knowledge feature - BMI
df['bmi'] = df['weight_kg'] / (df['height_m'] ** 2)

# Binning feature - age groups
df['age_group'] = pd.cut(df['age'], bins=[0, 12, 19, 59, 100], 
                        labels=['child', 'teen', 'adult', 'senior'])
```

## 7. Handling Imbalanced Data

### Penjelasan Sederhana
Imbalanced data seperti kelas dengan jumlah siswa yang sangat berbeda: 100 siswa kelas A vs 5 siswa kelas B.

**Analogi: Pemilu Tidak Adil**
- **Kelas mayoritas**: Partai besar dengan banyak pemilih
- **Kelas minoritas**: Partai kecil dengan sedikit pemilih
- **Masalah**: Model akan selalu pilih kelas mayoritas

### Dampak Imbalanced Data
- Model bias ke kelas mayoritas
- Akurasi tinggi tapi recall rendah untuk kelas minoritas
- False negative tinggi (misal: tidak terdeteksi penyakit langka)

### 7.1 Teknik Penanganan

#### Oversampling (SMOTE)
**Analogi: Mengundang Tamu Tambahan**
- Membuat data sintetis untuk kelas minoritas
- Seperti meng-clone siswa kelas B sampai jumlahnya sama dengan kelas A

#### Undersampling
**Analogi: Mengurangi Tamu**
- Mengurangi data kelas mayoritas
- Seperti mengeluarkan siswa kelas A sampai jumlahnya sama dengan kelas B

#### Class Weight Adjustment
**Analogi: Bobot Nilai Berbeda**
- Memberi penalti lebih besar untuk kesalahan di kelas minoritas
- Seperti nilai kelas B lebih berbobot daripada kelas A

### 7.2 Implementasi SMOTE
```python
from imblearn.over_sampling import SMOTE
from collections import Counter

print("Distribusi sebelum SMOTE:", Counter(y))

smote = SMOTE(random_state=42, k_neighbors=5)
X_resampled, y_resampled = smote.fit_resample(X, y)

print("Distribusi setelah SMOTE:", Counter(y_resampled))
# SMOTE akan membuat data sintetis untuk menyeimbangkan kelas
```

## 8. Data Splitting

### Penjelasan Sederhana
Data splitting seperti membagi kue untuk acara berbeda: sebagian untuk latihan, sebagian untuk latihan lagi, sebagian untuk acara utama.

**Analogi: Ujian Sekolah**
- **Training set**: Buku latihan di rumah (model belajar)
- **Validation set**: Ujian harian (tuning parameter)
- **Test set**: Ujian nasional (evaluasi final)

### Mengapa Perlu 3 Split?
- **Training**: Model belajar pola
- **Validation**: Cek performa selama training, pilih model terbaik
- **Test**: Evaluasi final dengan data yang benar-benar baru

### Proporsi yang Direkomendasikan
- **Small dataset** (< 1000): 60% train, 20% val, 20% test
- **Medium dataset** (1000-10000): 70% train, 15% val, 15% test  
- **Large dataset** (> 10000): 80% train, 10% val, 10% test

### 8.1 Train-Validation-Test Split
```python
from sklearn.model_selection import train_test_split

# Split awal: train+val vs test (80:20)
X_train_val, X_test, y_train_val, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y  # stratify untuk imbalanced data
)

# Split kedua: train vs validation (75:25 dari train_val)
X_train, X_val, y_train, y_val = train_test_split(
    X_train_val, y_train_val, test_size=0.25, random_state=42, stratify=y_train_val
)

print(f"Train: {len(X_train)}, Validation: {len(X_val)}, Test: {len(X_test)}")
print(f"Total: {len(X_train) + len(X_val) + len(X_test)}")
```

## Latihan Praktis

### Tugas 1: EDA pada Dataset Real
1. Pilih dataset dari Kaggle
2. Lakukan EDA lengkap
3. Identifikasi masalah data
4. Buat laporan preprocessing

### Tugas 2: Pipeline Preprocessing
1. Buat pipeline preprocessing menggunakan sklearn
2. Terapkan pada dataset baru
3. Bandingkan performa model sebelum dan sesudah preprocessing

## Referensi
- Scikit-learn Documentation
- "Feature Engineering for Machine Learning" - Alice Zheng & Amanda Casari
- Towards Data Science articles