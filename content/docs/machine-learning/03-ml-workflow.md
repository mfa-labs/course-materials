# Machine Learning Workflow

## Pendahuluan

Machine Learning (ML) bukan hanya tentang membuat model prediksi, tetapi juga tentang bagaimana membangun sebuah proses yang sistematis mulai dari pengumpulan data hingga deployment model ke lingkungan nyata.

Dalam praktik industri dan penelitian, sebagian besar waktu pengembangan Machine Learning justru dihabiskan pada pengolahan data, evaluasi, dan maintenance model, bukan hanya pada training model.

Machine Learning Workflow dapat dianalogikan seperti proses memasak.

| Proses Memasak     | Workflow ML        |
| ------------------ | ------------------ |
| Menentukan menu    | Problem Definition |
| Belanja bahan      | Data Collection    |
| Membersihkan bahan | Data Preprocessing |
| Mencicipi rasa     | Evaluation         |
| Menyajikan makanan | Deployment         |

Jika salah satu tahapan dilakukan dengan buruk, hasil akhirnya juga akan buruk. Model Machine Learning yang canggih sekalipun tidak akan bekerja optimal jika datanya buruk.

Konsep ini sering dikenal dengan istilah:

> Garbage In, Garbage Out (GIGO)

Artinya, kualitas output sangat dipengaruhi oleh kualitas data dan proses yang digunakan.

Workflow Machine Learning membantu pengembang dan peneliti untuk:

* Membuat proses pengembangan model lebih terstruktur
* Mempermudah evaluasi dan debugging
* Memastikan model dapat digunakan secara nyata
* Mempermudah maintenance dan improvement model

---

# Gambaran Umum Workflow Machine Learning

Alur umum Machine Learning dapat digambarkan sebagai berikut:

```text
Problem Definition
        ↓
Data Collection
        ↓
Data Preprocessing
        ↓
Exploratory Data Analysis
        ↓
Feature Engineering
        ↓
Model Selection
        ↓
Training
        ↓
Evaluation
        ↓
Hyperparameter Tuning
        ↓
Deployment
        ↓
Monitoring & Maintenance
```

---

# 1. Problem Definition

Tahapan ini sering menjadi penyebab utama kegagalan proyek Machine Learning.

Banyak tim langsung membuat model tanpa memahami masalah bisnis atau kebutuhan pengguna.

## Analogi

Bayangkan seseorang meminta Anda membuat kendaraan tercepat.

* Jika kebutuhan sebenarnya adalah mengangkut barang berat → truk lebih cocok
* Jika kebutuhan sebenarnya adalah hemat bahan bakar → motor lebih cocok
* Jika kebutuhan sebenarnya adalah balapan → mobil sport lebih cocok

Begitu juga dalam ML, memahami masalah jauh lebih penting daripada langsung memilih algoritma.

Tahap pertama adalah memahami masalah yang ingin diselesaikan.

## Pertanyaan Penting

* Apa tujuan sistem?
* Jenis prediksi apa yang dibutuhkan?
* Apa output yang diharapkan?
* Bagaimana mengukur keberhasilan model?

## Contoh

| Kasus                | Tujuan                                    |
| -------------------- | ----------------------------------------- |
| Deteksi spam         | Mengklasifikasikan email spam atau tidak  |
| Prediksi harga rumah | Memprediksi harga berdasarkan fitur rumah |
| Voice recognition    | Mengenali ucapan pengguna                 |

---

# 2. Data Collection

Dalam Machine Learning, data adalah bahan bakar utama.

Semakin baik kualitas data, semakin baik kemungkinan model menghasilkan prediksi yang akurat.

## Analogi

Jika model ML adalah seorang mahasiswa, maka data adalah buku dan materi belajar.

Mahasiswa yang belajar dari materi salah akan menghasilkan pemahaman yang salah.

Begitu juga model ML.

Model ML membutuhkan data sebagai bahan pembelajaran.

## Sumber Data

* Database internal
* API
* Sensor IoT
* Web scraping
* Dataset publik

## Contoh Dataset Publik

* Kaggle
* UCI Machine Learning Repository
* HuggingFace Dataset
* Google Dataset Search

## Tantangan

* Data tidak lengkap
* Data bias
* Data imbalance
* Data noisy

---

# 3. Data Preprocessing

Sebagian besar dataset di dunia nyata tidak bersih.

Data sering memiliki:

* Nilai kosong
* Format tidak konsisten
* Data duplikat
* Noise
* Outlier

Karena itu preprocessing menjadi salah satu tahapan paling penting.

## Analogi

Tahap preprocessing mirip seperti mencuci dan memotong bahan makanan sebelum dimasak.

Walaupun sederhana, kualitas hasil akhir sangat dipengaruhi oleh proses ini.

Data mentah biasanya tidak langsung dapat digunakan.

## Tahapan Preprocessing

### Cleaning

* Menghapus data duplikat
* Menangani missing value
* Menghapus outlier

### Transformation

* Normalisasi
* Standardisasi
* Encoding categorical data

### Splitting Data

Umumnya dataset dibagi menjadi:

| Data           | Fungsi         |
| -------------- | -------------- |
| Training Set   | Melatih model  |
| Validation Set | Tuning model   |
| Testing Set    | Evaluasi akhir |

---

# 4. Exploratory Data Analysis (EDA)

EDA dilakukan untuk memahami “cerita” di balik data.

Sebelum membangun model, seorang data scientist harus memahami pola, distribusi, hubungan antar fitur, serta kemungkinan masalah pada data.

## Analogi

EDA mirip seperti dokter memeriksa pasien sebelum memberikan obat.

Dokter tidak langsung memberi resep tanpa memahami kondisi pasien.

Begitu juga data scientist tidak langsung membuat model tanpa memahami data.

EDA digunakan untuk memahami pola pada data.

## Tujuan EDA

* Melihat distribusi data
* Menemukan korelasi
* Mendeteksi anomaly
* Menentukan fitur penting

## Teknik EDA

* Histogram
* Scatter plot
* Correlation matrix
* Boxplot

---

# 5. Feature Engineering

Feature engineering adalah seni mengubah data mentah menjadi informasi yang lebih bermakna bagi model.

Pada banyak kasus, kualitas feature engineering lebih berpengaruh dibanding pemilihan algoritma.

## Analogi

Bayangkan Anda ingin menilai performa mahasiswa.

Data mentah:

* Nilai tugas
* Nilai ujian
* Kehadiran

Feature engineering dapat membuat fitur baru seperti:

* Rata-rata nilai
* Tingkat kedisiplinan
* Konsistensi performa

Fitur baru ini sering membantu model memahami pola lebih baik.

Feature engineering adalah proses membuat fitur yang lebih informatif.

## Contoh

| Data Awal     | Feature Baru     |
| ------------- | ---------------- |
| Tanggal lahir | Umur             |
| Timestamp     | Hari, bulan, jam |
| Kalimat       | TF-IDF vector    |

## Teknik Umum

* Feature extraction
* Feature selection
* Dimensionality reduction
* Embedding

---

# 6. Model Selection

Tidak ada satu algoritma yang terbaik untuk semua kasus.

Pemilihan model bergantung pada:

* Jenis data
* Ukuran dataset
* Kompleksitas masalah
* Kebutuhan interpretasi

## Analogi

Memilih algoritma ML mirip memilih kendaraan.

| Kebutuhan     | Kendaraan   |
| ------------- | ----------- |
| Jalan sempit  | Motor       |
| Angkut barang | Truk        |
| Balapan       | Mobil sport |

Begitu juga model ML:

* Linear Regression cocok untuk masalah sederhana
* Random Forest cocok untuk data tabular
* Deep Learning cocok untuk data kompleks seperti gambar dan suara

Memilih algoritma yang sesuai dengan masalah.

## Jenis Permasalahan

| Jenis          | Contoh Algoritma                   |
| -------------- | ---------------------------------- |
| Classification | Logistic Regression, Random Forest |
| Regression     | Linear Regression, XGBoost         |
| Clustering     | K-Means                            |
| Deep Learning  | CNN, RNN, Transformer              |

## Faktor Pemilihan

* Ukuran dataset
* Kompleksitas data
* Interpretabilitas
* Resource komputasi

---

# 7. Training Model

Training adalah proses model belajar dari data.

Model akan mencoba menemukan pola dengan meminimalkan error menggunakan algoritma optimisasi.

## Analogi

Training mirip seperti siswa belajar mengerjakan soal latihan.

* Awalnya banyak salah
* Setelah latihan berulang, performa meningkat
* Jika terlalu menghafal soal latihan → overfitting

Model belajar dari data training.

## Proses Training

Model mencoba meminimalkan error menggunakan algoritma optimisasi.

## Konsep Penting

* Epoch
* Batch size
* Learning rate
* Loss function
* Optimizer

## Contoh Workflow Training

```python
model.fit(X_train, y_train)
```

---

# 8. Evaluation

Setelah training selesai, model harus diuji.

Tujuannya untuk memastikan model tidak hanya bagus pada data training tetapi juga pada data baru.

## Analogi

Evaluation mirip ujian akhir.

Mahasiswa yang hanya menghafal soal latihan mungkin gagal saat menghadapi soal baru.

Begitu juga model yang mengalami overfitting.

Model perlu diuji performanya.

## Metrics Classification

| Metric    | Fungsi                           |
| --------- | -------------------------------- |
| Accuracy  | Akurasi prediksi                 |
| Precision | Ketepatan prediksi positif       |
| Recall    | Kemampuan menemukan positif      |
| F1-Score  | Harmonic mean precision & recall |

## Metrics Regression

| Metric | Fungsi                  |
| ------ | ----------------------- |
| MAE    | Mean Absolute Error     |
| MSE    | Mean Squared Error      |
| RMSE   | Root Mean Squared Error |

---

# 9. Hyperparameter Tuning

Hyperparameter adalah konfigurasi yang ditentukan sebelum proses training.

Pengaturan hyperparameter yang tepat dapat meningkatkan performa model secara signifikan.

## Analogi

Hyperparameter mirip pengaturan saat memasak.

* Terlalu panas → makanan gosong
* Terlalu dingin → makanan belum matang

Dalam ML:

* Learning rate terlalu besar → model tidak stabil
* Learning rate terlalu kecil → training sangat lama

Hyperparameter mempengaruhi performa model.

## Contoh Hyperparameter

| Algoritma      | Hyperparameter |
| -------------- | -------------- |
| Random Forest  | n_estimators   |
| Neural Network | learning_rate  |
| SVM            | kernel         |

## Teknik Tuning

* Grid Search
* Random Search
* Bayesian Optimization

---

# 10. Deployment

Deployment adalah proses mengubah model menjadi aplikasi yang dapat digunakan pengguna.

Tanpa deployment, model hanya menjadi eksperimen di komputer developer.

## Analogi

Deployment mirip membuka restoran setelah resep berhasil dibuat.

Model akhirnya dapat digunakan oleh pengguna nyata.

Model yang sudah baik dapat digunakan di dunia nyata.

## Bentuk Deployment

* REST API
* Mobile App
* Embedded System
* Cloud Service

## Tools Deployment

* FastAPI
* Flask
* Docker
* Kubernetes
* TensorFlow Serving

---

# 11. Monitoring & Maintenance

Model ML bukan sistem yang selesai sekali dibuat.

Data di dunia nyata terus berubah sehingga performa model dapat menurun seiring waktu.

## Analogi

Monitoring model mirip servis kendaraan.

Walaupun kendaraan awalnya bekerja baik, performanya dapat menurun jika tidak dirawat.

Begitu juga model Machine Learning.

Model ML dapat mengalami penurunan performa seiring waktu.

## Penyebab

* Data drift
* Concept drift
* Perubahan perilaku pengguna

## Monitoring

* Accuracy monitoring
* Error logging
* Retraining otomatis

---

# Studi Kasus Sederhana

## Kasus: Prediksi Kelulusan Mahasiswa

### Workflow

1. Mengumpulkan data mahasiswa
2. Membersihkan data kosong
3. Analisis korelasi IPK dan kehadiran
4. Membuat fitur baru
5. Melatih model klasifikasi
6. Evaluasi model
7. Deploy ke dashboard akademik

---

# Tools dalam Workflow ML

| Tahapan         | Tools                    |
| --------------- | ------------------------ |
| Data Processing | Pandas, NumPy            |
| Visualization   | Matplotlib, Seaborn      |
| Modeling        | Scikit-Learn, TensorFlow |
| Deployment      | FastAPI, Docker          |
| Monitoring      | MLflow, Weights & Biases |

---

# Tantangan dalam Machine Learning Workflow

## Tantangan Teknis

* Data tidak konsisten
* Overfitting
* Resource GPU terbatas

## Tantangan Non-Teknis

* Privasi data
* Etika AI
* Bias algoritma

---

# Best Practice

## Gunakan Version Control

* Git
* DVC

## Dokumentasi

* Catat eksperimen
* Simpan konfigurasi model

## Reproducibility

Pastikan eksperimen dapat dijalankan ulang dengan hasil yang konsisten.

---

# Kesimpulan

Machine Learning Workflow adalah proses sistematis dalam membangun sistem ML yang efektif dan dapat digunakan secara nyata.

Workflow yang baik membantu:

* Mengurangi error
* Mempermudah maintenance
* Mempercepat development
* Meningkatkan kualitas model

---

# Latihan Mahasiswa

## Latihan 1

Identifikasi workflow Machine Learning pada sistem rekomendasi film.

## Latihan 2

Buat diagram workflow untuk proyek NLP sederhana.

## Latihan 3

Cari contoh data drift pada aplikasi nyata.

---

# Referensi

1. Aurélien Géron — Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow
2. Ian Goodfellow — Deep Learning
3. Scikit-Learn Documentation
4. TensorFlow Documentation
5. MLflow Documentation
