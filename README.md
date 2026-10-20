# Hotel Booking Demand — proyecto de aprendizaje supervisado

Machine Learning · MUCSI 2026/27 · Universidad de Deusto

## TL;DR

| | |
|---|---|
| **Qué hace** | Cuando entra una reserva de hotel, predice dos cosas |
| **Clasificación** | ¿Se cancelará o no se presentará (*no-show*)? → `is_canceled` (probabilidad 0–1) |
| **Regresión** | ¿Cuánto pagará por noche? → `adr` (€/noche) |
| **Para qué** | Decidir si se pide depósito y cuánta sobreventa hacer |
| **Momento de predicción** | Al **registrar** la reserva: no se usa nada que se sepa después. ⚠️ El dataset guarda los valores del día antes de la llegada (ver 01 §4) |
| **Datos** | 119 390 reservas reales de dos hoteles de Portugal (2015–2017) |

## Inicio rápido

| Paso | Comando o acción |
|---|---|
| 1 · Crear entorno | `python -m venv .venv` |
| 2 · Activarlo | Windows: `.venv\Scripts\activate` · Linux/macOS: `source .venv/bin/activate` |
| 3 · Instalar | `pip install -r requirements.txt` |
| 4 · Abrir | **VS Code**: abrir el notebook → *Select Kernel* → *Python Environments* → `.venv` · **Navegador**: `jupyter lab` |
| 5 · Ejecutar | Los notebooks **en orden numérico** (01, 02, …) |

- ⚠️ Sin el paso 3, el entorno está vacío y el notebook falla en el primer `import`.
- Si `.venv` no aparece en VS Code: `Ctrl+Shift+P` → **Developer: Reload Window**.
- Los notebooks se entregan **con las salidas ya generadas**: no hace falta ejecutarlos para ver los resultados.

## Notebooks

Uno por laboratorio, en orden. Cada uno lee lo que deja el anterior. Las salidas van a `outputs/<notebook>/`.

| # | Notebook | Pregunta que responde | Sale | Estado |
|---|---|---|---|---|
| 01 | `01-data-collection-and-quality` | ¿Son los datos correctos? ¿Qué está prohibido? ¿Avanza el lote? | `data_contract.json` (esquema y columnas prohibidas) · `quality_summary.json` (decisión del lote) · `scorecard.csv` (controles) | ✅ |
| 02 | `02-eda-and-cleaning` | ¿Cómo son los datos y cómo se limpian? | `hotels_clean.csv` · `quarantine.csv` (182 filas y su motivo) · `decisions.csv` (qué, por qué, cuántas filas) · `cleaning_report.json` · `fig_eda.png` | ✅ |
| 03 | `03-feature-engineering-and-transformation` | ¿Qué entra en el modelo y cómo se transforma? | variables derivadas + transformador (sin ajustar) | ⏳ |
| 04 | `04-experimental-design-partitioning-and-metrics` | ¿Cómo se parte y se evalúa? | partición, métricas, *baselines* | ⏳ |
| 05 | `05-classification` | ¿Qué modelo predice mejor la cancelación? | mejor clasificador | ⏳ |
| 06 | `06-regression` | ¿Qué modelo predice mejor el `adr`? | mejor regresor | ⏳ |
| 07 | `07-evaluation-and-error-analysis` | ¿Cómo rinde en test y dónde falla? | resultados finales, errores, uso combinado | ⏳ |

## Estructura de carpetas

| Ruta | Contenido |
|---|---|
| `data/raw/hotels.csv` | Fuente original. **Nunca se modifica**. Se descarga sola si falta |
| `data/interim/hotels_clean.csv` | Dataset limpio del 02. Se regenera ejecutando el 02 (no se versiona) |
| `outputs/<notebook>/` | Lo que genera cada notebook |
| `notebooks/` | Los notebooks, numerados |

## Datos y reproducibilidad

| | |
|---|---|
| **Fuente** | Antonio, de Almeida y Nunes (2019). *Hotel booking demand datasets*. Data in Brief 22, 41–49 · [DOI](https://doi.org/10.1016/j.dib.2018.11.126) · CC BY 4.0 |
| **Copia usada** | H1 (Resort) + H2 (City) unidos con la columna `hotel` — [TidyTuesday 2020-02-11](https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-02-11/hotels.csv) · 119 390 filas × 32 columnas |
| **SHA-256** | `7c2ae42a7353905ea136e5c2287f17c92c5435826598bfbb8491c6f0c7b1fc06` (lo comprueba el notebook 01) |
| **Entorno** | Ejecutado con Python 3.14.4 · `SEED = 42` · dependencias fijadas en `requirements.txt` (en 3.14 se instala numpy 2.3.x: 2.2.6 no tiene instalador) |
