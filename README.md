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

## 📈 Visualización

El documento incluye comparaciones gráficas **predicho vs observado** para cada modelo.  
Esto permite identificar:
- Sesgos sistemáticos
- Subajuste o sobreajuste
- Distribución de errores por rango

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
