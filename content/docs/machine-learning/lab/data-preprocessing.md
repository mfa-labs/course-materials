---

title: "Modul Praktikum: Data Preprocessing"
date: 2026-04-18
weight: 1
draft: false

# Metadata OBE

course: "Machine Learning"
module: "Data Preprocessing"
semester: 6
credits: 3 SKS

# Capaian Pembelajaran

cpmk:

* "Mampu memahami konsep dasar data preprocessing"
* "Mampu melakukan data cleaning"
* "Mampu melakukan encoding data kategorikal"
* "Mampu menerapkan feature scaling"
* "Mampu membangun pipeline preprocessing"

---

## 📘 Deskripsi

Data preprocessing merupakan tahapan penting dalam machine learning untuk menyiapkan data agar siap digunakan oleh model. Proses ini mencakup pembersihan data, transformasi, dan normalisasi.

Kerjakan praktikum di Google Colabs, kemudian sajikan laporan untuk menjawab setiap pertanyaan dalam modul.

Contoh data yang dapat digunakan : [Unduh Data CSV](/job_salary_prediction_dataset.csv)

---

## 🧪 Task 1: Eksplorasi Data

### Tujuan

Memahami struktur dataset dan mengidentifikasi permasalahan awal.

### Langkah

```python
import pandas as pd

df = pd.read_csv('data.csv')

print(df.head())
print(df.info())
print(df.describe())
```

### Tugas

* Identifikasi missing values
* Identifikasi tipe data
* Analisis distribusi data

---

## 🧪 Task 2: Data Cleaning

### Tujuan

Menangani missing values dan data tidak valid.

### Langkah

```python
print(df.isnull().sum())

df['Age'] = df['Age'].fillna(df['Age'].mean())

df = df.dropna()
```

### Tugas

* Bandingkan metode drop dan fill
* Analisis dampaknya terhadap dataset

---

## 🧪 Task 3: Encoding Data

### Tujuan

Mengubah data kategorikal menjadi numerik.

### Label Encoding

```python
from sklearn.preprocessing import LabelEncoder

le = LabelEncoder()
df['Gender'] = le.fit_transform(df['Gender'])
```

### One-Hot Encoding

```python
df = pd.get_dummies(df, columns=['City'])
```

### Tugas

* Bandingkan kedua metode
* Tentukan kapan masing-masing digunakan

---

## 🧪 Task 4: Feature Scaling

### Tujuan

Menyamakan skala data numerik.

### Normalisasi

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
df[['Salary']] = scaler.fit_transform(df[['Salary']])
```

### Standardisasi

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
df[['Age']] = scaler.fit_transform(df[['Age']])
```

### Tugas

* Bandingkan hasil normalisasi dan standardisasi
* Jelaskan kapan masing-masing digunakan

---

## 🧪 Task 5: Split Data

### Tujuan

Membagi dataset menjadi training dan testing.

```python
from sklearn.model_selection import train_test_split

X = df.drop('target', axis=1)
y = df['target']

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

### Tugas

* Uji berbagai rasio split
* Analisis hasilnya

---

## 🧪 Task 6: Pipeline

### Tujuan

Mengintegrasikan preprocessing dalam satu pipeline.

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.impute import SimpleImputer

pipeline = Pipeline([
    ('imputer', SimpleImputer(strategy='mean')),
    ('scaler', StandardScaler())
])

X_processed = pipeline.fit_transform(X)
```

### Tugas

* Tambahkan encoding ke pipeline
* Evaluasi hasil preprocessing

---

## 📊 Evaluasi

| Komponen     | Bobot |
| ------------ | ----- |
| Kode Program | 30%   |
| Analisis     | 30%   |
| Diskusi      | 20%   |
| Laporan      | 20%   |

---

## ❓ Pertanyaan Refleksi

1. Mengapa preprocessing penting?
2. Apa dampak jika tidak melakukan scaling?
3. Kapan menggunakan One-Hot Encoding?
4. Apa itu data leakage?

---

## 📚 Kesimpulan

Data preprocessing adalah langkah krusial dalam machine learning untuk memastikan kualitas data dan meningkatkan performa model.
