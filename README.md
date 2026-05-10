# 🏈 Beating the House — Predicción de Ganadores NFL

Proyecto final de **Minería de Datos** | ITAM
Metodología: **CRISP-DM** | Lenguaje: **Python**

---

## 📋 Descripción

¿Es posible construir un modelo predictivo que supere la probabilidad implícita
de las casas de apuestas en la NFL?

Este proyecto desarrolla y evalúa tres modelos de clasificación supervisada
(Regresión Logística, Random Forest y XGBoost) entrenados con datos históricos
de la NFL (2002–2023) para predecir el ganador de cada partido y evaluar
si existe una ventaja estadística explotable frente a las cuotas de las casas.

---

## 🎯 Pregunta de negocio

> ¿Puede un modelo de clasificación supervisado generar probabilidades de victoria
> suficientemente precisas como para identificar apuestas con valor esperado
> positivo frente a las cuotas históricas de las casas de apuestas NFL?

---

## 📊 Datos

| Fuente | Contenido | Cobertura |
|--------|-----------|-----------|
| `nfl_data_py` | Resultados, clima, spreads, moneylines | 2002–2023 |
| FiveThirtyEight | ELO ratings históricos | 2002–2023 |

**Muestra final:** 4,570 partidos de temporada regular
**Variable objetivo:** `home_win` (victoria del equipo local, 0/1)
**Tabla principal:** `dat1`

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

### Torneo de finalistas (Test Set 2022–2023)

| Modelo | AUC-ROC | Accuracy | F1 |
|--------|---------|----------|----|
| Regresión Logística (L1, C=0.1) | 0.6923 | 60.3% | 0.567 |
| Random Forest (depth=5) | 0.7031 | 60.6% | 0.567 |
| **XGBoost (depth=3, lr=0.01)** ✅ | **0.7031** | **65.5%** | **0.665** |
| Baseline (casas de apuestas) | 0.7126 | 68.4% | — |

### Simulación financiera ($100 por partido)

| Estrategia | Ganancia neta | ROI |
|------------|--------------|-----|
| **XGBoost (ganador predicho)** | **+$140.78** | **+0.30%** |
| Siempre apostar al local | -$81.68 | -0.17% |
| Apostar al azar | ~-$4,500 | ~-9.57% |

---

## 📁 Estructura del repositorio

```
beating-the-house/
│
├── beating_the_house.ipynb   ← Notebook principal (27 celdas)
├── modelo_xgb_final.pkl      ← Modelo XGBoost serializado
├── README.md                 ← Este archivo
```

---

## 🚀 Reproducibilidad

```
pip install nfl_data_py pandas numpy scikit-learn xgboost matplotlib
```

> **Nota:** Los datos se descargan automáticamente via `nfl_data_py`.
> No se requiere ningún archivo CSV externo.

---

## 🔑 Decisiones metodológicas clave

| ID | Decisión | Justificación |
|----|----------|---------------|
| DM-01 | Temporada 2020 excluida del modelado | COVID-19 eliminó la ventaja de localía (-6.9 pp) |
| DM-02 | temp/wind = 0 en estadios techados | El clima no aplica en estadios con techo |
| DM-03 | Moneylines faltantes (2002–2006) excluidos del cálculo de EV | No hay cuota disponible |
| DM-04 | Surface imputado por moda del equipo local | 41 faltantes (<1%) |

---

## 📌 Conclusión

El mercado de apuestas NFL es altamente eficiente pero no impenetrable.
El modelo XGBoost logra **65.5% de accuracy** y un **ROI de +0.30%**
apostando $100 por partido en el test set — superando la estrategia naive
y al azar. Para alcanzar ventaja estadística consistente se requieren
features en tiempo real (injury reports, movimiento de líneas) que
las casas ya incorporan en sus cuotas.

---

*Proyecto desarrollado para la materia de Minería de Datos — ITAM*