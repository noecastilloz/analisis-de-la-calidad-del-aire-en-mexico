# 🍃 Análisis Exploratorio de Datos (EDA): Calidad del Aire en México

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-3776AB)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

## 📌 Descripción del Proyecto
Este proyecto analiza un conjunto de datos histórico de calidad del aire y variables meteorológicas de más de 70 estaciones de monitoreo en México. El objetivo principal fue realizar un **Análisis Exploratorio de Datos (EDA)** riguroso, aplicando criterio físico e ingeniería de datos para solucionar problemas complejos de datos corruptos, lecturas inactivas de sensores y desalineación temporal.

---

## 🎯 Objetivos Clave
- **Limpieza Rigurosa y Criterio Físico:** Identificar y tratar valores corruptos o astronómicos ($>10,000\,\mu\text{g/m}^3$) producto de desbordamientos del sistema (*overflow*) o sensores dañados.
- **Tratamiento Avanzado de Series Temporales:** Implementar un pipeline de imputación temporal por estación mediante interpolación lineal y medianas locales, evitando el sesgo de la imputación global.
- **Manejo de Sensores Inactivos:** Detectar y re-imputar lecturas exactas en $0.0\,\mu\text{g/m}^3$ correspondientes a estaciones caídas.
- **Análisis Espacio-Temporal y Atmosférico:** Evaluar tendencias mensuales, identificar estaciones críticas y analizar la dinámica entre material particulado y gases fotoquímicos.

---

## 🛠️ Tecnologías Utilizadas
- **Lenguaje:** Python
- **Manipulación de Datos:** `Pandas`, `NumPy`
- **Visualización:** `Matplotlib`, `Seaborn`
- **Entorno de Desarrollo:** Google Colab / Jupyter Notebooks

---

## 💡 Aspectos Metodológicos Destacados

### 1. Pipeline de Limpieza en 3 Etapas
En lugar de aplicar imputaciones genéricas que distorsionan la distribución:
1. **Filtrado previo:** Reemplazo de lecturas $> 10,000$ por `NaN`.
2. **Interpolación temporal por estación:** Uso de interpolación lineal (`limit=3`) dentro de la serie de cada `station_id` y relleno secundario con la mediana específica de esa estación.
3. **Manejo de ceros:** Reemplazo de lecturas en $0.0$ por `NaN` y re-imputación local.

### 2. Agregación Mensual para Matriz de Correlación
Al evaluar correlaciones diarias aisladas, la falta de concurrencia entre sensores de distintas estaciones atenuaba artificialmente las relaciones ($r \approx 0$). Agrupar los datos a promedio mensual por estación permitió capturar las dinámicas físicas reales de la atmósfera.

---

## 📊 Hallazgos Principales

| Métrica / Variable | Valor / Resultado | Observación |
| :--- | :--- | :--- |
| **Mediana PM2.5** | $19.59\,\mu\text{g/m}^3$ | Nivel representativo nacional de la serie |
| **Percentil 95 (PM2.5)** | $44.21\,\mu\text{g/m}^3$ | El 95% de los datos se ubica en este rango |
| **Correlación PM2.5 vs PM10** | **0.56** | Fuerte relación por fuentes de emisión compartidas |
| **Correlación O3 vs NO2** | **0.46** | Refleja la dinámica fotoquímica de gases precursores |

---

## 📂 Estructura del Repositorio

```text
├── Calidad del aire en México.ipynb   # Notebook principal de Colab / EDA
├── stations_daily.csv                  # Dataset
└── README.md                          # Documentación del proyecto
