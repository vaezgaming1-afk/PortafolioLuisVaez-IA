# 📖 **Análisis Exploratorio del Dataset Titanic**

<span class="pill">Completado</span>
<span class="pill">#1</span>
<span class="pill">EDA</span>
<span class="pill">Titanic</span>
<span class="pill">Machine Learning</span>
<span class="pill">Análisis de Datos</span>

[**Ver Notebook en Google Colab**](https://colab.research.google.com/drive/1F0btMIVnncma9EYwR-2togcSPDW35evv)  
[**Ver Visualizaciones en Google Drive**](https://drive.google.com/drive/folders/1qglTzvqdFPrNMxUhH_MtQFcRrafXEG7x?usp=sharing)  
**Dataset:** Titanic — Kaggle  
**Tiempo estimado:** 2 h 30 m

---

## 📑 **Resumen Ejecutivo**

**Objetivo:** Realizar un análisis exploratorio detallado del dataset Titanic, enfocándonos en la relación entre las variables y cómo estas influyen en la supervivencia de los pasajeros. El análisis incluye visualizaciones y la construcción de un modelo preliminar para predecir la supervivencia.

**Datos:** El dataset incluye información sobre los pasajeros del Titanic, como `Sexo`, `Edad`, `Clase`, y `Tarifa`.  
**Hallazgos clave:**  
- La variable **Sexo** es fundamental, con una tasa de supervivencia significativamente más alta para las mujeres.  
- Los pasajeros de **1ª clase** tuvieron una mayor probabilidad de sobrevivir en comparación con los de otras clases.  
- Las visualizaciones muestran patrones clave, como la diferencia de supervivencia según la **edad** y **clase**.

---

## 🎯 **Objetivos del Análisis**

- [x] **Familiarizarse** con el flujo de trabajo en **Google Colab** y cargar el dataset.  
- [x] **Identificar las variables clave** que afectan la supervivencia de los pasajeros.  
- [x] **Realizar visualizaciones** básicas para explorar las relaciones entre variables usando **seaborn** y **matplotlib**.  
- [x] **Evaluar correlaciones** entre las variables numéricas y categóricas del dataset.

---

## ⏰ **Actividades y Tiempos Estimados**

| Actividad                                   | Estimado | Real  | Nota                                                   |
|---------------------------------------------|---------:|-------:|--------------------------------------------------------|
| Configuración del entorno en **Google Colab** | 30 m     | 28 m  | Instalación y carga de datos desde Kaggle.             |
| Exploración inicial del dataset             | 30 m     | 32 m  | Uso de `info()` y `describe()` para obtener resumen.   |
| Visualizaciones básicas                     | 30 m     | 35 m  | Creación de gráficos con **seaborn** y **matplotlib**. |
| Identificación de valores faltantes y outliers | 15 m     | 18 m  | Revisión de valores faltantes y distribuciones.        |
| Análisis de correlaciones                   | 20 m     | 22 m  | Evaluación de correlaciones entre variables numéricas. |
| Reflexión y preguntas de investigación      | 15 m     | 14 m  | Reflexión sobre hallazgos y preguntas clave.           |

> **Totales** — Estimado: **2 h 30 m** · Real: **2 h 39 m** · Δ: **+9 m** (**+6%**)

---

## 🔍 **Desarrollo del Análisis**

**Dataset:**  
- 891 observaciones, 12 variables.  
- Variables clave: `Survived`, `Pclass`, `Sex`, `Age`, `SibSp`, `Parch`, `Fare`, `Embarked`, `Cabin`, `Ticket`, `Name`.

**Análisis Univariado:**  
- **Sexo** y **Pclass** son las variables más relevantes para predecir la supervivencia.  
- La distribución de la **edad** muestra una alta concentración de adultos jóvenes, con pocos pasajeros de edad avanzada.

**Análisis Bivariado:**  
- Se observa una fuerte relación entre **Sexo** y **Survived**, donde las mujeres tienen una tasa de supervivencia mayor.  
- **Pclass** y **Fare** también están correlacionadas fuertemente con la supervivencia: los pasajeros de 1ª clase y con mayores tarifas tienen más probabilidades de sobrevivir.

**Correlaciones:**  
- **Survived** tiene correlaciones positivas con **Pclass** y **Fare**.  
- Las variables **Age** y **SibSp** no presentan correlaciones fuertes, lo que sugiere que no son tan determinantes para la supervivencia.

---

## 📊 **Métricas / Indicadores Exploratorios**

| Indicador                                | Valor / Observación               |
|------------------------------------------|-----------------------------------|
| **Clases (Survived)**                    | 2 (0 = No sobrevivió, 1 = Sobrevivió) |
| **Valores nulos / duplicados**           | 0 / 0                             |
| **Correlación `Pclass` vs `Fare`**       | Alta                              |
| **Correlación `Sex` vs `Survived`**      | Alta                              |

---

## 📚 **Diccionario de Datos**

| Variable     | Unidad | Rango Típico Aproximado | Nota |
|--------------|:------:|:-----------------------:|------|
| `Survived`   | —      | {0, 1}                 | Categórica (0 = No sobrevivió, 1 = Sobrevivió) |
| `Pclass`     | —      | {1, 2, 3}              | Categórica (Clase del pasajero) |
| `Sex`        | —      | {male, female}         | Categórica |
| `Age`        | años   | 0–80+                  | Numérico Continuo |
| `SibSp`      | —      | 0–8                    | Numérico (Hermanos/Esposos a bordo) |
| `Parch`      | —      | 0–6                    | Numérico (Padres/Hijos a bordo) |
| `Fare`       | £      | 0–512.33               | Numérico Continuo (Tarifa pagada) |
| `Embarked`   | —      | {C, Q, S}              | Categórica (Puerto de embarque) |
| `Cabin`      | —      | —                      | Categórica (Número de cabina, muchos nulos) |
| `Ticket`     | —      | —                      | Categórica |
| `Name`       | —      | —                      | Categórica |

---

## 📸 **Evidencias Visuales**

### Visualización de relaciones en el dataset Titanic

1. **Gráfico de supervivencia por clase y sexo:**
   ![Pairplot Titanic](../../assets/ImgPractica1/imgP1.png)
   - **Relación entre variables clave**: Sexo y clase, destacando la mayor tasa de supervivencia para las mujeres y los pasajeros de 1ª clase.

2. **Histograma de edad de los pasajeros:**
   ![Histograma Titanic](../../assets/ImgPractica1/imgP1.2.png)
   - **Distribución de edades**: Mayor concentración de adultos jóvenes.

[**Ver todas las visualizaciones aquí**](https://drive.google.com/drive/folders/1M4qND3ec7dxzzagT3HjI05VCggnWIZzy?usp=sharing)

---
# 🚀 **Explora el Notebook Interactivo en Google Colab** 🎓

Haz clic en el siguiente **botón** para acceder al **notebook** interactivo y realizar el análisis directamente en Google Colab:

[![Ver Notebook en Google Colab](https://img.shields.io/badge/Accede%20al%20Notebook%20en%20Google%20Colab-brightgreen?style=for-the-badge&logo=googlecolab)](https://colab.research.google.com/drive/1F0btMIVnncma9EYwR-2togcSPDW35evv)

> **¡Haz clic para empezar a trabajar directamente en el código y explorar las visualizaciones en tiempo real!**

---

Este diseño utiliza un **badge de color verde brillante** con el logo de Google Colab, lo que hará que se vea llamativo y visualmente atractivo. Además, se proporciona un mensaje claro y amigable para incentivar al usuario a hacer clic en el enlace.

¡Pruébalo y verás cómo resalta!


## 🏆 **Resultados Clave**

- **Variables más relevantes:** **Sexo** y **Pclass**. Las mujeres y los pasajeros de 1ª clase tuvieron mayores probabilidades de sobrevivir.  
- **Desafíos:** Muchos valores faltantes en **Cabin** y **Age**, sugiriendo la necesidad de imputación. Se recomienda imputar **Age** usando la mediana segmentada por **Pclass**.  
- **Próximos pasos:** Construir **modelos de clasificación** para predecir la supervivencia usando **Logistic Regression** y **Random Forest**.

---

## 🧩 **Criterios de Aceptación**

- [x] Dataset explorado con **EDA**.  
- [x] Se identificaron **correlaciones clave** entre las variables más importantes.  
- [x] Visualizaciones y análisis exportados a **Google Drive** para reproducibilidad.

---

## 🚀 **Decisiones Clave**

- **Variables prioritarias**: **Sexo** y **Pclass** son los predictores más importantes para la supervivencia.  
- **Imputación de datos faltantes**: Usar **mediana de Age** por **Pclass** para mejorar la imputación de valores faltantes.  
- **Modelo inicial recomendado**: **Logistic Regression** y **Random Forest** para pruebas iniciales.

---

## 🔄 **Reproducibilidad**
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

🧠 Reflexión Final

El análisis exploratorio del dataset Titanic nos permitió identificar que las variables Sexo y Pclass son determinantes para la supervivencia. Las próximas etapas incluyen la construcción de modelos predictivos más avanzados para mejorar la exactitud y tomar decisiones basadas en estos factores clave.

⏩ Próximos Pasos

Entrenar modelos como Logistic Regression y Random Forest.

Implementar curvas ROC y métricas por clase para análisis de rendimiento del modelo.

Experimentar con imputación avanzada de datos faltantes.