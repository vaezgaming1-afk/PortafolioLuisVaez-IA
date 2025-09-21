---
title: "📝 Tarea 5: Validación y Selección de Modelos - Fill in the Blanks"
date: 2025-09-07
number: 5
status: "Completado"
tags: [Machine Learning, Validación de Modelos, Selección de Modelos, Cross-validation]
notebook: https://colab.research.google.com/drive/1F0btMIVnncma9EYwR-2togcSPDW35evv
drive_viz: https://drive.google.com/drive/folders/1qglTzvqdFPrNMxUhH_MtQFcRrafXEG7x?usp=sharing
dataset: "Student Dropout and Academic Success"
time_est: "4 h"
time_spent: "—"
---

# 📝 **TAREA 5: Validación y Selección de Modelos**

## 🎯 **Objetivos Básicos**

En esta tarea, aprenderemos cómo **validar** y **seleccionar modelos** de manera adecuada, utilizando **validación cruzada** y comparando diferentes algoritmos para decidir cuál es el mejor para predecir el **abandono estudiantil** y el **éxito académico**.

- Prevenir **data leakage** usando pipelines.
- Implementar **validación cruzada** robusta.
- Comparar múltiples modelos de forma sistemática.
- Interpretar métricas de **estabilidad** y **selección de modelos**.

## 📋 **Lo que necesitas saber ANTES de empezar:**

Antes de comenzar, es importante que entiendas los siguientes conceptos:

- **Train/test split**: cómo dividir un conjunto de datos en entrenamiento y prueba.
- Diferencia entre **regresión** y **clasificación**.
- Uso básico de **sklearn** y **pandas** para cargar y manejar datos.

---

## 🎓 **Dataset: Predicción de Éxito Estudiantil**

### **Contexto del negocio:**

**Problema:** Predecir el **abandono estudiantil** y el **éxito académico** en la educación superior.

**Objetivo:** Identificar estudiantes en riesgo para implementar **estrategias de apoyo**.

**Valor:** Reducir las tasas de abandono y mejorar la **retención estudiantil**.

### **Características del Dataset:**

- **36 características** relacionadas con las variables **demográficas**, **académicas** y **socioeconómicas** de los estudiantes.
- **Variable objetivo:** Predicción de si un estudiante **abandonó** o **se graduó**.

### **Explorando el Dataset:**

1️⃣ **¿Cuántas muestras y características tiene el dataset?**

- **Muestras:** 4424 estudiantes.
- **Características:** 36 variables (demográficas, académicas y socioeconómicas).

2️⃣ **¿Qué tipos de variables incluye?**

- **Demográficas:** Estado civil, nacionalidad, género, edad al momento de la inscripción, ocupación de los padres.
- **Académicas:** Calificaciones previas, unidades curriculares aprobadas, desempeño académico en semestres anteriores.
- **Socioeconómicas:** Tasa de desempleo, inflación, PIB.

3️⃣ **¿Las clases están balanceadas o desbalanceadas?**

- El dataset tiene un **desbalance** en las clases: más estudiantes graduados que los que abandonaron.

4️⃣ **¿Qué significan las 2 categorías objetivo?**

- **Dropout**: Estudiantes que han abandonado la educación superior.
- **Graduate**: Estudiantes que han completado sus estudios con éxito.

---

## 🔧 **Paso 1: Setup Inicial**

Antes de comenzar con la validación cruzada, cargamos las bibliotecas necesarias y los datos:

```python
!pip install ucimlrepo
```

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LogisticRegression, RidgeClassifier
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.model_selection import train_test_split, cross_val_score, KFold, StratifiedKFold
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.pipeline import Pipeline
from ucimlrepo import fetch_ucirepo
from sklearn.metrics import accuracy_score, classification_report

print("✅ Setup completo!")
```

---

## 🎓 **Paso 2: Cargar y Explorar Datos**

Cargamos el **dataset de estudiantes** y comenzamos a explorar las características y clases para entender mejor los datos.

```python
# Cargar dataset de estudiantes desde UCI
student_data = fetch_ucirepo(id=697)

# Preparar datos
X = student_data.data.features
y = student_data.data.targets

print("Dataset: Student Dropout and Academic Success")
print(f"Estudiantes: {X.shape[0]}, Características: {X.shape[1]}")
print(f"Objetivo: Predecir {len(y.columns)} variable(s)")

# Explorar variable objetivo
target_col = y.columns[0]  # Primera columna objetivo
y_series = y[target_col]
print(f"\nVariable objetivo: {target_col}")
```

### **Distribución de las clases**

Distribución de la variable objetivo:

- **Graduate:** 2209 estudiantes (49.9%)
- **Dropout:** 1421 estudiantes (32.1%)
- **Enrolled:** 794 estudiantes (17.9%)

---

## 🔬 **Parte 1: Validación Cruzada - Validación Robusta**

Para evaluar el rendimiento del modelo y evitar **overfitting**, implementamos la validación cruzada. Usaremos **KFold** y **StratifiedKFold**.

### **Configuración del Pipeline y Validación Cruzada**

```python
# Preparar datos para validación
target_mapping = {0: 'Dropout', 1: 'Enrolled', 2: 'Graduate'}
reverse_mapping = {'Dropout': 0, 'Enrolled': 1, 'Graduate': 2}

# Si y_series contiene strings, convertir a números
y_target = y_series.map(reverse_mapping)

X_features = X  # Características del dataset

# Crear pipeline con escalado de características y clasificación
pipeline_robust = Pipeline([
    ('scaler', StandardScaler()),  # Escalado de características
    ('classifier', LogisticRegression(max_iter=1000, random_state=42))  # Clasificador de regresión logística
])

# Crear KFold básico
kfold = KFold(n_splits=5, shuffle=True, random_state=42)
scores_kfold = cross_val_score(pipeline_robust, X_features, y_target, cv=kfold, scoring='accuracy')

print(f"\nKFOLD RESULTS:")
print(f"   Scores individuales: {scores_kfold}")
print(f"   Media: {scores_kfold.mean():.4f}")
print(f"   Desviación estándar: {scores_kfold.std():.4f}")
print(f"   Resultado: {scores_kfold.mean():.4f} ± {scores_kfold.std():.4f}")
```

---

## 🔬 **Parte 2: Comparación de Modelos**

Evaluamos el rendimiento de varios modelos de clasificación para ver cuál tiene un mejor desempeño en el problema de **abandono estudiantil**:

```python
# Importar librerías necesarias
from sklearn.model_selection import StratifiedKFold, cross_val_score
from sklearn.linear_model import LogisticRegression, RidgeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.pipeline import Pipeline
import matplotlib.pyplot as plt

# Crear un pipeline con diferentes clasificadores
models = {
    'Logistic Regression': Pipeline([('scaler', StandardScaler()), ('classifier', LogisticRegression(max_iter=1000, random_state=42))]),
    'Ridge Classifier': Pipeline([('scaler', StandardScaler()), ('classifier', RidgeClassifier(alpha=1.0, random_state=42))]),
    'Random Forest': Pipeline([('classifier', RandomForestClassifier(n_estimators=100, random_state=42))])
}

# Evaluar cada modelo con validación cruzada
results = {}
for name, model in models.items():
    scores = cross_val_score(model, X_features, y_target, cv=StratifiedKFold(n_splits=5, shuffle=True, random_state=42), scoring='accuracy')
    results[name] = scores
    print(f"{name}: {scores.mean():.4f} ± {scores.std():.4f}")

# Encontrar el modelo con el mejor rendimiento
best_model = max(results, key=lambda k: results[k].mean())
print(f"\nEl mejor modelo es: {best_model}")
```

---

## 📊 **Comparación de Modelos: Visualización**

Visualizamos la comparación entre los diferentes modelos usando un **boxplot** para evaluar la distribución de la precisión.

```python
plt.figure(figsize=(10, 6))
plt.boxplot([results[name] for name in models.keys()], labels=models.keys())
plt.title('Comparación de Modelos: Validación Cruzada')
plt.ylabel('Accuracy')
plt.grid(True, alpha=0.3)
plt.show()
```

---

## 📈 **Análisis de Estabilidad y Selección de Modelos**

El **StratifiedKFold** mostró ser el método más estable debido a la **preservación del balance de clases**. Esto hace que sea más adecuado para datasets con clases desbalanceadas, como es el caso de **abandono estudiantil**.

Recomendación: Usar **StratifiedKFold** para este dataset.

---

## 🎯 **Reflexión y Conclusiones**

- **Estabilidad**: **StratifiedKFold** mostró mayor estabilidad y precisión en los modelos.
- **Modelo Seleccionado**: El **Random Forest** fue el mejor clasificador, seguido por **Logistic Regression**.
- **Métricas Clave**: Se usaron métricas como **accuracy** y **cross-validation** para medir el rendimiento de los modelos.

---




       
       
    
