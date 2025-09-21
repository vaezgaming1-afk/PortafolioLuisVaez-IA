---
title: "📖 Análisis Exploratorio del dataset Titanic"
date: 2025-09-07
number: 1
status: "Completado"
tags: [EDA, Titanic, Machine Learning, Análisis de Datos]
notebook: https://colab.research.google.com/drive/1F0btMIVnncma9EYwR-2togcSPDW35evv
drive_viz: https://drive.google.com/drive/folders/1qglTzvqdFPrNMxUhH_MtQFcRrafXEG7x?usp=sharing
dataset: "Titanic — Kaggle"
time_est: "2 h 30 m"
time_spent: "—"
---

# {{ page.meta.title }}

<span class="pill">{{ page.meta.status }}</span>
<span class="pill">#{{ page.meta.number }}</span>
{% if page.meta.tags %}{% for t in page.meta.tags %}<span class="pill">{{ t }}</span>{% endfor %}{% endif %}

!!! abstract "Resumen ejecutivo"
    **Objetivo:** Realizar un análisis exploratorio del dataset Titanic, evaluar la relación entre variables y realizar visualizaciones para la posterior construcción de modelos.  
    **Datos:** Información de pasajeros del Titanic, incluyendo características como `Sexo`, `Edad`, `Clase`, y `Tarifa`.  
    **Hallazgos:** La variable **Sexo** es determinante para la supervivencia, con las mujeres presentando una tasa de supervivencia más alta. También se observa que las personas de **1ª clase** tuvieron mayor probabilidad de sobrevivir.  
    **Resultado:** Notebook reproducible en Colab, visualizaciones en Drive y lineamientos para la exploración de datos.

**Enlaces rápidos:**  
[Consigna Práctica 1](https://juanfkurucz.com/ucu-ia/ut1/01-eda-titanic/)

---

## Contexto
En esta práctica, se exploran los datos del Titanic para comprender qué factores pudieron haber influido en la supervivencia de los pasajeros. A través de un análisis exploratorio, se buscan patrones y relaciones en las variables del dataset.

## Objetivos
- [x] Familiarizarse con el flujo del análisis y la carga de datos en **Google Colab**.  
- [x] Comprender las principales variables del dataset Titanic.  
- [x] Identificar las variables más relevantes para la supervivencia.  
- [x] Realizar visualizaciones básicas usando **seaborn** y **matplotlib**.

---

## Actividades (con tiempos estimados)

| Actividad                                   | Estimado | Real | Nota |
|---|---:|---:|---|
| Configuración de entorno en Colab            | 30 m | **28 m** | Configuración inicial del entorno y carga de datos desde Kaggle. |
| Carga y exploración inicial del dataset     | 30 m | **32 m** | Carga de datos usando `pandas`, primeros chequeos con `info()` y `describe()`. |
| Visualizaciones básicas                     | 30 m | **35 m** | Creación de gráficos básicos para explorar la relación entre variables. |
| Identificación de valores faltantes y outliers | 15 m | **18 m** | Revisión de valores faltantes, duplicados y análisis de distribuciones. |
| Análisis de correlaciones                   | 20 m | **22 m** | Evaluación de correlaciones entre variables numéricas. |
| Reflexión y preguntas de investigación      | 15 m | **14 m** | Reflexión sobre los hallazgos y preguntas clave para el equipo. |

> **Totales** — Estimado: **2 h 30 m** · Real: **2 h 39 m** · Δ: **+9 m** (**+6%**).

---

## Desarrollo

- **Carga y schema:** 891 observaciones; 12 variables (`Survived`, `Pclass`, `Sex`, `Age`, `SibSp`, `Parch`, `Fare`, `Embarked`, `Cabin`, `Ticket`, `Name`, `Age`). Sin duplicados.  
- **Univariado:** Las variables más relevantes son `Sex`, `Pclass` y `Age`. La distribución de la edad muestra una alta concentración de adultos jóvenes.  
- **Bivariado:** Se observan relaciones fuertes entre `Sex` y `Survived`, y `Pclass` y `Fare`.  
- **Correlaciones:** **Survived** tiene correlaciones positivas con `Pclass` y `Fare`. Las variables `Age` y `SibSp` no presentan correlaciones fuertes.

---

## Métricas / Indicadores exploratorios

| Indicador                                  | Valor / Observación |
|---|---|
| **Clases**                                 | 2 (0 = No sobrevivió, 1 = Sobrevivió) |
| **Nulos / Duplicados**                     | 0 / 0 |
| **Correlación `Pclass` vs `Fare`**         | Alta |
| **Correlación `Sex` vs `Survived`**        | Alta |

---

## Diccionario de datos (plausibilidad)
| Variable       | Unidad | Rango típico aprox. | Nota |
|---|:---:|:---:|---|
| `Survived`     | —     | {0, 1}             | Categórica (0 = No sobrevivió, 1 = Sobrevivió) |
| `Pclass`       | —     | {1, 2, 3}          | Categórica (Clase del pasajero) |
| `Sex`          | —     | {male, female}     | Categórica |
| `Age`          | años  | 0–80+              | Númerico continuo |
| `SibSp`        | —     | 0–8                | Númerico (Número de hermanos/esposos a bordo) |
| `Parch`        | —     | 0–6                | Númerico (Número de padres/hijos a bordo) |
| `Fare`         | £     | 0–512.33           | Númerico continuo (Tarifa pagada) |
| `Embarked`     | —     | {C, Q, S}          | Categórica (Puerto de embarque) |
| `Cabin`        | —     | —                  | Categórica (Número de cabina, muchos nulos) |
| `Ticket`       | —     | —                  | Categórica |
| `Name`         | —     | —                  | Categórica |

---

## Resultados finales

- **Variables clave para supervivencia:** *Sexo* y *Clase*. Las mujeres y los pasajeros de 1ª clase tuvieron mayores probabilidades de sobrevivir.  
- **Desafíos:** Muchos valores faltantes en `Cabin` y `Age`. Se recomienda imputar `Age` con la mediana segmentada por `Pclass` o `Title`.  
- **Recomendación:** Usar **modelos de clasificación** con variables como `Sex`, `Pclass`, `Age` y `Fare`.

!!! tip "Criterios de aceptación"
    - [x] Dataset explorado con **EDA**.  
    - [x] Se identificaron **correlaciones clave**.  
    - [x] Resultados documentados y visualizaciones exportadas a **Google Drive**.

---

## Decisiones clave (ADR-lite)
- **Variables clave:** Priorizar **Sexo** y **Pclass** como predictores principales.  
- **Imputación de valores faltantes:** Usar **mediana** de `Age` por `Pclass` y **HasCabin** en lugar de `Cabin`.  
- **Modelo inicial:** Empezar con **Logistic Regression** y **Random Forest**.

---

## Reproducibilidad

```bash
pip install -q scikit-learn matplotlib seaborn
```

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split

# Cargar datos
data = pd.read_csv('titanic.csv')

# Análisis exploratorio
sns.histplot(data=data, x='Age', hue='Survived', kde=True)
plt.tight_layout()
plt.show()
```

---

## Reflexión

El análisis del dataset Titanic permitió identificar las variables más relevantes para la supervivencia, como **Sexo** y **Pclass**. Los próximos pasos incluyen la construcción de modelos de clasificación para predecir la supervivencia con base en estas variables clave.

## Próximos pasos

- [x] Entrenar modelos como **Logistic Regression** y **Random Forest**.  
- [ ] Implementar **curvas ROC** y **métricas por clase** para el análisis del modelo.  
- [ ] Experimentar con la **imputación avanzada** de datos faltantes.
