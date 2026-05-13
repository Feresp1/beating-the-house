# 🏈 Beating the House — Predicción de Ganadores NFL

Proyecto final de **Minería de Datos** | ITAM
Metodología: **CRISP-DM** | Lenguaje: **Python**

---

## 📋 Descripción

¿Es posible construir un modelo predictivo que supere la probabilidad implícita de las casas de apuestas en la NFL?

Este proyecto desarrolla y evalúa tres modelos de clasificación supervisada (Regresión Logística, Random Forest y XGBoost) entrenados con datos históricos de la NFL (2002–2023) para predecir el ganador de cada partido.

---

## 🎯 Pregunta de negocio

> ¿Puede un modelo de clasificación supervisado generar probabilidades de victoria suficientemente precisas como para identificar apuestas con valor esperado positivo frente a las cuotas históricas de las casas?

---

## 📊 Datos

| Fuente | Contenido | Cobertura |
|--------|-----------|-----------|
| `nfl_data_py` | Resultados, clima, spreads, moneylines | 2002–2023 |
| FiveThirtyEight | ELO ratings históricos | 2002–2023 |

**Muestra final:** 4,570 partidos · **Variable objetivo:** `home_win` · **Tabla principal:** `dat1`

---

## 🔬 Metodología CRISP-DM

| Fase | Descripción |
|------|-------------|
| 1. Business Understanding | Definición del problema, criterios de éxito |
| 2. Data Understanding | EDA, análisis de clima, cuotas y efecto COVID-19 |
| 3. Data Preparation | Limpieza, feature engineering, división temporal |
| 4. Modeling | Iteración de RL · RF · XGBoost → torneo de finalistas |
| 5. Evaluation | Métricas, simulación de ROI, conclusión de negocio |
| 6. Deployment | Pipeline productivo, estrategia de monitoreo |

---

## 🏆 Resultados

| Modelo | AUC-ROC | Accuracy | ROI ($100/partido) |
|--------|---------|----------|--------------------|
| Regresión Logística | 0.6923 | 60.3% | — |
| Random Forest | 0.7031 | 60.6% | — |
| **XGBoost** ✅ | **0.7031** | **65.5%** | **+0.30%** |
| Baseline (casas) | 0.7126 | 68.4% | — |

---

## 🚀 Reproducibilidad

```
pip install nfl_data_py pandas numpy scikit-learn xgboost matplotlib
```

> Los datos se descargan automáticamente via `nfl_data_py`. No se requiere ningún CSV externo.

---

## 🔑 Decisiones metodológicas clave

| ID | Decisión | Justificación |
|----|----------|---------------|
| DM-01 | Temporada 2020 excluida | COVID-19 eliminó la ventaja de localía (-6.9 pp) |
| DM-02 | temp/wind = 0 en estadios techados | El clima no aplica en estadios con techo |
| DM-03 | Moneylines 2002–2006 excluidos del cálculo de EV | No hay cuota disponible |
| DM-04 | Surface imputado por moda del equipo local | 41 faltantes (<1%) |

---

*Proyecto desarrollado para la materia de Minería de Datos — ITAM*