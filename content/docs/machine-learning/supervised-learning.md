---
title: "Supervised Learning"
date: 2026-04-13
draft: false
weight: 3
---

# Supervised Learning

## Deskripsi Modul
Modul ini membahas algoritma supervised learning yang merupakan fondasi machine learning modern. Mahasiswa akan belajar mengimplementasikan dan mengevaluasi model regresi dan klasifikasi.

### Mengapa Supervised Learning Populer?

**Analogi: Belajar dengan Guru**
- **Guru** = Data berlabel (contoh dengan jawaban)
- **Siswa** = Model ML
- **Ujian** = Prediksi pada data baru

**Fakta Menarik**: 70% masalah ML di dunia nyata menggunakan supervised learning!

## Learning Outcomes Modul
Setelah menyelesaikan modul ini, mahasiswa akan mampu:
- Mengimplementasikan algoritma regresi linear dan polynomial
- Menerapkan algoritma klasifikasi (Logistic Regression, KNN, SVM, Decision Trees)
- Mengevaluasi performa model menggunakan metrik yang tepat
- Melakukan hyperparameter tuning dan model selection
- Memahami bias-variance tradeoff

---

## 1. Regression

### Penjelasan Sederhana
Regression adalah cara memprediksi nilai numerik, seperti menebak harga rumah berdasarkan ukuran dan lokasi.

**Analogi: Menebak Harga Rumah**
- **Input**: Luas tanah, jumlah kamar, lokasi
- **Output**: Harga rumah (angka)
- **Tujuan**: Garis lurus terbaik yang menghubungkan titik-titik data

### Tipe Regression:
- **Linear**: Hubungan lurus (y = mx + c)
- **Polynomial**: Hubungan melengkung (y = ax² + bx + c)
- **Regularized**: Menghindari overfitting dengan penalti

### 1.1 Linear Regression
**Analogi: Garis Tren**
- Mencari garis lurus yang paling mendekati semua titik data
- **Rumus**: y = β₀ + β₁x₁ + β₂x₂ + ... + ε

**Kelebihan**: Sederhana, mudah diinterpretasi
**Kekurangan**: Hanya untuk hubungan linear

#### Implementasi
```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

# Model training - seperti mencari garis terbaik
lr = LinearRegression()
lr.fit(X_train, y_train)

# Prediction - menggunakan garis untuk menebak
y_pred = lr.predict(X_test)

# Evaluation - mengukur seberapa akurat garis tersebut
mse = mean_squared_error(y_test, y_pred)  # Rata-rata error kuadrat
r2 = r2_score(y_test, y_pred)  # Seberapa baik model menjelaskan data (0-1)
print(f"MSE: {mse:.2f}, R²: {r2:.3f}")
```

### 1.2 Polynomial Regression
**Analogi: Garis Lengkung**
- Untuk data yang tidak lurus, gunakan kurva
- **Contoh**: Harga rumah vs ukuran (semakin besar, harga naik tapi melambat)

```python
from sklearn.preprocessing import PolynomialFeatures

# Create polynomial features - menambah fitur x², x³, dll
poly = PolynomialFeatures(degree=2)  # Derajat 2: x, x²
X_poly = poly.fit_transform(X)  # Dari [x] jadi [1, x, x²]

# Fit polynomial regression
poly_reg = LinearRegression()
poly_reg.fit(X_poly, y)
```

### 1.3 Regularization
**Analogi: Denda untuk Model yang Terlalu Rumit**
- **Ridge (L2)**: Denda proporsional dengan kuadrat koefisien
- **Lasso (L1)**: Denda proporsional dengan absolut koefisien (bisa bikin koefisien jadi 0)
- **Elastic Net**: Kombinasi Ridge + Lasso

```python
from sklearn.linear_model import Ridge, Lasso, ElasticNet

# Ridge - seperti denda parkir proporsional kuadrat pelanggaran
ridge = Ridge(alpha=1.0)  # Alpha = kekuatan regularisasi
ridge.fit(X_train, y_train)

# Lasso - bisa bikin fitur yang tidak penting hilang (koefisien = 0)
lasso = Lasso(alpha=0.1)
lasso.fit(X_train, y_train)

print("Ridge coef:", ridge.coef_[:5])
print("Lasso coef:", lasso.coef_[:5])  # Beberapa bisa 0
```

## 2. Classification

### Penjelasan Sederhana
Classification adalah cara memprediksi kategori atau kelas, seperti membedakan email spam atau bukan.

**Analogi: Menebak Jenis Buah**
- **Input**: Warna, bentuk, ukuran buah
- **Output**: Apel, Jeruk, atau Pisang
- **Tujuan**: Garis batas yang memisahkan kelas-kelas

### Algoritma Utama:
- **Logistic Regression**: Probabilitas kelas (0-1)
- **KNN**: Voting dari tetangga terdekat
- **SVM**: Garis pemisah optimal
- **Decision Trees**: Aturan if-then
- **Random Forest**: Hutan keputusan

### 2.1 Logistic Regression
**Analogi: Probabilitas Lulus Ujian**
- Mengubah output linear (-∞ sampai ∞) jadi probabilitas (0-1)
- **Fungsi Sigmoid**: σ(z) = 1/(1+e^(-z))

**Kelebihan**: Sederhana, probabilitas output
**Kekurangan**: Hanya untuk hubungan linear

#### Sigmoid Function
$$\sigma(z) = \frac{1}{1 + e^{-z}}$$

```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, classification_report

# Model training - belajar probabilitas
log_reg = LogisticRegression(random_state=42)
log_reg.fit(X_train, y_train)

# Prediction - menebak kelas
y_pred = log_reg.predict(X_test)
y_prob = log_reg.predict_proba(X_test)  # Probabilitas untuk setiap kelas

# Evaluation
accuracy = accuracy_score(y_test, y_pred)
print(f"Accuracy: {accuracy:.3f}")
print(classification_report(y_test, y_pred))
```

### 2.2 K-Nearest Neighbors (KNN)
**Analogi: Voting Tetangga**
- Lihat 5 orang tetangga terdekat, ikuti mayoritas
- **K=5**: 5 tetangga, mayoritas menang

**Kelebihan**: Sederhana, tidak butuh training
**Kekurangan**: Lambat untuk data besar, sensitif terhadap skala

```python
from sklearn.neighbors import KNeighborsClassifier

# Model training - hanya menyimpan data
knn = KNeighborsClassifier(n_neighbors=5, metric='euclidean')
knn.fit(X_train, y_train)

# Prediction - cari tetangga terdekat
y_pred = knn.predict(X_test)
print(f"KNN dengan k=5 accuracy: {accuracy_score(y_test, y_pred):.3f}")
```

### 2.3 Support Vector Machine (SVM)
**Analogi: Garis Pemisah Terbaik**
- Mencari jalan tol terlebar yang memisahkan dua kelas
- **Margin**: Lebar jalan tol tersebut

**Kelebihan**: Efektif untuk high-dimensional data
**Kekurangan**: Lambat untuk data besar

```python
from sklearn.svm import SVC

# Linear SVM - garis lurus
svm_linear = SVC(kernel='linear', C=1.0)
svm_linear.fit(X_train, y_train)

# RBF SVM - garis lengkung
svm_rbf = SVC(kernel='rbf', gamma='scale', C=1.0)
svm_rbf.fit(X_train, y_train)

print("Linear SVM accuracy:", accuracy_score(y_test, svm_linear.predict(X_test)))
print("RBF SVM accuracy:", accuracy_score(y_test, svm_rbf.predict(X_test)))
```

### 2.4 Decision Trees
**Analogi: Flowchart Keputusan**
- Seri pertanyaan ya/tidak seperti pohon keputusan
- **Root**: Pertanyaan pertama
- **Leaf**: Keputusan akhir

**Kelebihan**: Mudah diinterpretasi, handle kategorikal
**Kekurangan**: Mudah overfitting

```python
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree

# Model training
dt = DecisionTreeClassifier(max_depth=5, random_state=42, criterion='gini')
dt.fit(X_train, y_train)

# Visualize tree - lihat struktur keputusan
plt.figure(figsize=(20,10))
tree.plot_tree(dt, feature_names=X.columns.tolist(), 
               class_names=['Class 0', 'Class 1'], filled=True, rounded=True)
plt.show()

print(f"Tree depth: {dt.get_depth()}")
print(f"Number of leaves: {dt.get_n_leaves()}")
```

### 2.5 Random Forest
**Analogi: Voting Para Ahli**
- Banyak decision trees voting
- **Wisdom of crowd**: Mayoritas lebih pintar dari individu

**Kelebihan**: Robust, feature importance
**Kekurangan**: Lambat training, kurang interpretable

```python
from sklearn.ensemble import RandomForestClassifier

# Model training - ensemble dari banyak trees
rf = RandomForestClassifier(n_estimators=100, max_depth=10, random_state=42, 
                           criterion='gini', bootstrap=True)
rf.fit(X_train, y_train)

# Feature importance - fitur mana yang paling penting
feature_importance = pd.DataFrame({
    'feature': X.columns,
    'importance': rf.feature_importances_
}).sort_values('importance', ascending=False)

print("Top 5 important features:")
print(feature_importance.head())

# OOB Score - akurasi dari data yang tidak digunakan training
print(f"OOB Score: {rf.oob_score_:.3f}")
```

## 3. Model Evaluation

### Penjelasan Sederhana
Model evaluation seperti ujian untuk mengukur seberapa baik model belajar.

**Analogi: Ujian Sekolah**
- **Accuracy**: Berapa persen jawaban benar
- **Precision**: Dari yang dibilang benar, berapa yang benar-benar benar
- **Recall**: Dari yang seharusnya benar, berapa yang berhasil dideteksi

### Regression vs Classification Metrics

#### Regression Metrics
**Analogi: Menebak Harga**
- **MAE**: Rata-rata error absolut (seperti selisih harga rata-rata)
- **MSE**: Rata-rata error kuadrat (penalti lebih besar untuk error besar)
- **RMSE**: Akar MSE (dalam unit yang sama dengan target)
- **R²**: Seberapa baik model menjelaskan variasi data (0-1)

#### Classification Metrics
**Analogi: Deteksi Spam Email**
- **Accuracy**: Total email yang benar diklasifikasi
- **Precision**: Dari email yang dibilang spam, berapa yang benar spam
- **Recall**: Dari email spam sebenarnya, berapa yang terdeteksi
- **F1-Score**: Rata-rata harmonik precision dan recall

### Confusion Matrix
**Analogi: Tabel Kebenaran**
```
                  Predicted
                Spam    Not Spam
Actual   Spam    TP      FN
        Not Spam FP      TN
```

### 3.2 Classification Metrics
```python
from sklearn.metrics import confusion_matrix, roc_curve, auc, classification_report

# Confusion Matrix - tabel kebenaran
cm = confusion_matrix(y_test, y_pred)
print("Confusion Matrix:")
print(cm)

# Visualisasi
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues',
            xticklabels=['Predicted 0', 'Predicted 1'],
            yticklabels=['Actual 0', 'Actual 1'])
plt.title('Confusion Matrix')
plt.show()

# Detailed metrics
print("\nDetailed Classification Report:")
print(classification_report(y_test, y_pred))

# ROC Curve - trade-off antara true positive dan false positive
y_pred_proba = model.predict_proba(X_test)[:,1]  # Probabilitas kelas positif
fpr, tpr, thresholds = roc_curve(y_test, y_pred_proba)
roc_auc = auc(fpr, tpr)

plt.figure(figsize=(8, 6))
plt.plot(fpr, tpr, label=f'AUC = {roc_auc:.3f}', linewidth=2)
plt.plot([0, 1], [0, 1], 'k--', label='Random Guessing')
plt.xlabel('False Positive Rate (1 - Specificity)')
plt.ylabel('True Positive Rate (Sensitivity)')
plt.title('ROC Curve')
plt.legend()
plt.grid(True)
plt.show()
```

### Kapan Menggunakan Metric Mana?

| Skenario | Metric Utama | Alasan |
|----------|-------------|---------|
| **Data balanced** | Accuracy | Sederhana dan intuitif |
| **Data imbalanced** | Precision/Recall/F1 | Fokus pada kelas minoritas |
| **Medical diagnosis** | Recall | Lebih baik false positive daripada false negative |
| **Spam detection** | Precision | Lebih baik false negative daripada false positive |
| **General purpose** | F1-Score | Balance precision dan recall |

## 4. Cross-Validation

### Penjelasan Sederhana
Cross-validation seperti ujian berulang untuk memastikan model benar-benar pintar, bukan hanya hafal.

**Analogi: Ujian di Sekolah yang Berbeda**
- **Tanpa CV**: Belajar di sekolah A, ujian di sekolah A (hasil bagus tapi mungkin hafal)
- **Dengan CV**: Belajar di sekolah A,B,C,D,E, ujian di masing-masing (hasil lebih reliable)

### Mengapa Cross-Validation Penting?
- **Overfitting detection**: Mencegah model yang hanya bagus di data training
- **Reliable evaluation**: Estimasi performa yang lebih akurat
- **Data efficiency**: Semua data digunakan untuk training dan testing

### Teknik Cross-Validation

#### K-Fold Cross-Validation
**Analogi: Rotasi Kelompok Belajar**
- Data dibagi 5 kelompok
- Setiap kelompok bergantian jadi test set
- 4 kelompok sisanya jadi training set

```python
from sklearn.model_selection import cross_val_score, KFold

# K-Fold CV - rotasi test set
kf = KFold(n_splits=5, shuffle=True, random_state=42)
scores = cross_val_score(model, X, y, cv=kf, scoring='accuracy')

print(f"Cross-validation scores: {scores}")
print(f"Mean CV score: {scores.mean():.3f} (+/- {scores.std() * 2:.3f})")

# Visualisasi distribusi scores
plt.figure(figsize=(8, 4))
plt.plot(range(1, 6), scores, 'bo-', linewidth=2, markersize=8)
plt.axhline(y=scores.mean(), color='r', linestyle='--', label=f'Mean: {scores.mean():.3f}')
plt.xlabel('Fold')
plt.ylabel('Accuracy')
plt.title('K-Fold Cross-Validation Scores')
plt.legend()
plt.grid(True)
plt.show()
```

#### Stratified K-Fold
**Analogi: Memastikan Komposisi Kelas Sama**
- Untuk data imbalanced, setiap fold punya proporsi kelas yang sama
- Seperti memastikan setiap kelompok diskusi punya perwakilan semua jenis siswa

```python
from sklearn.model_selection import StratifiedKFold

# Stratified K-Fold - untuk data imbalanced
skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
scores = cross_val_score(model, X, y, cv=skf, scoring='f1_macro')

print(f"Stratified CV scores: {scores}")
print(f"Mean stratified CV: {scores.mean():.3f}")
```

### Kapan Menggunakan Teknik Mana?

| Teknik | Kapan Digunakan | Kelebihan |
|--------|----------------|-----------|
| **K-Fold** | Data balanced, ukuran sedang | Sederhana, comprehensive |
| **Stratified K-Fold** | Data imbalanced | Proporsi kelas terjaga |
| **Leave-One-Out** | Data kecil (< 100) | Maksimal training data |
| **Time Series Split** | Data time series | Respect temporal order |

## 5. Hyperparameter Tuning

### Penjelasan Sederhana
Hyperparameter tuning seperti mencari setting optimal untuk model, seperti mengatur suhu AC yang paling nyaman.

**Analogi: Setting Kompor Gas**
- **Parameter**: Suhu yang dipelajari model (otomatis)
- **Hyperparameter**: Setting kompor (manual) - besar api, jenis tungku
- **Tuning**: Coba berbagai setting untuk masak yang paling enak

### Mengapa Perlu Tuning?
- Model default jarang yang optimal
- Hyperparameter mempengaruhi performa signifikan
- Trade-off antara bias dan variance

### Teknik Tuning

#### Grid Search
**Analogi: Coba Semua Kombinasi**
- Coba semua kombinasi parameter yang mungkin
- Seperti mencoba semua setting AC: suhu 16-30°C, mode auto/fan
- **Kelebihan**: Comprehensive, menemukan optimum global
- **Kekurangan**: Lambat untuk banyak parameter

```python
from sklearn.model_selection import GridSearchCV

# Parameter grid - semua kombinasi yang akan dicoba
param_grid = {
    'n_estimators': [50, 100, 200],        # Jumlah trees
    'max_depth': [None, 10, 20, 30],      # Kedalaman tree
    'min_samples_split': [2, 5, 10],      # Minimum samples untuk split
    'criterion': ['gini', 'entropy']      # Kriteria split
}

# Grid search - exhaustive search
grid_search = GridSearchCV(
    RandomForestClassifier(random_state=42), 
    param_grid, 
    cv=5, 
    scoring='accuracy',
    n_jobs=-1,  # Gunakan semua CPU
    verbose=1
)

grid_search.fit(X_train, y_train)

print(f"Best parameters: {grid_search.best_params_}")
print(f"Best CV score: {grid_search.best_score_:.3f}")
print(f"Test score: {grid_search.score(X_test, y_test):.3f}")

# Visualisasi grid search results
results = pd.DataFrame(grid_search.cv_results_)
pivot = results.pivot_table(values='mean_test_score', 
                           index='param_max_depth', 
                           columns='param_n_estimators')
sns.heatmap(pivot, annot=True, cmap='viridis')
plt.title('Grid Search Results: Max Depth vs N Estimators')
plt.show()
```

#### Random Search
**Analogi: Coba Acak tapi Pintar**
- Coba kombinasi parameter secara acak
- Lebih efisien untuk parameter space yang besar
- **Kelebihan**: Cepat, bisa menemukan optimum lokal yang bagus

```python
from sklearn.model_selection import RandomizedSearchCV
from scipy.stats import randint, uniform

# Random parameter distributions
param_dist = {
    'n_estimators': randint(50, 300),      # Random integer 50-300
    'max_depth': [None] + list(range(5, 31, 5)),  # None atau 5,10,15,...,30
    'min_samples_split': randint(2, 11),   # Random 2-10
    'min_samples_leaf': randint(1, 5),     # Random 1-4
    'bootstrap': [True, False]             # True or False
}

# Random search - sampling acak
random_search = RandomizedSearchCV(
    RandomForestClassifier(random_state=42),
    param_dist,
    n_iter=20,  # Coba 20 kombinasi acak
    cv=5,
    scoring='accuracy',
    n_jobs=-1,
    random_state=42,
    verbose=1
)

random_search.fit(X_train, y_train)

print(f"Best random search params: {random_search.best_params_}")
print(f"Best random search score: {random_search.best_score_:.3f}")

# Bandingkan dengan grid search
print(f"\nPerbandingan:")
print(f"Grid Search best: {grid_search.best_score_:.3f}")
print(f"Random Search best: {random_search.best_score_:.3f}")
```

### Bayesian Optimization
**Analogi: Learning dari Percobaan Sebelumnya**
- Gunakan hasil percobaan sebelumnya untuk memilih percobaan selanjutnya
- Lebih pintar daripada random search

### Tips Tuning

| Algoritma | Hyperparameter Utama | Range Rekomendasi |
|-----------|---------------------|-------------------|
| **Random Forest** | n_estimators, max_depth | 100-500 trees, depth 10-30 |
| **SVM** | C, gamma | C: 0.1-100, gamma: scale/auto |
| **KNN** | n_neighbors | 3-31 (ganjil) |
| **Neural Network** | learning_rate, batch_size | lr: 0.001-0.1, batch: 16-128 |

## 6. Bias-Variance Tradeoff

### Penjelasan Sederhana
Bias-variance tradeoff seperti mencari keseimbangan antara hafal dan paham dalam belajar.

**Analogi: Belajar Matematika**
- **High Bias (Underfitting)**: Siswa yang hanya hafal rumus tanpa paham konsep
- **High Variance (Overfitting)**: Siswa yang hafal semua soal latihan tapi gagal di soal baru
- **Balance**: Siswa yang paham konsep dan bisa menerapkan di berbagai soal

### Konsep Utama

#### Bias (Error Sistemik)
**Analogi: Asumsi yang Salah**
- Model terlalu sederhana (linear untuk data kompleks)
- Selalu salah dengan cara yang sama
- **Contoh**: Mengukur tinggi orang dengan penggaris 30cm

#### Variance (Error Acak)
**Analogi: Terlalu Sensitif**
- Model terlalu kompleks dan hafal noise
- Berubah drastis dengan data training berbeda
- **Contoh**: Hafal semua detail foto tapi gagal kenali orang yang sama dari angle berbeda

#### Overfitting vs Underfitting
```python
# Visualisasi bias-variance tradeoff
from sklearn.metrics import mean_squared_error

def plot_bias_variance_tradeoff():
    """
    Visualisasi tradeoff dengan polynomial degrees
    """
    degrees = range(1, 15)
    train_errors = []
    val_errors = []
    
    for degree in degrees:
        # Create polynomial features
        poly = PolynomialFeatures(degree=degree)
        X_poly = poly.fit_transform(X_train.reshape(-1, 1))
        
        # Train model
        model = LinearRegression()
        model.fit(X_poly, y_train)
        
        # Calculate errors
        y_train_pred = model.predict(X_poly)
        train_error = mean_squared_error(y_train, y_train_pred)
        train_errors.append(train_error)
        
        # Validation error
        X_val_poly = poly.transform(X_val.reshape(-1, 1))
        y_val_pred = model.predict(X_val_poly)
        val_error = mean_squared_error(y_val, y_val_pred)
        val_errors.append(val_error)
    
    # Plot
    plt.figure(figsize=(10, 6))
    plt.plot(degrees, train_errors, 'b-', label='Training Error (Bias)', linewidth=2)
    plt.plot(degrees, val_errors, 'r-', label='Validation Error (Variance)', linewidth=2)
    plt.xlabel('Model Complexity (Polynomial Degree)')
    plt.ylabel('Mean Squared Error')
    plt.title('Bias-Variance Tradeoff')
    plt.legend()
    plt.grid(True)
    
    # Mark optimal point
    optimal_degree = np.argmin(val_errors)
    plt.axvline(x=degrees[optimal_degree], color='g', linestyle='--', 
                label=f'Optimal: degree {degrees[optimal_degree]}')
    plt.legend()
    plt.show()

plot_bias_variance_tradeoff()
```

### Teknik Mengatasi

#### Regularization
**Analogi: Denda untuk Model Rumit**
- Ridge (L2): Penalti kuadrat koefisien besar
- Lasso (L1): Bisa bikin koefisien jadi nol
- Elastic Net: Kombinasi L1 + L2

#### Cross-Validation
**Analogi: Ujian Berulang**
- Pastikan model bagus di berbagai "ujian"
- Deteksi overfitting dengan validation set

#### Ensemble Methods
**Analogi: Voting Para Ahli**
- Random Forest: Banyak decision trees voting
- Gradient Boosting: Model belajar dari kesalahan model sebelumnya

#### Early Stopping
**Analogi: Berhenti Belajar Saat Cukup**
- Stop training ketika validation error naik
- Mencegah overfitting

### Cara Praktis Menangani

| Masalah | Gejala | Solusi |
|---------|--------|--------|
| **High Bias** | Training & validation error tinggi | Tambah complexity, fitur baru |
| **High Variance** | Training error rendah, validation tinggi | Regularization, cross-validation, ensemble |
| **Balanced** | Training & validation error reasonable | Model sudah optimal |

### Contoh Real-World

```python
# Contoh: Regularization untuk atasi overfitting
from sklearn.linear_model import RidgeCV

# Ridge regression dengan cross-validation
ridge_cv = RidgeCV(alphas=[0.1, 1.0, 10.0, 100.0], cv=5)
ridge_cv.fit(X_train, y_train)

print(f"Best alpha: {ridge_cv.alpha_}")
print(f"Training score: {ridge_cv.score(X_train, y_train):.3f}")
print(f"Test score: {ridge_cv.score(X_test, y_test):.3f}")

# Bandingkan dengan model tanpa regularization
lr = LinearRegression()
lr.fit(X_train, y_train)
print(f"\nLinear Regression (no reg):")
print(f"Training score: {lr.score(X_train, y_train):.3f}")
print(f"Test score: {lr.score(X_test, y_test):.3f}")
```

## Latihan Praktis

### Tugas 1: Regression Analysis
1. Implementasikan linear regression pada dataset Boston Housing
2. Bandingkan dengan polynomial regression
3. Evaluasi menggunakan berbagai metrik

### Tugas 2: Classification Project
1. Pilih dataset klasifikasi dari UCI ML Repository
2. Implementasikan minimal 3 algoritma berbeda
3. Lakukan hyperparameter tuning
4. Buat laporan perbandingan performa

### Tugas 3: Model Interpretation
1. Analisis feature importance pada Random Forest
2. Interpretasi koefisien Logistic Regression
3. Buat visualisasi decision boundary

## Studi Kasus
- Prediksi harga rumah
- Klasifikasi spam email
- Deteksi penyakit jantung
- Prediksi churn pelanggan

## Referensi
- "An Introduction to Statistical Learning" - Gareth James et al.
- Scikit-learn Documentation
- "Machine Learning: A Probabilistic Perspective" - Kevin Murphy