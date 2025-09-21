title: "Análisis y Modelado de Enfermedad Cardíaca Coronaria con Machine Learning"
date: 2025-09-21
number: 1
status: "Completado"
tags: [Regresión Logística, Árboles de Decisión, Random Forest, Machine Learning, Enfermedad Cardíaca]
notebook: https://colab.research.google.com/drive/1VOqQYbdGN4PHzd0W5ngqXALFOmIQAcpx
drive_viz: https://drive.google.com/drive/folders/1qglTzvqdFPrNMxUhH_MtQFcRrafXEG7x?usp=sharing
dataset: "Heart Disease (Cleveland) — UCI"
time_est: "5 h 00 m"
time_spent: "—"
---

# {{ page.meta.title }}

<span class="pill">{{ page.meta.status }}</span>
<span class="pill">#{{ page.meta.number }}</span>
{% if page.meta.tags %}{% for t in page.meta.tags %}<span class="pill">{{ t }}</span>{% endfor %}{% endif %}

!!! abstract "Resumen ejecutivo"
    **Objetivo:** aplicar modelos de clasificación binaria para predecir la presencia de enfermedad cardíaca utilizando el dataset de Cleveland.
    **Datos:** 303 observaciones con 13 variables, incluyendo características clínicas y de laboratorio.
    **Hallazgos:** las variables relacionadas con el `pétalo` y las condiciones clínicas tienen la mayor influencia en la predicción.
    **Resultado:** notebook reproducible en Colab con visualizaciones, entrenamiento de modelos y evaluación de rendimiento.
    
**Enlaces rápidos:**  
[Consigna Práctica 1](https://juanfkurucz.com/ucu-id/ut1/01-exploracion-iris/)

---

## Contexto
Este análisis utiliza el dataset de enfermedad cardíaca de Cleveland para explorar técnicas de Machine Learning y clasificación binaria. El objetivo es predecir si un paciente tiene enfermedad cardíaca basándose en características clínicas, aplicando modelos como regresión logística, árboles de decisión y random forest.

## Objetivos
- [x] Familiarizarme con el flujo del portafolio y las técnicas de Machine Learning aplicadas a la clasificación.
- [x] Aplicar modelos de clasificación como **regresión logística**, **árboles de decisión** y **random forest**.
- [x] Evaluar los modelos mediante métricas de rendimiento como **accuracy**, **precision**, **recall**, **AUC-ROC**.
- [x] Organizar outputs en **Google Drive** para facilitar su reproducción.

---

## Actividades (con tiempos estimados)

| Actividad                                   | Estimado | Real | Nota |
|---|---:|---:|---|
| Configuración del repositorio                | 30 m | **28 m** | Estructura básica para almacenamiento de artefactos. |
| Carga de datos y limpieza                    | 45 m | **42 m** | Carga del dataset y limpieza de valores nulos. |
| Análisis exploratorio de datos (EDA)         | 1 h  | **1 h 15 m** | Análisis univariado y bivariado, visualización de correlaciones. |
| Entrenamiento de modelos                     | 1 h  | **1 h 30 m** | Implementación de modelos de regresión logística, árboles de decisión y random forest. |
| Evaluación de modelos y métricas             | 45 m | **40 m** | Evaluación con métricas como AUC-ROC, precision, recall. |
| Optimización y ajuste de hiperparámetros     | 1 h  | **1 h 10 m** | Búsqueda de hiperparámetros con GridSearchCV. |
| Comparación de resultados                    | 30 m | **25 m** | Comparación entre los tres modelos entrenados. |

> **Totales** — Estimado: **5 h 00 m** · Real: **5 h 30 m** · Δ: **+30 m** (**+10%**).  
> **Desvío principal:** tiempo extra en ajuste de hiperparámetros y comparación de modelos.

**Lecciones para la próxima práctica**  
- Reutilizar los pipelines de preprocesamiento para facilitar la implementación de nuevos modelos.  
- Priorizar la evaluación de **recall** en problemas clínicos, dado que los **falsos negativos** tienen un alto costo.

---

## Desarrollo

- **Carga de datos:** Se cargaron 303 observaciones y 13 variables. Se limpiaron valores nulos y se prepararon las columnas para su uso en los modelos.  
- **Univariado y bivariado:** Se realizó un análisis exploratorio utilizando histogramas, boxplots y scatter plots para identificar posibles correlaciones y patrones en los datos.  
- **Modelos aplicados:** Se entrenaron tres modelos: regresión logística, árboles de decisión y random forest. Cada modelo se evaluó utilizando métricas como **accuracy**, **precision**, **recall**, **F1 score**, **AUC-ROC** y **AUC-PR**.  
- **Optimización:** Se utilizaron técnicas de optimización como **GridSearchCV** para afinar los hiperparámetros de los modelos.  
- **Priorización de pacientes:** Se calculó la probabilidad de enfermedad y se priorizaron los pacientes con mayor riesgo utilizando un umbral adaptativo.

<details class="md-details">
  <summary><strong>Paso a paso (ejecución)</strong></summary>

  <ol>
    <li><strong>Preparar entorno</strong>
      <ul>
        <li>Montar Drive en Colab y definir rutas para almacenar artefactos.</li>
      </ul>
    </li>
    <li><strong>Cargar datos</strong>
      <ul>
        <li>Usar `fetch_ucirepo` para cargar el dataset y realizar preprocesamiento.</li>
      </ul>
    </li>
    <li><strong>Chequeos básicos</strong>
      <ul>
        <li>Revisar nulos, duplicados y realizar un análisis inicial con `df.info()` y `describe()`.</li>
      </ul>
    </li>
    <li><strong>EDA</strong>
      <ul>
        <li>Explorar las distribuciones y relaciones entre variables usando visualizaciones.</li>
      </ul>
    </li>
    <li><strong>Entrenamiento de modelos</strong>
      <ul>
        <li>Entrenar los modelos de regresión logística, árbol de decisión y random forest.</li>
      </ul>
    </li>
    <li><strong>Evaluación y métricas</strong>
      <ul>
        <li>Evaluar los modelos con métricas de clasificación y visualización de curvas ROC/PR.</li>
      </ul>
    </li>
  </ol>
</details>

---

## Métricas / Indicadores exploratorios

| Indicador                                  | Valor / Observación |
|---|---|
| Clases                                     | 2 (sano, enfermo) |
| Nulos / Duplicados                         | 0 / 0 |
| Correlación entre `thalach` y `chol`       | Alta |
| Heurística para priorización de pacientes  | Ajuste de umbral en **recall** |

!!! tip "Criterios de aceptación"
    - [x] Dataset auditado y sin problemas de calidad.  
    - [x] Implementación y evaluación de al menos tres modelos.  
    - [x] Resultados exportados y visualizaciones claras.

---

## Diccionario de datos (plausibilidad)
| Variable       | Unidad | Rango típico aprox. | Nota |
|---|:---:|:---:|---|
| `age`          | años  | 29–77 | númerico continuo |
| `sex`          | —     | {0,1} | categórica |
| `cp`           | —     | {0,1,2,3} | categórica |
| `chol`         | mg/dl | 126–564 | númerico continuo |
| `thalach`      | bpm   | 71–202 | númerico continuo |
| `target`       | —     | {0,1} | categórica |

---

## Evidencias

-  [**Práctica en Colab:**](https://colab.research.google.com/drive/1VOqQYbdGN4PHzd0W5ngqXALFOmIQAcpx)
-  [**Visualizaciones (Drive):**](https://drive.google.com/drive/folders/1qglTzvqdFPrNMxUhH_MtQFcRrafXEG7x?usp=sharing) 

<div class="cards-grid media">

  <div class="card">
    <img src="../../assets/Práctica1/roc_curve.png" alt="Curva ROC" loading="lazy">
    <div class="caption">
      Curva ROC para regresión logística
      <small><a href="{{ page.meta.drive_viz }}" target="_blank">Abrir carpeta</a></small>
    </div>
  </div>

  <div class="card">
    <img src="../../assets/Práctica1/decision_tree.png" alt="Árbol de decisión" loading="lazy">
    <div class="caption">
      Árbol de decisión
      <small>Reglas de clasificación</small>
    </div>
  </div>

  <div class="card">
    <img src="../../assets/Práctica1/random_forest.png" alt="Importancia de características - Random Forest" loading="lazy">
    <div class="caption">
      Importancia de características
      <small>Random Forest</small>
    </div>
  </div>

</div>

---

## Decisiones clave (ADR-lite)
- **Variables foco:** priorizar **thalach**, **chol**, y **age**.
- **Preprocesamiento:** realizar estandarización en variables numéricas.
- **Modelo de referencia:** comenzar con **regresión logística** para establecer baseline.
- **Optimización:** usar GridSearchCV para ajustar hiperparámetros de Random Forest y Árbol de Decisión.

!!! warning "Riesgos / Supuestos"
    - **Supuesto**: distribución de clases balanceada.
    - **Riesgo**: sobreajuste en árboles de decisión; mitigación mediante validación cruzada.
    
---

## Reproducibilidad
- Entorno: `python 3.11`; libs: `pandas`, `matplotlib`, `seaborn`, `scikit-learn`.  
- Cómo correr el análisis:

    ```bash
    pip install -q pandas matplotlib seaborn scikit-learn
    ```

    ```python
    from sklearn.datasets import fetch_ucirepo
    import pandas as pd, seaborn as sns
    import matplotlib.pyplot as plt

    heart = fetch_ucirepo(id=45)
    df = heart.data.frame
    sns.scatterplot(data=df, x='thalach', y='chol', hue='target')
    plt.tight_layout()
    plt.show()
    ```

--- 

!!! note "Reflexión"
    El reto fue equilibrar la optimización de los modelos y la interpretación clínica de los errores. La comparación de modelos muestra que **Random Forest** es el más robusto, pero **regresión logística** ofrece un buen baseline. El siguiente paso es ajustar el umbral para maximizar **recall**.

## Próximos posibles pasos:
- [x] Ajustar el umbral para **priorizar recall**.
- [ ] Implementar técnicas de **oversampling** para balancear clases.
- [ ] Comparar modelos de **ensemble** como **AdaBoost** y **Gradient Boosting**.

## Referencias Particulares
- Dataset: UCI Machine Learning Repository — *Heart Disease (Cleveland)*
