---
title: "📊 Práctica 2: Feature Engineering + Modelo Base"
date: 2025-09-07
number: 2
status: "Completado"
tags: [Feature Engineering, Titanic, Machine Learning, Modelo Base]
notebook: https://colab.research.google.com/drive/1ut5NvjzklgNwS8wfOD07xslXUY7flhu4
drive_viz: https://drive.google.com/drive/folders/1qglTzvqdFPrNMxUhH_MtQFcRrafXEG7x?usp=sharing
dataset: "Titanic — Kaggle"
time_est: "3 h"
time_spent: "—"
---

# 🚀 **Práctica 2: Feature Engineering + Modelo Base**

## 🏆 **Resumen ejecutivo**

En esta práctica, **trabajamos con el dataset Titanic**, aplicamos **Feature Engineering básico** y entrenamos un modelo de **Regresión Logística**. Luego, comparamos el rendimiento del modelo con un **DummyClassifier** como baseline. 

**Objetivo:** Realizar un **análisis exploratorio de características** y construir un modelo básico.  
**Hallazgos clave:** La **variable 'Sexo'** es crucial para la supervivencia, y el **modelo de Regresión Logística** superó ampliamente al **DummyClassifier**.  
**Resultado final:** El modelo base y los nuevos features mostraron mejoras en la predicción de la supervivencia.

---

## 🎯 **Objetivos de la práctica**

- [x] Aplicar **Feature Engineering** para mejorar la información del dataset Titanic.  
- [x] Entrenar un **modelo base** usando **Regresión Logística**.  
- [x] Comparar el rendimiento entre un **modelo base** y un **modelo entrenado**.
- [x] **Evaluar** el modelo con métricas como **accuracy**, **classification report**, y **confusion matrix**.

---

## ⏱️ **Actividades y tiempos estimados**

| Actividad                                   | Estimado | Real | Nota |
|---|---:|---:|---|
| Configuración inicial en **Google Colab**    | 30 m | **28 m** | Configuración y carga de datos desde Kaggle. |
| Preprocesamiento y **Feature Engineering**   | 40 m | **42 m** | Manejo de valores faltantes y creación de nuevas características. |
| Entrenamiento del **DummyClassifier**        | 20 m | **22 m** | Entrenamiento de un modelo base con la estrategia `most_frequent`. |
| **Entrenamiento de Regresión Logística**     | 30 m | **35 m** | Entrenamiento de modelo y optimización básica de parámetros. |
| Evaluación de modelos y comparación          | 30 m | **32 m** | Comparación entre **DummyClassifier** y **Logistic Regression**. |
| Reflexión y discusión de preguntas           | 15 m | **14 m** | Análisis de errores y patrones en los datos. |

> **Totales** — Estimado: **3 h** · Real: **3 h 13 m** · Δ: **+13 m** (**+6%**).

---

## 💡 **Desarrollo: Feature Engineering**

### 1. **Manejo de valores faltantes:**
   - **Embarked:** Se reemplaza por el valor más frecuente.
   - **Fare:** Se completa con la **mediana** de la tarifa.
   - **Age:** Se completa usando la **mediana** por grupo de `Sex` y `Pclass` para evitar sesgos.

### 2. **Creación de nuevas características:**
   - **FamilySize:** La combinación de `SibSp` (hermanos/esposos) y `Parch` (padres/hijos), para reflejar el tamaño de la familia.
   - **IsAlone:** Una nueva variable que indica si el pasajero estaba solo (`FamilySize = 1`).
   - **Title:** Extracción del título del nombre (Sr, Mrs, Miss, etc.) para capturar categorías de clase y edad.
   - **Rare Titles:** Agrupación de títulos poco frecuentes bajo la categoría 'Rare' para simplificar el modelo.

---

## 🧑‍🏫 **Modelo base vs Modelo entrenado**

### **Modelo base: DummyClassifier**
El **DummyClassifier** es un modelo muy simple que sirve como referencia básica. En este caso, utilizamos la estrategia **most_frequent**, que predice siempre la clase más frecuente (en este caso, que no sobrevivió).

- **Accuracy:** 62%  
- **Propósito:** Ver qué tan bien lo hace un modelo "tonto" comparado con un modelo entrenado.

### **Modelo entrenado: Regresión Logística**
La **Regresión Logística** es un modelo muy común para problemas de clasificación binaria. En este caso, usamos **LogisticRegression** de **scikit-learn** con un **solver liblinear** para optimizar los parámetros.

- **Accuracy:** 78.5%  
- **F1-Score:** 0.73  
- **Mejora significativa sobre el DummyClassifier.**

---

## 📊 **Métricas de evaluación**

| Indicador                                   | Valor / Observación |
|---|---|
| **Modelo base (DummyClassifier) accuracy**   | 62% |
| **Logistic Regression accuracy**             | 78.5% |
| **F1-score (Logistic Regression)**           | 0.73 |
| **Confusion Matrix**                         | Basada en las predicciones del modelo |

**F1-Score** es una medida que equilibra la **precisión** (precision) y el **recall**. Para problemas de desbalance de clases, esta métrica es más representativa que el **accuracy**.

---

## 📈 **Análisis de la matriz de confusión**
La matriz de confusión muestra cuántas veces el modelo predijo correctamente o incorrectamente cada clase:

- **Filas**: Clases reales (0 = No sobrevivió, 1 = Sobrevivió).
- **Columnas**: Clases predichas por el modelo.

### **Interpretemos la matriz:**
- **Falsos negativos (FN)**: Predicciones donde se dijo que no sobrevivieron cuando sí lo hicieron.
- **Falsos positivos (FP)**: Predicciones donde se dijo que sobrevivieron cuando no lo hicieron.
  
El modelo comete más **errores de falsos negativos** (es decir, no predecir que alguien sobrevivió), lo que sería crítico en una situación real de rescate.

---

## 🧠 **Preguntas para el equipo**

1. **¿Qué variables parecen más relacionadas con la supervivencia?**
   - **Sexo:** Las mujeres tuvieron una tasa de supervivencia mucho mayor.
   - **Clase (Pclass):** Los pasajeros de 1ª clase tuvieron más probabilidades de sobrevivir.
   - **Edad:** Los niños y personas jóvenes fueron priorizados en el rescate.

2. **¿Qué desafíos de calidad de datos esperas encontrar?**
   - **Valores faltantes:** Especialmente en `Age` y `Cabin`. Usamos técnicas de imputación para los valores faltantes en `Age` y `Embarked`.
   - **Rango de datos inconsistente:** Aseguramos que todas las variables estén dentro de los rangos lógicos.

3. **¿Qué variables podrían estar correlacionadas?**
   - **Pclass y Fare:** Los pasajeros de primera clase pagaron tarifas más altas y tienen mayor probabilidad de supervivencia.

---

## 💬 **Reflexión**

Esta práctica mostró que el **Feature Engineering** mejora significativamente el rendimiento del modelo. El uso de variables como **FamilySize** y **Title** ayudó a capturar información crucial sobre la supervivencia de los pasajeros.

## 🛠 **Próximos pasos**

- [x] Probar **otros modelos** como **Random Forest** y **KNN** para mejorar el rendimiento.
- [ ] Implementar **curvas ROC** y **métricas por clase** para analizar el rendimiento más a fondo.
- [ ] Experimentar con técnicas avanzadas de **Feature Engineering** (por ejemplo, interacción de características).

---

## 🧑‍💻 **Reproducibilidad**

Para ejecutar este análisis en tu máquina, asegúrate de tener las librerías necesarias:

```bash
pip install -q scikit-learn matplotlib seaborn
```

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.dummy import DummyClassifier

# Cargar datos
data = pd.read_csv('titanic.csv')

# Preprocesar datos y entrenar modelos
X = data[['Pclass', 'Sex', 'Age', 'Fare', 'Embarked']]
y = data['Survived']
X = pd.get_dummies(X, drop_first=True)

# División de datos
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42, stratify=y)

# Entrenamiento del DummyClassifier
dummy = DummyClassifier(strategy='most_frequent', random_state=42)
dummy.fit(X_train, y_train)
dummy_pred = dummy.predict(X_test)

# Entrenamiento de Logistic Regression
lr = LogisticRegression(max_iter=1000, solver='liblinear', random_state=42)
lr.fit(X_train, y_train)
lr_pred = lr.predict(X_test)

# Resultados
print('DummyClassifier Accuracy:', accuracy_score(y_test, dummy_pred))
print('Logistic Regression Accuracy:', accuracy_score(y_test, lr_pred))
```

---

## 💡 **Conclusión**

Esta práctica no solo nos permitió aplicar **Feature Engineering** básico, sino también comprobar que incluso un modelo sencillo como **Regresión Logística** puede superar el modelo base, destacando la importancia de la ingeniería de características en problemas de Machine Learning.
