---
title: "Model Evaluation and Deployment"
date: 2026-04-13
draft: false
weight: 6
---

# Model Evaluation and Deployment

## Deskripsi Modul
Modul ini membahas teknik evaluasi model yang komprehensif dan proses deployment model machine learning ke production. Mahasiswa akan belajar best practices untuk memastikan model dapat diandalkan dan scalable.

## Learning Outcomes Modul
Setelah menyelesaikan modul ini, mahasiswa akan mampu:
- Melakukan evaluasi model yang komprehensif dengan berbagai metrik
- Mengimplementasikan cross-validation yang tepat
- Mengatasi masalah overfitting dan underfitting
- Membuat pipeline ML yang robust
- Mendeploy model ke production environment
- Memantau performa model di production
- Mengimplementasikan A/B testing untuk model comparison

## 1. Advanced Model Evaluation

### 1.1 Cross-Validation Techniques

#### K-Fold Cross-Validation
```python
from sklearn.model_selection import KFold, StratifiedKFold
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

def evaluate_model_cv(model, X, y, cv_folds=5, stratified=True):
    if stratified:
        cv = StratifiedKFold(n_splits=cv_folds, shuffle=True, random_state=42)
    else:
        cv = KFold(n_splits=cv_folds, shuffle=True, random_state=42)
    
    scores = {
        'accuracy': [],
        'precision': [],
        'recall': [],
        'f1': []
    }
    
    for train_idx, val_idx in cv.split(X, y):
        X_train_fold, X_val_fold = X[train_idx], X[val_idx]
        y_train_fold, y_val_fold = y[train_idx], y[val_idx]
        
        model.fit(X_train_fold, y_train_fold)
        y_pred = model.predict(X_val_fold)
        
        scores['accuracy'].append(accuracy_score(y_val_fold, y_pred))
        scores['precision'].append(precision_score(y_val_fold, y_pred, average='weighted'))
        scores['recall'].append(recall_score(y_val_fold, y_pred, average='weighted'))
        scores['f1'].append(f1_score(y_val_fold, y_pred, average='weighted'))
    
    # Print results
    for metric, values in scores.items():
        print(f"{metric.capitalize()}: {np.mean(values):.3f} (+/- {np.std(values) * 2:.3f})")
    
    return scores
```

#### Time Series Cross-Validation
```python
from sklearn.model_selection import TimeSeriesSplit

def time_series_cv(model, X, y, n_splits=5):
    tscv = TimeSeriesSplit(n_splits=n_splits)
    
    scores = []
    for train_idx, val_idx in tscv.split(X):
        X_train, X_val = X[train_idx], X[val_idx]
        y_train, y_val = y[train_idx], y[val_idx]
        
        model.fit(X_train, y_train)
        y_pred = model.predict(X_val)
        score = mean_squared_error(y_val, y_pred)
        scores.append(score)
    
    print(f"Time Series CV MSE: {np.mean(scores):.3f} (+/- {np.std(scores) * 2:.3f})")
    return scores
```

### 1.2 Learning Curves
```python
from sklearn.model_selection import learning_curve

def plot_learning_curve(model, X, y, cv=5, train_sizes=np.linspace(0.1, 1.0, 10)):
    train_sizes, train_scores, val_scores = learning_curve(
        model, X, y, cv=cv, train_sizes=train_sizes, 
        scoring='accuracy', n_jobs=-1
    )
    
    train_mean = np.mean(train_scores, axis=1)
    train_std = np.std(train_scores, axis=1)
    val_mean = np.mean(val_scores, axis=1)
    val_std = np.std(val_scores, axis=1)
    
    plt.figure(figsize=(10, 6))
    plt.plot(train_sizes, train_mean, 'o-', color='blue', label='Training score')
    plt.fill_between(train_sizes, train_mean - train_std, train_mean + train_std, alpha=0.1, color='blue')
    plt.plot(train_sizes, val_mean, 'o-', color='red', label='Validation score')
    plt.fill_between(train_sizes, val_mean - val_std, val_mean + val_std, alpha=0.1, color='red')
    
    plt.xlabel('Training Set Size')
    plt.ylabel('Accuracy Score')
    plt.title('Learning Curve')
    plt.legend(loc='best')
    plt.grid(True)
    plt.show()
```

### 1.3 Validation Curves
```python
from sklearn.model_selection import validation_curve

def plot_validation_curve(model, X, y, param_name, param_range, cv=5):
    train_scores, val_scores = validation_curve(
        model, X, y, param_name=param_name, param_range=param_range,
        cv=cv, scoring='accuracy', n_jobs=-1
    )
    
    train_mean = np.mean(train_scores, axis=1)
    train_std = np.std(train_scores, axis=1)
    val_mean = np.mean(val_scores, axis=1)
    val_std = np.std(val_scores, axis=1)
    
    plt.figure(figsize=(10, 6))
    plt.plot(param_range, train_mean, 'o-', color='blue', label='Training score')
    plt.fill_between(param_range, train_mean - train_std, train_mean + train_std, alpha=0.1, color='blue')
    plt.plot(param_range, val_mean, 'o-', color='red', label='Validation score')
    plt.fill_between(param_range, val_mean - val_std, val_mean + val_std, alpha=0.1, color='red')
    
    plt.xlabel(param_name)
    plt.ylabel('Accuracy Score')
    plt.title(f'Validation Curve for {param_name}')
    plt.legend(loc='best')
    plt.grid(True)
    plt.show()
```

## 2. Model Interpretability

### 2.1 Feature Importance
```python
# For tree-based models
def plot_feature_importance(model, feature_names, top_n=20):
    if hasattr(model, 'feature_importances_'):
        importance = model.feature_importances_
    elif hasattr(model, 'coef_'):
        importance = np.abs(model.coef_[0])
    else:
        print("Model doesn't support feature importance")
        return
    
    # Create dataframe
    feat_importance = pd.DataFrame({
        'feature': feature_names,
        'importance': importance
    }).sort_values('importance', ascending=False).head(top_n)
    
    # Plot
    plt.figure(figsize=(10, 6))
    sns.barplot(x='importance', y='feature', data=feat_importance)
    plt.title('Feature Importance')
    plt.xlabel('Importance')
    plt.ylabel('Features')
    plt.show()
```

### 2.2 SHAP Values
```python
import shap

def explain_model_predictions(model, X_train, X_test, feature_names):
    # Create explainer
    if hasattr(model, 'predict_proba'):
        explainer = shap.TreeExplainer(model)
    else:
        explainer = shap.LinearExplainer(model, X_train)
    
    # Calculate SHAP values
    shap_values = explainer.shap_values(X_test)
    
    # Summary plot
    plt.figure(figsize=(10, 6))
    shap.summary_plot(shap_values, X_test, feature_names=feature_names, show=False)
    plt.show()
    
    # Waterfall plot for single prediction
    if len(shap_values.shape) == 3:  # Multi-class
        shap_values_single = shap_values[0][:, 0]  # First class
    else:
        shap_values_single = shap_values[0]
    
    plt.figure(figsize=(10, 6))
    shap.waterfall_plot(shap.Explanation(
        values=shap_values_single,
        base_values=explainer.expected_value,
        data=X_test.iloc[0],
        feature_names=feature_names
    ), show=False)
    plt.show()
```

### 2.3 Partial Dependence Plots
```python
from sklearn.inspection import partial_dependence, PartialDependenceDisplay

def plot_partial_dependence(model, X, features, feature_names):
    features_idx = [feature_names.index(f) for f in features]
    
    fig, ax = plt.subplots(figsize=(12, 8))
    display = PartialDependenceDisplay.from_estimator(
        model, X, features_idx, feature_names=features,
        ax=ax, kind='both'
    )
    plt.show()
```

## 3. Model Calibration

### 3.1 Probability Calibration
```python
from sklearn.calibration import calibration_curve, CalibratedClassifierCV
import matplotlib.pyplot as plt

def plot_calibration_curve(model, X_test, y_test, n_bins=10):
    # Get predicted probabilities
    y_prob = model.predict_proba(X_test)[:, 1]
    
    # Calculate calibration curve
    prob_true, prob_pred = calibration_curve(y_test, y_prob, n_bins=n_bins, strategy='uniform')
    
    # Plot
    plt.figure(figsize=(8, 6))
    plt.plot(prob_pred, prob_true, 's-', label='Model')
    plt.plot([0, 1], [0, 1], 'k--', label='Perfectly calibrated')
    plt.xlabel('Mean predicted probability')
    plt.ylabel('Fraction of positives')
    plt.title('Calibration Curve')
    plt.legend()
    plt.grid(True)
    plt.show()

# Calibrate model
calibrated_model = CalibratedClassifierCV(model, method='isotonic', cv=5)
calibrated_model.fit(X_train, y_train)
```

## 4. Model Deployment

### 4.1 Saving and Loading Models
```python
import joblib
import pickle
from tensorflow.keras.models import load_model

# Scikit-learn models
def save_sklearn_model(model, filename):
    joblib.dump(model, filename)

def load_sklearn_model(filename):
    return joblib.load(filename)

# TensorFlow/Keras models
def save_keras_model(model, filename):
    model.save(filename)

def load_keras_model(filename):
    return load_model(filename)

# Example usage
# save_sklearn_model(best_model, 'model.pkl')
# loaded_model = load_sklearn_model('model.pkl')
```

### 4.2 Creating ML Pipeline
```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier

def create_ml_pipeline():
    # Create pipeline
    pipeline = Pipeline([
        ('scaler', StandardScaler()),
        ('classifier', RandomForestClassifier(random_state=42))
    ])
    
    return pipeline

# Train pipeline
pipeline = create_ml_pipeline()
pipeline.fit(X_train, y_train)

# Save pipeline
joblib.dump(pipeline, 'ml_pipeline.pkl')

# Load and use pipeline
loaded_pipeline = joblib.load('ml_pipeline.pkl')
predictions = loaded_pipeline.predict(X_test)
```

### 4.3 Flask API untuk Model Serving
```python
from flask import Flask, request, jsonify
import numpy as np

app = Flask(__name__)

# Load model
model = joblib.load('model.pkl')

@app.route('/predict', methods=['POST'])
def predict():
    try:
        # Get data from request
        data = request.get_json()
        
        # Convert to numpy array
        features = np.array(data['features']).reshape(1, -1)
        
        # Make prediction
        prediction = model.predict(features)[0]
        probability = model.predict_proba(features)[0]
        
        # Return response
        response = {
            'prediction': int(prediction),
            'probability': probability.tolist(),
            'status': 'success'
        }
        
        return jsonify(response)
    
    except Exception as e:
        return jsonify({'error': str(e), 'status': 'error'})

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)
```

### 4.4 Docker untuk Model Deployment
```dockerfile
# Dockerfile
FROM python:3.8-slim

WORKDIR /app

# Copy requirements
COPY requirements.txt .
RUN pip install -r requirements.txt

# Copy model and application
COPY model.pkl .
COPY app.py .

EXPOSE 5000

CMD ["python", "app.py"]
```

```yaml
# docker-compose.yml
version: '3.8'

services:
  ml-api:
    build: .
    ports:
      - "5000:5000"
    environment:
      - FLASK_ENV=production
```

## 5. Model Monitoring and Maintenance

### 5.1 Performance Monitoring
```python
def monitor_model_performance(model, X_monitor, y_monitor, threshold=0.8):
    """
    Monitor model performance and alert if below threshold
    """
    predictions = model.predict(X_monitor)
    accuracy = accuracy_score(y_monitor, predictions)
    
    if accuracy < threshold:
        print(f"ALERT: Model accuracy {accuracy:.3f} below threshold {threshold}")
        # Send alert (email, Slack, etc.)
        return False
    else:
        print(f"Model performance OK: {accuracy:.3f}")
        return True
```

### 5.2 Data Drift Detection
```python
from scipy.stats import ks_2samp

def detect_data_drift(X_reference, X_current, threshold=0.05):
    """
    Detect data drift using Kolmogorov-Smirnov test
    """
    drift_detected = False
    
    for i, feature in enumerate(X_reference.columns):
        stat, p_value = ks_2samp(X_reference[feature], X_current[feature])
        
        if p_value < threshold:
            print(f"Data drift detected in feature '{feature}' (p-value: {p_value:.4f})")
            drift_detected = True
    
    if not drift_detected:
        print("No significant data drift detected")
    
    return drift_detected
```

### 5.3 A/B Testing untuk Model Comparison
```python
def ab_test_model_performance(model_a, model_b, X_test, y_test, alpha=0.05):
    """
    Perform A/B test to compare two models
    """
    from statsmodels.stats.proportion import proportions_ztest
    
    # Get predictions
    pred_a = model_a.predict(X_test)
    pred_b = model_b.predict(X_test)
    
    # Calculate accuracies
    acc_a = accuracy_score(y_test, pred_a)
    acc_b = accuracy_score(y_test, pred_b)
    
    print(f"Model A accuracy: {acc_a:.4f}")
    print(f"Model B accuracy: {acc_b:.4f}")
    
    # Perform z-test for proportions
    n = len(y_test)
    successes_a = int(acc_a * n)
    successes_b = int(acc_b * n)
    
    stat, p_value = proportions_ztest([successes_a, successes_b], [n, n])
    
    if p_value < alpha:
        if acc_a > acc_b:
            print("Model A significantly better than Model B")
        else:
            print("Model B significantly better than Model A")
    else:
        print("No significant difference between models")
    
    return p_value
```

## 6. MLOps Best Practices

### 6.1 Version Control untuk Models
```python
import mlflow
import mlflow.sklearn

# Start MLflow run
with mlflow.start_run():
    # Log parameters
    mlflow.log_param("n_estimators", 100)
    mlflow.log_param("max_depth", 10)
    
    # Train model
    model = RandomForestClassifier(n_estimators=100, max_depth=10)
    model.fit(X_train, y_train)
    
    # Log metrics
    accuracy = accuracy_score(y_test, model.predict(X_test))
    mlflow.log_metric("accuracy", accuracy)
    
    # Log model
    mlflow.sklearn.log_model(model, "model")
```

### 6.2 Continuous Integration/Continuous Deployment (CI/CD)
```yaml
# .github/workflows/ml-ci-cd.yml
name: ML CI/CD

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.8'
    
    - name: Install dependencies
      run: |
        pip install -r requirements.txt
        pip install pytest
    
    - name: Run tests
      run: pytest
    
    - name: Train and validate model
      run: python train.py
      
  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
    - name: Deploy to production
      run: echo "Deploy model to production"
```

## Latihan Praktis

### Tugas 1: Comprehensive Model Evaluation
1. Implementasikan berbagai teknik cross-validation
2. Buat learning curves dan validation curves
3. Analisis bias-variance tradeoff

### Tugas 2: Model Interpretability
1. Implementasikan SHAP untuk model Random Forest
2. Buat partial dependence plots
3. Analisis feature importance

### Tugas 3: Model Deployment
1. Buat Flask API untuk serving model
2. Containerize dengan Docker
3. Deploy ke cloud platform (AWS/Heroku)

### Tugas 4: Model Monitoring
1. Implementasikan monitoring sistem
2. Deteksi data drift
3. Buat A/B testing framework

## Studi Kasus
- Deployment model credit scoring
- Monitoring model rekomendasi
- A/B testing untuk model personalization
- MLOps untuk model computer vision

## Referensi
- "Building Machine Learning Pipelines" - Hannes Hapke & Catherine Nelson
- "Machine Learning Engineering" - Andriy Burkov
- MLflow Documentation
- "Practical MLOps" - Noah Gift & Alfredo Deza