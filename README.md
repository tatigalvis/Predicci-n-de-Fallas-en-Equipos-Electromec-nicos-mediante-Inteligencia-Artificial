# 🔧 Predicción de Fallas en Equipos Electromecánicos mediante Inteligencia Artificial

## 📌 Descripción del proyecto

Este proyecto desarrolla un prototipo de **mantenimiento predictivo mediante técnicas de Machine Learning**, utilizando el algoritmo **Random Forest** para identificar patrones asociados con fallas en equipos electromecánicos.

El objetivo es analizar variables operacionales de equipos industriales y desarrollar un modelo de clasificación capaz de estimar la probabilidad de falla, proporcionando información que podría apoyar la toma de decisiones en mantenimiento.

El proyecto fue desarrollado como parte de un **Diplomado en Inteligencia Artificial**.

---

## 🎯 Objetivo general

Desarrollar y evaluar un modelo de Inteligencia Artificial basado en Random Forest para identificar condiciones operacionales asociadas con fallas en equipos electromecánicos y explorar su aplicación como herramienta de apoyo al mantenimiento predictivo.

## 📊 Dataset

Se utilizó el conjunto de datos **AI4I 2020 Predictive Maintenance Dataset**, compuesto por registros sintéticos de condiciones operacionales industriales.

**Características principales:**

- 10.000 registros.
- 14 columnas originales.
- 9.661 registros sin falla (96,61 %).
- 339 registros con falla (3,39 %).
- Variable objetivo: `Machine failure`.

### Variables utilizadas

| Variable | Descripción |
|---|---|
| Type | Tipo de equipo (L, M, H) |
| Air temperature [K] | Temperatura del aire |
| Process temperature [K] | Temperatura del proceso |
| Rotational speed [rpm] | Velocidad de rotación |
| Torque [Nm] | Torque |
| Tool wear [min] | Desgaste de herramientas |
| Machine failure | Variable objetivo: 0 = sin falla, 1 = falla |

---

## 🔍 Metodología

### 1. Análisis exploratorio de datos (EDA)

Se realizó una exploración inicial para comprender la estructura del dataset y analizar el comportamiento de las variables operacionales.

Las actividades incluyeron:

- Identificación de valores nulos y registros duplicados.
- Análisis estadístico descriptivo.
- Evaluación de la distribución de la variable objetivo.
- Identificación de valores extremos.
- Comparación de variables operacionales entre registros con y sin falla.
- Visualización de patrones mediante gráficos.

### 2. Preparación de datos

Se seleccionaron las variables operacionales relevantes para el entrenamiento.

La variable categórica `Type` se transformó mediante **One-Hot Encoding**.

Se excluyeron los identificadores `UDI` y `Product ID`, así como los indicadores específicos de falla `TWF`, `HDF`, `PWF`, `OSF` y `RNF`, para evitar fugas de información (*data leakage*).

### 3. Desarrollo del modelo

Se implementó un modelo de clasificación supervisada utilizando:

**Random Forest Classifier**

Se entrenó un modelo inicial y posteriormente se desarrolló una versión optimizada.

### 4. Optimización

Se aplicó `RandomizedSearchCV` para explorar diferentes configuraciones de hiperparámetros.

También se ajustó el umbral de clasificación de **0,50 a 0,40**, buscando mejorar la identificación de fallas.

### 5. Evaluación

El desempeño se analizó utilizando:

- Accuracy
- Precision
- Recall
- F1-score
- Matriz de confusión
- ROC-AUC
- PR-AUC

---

## 📈 Resultados

### Comparación de modelos

| Métrica | Random Forest inicial | Random Forest optimizado |
|---|---:|---:|
| Accuracy | 97,95 % | 96,30 % |
| Precision | 72,13 % | 47,50 % |
| Recall | 64,71 % | 83,82 % |
| F1-score | 68,00 % | 60,64 % |

El modelo optimizado presentó un mayor Recall, lo que indica una mejor capacidad para identificar las fallas reales en su conjunto de prueba.

Sin embargo, esta mejora estuvo acompañada de una reducción de Precision y un incremento de falsas alarmas.

**Nota metodológica:** La comparación es exploratoria, ya que los modelos se entrenaron con diferentes cantidades de datos. Por tanto, estos resultados no constituyen una demostración definitiva de superioridad del modelo optimizado.

### Matriz de confusión del modelo optimizado

| Resultado | Registros |
|---|---:|
| Verdaderos positivos | 57 |
| Falsos negativos | 11 |
| Falsos positivos | 63 |
| Verdaderos negativos | 1.869 |

El modelo identificó correctamente **57 de las 68 fallas reales** presentes en el conjunto de prueba, alcanzando un Recall del **83,82 %**.

---

## ⚙️ Importancia de las variables

Entre las variables operacionales analizadas, las de mayor importancia relativa aproximada para el Random Forest optimizado fueron:

| Variable | Importancia aproximada |
|---|---:|
| Torque | 32,4 % |
| Velocidad de rotación | 31,4 % |
| Desgaste de herramientas | 19,7 % |
| Temperatura del aire | 9,2 % |
| Temperatura del proceso | 5,8 % |

Estos valores representan la importancia relativa de las variables en el modelo y no deben interpretarse como relaciones causales ni probabilidades individuales de falla.

---

## 🛠️ Tecnologías utilizadas

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Power BI

---

## 🏭 Aplicaciones potenciales

El modelo podría utilizarse como herramienta de apoyo para:

- Identificar condiciones operacionales asociadas con fallas.
- Priorizar inspecciones de mantenimiento.
- Analizar variables relevantes para el funcionamiento de los equipos.
- Apoyar la toma de decisiones mediante información predictiva.
- Visualizar indicadores de mantenimiento industrial.

---

## ⚠️ Limitaciones

Este proyecto presenta algunas limitaciones importantes:

1. El dataset utilizado contiene información sintética.
2. Existe un desbalance significativo entre registros con y sin falla.
3. El modelo optimizado todavía genera falsas alarmas y no identifica todas las fallas.
4. El modelo clasifica condiciones asociadas con fallas, pero no predice el momento exacto de una avería.
5. Se requiere validación adicional con datos industriales reales antes de considerar su implementación operativa.

---

## 🚀 Mejoras futuras

- Validar el modelo con información de equipos industriales reales.
- Explorar técnicas adicionales para manejar el desbalance de clases.
- Comparar Random Forest con otros algoritmos de clasificación.
- Evaluar umbrales de decisión según los costos de mantenimiento.
- Realizar pruebas con nuevos conjuntos de datos independientes.
- Explorar su integración con sistemas de monitoreo industrial.

---

## 🎓 Conclusión

Este proyecto demuestra cómo las técnicas de Machine Learning pueden aplicarse al análisis de condiciones operacionales para identificar patrones asociados con fallas en equipos electromecánicos.

El modelo Random Forest optimizado alcanzó un Recall del **83,82 %**, lo que representa un resultado prometedor para un prototipo experimental de mantenimiento predictivo.

No obstante, la presencia de falsas alarmas y el uso de datos sintéticos hacen necesaria una validación adicional antes de cualquier aplicación industrial.

La Inteligencia Artificial debe considerarse una herramienta complementaria al conocimiento y criterio de los profesionales de mantenimiento.

---

## 👩‍💻 Autora

**Tatiana Almario**

Proyecto académico — Diplomado en Inteligencia Artificial

**Octubre de 2026**
