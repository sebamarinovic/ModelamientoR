# 📘 Modelamiento Térmico Operacional — Informe RMarkdown

Este documento contiene el desarrollo analítico del comportamiento térmico en las plantas industriales **GCP-2** y **GCP-4**, usando herramientas estadísticas y de machine learning para entender y predecir la temperatura de gases de salida, en relación con variables críticas del sistema de enfriamiento.

---

## 📌 Objetivo del Informe

- Analizar la relación entre **Δ Agua** y la **temperatura de gases de salida**.
- Evaluar el aporte de variables operativas como:
  - `Temp.Entrada.Agua.Torre`
  - `Grupo_Tren_Equipo` (línea A/B, planta GCP-2/4)
  - `TempGas` promedio diario
- Comparar el rendimiento de distintos modelos de regresión aplicados al problema.

---

## 🧪 Modelos Comparados

Se construyen y validan los siguientes modelos predictivos para estimar `Temperatura`:

| Modelo             | Variables Consideradas                                         | Notas |
|--------------------|---------------------------------------------------------------|-------|
| Lineal Simple      | Solo `Delta.Agua`                                             | Referencial |
| Lineal Múltiple    | `Delta.Agua`, `Temp.Entrada.Agua.Torre`, `TempGas`, `Grupo_Tren_Equipo` | Base extendida |
| Polinomial         | Término cuadrático en `Delta.Agua` + variables múltiples      | Modela no linealidad parcial |
| GAM                | Ajuste suave sobre `Delta.Agua`                               | Flexible y explicativo |
| MARS               | Modelos aditivos multivariados con particiones                | Interpretable y no lineal |
| XGBoost            | Árboles de decisión optimizados                               | 🏆 Mejor desempeño |

---

## 📊 Resultados Comparativos

| Modelo          | RMSE    | R² (%)  |
|-----------------|---------|---------|
| Lineal Simple   | 4.38    | 2.2     |
| Lineal Múltiple | 1.88    | 82.1    |
| Polinomial      | 1.84    | 82.7    |
| GAM             | 1.85    | 82.6    |
| MARS            | 1.85    | 82.5    |
| **XGBoost**     | **1.13**| **93.5**|

🔴 *XGBoost* es el modelo con **mayor precisión predictiva**, logrando un ajuste sobresaliente con R² ≈ 93.5%.

---

## 📊 Resultados del Análisis PDP

Se utilizó la librería `pdp` para analizar el efecto marginal de `TempGas` sobre `Δ Agua` usando el modelo entrenado `XGBoost`.

🔺 **Pendiente PDP (TempGas → Δ Agua):**  
> Por cada incremento de **1 °C en TempGas**, se estima una **disminución de `X` °C en Δ Agua**.  
> Este valor fue estimado mediante ajuste lineal al gráfico de dependencia parcial.

✏️ Este resultado entrega una **interpretación cuantitativa** crucial para comprender cómo afecta el sobrecalentamiento del sistema de gases a la eficiencia térmica del sistema de enfriamiento.

---

## 🖥️ Aplicación Shiny

El proyecto cuenta con una app `Shiny` para diagnóstico operativo que incluye:

- Identificación de **equipos críticos**.
- Visualización de **ciclos de mantenimiento**.
- Series de tiempo y boxplots de Δ Agua.
- Análisis automatizado con XGBoost.

📎 Se exporta una figura en `"comparacion_modelos_real_vs_pred_test.png"` para revisión visual.
![image](https://github.com/user-attachments/assets/e1f5bba4-5d1f-4f8f-b0b6-bb263164c993)

---

## 📦 Requisitos

```r
install.packages(c("tidyverse", "xgboost", "caret", "earth", "mgcv", "lubridate", "patchwork"))
```

## ✍️ Autor
**Sebastian Marinovic Leiva** - Junio 2025

📄 RMarkdown: modelamiento.Rmd

🧠 Proyecto: Análisis de Eficiencia Térmica EP-110
