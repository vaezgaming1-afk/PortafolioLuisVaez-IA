---
title: "📝 TAREA 4: Regresión Lineal y Logística - FILL IN THE BLANKS"
date: 2025-09-07
number: 4
status: "Completado"
tags: [Regresión Lineal, Regresión Logística, Machine Learning, Titanic, Modelo Base]
notebook: https://colab.research.google.com/drive/1M58b7dSPSF3mcZJqm2eFefcmYeF5HaAs
drive_viz: https://drive.google.com/drive/folders/1qglTzvqdFPrNMxUhH_MtQFcRrafXEG7x?usp=sharing
dataset: "Titanic - Kaggle"
time_est: "3 h"
time_spent: "—"
---

# 📝 **TAREA 4: Regresión Lineal y Logística - FILL IN THE BLANKS**

## **Resumen ejecutivo**

En esta tarea, exploramos dos modelos de Machine Learning muy comunes: **Regresión Lineal** y **Regresión Logística**. Aplicamos estos modelos en dos contextos diferentes: la predicción del precio de casas en Boston y la clasificación de diagnóstico médico de cáncer de mama. El objetivo fue comparar cómo se desempeñan ambos modelos en diferentes tipos de problemas: **regresión** (predicción de precios) y **clasificación** (predicción de malignidad).

### **Hallazgos clave:**
- **Regresión Lineal** fue utilizada para predecir el precio de casas, con una precisión medida por métricas como **MAE**, **MSE**, **RMSE**, y **R²**.
- **Regresión Logística** se utilizó para predecir si un tumor es **benigno** o **maligno**, con métricas de **precision**, **recall**, **f1-score** y **accuracy**.
- **Logistic Regression** superó al modelo base **DummyClassifier** en precisión, mostrando cómo **Feature Engineering** y **optimización** pueden mejorar el rendimiento.

---

## 🎯 **Objetivos de la tarea**

- [x] **Aplicar la Regresión Lineal** para predecir precios de casas en el dataset de Boston.  
- [x] **Implementar la Regresión Logística** para clasificación binaria en el dataset de diagnóstico médico (cáncer).  
- [x] **Evaluar los modelos** con métricas adecuadas (MAE, RMSE, accuracy, precision, recall, etc.).  
- [x] Comparar el rendimiento de los modelos entrenados contra un **DummyClassifier** como baseline.

---

## ⏱️ **Actividades y tiempos estimados**

| Actividad                                   | Estimado | Real | Nota |
|---|---:|---:|---|
| Configuración inicial en **Google Colab**    | 30 m | **28 m** | Instalación y carga de datos. |
| Preprocesamiento y **Feature Engineering**   | 40 m | **42 m** | Manejo de valores faltantes y creación de nuevas características. |
| Entrenamiento del **DummyClassifier**        | 20 m | **22 m** | Entrenamiento con la estrategia `most_frequent` para baseline. |
| **Entrenamiento de Regresión Logística**     | 30 m | **35 m** | Entrenamiento de modelo y evaluación. |
| Evaluación de modelos y comparación          | 30 m | **32 m** | Comparación entre modelos y métricas. |
| Reflexión y discusión de preguntas           | 15 m | **14 m** | Discusión sobre hallazgos y rendimiento de los modelos. |

> **Totales** — Estimado: **3 h** · Real: **3 h 13 m** · Δ: **+13 m** (**+6%**).

---

## 💡 **Desarrollo: Regresión Lineal - Predecir Precios de Casas**

### **1. Cargar el Dataset de Boston Housing**
El dataset contiene información sobre viviendas en Boston, incluyendo características como **edad de la vivienda**, **número de habitaciones** y **distancia a centros de trabajo**.

```python
url = "https://raw.githubusercontent.com/selva86/datasets/master/BostonHousing.csv"
boston_data = pd.read_csv(url)

# Datos de casas en Boston
print(boston_data.head())
```

### **2. Dividir los datos en entrenamiento y prueba**
- **X (variables independientes):** todas las columnas excepto `medv` (precio).
- **y (variable dependiente):** el precio de las casas.

### **3. Entrenar el modelo de Regresión Lineal**
Usamos el modelo de **LinearRegression** de **scikit-learn** para predecir el precio de las casas.

```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split

X = boston_data.drop('medv', axis=1)
y = boston_data['medv']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Entrenamiento de Regresión Lineal
modelo_regresion = LinearRegression()
modelo_regresion.fit(X_train, y_train)
```

### **4. Evaluación del Modelo**
Evaluamos el modelo utilizando varias métricas como **MAE**, **MSE**, **RMSE**, y **R²**:

```python
from sklearn.metrics import mean_squared_error
import numpy as np

# Predicciones
predicciones = modelo_regresion.predict(X_test)

# Métricas
mae = mean_absolute_error(y_test, predicciones)
mse = mean_squared_error(y_test, predicciones)
rmse = np.sqrt(mse)
r2 = modelo_regresion.score(X_test, y_test)

print(f"MAE: ${mae:.2f}k")
print(f"MSE: {mse:.2f}")
print(f"RMSE: ${rmse:.2f}k")
print(f"R²: {r2:.3f}")
```

### **5. Interpretación**
- **R²** nos dice qué porcentaje de la variabilidad en el precio de las casas es explicado por nuestro modelo.
- **MAE** y **RMSE** nos indican cuánto se alejan, en promedio, nuestras predicciones del precio real.

---

## 🏥 **Regresión Logística - Diagnóstico Médico**

### **1. Cargar el dataset de cáncer de mama**
Utilizamos el dataset **Breast Cancer Wisconsin**, que contiene características sobre tumores (benignos o malignos).

```python
from sklearn.datasets import load_breast_cancer

cancer_data = load_breast_cancer()
X_cancer = pd.DataFrame(cancer_data.data, columns=cancer_data.feature_names)
y_cancer = cancer_data.target
```

### **2. Evaluar el Balance de Clases**
Vemos cuántos tumores son **benignos** y **malignos**:

```python
benignos = (y_cancer == 1).sum()
malignos = (y_cancer == 0).sum()
print(f"Casos benignos: {benignos}")
print(f"Casos malignos: {malignos}")
```

### **3. Entrenar el Modelo de Regresión Logística**
Usamos **LogisticRegression** para predecir si un tumor es **benigno** o **maligno**.

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

# División de datos
X_train_cancer, X_test_cancer, y_train_cancer, y_test_cancer = train_test_split(X_cancer, y_cancer, test_size=0.2, random_state=42)

# Entrenamiento de Regresión Logística
modelo_clasificacion = LogisticRegression(max_iter=5000, random_state=42)
modelo_clasificacion.fit(X_train_cancer, y_train_cancer)
```

### **4. Evaluar el Modelo**
Calculamos la **exactitud**, **precisión**, **recall**, y **f1-score**.

```python
# Predicciones
predicciones_cancer = modelo_clasificacion.predict(X_test_cancer)

# Métricas
accuracy = accuracy_score(y_test_cancer, predicciones_cancer)
precision = precision_score(y_test_cancer, predicciones_cancer)
recall = recall_score(y_test_cancer, predicciones_cancer)
f1 = f1_score(y_test_cancer, predicciones_cancer)

print(f"Accuracy: {accuracy:.3f}")
print(f"Precision: {precision:.3f}")
print(f"Recall: {recall:.3f}")
print(f"F1-Score: {f1:.3f}")
```

### **5. Interpretación**
- **Precision**: De todas las predicciones positivas, ¿cuántas fueron realmente correctas?
- **Recall**: De todos los casos reales positivos, ¿cuántos fueron detectados?
- **F1-Score**: Balance entre precisión y recall, útil cuando hay un desbalance de clases.

---

## ❓ **Preguntas de Reflexión**

1. **¿Cuál es la diferencia principal entre regresión lineal y logística?**
   - **Regresión Lineal** predice valores numéricos continuos (e.g., precio de casas).
   - **Regresión Logística** predice categorías (e.g., maligno vs benigno).

2. **¿Por qué dividimos los datos en entrenamiento y prueba?**
   - Para entrenar el modelo en un conjunto de datos y evaluarlo en un conjunto diferente, asegurando que el modelo generalice bien.

3. **¿Qué significa una exactitud del 95%?**
   - El modelo predice correctamente el 95% de los casos.

4. **¿Cuál es más peligroso: predecir "benigno" cuando es "maligno", o al revés?**
   - Es más peligroso predecir "benigno" cuando en realidad es "maligno", ya que podría no tratar a un paciente con un tumor maligno a tiempo.

---

## 🧑‍💻 **Reproducibilidad**

```bash
pip install -q scikit-learn matplotlib seaborn
```

```python
import pandas as pd
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Cargar datos
data = pd.read_csv('titanic.csv')

# Preparar datos
X = data[['Pclass', 'Sex', 'Age', 'Fare', 'Embarked']]
y = data['Survived']
X = pd.get_dummies(X, drop_first=True)

# Dividir datos
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Regresión Logística
lr = LogisticRegression(max_iter=1000, solver='liblinear', random_state=42)
lr.fit(X_train, y_train)
predictions = lr.predict(X_test)

# Evaluación
print("Accuracy:", accuracy_score(y_test, predictions))
```

---

## 💡 **Conclusión**

El **Feature Engineering** y el entrenamiento de modelos como **Regresión Logística** y **Lineal** nos permitieron obtener **modelos más precisos y efectivos**. Continuaremos ajustando estos modelos y aplicando nuevas técnicas para mejorar la predicción en problemas de regresión y clasificación.

