# Fundamentos de Ciencia de Datos — De los Datos Crudos a la IA Confiable

Repositorio de ejercicios prácticos, notebooks y material de clase de **Fundamentos de Ciencia de Datos**, un recorrido completo por el pipeline analítico moderno: desde la recolección y el diseño muestral de los datos, pasando por su limpieza, transformación y exploración, hasta el entrenamiento de modelos predictivos, su comunicación ejecutiva y la gobernanza ética que debe sostener todo el proceso.

> **Autor:** Roy Umaña — Estudiante de Ing. En Ciencias de Datos E Inteligencia Artificial
> **Formato:** Jupyter Notebooks (`.ipynb`) 

---

## 🧭 Filosofía del curso


> **"Garbage In, Garbage Out."** Si la recolección es deficiente, sesgada o incompleta, cualquier modelo de Inteligencia Artificial posterior fallará irremediablemente, sin importar qué tan sofisticado sea el algoritmo.

Por eso el curso no empieza en el modelado: empieza en el **origen del dato** (scraping, APIs, muestreo) y solo después avanza hacia la limpieza, el análisis y finalmente la Inteligencia Artificial — cerrando con los marcos de gobernanza, ética y comunicación que hacen que esos modelos sean confiables y accionables para una organización.

```
Entendimiento → Recolección de Datos → Almacenamiento → Limpieza/EDA → Modelado IA → Comunicación → Gobernanza
```

---


## 📚 Contenido del curso

### 1️⃣ Fundamentos y Ecosistema de Datos

| Recurso | Descripción |
|---|---|
| 🖥️ *Introducción al Ecosistema y Tipos de Datos* | Clasificación de datos **estructurados, semiestructurados y no estructurados**; proporción global de cada tipo (80% del mundo son datos no estructurados); fuentes primarias vs. secundarias; datos internos vs. Open Data; arquitectura *Lakehouse* combinando SQL, NoSQL y Data Lake. |

**Ideas clave:** la elección de la arquitectura de almacenamiento depende del nivel de estructura, volumen y velocidad de los datos que ingresan a la organización.

---

### 2️⃣ Recolección de Datos: Web Scraping, APIs y Pipelines

| Notebook | Diapositivas | Descripción |
|---|---|---|
| `PrimerScraper.ipynb` | 🖥️ *Web Scraping* | Scraping de `books.toscrape.com` con **Requests + BeautifulSoup**: extracción de título, precio y disponibilidad hacia un DataFrame y export a CSV. Cubre el DOM, `robots.txt`, buenas prácticas éticas (rate limiting) y simulación de errores reales (HTTP 429, selectores rotos). |
| `UsoApi.ipynb` | 🖥️ *Conectando con APIs* | Consumo de la API pública JSONPlaceholder sin autenticación; transformación del JSON anidado a un DataFrame plano. |
| `UsoApiAutorizacion.ipynb` | 🖥️ *Conectando con APIs* | Consumo autenticado con **API Key** contra la API de la NASA (APOD). Cubre arquitectura REST, verbos GET/POST, y matriz de autenticación (API Keys, Bearer Tokens, OAuth). |
| `ConsolidadorDeDatos.ipynb` | 🖥️ *Pipeline de Consumo* | Integración de datos de scraping + API simulada mediante `pd.merge()`, verificación de integridad y persistencia dual en **CSV y Parquet** (comparativa de rendimiento columnar vs. por filas). |

**Ideas clave:** una API es un "puente digital" entre dos software (arquitectura cliente-servidor sobre HTTP); JSON es el estándar de intercambio; Parquet es superior a CSV para consultas analíticas a gran escala por su orientación columnar.

---

### 3️⃣ Muestreo y Diseño Muestral

| Notebook | Diapositivas | Descripción |
|---|---|---|
| `Muestra_Probabilistica.ipynb` | 🖥️ *Fundamentos de Muestreo Probabilística* | Simulación de una población de 10,000 clientes y comparación de **muestreo aleatorio simple, sistemático y estratificado** (con `train_test_split`), midiendo el error respecto a la media poblacional real. |
| `Calculadora_Muestral.ipynb` | 🖥️ *Diseño de muestra No probabilística* | Cálculo del tamaño de muestra para **población finita e infinita** (fórmulas con nivel de confianza *Z* y margen de error), más análisis de sensibilidad. También cubre muestreo no probabilístico (conveniencia, cuotas, bola de nieve, juicio experto) y sesgos de selección, supervivencia y representación. |

**Ideas clave:** *Parámetro* (población, letras griegas: μ, σ) vs. *Estadístico* (muestra, letras romanas: x̄, s); "el modelo no aprende la realidad, aprende la muestra" — un dataset de entrenamiento sesgado (p. ej. 95% hombres) produce un sesgo algorítmico estructural, no corregible después.

---

### 4️⃣ Calidad, Limpieza y Transformación de Datos

| Notebook | Diapositivas | Descripción |
|---|---|---|
| `LimpiezaDatos.ipynb` | 🖥️ *Valores faltantes* | Diagnóstico de nulos con `isnull()`, visualización con **missingno**, clasificación MCAR/MAR/MNAR, y estrategias de tratamiento: eliminación (listwise/pairwise), imputación simple (media/mediana/moda) e imputación avanzada con **KNNImputer**. |
| `Depuracion_De_Anomalias.ipynb` | 🖥️ *Depuración de anomalías* | Detección de duplicados totales/parciales y outliers mediante el **método IQR** (rango intercuartílico) y **Z-Score**; estrategias de tratamiento: *trimming*, *capping* y transformación logarítmica. |
| `Calidad.ipynb` | 🖥️ *Arquitectura de la Fiabilidad del Dato* | Construcción de una "matriz de calidad" con las 6 dimensiones: **exactitud, completitud, consistencia, oportunidad, validez y unicidad**; validación de formato de correo con regex y consistencia lógica (estado civil vs. años casado). |
| `Variables_Categoricas.ipynb` | 🖥️ *Transformación II: Ingeniería de Características* | **Label Encoding** (variables ordinales) vs. **One-Hot Encoding** (variables nominales, `get_dummies`); extracción de características desde fechas (año, mes, día de la semana). |
| 🖥️ *Transformación I: Escalado y Normalización* | — | **Min-Max Scaling** vs. **Estandarización (Z-Score)**: cuándo usar cada técnica según la sensibilidad del algoritmo a outliers (KNN, SVM, redes neuronales vs. árboles de decisión). |
| `Enmascarar_Anonimizar.ipynb` | 🖥️ *Ciclo de vida y seguridad de los datos* | Anonimización con **hashing SHA-256**, enmascaramiento de tarjetas de crédito, y perturbación estadística (ruido gaussiano) sobre salarios — técnicas de protección de PII (Información de Identificación Personal). |

**Ideas clave:** *"la calidad no se soluciona al final, en el modelo de IA — se debe interceptar en la etapa más temprana del linaje de datos"*; la maldición de la dimensionalidad al aplicar One-Hot sobre variables de alta cardinalidad.

---

### 5️⃣ Análisis Exploratorio de Datos (EDA)

| Notebook | Diapositivas | Descripción |
|---|---|---|
| `Analisis_Univariado.ipynb` | 🖥️ *Análisis Univariado* | Medidas de tendencia central (media, mediana, moda), dispersión (desviación estándar, varianza, IQR), sesgo y curtosis sobre variables de edad e ingresos; histogramas y boxplots. |
| `Analisis_Bibariado.ipynb` | 🖥️ *Análisis Bivariado* | Correlación de **Pearson** (relaciones lineales) vs. **Spearman** (relaciones monótonas), mapas de calor, tablas de contingencia, y la advertencia central: *correlación no implica causalidad*. |
| `Analisis_Avanzado.ipynb` | 🖥️ *Análisis Avanzado y Técnicas de Agrupación* | Patrón **Split-Apply-Combine** con `groupby()` y `agg()`; tablas dinámicas (`pivot_table`); visualización avanzada con violin plots vs. boxplots, sobre un dataset simulado de viajes tipo Uber. |
| `Reporte_EDA.ipynb` | 🖥️ *Reportes de EDA y Automatización (AutoEDA)* | Generación de un reporte automatizado con **ydata-profiling**, redacción de un informe ejecutivo con hallazgos de negocio (relación entre tickets de soporte y cancelación de clientes) y próximos pasos para modelado. |

**Ideas clave:** el EDA es "el guardián entre los datos crudos y los algoritmos"; un reporte de AutoEDA acelera el diagnóstico pero no reemplaza el criterio humano ni la narrativa de negocio.

---

### 6️⃣ Machine Learning: Regresión, Clasificación y Regularización

| Notebook | Diapositivas | Descripción |
|---|---|---|
| `RegresionLineal.ipynb` | 🖥️ *Problema Predictivo y Regresión Lineal* | Formulación del problema predictivo, entrenamiento de una **Regresión Lineal Simple** (Mínimos Cuadrados Ordinarios) sobre horas de estudio vs. notas de examen; interpretación de β₀ (intercepto) y β₁ (pendiente). |
| `Regresion_Logistica.ipynb` | 🖥️ *Regresión Logística, Umbrales y Métricas de Error* | Función **Sigmoide**, matriz de confusión (VP/VN/FP/FN), y el impacto de mover el **umbral de decisión** (0.2, 0.5, 0.8) en el trade-off entre falsos positivos y falsos negativos para un modelo de riesgo bancario. |
| `Optimizacion_y_Generalizacion.ipynb` | 🖥️ *ML: Optimización y Generalización* | Simulación manual del **Descenso del Gradiente** (efecto de la tasa de aprendizaje α), y **validación cruzada K-Fold** (`cross_val_score`) para estimar el error de generalización real de un modelo. |
| `Regularizacion_Lasso.ipynb` | 🖥️ *Regularización* | Dilema **sesgo-varianza**, comparación de un polinomio de grado 10 con y sin **regularización Lasso (L1)**, mostrando cómo se reduce el sobreajuste (*overfitting*) y se controla el MSE de prueba. |

**Ideas clave:** *Error Total = Sesgo² + Varianza + Ruido Irreducible*; Ridge (L2) encoge coeficientes suavemente, Lasso (L1) los lleva a cero exacto (selección automática de variables); un modelo con 98% de precisión en entrenamiento y 72% en validación está sobreajustado, no es exitoso.

---

### 7️⃣ Comunicación de Datos y Storytelling

| Notebook | Diapositivas | Descripción |
|---|---|---|
| `Diseño_grafico.ipynb` | 🖥️ *Gramática Visual y Data Storytelling* | Dashboard interactivo con **Plotly** (`go.Figure`) comparando ventas reales vs. meta por región, aplicando atributos pre-atentivos (color estratégico) y evitando gráficos 3D engañosos. |
| `Traduccion_Financiera.ipynb` | 🖥️ *Métricas Técnicas → Impacto Financiero* | Traducción de métricas técnicas (Recall, MAE, MSE, matriz de confusión) a un **reporte de impacto financiero** para gerencia: ahorro por fallas detectadas, costo de falsas alarmas y retorno neto de un modelo de mantenimiento predictivo. |

**Ideas clave:** *"todo error técnico se traduce inevitablemente en dinero o en horas operativas"*; principios éticos de visualización — evitar ejes truncados, escalas distorsionadas y la paradoja de Simpson.

---

### 8️⃣ Gobernanza, Ética y Seguridad de Datos

| Recurso | Descripción |
|---|---|
| 🖥️ *Gobernanza de Datos y Modelos de Almacenamiento* | Roles del ecosistema de gobernanza (CDO, Propietario, Custodio, Arquitecto de datos); comparativa **SQL (OLTP, esquema rígido)** vs. **NoSQL (flexible, escalabilidad horizontal)**; **Data Warehouse** vs. **Data Lake** en el almacenamiento analítico. |
| 🖥️ *Arquitectura de la Fiabilidad del Dato* | Ecuación de la fiabilidad = Dimensiones de Calidad × Linaje Trazable; el "Compás de 3 preguntas" del linaje (¿de dónde viene? ¿a dónde va? ¿cómo cambió?); la importancia de interceptar errores de calidad temprano en el pipeline. |
| 🖥️ *Ciclo de vida y seguridad de los datos* | Modelo de **defensa en profundidad**: encriptación en tránsito/reposo, **RBAC** (control de acceso basado en roles), enmascaramiento vs. anonimización, ruido sintético (privacidad diferencial). |
| 🖥️ *Ética de Datos y Marcos Regulatorios* | **GDPR vs. CCPA**, requisitos de consentimiento válido (libre, específico, informado, inequívoco, revocable), patrones oscuros (*dark patterns*) en interfaces de consentimiento, y el peligro de la discriminación algorítmica por "caja negra" (casos de contratación automatizada y aprobación de créditos). |

**Ideas clave:** *"la información solo tiene valor si está gobernada y correctamente almacenada"*; los modelos de IA pueden descubrir y amplificar sesgos históricos presentes en los datos de entrenamiento, automatizando la discriminación a gran escala.

---

## 🛠️ Stack Tecnológico

| Categoría | Herramientas |
|---|---|
| **Lenguaje** | Python 3.11 |
| **Manipulación de datos** | `pandas`, `numpy` |
| **Web Scraping / APIs** | `requests`, `BeautifulSoup4` |
| **Visualización** | `matplotlib`, `seaborn`, `plotly` |
| **Machine Learning** | `scikit-learn` (`LinearRegression`, `Lasso`, `confusion_matrix`, `KFold`, `cross_val_score`, `train_test_split`, `PolynomialFeatures`, `KNNImputer`) |
| **Calidad y diagnóstico de datos** | `missingno`, `ydata-profiling` (AutoEDA) |
| **Formatos de almacenamiento** | CSV, Parquet |
| **Seguridad** | `hashlib` (SHA-256) |

---

## 🚀 Cómo usar este repositorio

```bash
# Clonar el repositorio
git clone https://github.com/<usuario>/fundamentos-ciencia-de-datos.git
cd fundamentos-ciencia-de-datos

# Crear entorno virtual e instalar dependencias
python -m venv venv
source venv/bin/activate    # En Windows: venv\Scripts\activate
pip install pandas numpy requests beautifulsoup4 matplotlib seaborn plotly scikit-learn missingno ydata-profiling

# Abrir los notebooks
jupyter notebook
```

---

## 📖 Bibliografía destacada

- Kleppmann, M. (2017). *Designing Data-Intensive Applications*. O'Reilly Media.
- McKinney, W. (2022). *Python for Data Analysis* (3rd ed.). O'Reilly Media.
- James, G., Witten, D., Hastie, T., & Tibshirani, R. (2021). *An Introduction to Statistical Learning*. Springer.
- Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of Statistical Learning*. Springer.
- Géron, A. (2019). *Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow* (2nd ed.). O'Reilly Media.
- Cochran, W. G. (1977). *Sampling Techniques* (3rd ed.). John Wiley & Sons.
- O'Neil, C. (2016). *Weapons of Math Destruction*. Crown Publishing.
- Knaflic, C. N. (2015). *Storytelling with Data*. John Wiley & Sons.
- Reglamento (UE) 2016/679 (GDPR). (2016). Diario Oficial de la Unión Europea.

---

## 📌 Notas

Este repositorio corresponde a la presentación final de la clase de **Fundamentos de Ciencia de Datos**, consolidando el trabajo práctico (notebooks) realizado a lo largo del curso junto con el material teórico revisado en cada sesión.
