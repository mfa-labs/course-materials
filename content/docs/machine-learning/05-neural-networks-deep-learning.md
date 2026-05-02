---
title: "Neural Networks and Deep Learning"
date: 2026-04-13
draft: false
weight: 5
---

# Neural Networks and Deep Learning

## Deskripsi Modul
Modul ini membahas arsitektur neural network dan deep learning. Mahasiswa akan belajar membangun, melatih, dan mengoptimalkan model neural network untuk berbagai tugas.

## Learning Outcomes Modul
Setelah menyelesaikan modul ini, mahasiswa akan mampu:
- Memahami arsitektur dan komponen neural network
- Mengimplementasikan neural network menggunakan TensorFlow/Keras
- Melatih model dengan backpropagation dan gradient descent
- Mengatasi masalah overfitting dan underfitting
- Menerapkan CNN untuk computer vision
- Menerapkan RNN untuk sequential data
- Mengoptimalkan hyperparameter neural network

## 1. Artificial Neural Networks (ANN)

### 1.1 Struktur Neuron
Neuron adalah unit dasar neural network yang terinspirasi dari neuron biologis.

#### Komponen Neuron
- **Input**: x₁, x₂, ..., xₙ
- **Weight**: w₁, w₂, ..., wₙ
- **Bias**: b
- **Activation Function**: f
- **Output**: y = f(∑wᵢxᵢ + b)

### 1.2 Activation Functions
```python
import numpy as np
import matplotlib.pyplot as plt

# Sigmoid
def sigmoid(x):
    return 1 / (1 + np.exp(-x))

# ReLU
def relu(x):
    return np.maximum(0, x)

# Tanh
def tanh(x):
    return np.tanh(x)

# Plot activation functions
x = np.linspace(-5, 5, 100)
plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.plot(x, sigmoid(x))
plt.title('Sigmoid')
plt.grid(True)

plt.subplot(1, 3, 2)
plt.plot(x, relu(x))
plt.title('ReLU')
plt.grid(True)

plt.subplot(1, 3, 3)
plt.plot(x, tanh(x))
plt.title('Tanh')
plt.grid(True)

plt.show()
```

### 1.3 Multi-Layer Perceptron (MLP)
```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.optimizers import Adam

# Create MLP model
model = Sequential([
    Dense(64, activation='relu', input_shape=(input_dim,)),
    Dense(32, activation='relu'),
    Dense(16, activation='relu'),
    Dense(output_dim, activation='softmax')  # or 'sigmoid' for binary
])

# Compile model
model.compile(optimizer=Adam(learning_rate=0.001),
              loss='categorical_crossentropy',  # or 'binary_crossentropy'
              metrics=['accuracy'])

# Model summary
model.summary()
```

## 2. Training Neural Networks

### 2.1 Backpropagation
Algoritma untuk menghitung gradient dan update weight.

### 2.2 Gradient Descent Variants
- **Batch Gradient Descent**: Update weight setelah seluruh dataset
- **Stochastic Gradient Descent (SGD)**: Update weight per sample
- **Mini-batch Gradient Descent**: Update weight per batch

```python
# Training the model
history = model.fit(X_train, y_train,
                    epochs=100,
                    batch_size=32,
                    validation_split=0.2,
                    callbacks=[early_stopping])

# Plot training history
plt.figure(figsize=(12, 4))

plt.subplot(1, 2, 1)
plt.plot(history.history['loss'], label='Training Loss')
plt.plot(history.history['val_loss'], label='Validation Loss')
plt.title('Model Loss')
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.legend()

plt.subplot(1, 2, 2)
plt.plot(history.history['accuracy'], label='Training Accuracy')
plt.plot(history.history['val_accuracy'], label='Validation Accuracy')
plt.title('Model Accuracy')
plt.xlabel('Epoch')
plt.ylabel('Accuracy')
plt.legend()

plt.show()
```

### 2.3 Optimization Algorithms
```python
from tensorflow.keras.optimizers import SGD, RMSprop, Adam, AdamW

# SGD with momentum
sgd = SGD(learning_rate=0.01, momentum=0.9)

# RMSprop
rmsprop = RMSprop(learning_rate=0.001, rho=0.9)

# Adam
adam = Adam(learning_rate=0.001, beta_1=0.9, beta_2=0.999)

# AdamW (Adam with weight decay)
adamw = AdamW(learning_rate=0.001, weight_decay=0.01)
```

## 3. Regularization Techniques

### 3.1 Dropout
```python
from tensorflow.keras.layers import Dropout

model = Sequential([
    Dense(128, activation='relu', input_shape=(input_dim,)),
    Dropout(0.2),  # 20% dropout
    Dense(64, activation='relu'),
    Dropout(0.2),
    Dense(32, activation='relu'),
    Dropout(0.2),
    Dense(output_dim, activation='softmax')
])
```

### 3.2 Batch Normalization
```python
from tensorflow.keras.layers import BatchNormalization

model = Sequential([
    Dense(128, input_shape=(input_dim,)),
    BatchNormalization(),
    Activation('relu'),
    Dropout(0.2),
    Dense(64),
    BatchNormalization(),
    Activation('relu'),
    Dropout(0.2),
    Dense(output_dim, activation='softmax')
])
```

### 3.3 Early Stopping
```python
from tensorflow.keras.callbacks import EarlyStopping

early_stopping = EarlyStopping(
    monitor='val_loss',
    patience=10,
    restore_best_weights=True
)
```

### 3.4 Weight Regularization
```python
from tensorflow.keras.regularizers import l1, l2, l1_l2

model = Sequential([
    Dense(64, activation='relu', input_shape=(input_dim,),
          kernel_regularizer=l2(0.01)),  # L2 regularization
    Dense(32, activation='relu',
          kernel_regularizer=l1_l2(l1=0.01, l2=0.01)),  # Elastic Net
    Dense(output_dim, activation='softmax')
])
```

## 4. Convolutional Neural Networks (CNN)

### 4.1 Arsitektur CNN
```python
from tensorflow.keras.layers import Conv2D, MaxPooling2D, Flatten

model = Sequential([
    # Convolutional layers
    Conv2D(32, (3, 3), activation='relu', input_shape=(height, width, channels)),
    MaxPooling2D((2, 2)),
    Conv2D(64, (3, 3), activation='relu'),
    MaxPooling2D((2, 2)),
    Conv2D(128, (3, 3), activation='relu'),
    MaxPooling2D((2, 2)),
    
    # Fully connected layers
    Flatten(),
    Dense(128, activation='relu'),
    Dropout(0.5),
    Dense(num_classes, activation='softmax')
])

model.compile(optimizer='adam',
              loss='categorical_crossentropy',
              metrics=['accuracy'])
```

### 4.2 Data Augmentation
```python
from tensorflow.keras.preprocessing.image import ImageDataGenerator

train_datagen = ImageDataGenerator(
    rescale=1./255,
    rotation_range=20,
    width_shift_range=0.2,
    height_shift_range=0.2,
    shear_range=0.2,
    zoom_range=0.2,
    horizontal_flip=True,
    fill_mode='nearest'
)

train_generator = train_datagen.flow_from_directory(
    'train_dir',
    target_size=(150, 150),
    batch_size=32,
    class_mode='categorical'
)
```

### 4.3 Transfer Learning
```python
from tensorflow.keras.applications import VGG16
from tensorflow.keras.models import Model

# Load pre-trained VGG16
base_model = VGG16(weights='imagenet', include_top=False, input_shape=(150, 150, 3))

# Freeze base model layers
for layer in base_model.layers:
    layer.trainable = False

# Add custom layers
x = Flatten()(base_model.output)
x = Dense(256, activation='relu')(x)
x = Dropout(0.5)(x)
output = Dense(num_classes, activation='softmax')(x)

# Create model
model = Model(inputs=base_model.input, outputs=output)

# Compile
model.compile(optimizer=Adam(learning_rate=0.0001),
              loss='categorical_crossentropy',
              metrics=['accuracy'])
```

## 5. Recurrent Neural Networks (RNN)

### 5.1 Vanilla RNN
```python
from tensorflow.keras.layers import SimpleRNN

model = Sequential([
    SimpleRNN(64, input_shape=(timesteps, features)),
    Dense(32, activation='relu'),
    Dense(output_dim, activation='softmax')
])
```

### 5.2 Long Short-Term Memory (LSTM)
```python
from tensorflow.keras.layers import LSTM

model = Sequential([
    LSTM(64, input_shape=(timesteps, features), return_sequences=True),
    LSTM(32),
    Dense(16, activation='relu'),
    Dense(output_dim, activation='softmax')
])
```

### 5.3 Gated Recurrent Unit (GRU)
```python
from tensorflow.keras.layers import GRU

model = Sequential([
    GRU(64, input_shape=(timesteps, features), return_sequences=True),
    GRU(32),
    Dense(16, activation='relu'),
    Dense(output_dim, activation='sigmoid')
])
```

## 6. Hyperparameter Tuning

### 6.1 Grid Search untuk Neural Networks
```python
from sklearn.model_selection import GridSearchCV
from tensorflow.keras.wrappers.scikit_learn import KerasClassifier

def create_model(optimizer='adam', neurons=32, dropout_rate=0.2):
    model = Sequential([
        Dense(neurons, activation='relu', input_shape=(input_dim,)),
        Dropout(dropout_rate),
        Dense(neurons//2, activation='relu'),
        Dropout(dropout_rate),
        Dense(output_dim, activation='softmax')
    ])
    model.compile(optimizer=optimizer, loss='categorical_crossentropy', metrics=['accuracy'])
    return model

# Wrap model
model = KerasClassifier(build_fn=create_model, verbose=0)

# Parameter grid
param_grid = {
    'optimizer': ['adam', 'rmsprop'],
    'neurons': [32, 64, 128],
    'dropout_rate': [0.2, 0.3, 0.4],
    'batch_size': [16, 32, 64],
    'epochs': [50, 100]
}

# Grid search
grid = GridSearchCV(estimator=model, param_grid=param_grid, cv=3)
grid_result = grid.fit(X_train, y_train)

print(f"Best: {grid_result.best_score_} using {grid_result.best_params_}")
```

## 7. Advanced Topics

### 7.1 Autoencoders
```python
from tensorflow.keras.layers import Input, Dense

# Encoder
input_layer = Input(shape=(input_dim,))
encoded = Dense(encoding_dim, activation='relu')(input_layer)

# Decoder
decoded = Dense(input_dim, activation='sigmoid')(encoded)

# Autoencoder
autoencoder = Model(input_layer, decoded)
autoencoder.compile(optimizer='adam', loss='binary_crossentropy')

# Training
autoencoder.fit(X_train, X_train, epochs=50, batch_size=256, validation_data=(X_test, X_test))
```

### 7.2 Generative Adversarial Networks (GANs)
```python
from tensorflow.keras.layers import LeakyReLU

# Generator
def build_generator(latent_dim, output_dim):
    model = Sequential([
        Dense(128, input_dim=latent_dim),
        LeakyReLU(alpha=0.2),
        Dense(256),
        LeakyReLU(alpha=0.2),
        Dense(output_dim, activation='tanh')
    ])
    return model

# Discriminator
def build_discriminator(input_dim):
    model = Sequential([
        Dense(256, input_dim=input_dim),
        LeakyReLU(alpha=0.2),
        Dense(128),
        LeakyReLU(alpha=0.2),
        Dense(1, activation='sigmoid')
    ])
    model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])
    return model
```

## Latihan Praktis

### Tugas 1: MLP untuk Klasifikasi
1. Implementasikan MLP untuk dataset MNIST
2. Eksplorasi berbagai arsitektur dan hyperparameter
3. Analisis overfitting dan regularization

### Tugas 2: CNN untuk Computer Vision
1. Bangun CNN untuk klasifikasi CIFAR-10
2. Implementasikan data augmentation
3. Gunakan transfer learning dengan model pre-trained

### Tugas 3: RNN untuk Time Series
1. Implementasikan LSTM untuk prediksi time series
2. Bandingkan dengan ARIMA dan model ML tradisional
3. Analisis performa pada data real

### Tugas 4: Autoencoder Project
1. Implementasikan autoencoder untuk dimensionality reduction
2. Gunakan untuk denoising images
3. Evaluasi rekonstruksi error

## Studi Kasus
- Klasifikasi gambar dengan CNN
- Sentiment analysis dengan RNN
- Generative models untuk text
- Anomaly detection dengan autoencoders
- Time series forecasting

## Referensi
- "Deep Learning" - Ian Goodfellow, Yoshua Bengio, Aaron Courville
- "Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow" - Aurélien Géron
- TensorFlow/Keras Documentation
- Papers: AlexNet, ResNet, Transformer, BERT