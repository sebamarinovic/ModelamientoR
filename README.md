# 📊 Dashboard de Análisis Térmico EP-110

Esta aplicación **Shiny** permite monitorear y analizar la eficiencia térmica de equipos de enfriamiento tipo EP-110 en plantas industriales. Utiliza registros operacionales y de mantenimiento para detectar equipos críticos, analizar el rendimiento térmico, visualizar tendencias temporales y aplicar modelos predictivos como **MARS (Multivariate Adaptive Regression Splines)**.

---

## 🚀 ¿Qué hace esta app?

### 🔍 1. Equipos Críticos
- Identifica automáticamente el equipo con **mayor proporción de registros bajo 4°C de Δ Agua**.
- Resume el rendimiento promedio y la criticidad operativa.

### 🛠️ 2. Ciclos de Mantenimiento
- Muestra la frecuencia y distribución de eventos de mantención.
- Calcula:
  - Última fecha de mantención.
  - Intervalo promedio entre mantenciones.
  - Recomendación sobre equipos no intervenidos.

### 🧠 3. Modelo MARS
- Entrena un modelo de regresión MARS para predecir la eficiencia térmica en base a:
  - Temperatura de entrada del agua.
  - Estado del equipo.
  - Identificador del equipo.
- Reporta métricas de desempeño (RMSE y R²).
- Visualiza **predicción vs valor real**.
- Incluye interpretación operacional del modelo.

### 📈 4. Visualizaciones
- Serie temporal de Δ Agua por equipo.
- Distribución de Δ Agua por equipo y estado (servicio o mantención).
- Texto interpretativo sobre comportamiento térmico.

---

## 📂 Archivos requeridos

- `data.csv` → Datos operacionales (variables como Fecha, Hora, Delta Agua, Estado, Equipo, Temp Entrada Agua Torre).
- `temp_gcp_data.csv` → Temperatura de gases por FechaHora para análisis de correlación (no obligatorio).

---

## 🛠️ Librerías necesarias

La app requiere las siguientes librerías de R:

```r
library(shiny)
library(tidyverse)
library(lubridate)
library(DT)
library(plotly)
library(earth)
library(glue)
