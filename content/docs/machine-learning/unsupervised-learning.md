---
title: "Unsupervised Learning"
date: 2026-04-13
draft: false
weight: 4
---

# Unsupervised Learning

## Deskripsi Modul
Modul ini membahas algoritma unsupervised learning yang bekerja tanpa label target. Mahasiswa akan belajar teknik clustering, dimensionality reduction, dan anomaly detection.

## Learning Outcomes Modul
Setelah menyelesaikan modul ini, mahasiswa akan mampu:
- Mengimplementasikan algoritma clustering (K-Means, Hierarchical, DBSCAN)
- Menerapkan teknik dimensionality reduction (PCA, t-SNE)
- Mengevaluasi hasil clustering tanpa ground truth
- Memahami aplikasi unsupervised learning di dunia nyata
- Mendeteksi anomaly menggunakan unsupervised methods

## 1. Clustering

### 1.1 K-Means Clustering
Algoritma partitioning yang membagi data ke dalam k cluster.

#### Algoritma
1. Inisialisasi k centroid secara random
2. Assign setiap titik ke centroid terdekat
3. Update centroid berdasarkan mean titik-titik di cluster
4. Ulangi sampai konvergen

```python
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# K-Means clustering
kmeans = KMeans(n_clusters=3, random_state=42, n_init=10)
clusters = kmeans.fit_predict(X)

# Visualize clusters
plt.scatter(X[:, 0], X[:, 1], c=clusters, cmap='viridis')
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], s=300, c='red', marker='x')
plt.show()
```

#### Menentukan Jumlah Cluster Optimal
```python
from sklearn.metrics import silhouette_score

# Elbow method
inertia = []
silhouette_scores = []
k_range = range(2, 11)

for k in k_range:
    kmeans = KMeans(n_clusters=k, random_state=42, n_init=10)
    kmeans.fit(X)
    inertia.append(kmeans.inertia_)
    silhouette_scores.append(silhouette_score(X, kmeans.labels_))

# Plot elbow curve
plt.figure(figsize=(12, 4))

plt.subplot(1, 2, 1)
plt.plot(k_range, inertia, 'bx-')
plt.xlabel('k')
plt.ylabel('Inertia')
plt.title('Elbow Method')

plt.subplot(1, 2, 2)
plt.plot(k_range, silhouette_scores, 'rx-')
plt.xlabel('k')
plt.ylabel('Silhouette Score')
plt.title('Silhouette Analysis')

plt.show()
```

### 1.2 Hierarchical Clustering
Membuat struktur pohon (dendrogram) dari data.

```python
from scipy.cluster.hierarchy import dendrogram, linkage
from sklearn.cluster import AgglomerativeClustering

# Create linkage matrix
linkage_matrix = linkage(X, method='ward')

# Plot dendrogram
plt.figure(figsize=(10, 7))
dendrogram(linkage_matrix)
plt.title('Hierarchical Clustering Dendrogram')
plt.show()

# Agglomerative clustering
agg_clust = AgglomerativeClustering(n_clusters=3)
clusters = agg_clust.fit_predict(X)
```

### 1.3 DBSCAN (Density-Based Spatial Clustering)
Clustering berdasarkan density, dapat mendeteksi cluster dengan bentuk arbitrer.

```python
from sklearn.cluster import DBSCAN

# DBSCAN clustering
dbscan = DBSCAN(eps=0.5, min_samples=5)
clusters = dbscan.fit_predict(X)

# Visualize
plt.scatter(X[:, 0], X[:, 1], c=clusters, cmap='viridis')
plt.title('DBSCAN Clustering')
plt.show()
```

## 2. Dimensionality Reduction

### 2.1 Principal Component Analysis (PCA)
Mengurangi dimensi dengan mempertahankan variance maksimal.

```python
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler

# Standardize data
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# PCA
pca = PCA(n_components=2)
X_pca = pca.fit_transform(X_scaled)

# Explained variance
print(f"Explained variance ratio: {pca.explained_variance_ratio_}")
print(f"Cumulative explained variance: {pca.explained_variance_ratio_.cumsum()}")

# Visualize
plt.scatter(X_pca[:, 0], X_pca[:, 1], c=y, cmap='viridis')
plt.xlabel('PC1')
plt.ylabel('PC2')
plt.title('PCA Projection')
plt.show()
```

### 2.2 t-Distributed Stochastic Neighbor Embedding (t-SNE)
Teknik non-linear dimensionality reduction untuk visualisasi.

```python
from sklearn.manifold import TSNE

# t-SNE
tsne = TSNE(n_components=2, random_state=42, perplexity=30)
X_tsne = tsne.fit_transform(X_scaled)

# Visualize
plt.scatter(X_tsne[:, 0], X_tsne[:, 1], c=y, cmap='viridis')
plt.title('t-SNE Projection')
plt.show()
```

### 2.3 Autoencoders
Neural network untuk dimensionality reduction.

```python
from tensorflow.keras.layers import Input, Dense
from tensorflow.keras.models import Model

# Encoder
input_dim = X.shape[1]
encoding_dim = 2

input_layer = Input(shape=(input_dim,))
encoder = Dense(encoding_dim, activation='relu')(input_layer)

# Decoder
decoder = Dense(input_dim, activation='sigmoid')(encoder)

# Autoencoder model
autoencoder = Model(input_layer, decoder)

# Encoder model
encoder_model = Model(input_layer, encoder)

# Compile and train
autoencoder.compile(optimizer='adam', loss='mse')
autoencoder.fit(X_scaled, X_scaled, epochs=50, batch_size=32, validation_split=0.2)

# Get encoded representation
X_encoded = encoder_model.predict(X_scaled)
```

## 3. Anomaly Detection

### 3.1 Isolation Forest
Algoritma berbasis tree untuk deteksi anomaly.

```python
from sklearn.ensemble import IsolationForest

# Isolation Forest
iso_forest = IsolationForest(contamination=0.1, random_state=42)
anomaly_scores = iso_forest.fit_predict(X)

# Visualize
plt.scatter(X[:, 0], X[:, 1], c=anomaly_scores, cmap='coolwarm')
plt.title('Isolation Forest Anomaly Detection')
plt.show()
```

### 3.2 One-Class SVM
SVM untuk klasifikasi satu kelas.

```python
from sklearn.svm import OneClassSVM

# One-Class SVM
oc_svm = OneClassSVM(kernel='rbf', gamma='auto', nu=0.1)
anomaly_scores = oc_svm.fit_predict(X)
```

## 4. Evaluation Metrics untuk Unsupervised Learning

### 4.1 Internal Metrics
- Silhouette Score
- Calinski-Harabasz Index
- Davies-Bouldin Index

```python
from sklearn.metrics import silhouette_score, calinski_harabasz_score, davies_bouldin_score

# Silhouette Score
sil_score = silhouette_score(X, clusters)
print(f"Silhouette Score: {sil_score}")

# Calinski-Harabasz Index
ch_score = calinski_harabasz_score(X, clusters)
print(f"Calinski-Harabasz Score: {ch_score}")

# Davies-Bouldin Index
db_score = davies_bouldin_score(X, clusters)
print(f"Davies-Bouldin Score: {db_score}")
```

### 4.2 External Metrics (jika ada ground truth)
- Adjusted Rand Index (ARI)
- Adjusted Mutual Information (AMI)
- Homogeneity, Completeness, V-measure

```python
from sklearn.metrics import adjusted_rand_score, adjusted_mutual_info_score

# ARI
ari = adjusted_rand_score(y_true, clusters)
print(f"Adjusted Rand Index: {ari}")

# AMI
ami = adjusted_mutual_info_score(y_true, clusters)
print(f"Adjusted Mutual Information: {ami}")
```

## 5. Aplikasi Unsupervised Learning

### 5.1 Customer Segmentation
```python
# Load customer data
customer_data = pd.read_csv('customer_data.csv')

# Select features
features = ['age', 'income', 'spending_score']
X = customer_data[features]

# K-Means clustering
kmeans = KMeans(n_clusters=5, random_state=42, n_init=10)
customer_data['segment'] = kmeans.fit_predict(X)

# Analyze segments
segment_analysis = customer_data.groupby('segment')[features].mean()
print(segment_analysis)
```

### 5.2 Image Compression dengan PCA
```python
from sklearn.datasets import load_digits

# Load digits data
digits = load_digits()
X = digits.data
y = digits.target

# PCA for compression
pca = PCA(n_components=0.95)  # Retain 95% variance
X_compressed = pca.fit_transform(X)

print(f"Original dimensions: {X.shape[1]}")
print(f"Compressed dimensions: {X_compressed.shape[1]}")
print(f"Variance retained: {pca.explained_variance_ratio_.sum():.3f}")
```

## Latihan Praktis

### Tugas 1: Clustering Analysis
1. Implementasikan K-Means, Hierarchical, dan DBSCAN pada dataset Iris
2. Bandingkan hasil clustering dengan label sebenarnya
3. Analisis kelebihan dan kekurangan masing-masing algoritma

### Tugas 2: Dimensionality Reduction
1. Terapkan PCA dan t-SNE pada dataset MNIST
2. Visualisasikan hasil reduksi dimensi
3. Bandingkan performa klasifikasi sebelum dan sesudah dimensionality reduction

### Tugas 3: Anomaly Detection Project
1. Pilih dataset dengan anomaly (misal: credit card fraud)
2. Implementasikan Isolation Forest dan One-Class SVM
3. Evaluasi performa deteksi anomaly

## Studi Kasus
- Segmentasi pelanggan e-commerce
- Kompresi gambar
- Deteksi fraud
- Analisis genetik
- Sistem rekomendasi berbasis clustering

## Referensi
- "Unsupervised Learning" - Geoffrey Hinton and Terrence Sejnowski
- "Elements of Statistical Learning" - Hastie, Tibshirani, Friedman
- Scikit-learn Documentation