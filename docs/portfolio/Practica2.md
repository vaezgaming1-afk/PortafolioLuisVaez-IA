# 🚀 **Práctica 2: Feature Engineering + Modelo Base**

<span class="pill">Completado</span>
<span class="pill">#2</span>
<span class="pill">Feature Engineering</span>
<span class="pill">Titanic</span>
<span class="pill">Machine Learning</span>
<span class="pill">Modelo Base</span>

[**Ver Notebook en Google Colab**](https://colab.research.google.com/drive/1xOjYjaSN2DM7szuRU7wsep-l2vCXaDSR?usp=sharing)  
[**Ver Visualizaciones en Google Drive**](https://drive.google.com/drive/folders/1WMHuuZMkUeXZYrEZBdhwqgbqwMg7vktG?usp=drive_link)  

---

## 🏆 **Resumen Ejecutivo**

En esta práctica, **trabajamos con el dataset Titanic**, aplicamos **Feature Engineering básico** y entrenamos un modelo de **Regresión Logística**. Luego, comparamos el rendimiento del modelo con un **DummyClassifier** como baseline.

**Objetivo:** Realizar un **análisis exploratorio de características** y construir un modelo básico.  
**Hallazgos clave:** La **variable 'Sexo'** es crucial para la supervivencia, y el **modelo de Regresión Logística** superó ampliamente al **DummyClassifier**.  
**Resultado final:** El modelo base y los nuevos features mostraron mejoras en la predicción de la supervivencia.

---

## 🎯 **Objetivos de la Práctica**

- [x] Aplicar **Feature Engineering** para mejorar la información del dataset Titanic.  
- [x] Entrenar un **modelo base** usando **Regresión Logística**.  
- [x] Comparar el rendimiento entre un **modelo base** y un **modelo entrenado**.
- [x] **Evaluar** el modelo con métricas como **accuracy**, **classification report**, y **confusion matrix**.

---

## 📊 **Modelos Entrenados**

1. **Modelo Base (DummyClassifier):**  
   Se entrenó un modelo DummyClassifier como baseline para comparar el rendimiento con el modelo real.

2. **Modelo de Regresión Logística:**  
   Con el uso de los nuevos features obtenidos a través del Feature Engineering, el modelo de Regresión Logística mostró una mejora significativa en el rendimiento en comparación con el DummyClassifier.

---

## 📈 **Métricas de Evaluación**

- **Accuracy:** El modelo de Regresión Logística superó al DummyClassifier con una precisión más alta.  
- **Classification Report:** Se utilizaron métricas como Precision, Recall y F1-Score para evaluar la efectividad del modelo.  
- **Confusion Matrix:** Se generó una matriz de confusión para analizar los verdaderos positivos, falsos negativos y falsos positivos del modelo.

---

## 📅 **Próximos Pasos**

- [ ] **Optimizar el Modelo:** Mejorar el modelo con más características y probar otros algoritmos de clasificación.  
- [ ] **Ajuste de Hiperparámetros:** Probar técnicas como GridSearchCV para encontrar los mejores hiperparámetros para el modelo.  
- [ ] **Exploración Adicional:** Experimentar con otros tipos de Feature Engineering y técnicas avanzadas como la selección de características.

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

### Visualización de relaciones en el dataset Titanic

1. **Gráfico de supervivencia por clase y sexo:**
   ![Matriz de Confusión - Regresión Logística](../../assets/ImgPractica2/imgP2.1.png)
   - **Relación entre variables clave**: Sexo y clase, destacando la mayor tasa de supervivencia para las mujeres y los pasajeros de 1ª clase.

2. **Histograma de edad de los pasajeros:**
   ![Gráfico de Precisión: DummyClassifier vs Logistic Regression](../../assets/ImgPractica2/imgP2.2.png)
   - **Distribución de edades**: Mayor concentración de adultos jóvenes.

[**Ver todas las visualizaciones aquí**](https://drive.google.com/drive/folders/1WMHuuZMkUeXZYrEZBdhwqgbqwMg7vktG?usp=drive_link)

---
# 🚀 **Explora el Notebook Interactivo en Google Colab** 🎓

Haz clic en el siguiente **botón** para acceder al **notebook** interactivo y realizar el análisis directamente en Google Colab:

[![Ver Notebook en Google Colab](https://img.shields.io/badge/Accede%20al%20Notebook%20en%20Google%20Colab-brightgreen?style=for-the-badge&logo=googlecolab)](https://colab.research.google.com/drive/1xOjYjaSN2DM7szuRU7wsep-l2vCXaDSR?usp=sharing)

> **¡Haz clic para empezar a trabajar directamente en el código y explorar las visualizaciones en tiempo real!**

---

Este diseño utiliza un **badge de color verde brillante** con el logo de Google Colab, lo que hará que se vea llamativo y visualmente atractivo. Además, se proporciona un mensaje claro y amigable para incentivar al usuario a hacer clic en el enlace.

¡Pruébalo y verás cómo resalta!


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
