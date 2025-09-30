# Predicción del churn de clientes en una empresa de Telecomunicaciones
# 📄 Informe de Solución del Proyecto

## 1️⃣ Pasos del plan realizados

- **Análisis exploratorio de datos (EDA):** Se revisaron las características de la base, detectando variables que podían influir en la predicción y potenciales riesgos de *data leak*.
- **Preprocesamiento de datos:** Incluyó limpieza, codificación de variables y separación en conjunto de entrenamiento y prueba.
- **Detección y resolución de *data leak*:** Se identificó que la columna `DaysContractDuration` filtraba información futura, generando resultados artificialmente altos. Se eliminó o ajustó esta variable.
- **Entrenamiento de múltiples modelos:** Se entrenaron y optimizaron con *GridSearchCV* los modelos:
  - Dummy Classifier
  - Regresión Logística
  - Árbol de Decisión
  - Random Forest
  - Gradient Boosting
- **Evaluación de modelos:** Se analizaron métricas clave (`accuracy`, `precision`, `recall`, `F1-score`, `AUC-ROC`) y se interpretaron resultados.
- **Comparación y selección final:** Se construyó una tabla comparativa y gráficas para identificar el mejor modelo.
- **Documentación de resultados:** Se redactaron interpretaciones detalladas por modelo y conclusiones globales.

---

## 2️⃣ Dificultades encontradas y soluciones aplicadas

**Dificultad:** Resultados iniciales extremadamente altos (cercanos a 1.0 en todas las métricas), lo que indicaba sobreajuste severo.  
**Solución:** Investigación de *data leak* y detección de que `DaysContractDuration` revelaba información posterior al evento de cancelación. Se corrigió removiendo/transformando esa variable.

**Dificultad:** Diferencias en rendimiento entre clases, especialmente baja precisión para la clase 1 (clientes que cancelan).  
**Solución:** Ajuste de hiperparámetros y prueba de varios algoritmos para equilibrar métricas sin sacrificar discriminación general.

---

## 3️⃣ Pasos clave para resolver la tarea

- **Detección del *data leak***: Sin este paso, el modelo habría tenido un rendimiento ficticio y no generalizable.
- **Comparación justa de modelos**: Usar el mismo conjunto de datos y validación cruzada permitió medir de forma coherente.
- **Análisis de métricas más allá del accuracy**: El uso de `precision`, `recall`, `F1` y `AUC-ROC` permitió ver debilidades ocultas en cada modelo.

---

## 4️⃣ Modelo final y nivel de calidad

El modelo final seleccionado fue **Gradient Boosting**, con los hiperparámetros:
- learning_rate=0.1
- max_depth=4
- min_samples_leaf=5
- min_samples_split=20
- n_estimators=100


**Rendimiento en test:**
- Accuracy: **0.71**
- AUC-ROC: **0.8012**
- Precision (Clase 1): **0.55**
- Recall (Clase 1): **0.74**
- F1-Score (Clase 1): **0.63**

Esto indica un modelo **balanceado y con buena capacidad discriminativa**, especialmente útil para identificar clientes que probablemente cancelarán.


