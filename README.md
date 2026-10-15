# Hotel Booking Demand — proyecto de aprendizaje supervisado

Machine Learning · MUCSI 2026/27 · Universidad de Deusto

## TL;DR

| | |
|---|---|
| **Qué hace** | Cuando entra una reserva de hotel, predice dos cosas |
| **Clasificación** | ¿Se cancelará? → `is_canceled` (probabilidad 0–1) |
| **Regresión** | ¿Cuánto pagará por noche? → `adr` (€/noche) |
| **Para qué** | Decidir si se pide depósito y cuánta sobreventa hacer |
| **Momento de predicción** | Al **registrar** la reserva: no se usa nada que se sepa después |
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

Uno por sesión de la asignatura, en el mismo orden que los laboratorios. Cada uno lee lo que deja el anterior.

| # | Notebook | Pregunta que responde | Entra | Sale | Estado |
|---|---|---|---|---|---|
| 01 | `01-data-collection-and-quality` | ¿Son los datos correctos? ¿Qué está prohibido? ¿Avanza el lote? | `content/data/raw/hotels.csv` | contrato, scorecard, columnas prohibidas | ✅ |
| 02 | `02-eda-and-cleaning` | ¿Cómo son los datos y cómo se limpian? | salidas del 01 | dataset limpio, cuarentena, decisiones | ⏳ |
| 03 | `03-feature-engineering-and-transformation` | ¿Qué entra en el modelo y cómo se transforma? | dataset limpio | variables derivadas + transformador (sin ajustar) | ⏳ |
| 04 | `04-experimental-design-partitioning-and-metrics` | ¿Cómo se parte y se evalúa? | dataset limpio + transformador | partición, métricas, *baselines* | ⏳ |
| 05 | `05-classification` | ¿Qué modelo predice mejor la cancelación? | partición | mejor clasificador | ⏳ |
| 06 | `06-regression` | ¿Qué modelo predice mejor el `adr`? | partición | mejor regresor | ⏳ |
| 07 | `07-evaluation-and-error-analysis` | ¿Cómo rinde en test y dónde falla? | los dos modelos | resultados finales, errores, uso combinado | ⏳ |

## Salidas del notebook 01

Carpeta `content/outputs/01-data-collection-and-quality/`:

| Archivo | Qué contiene |
|---|---|
| `source_inventory.csv` | Fichero recibido: filas, columnas, tamaño, hash |
| `availability_at_prediction_time.csv` | Cada columna: ¿se conoce al reservar? (sí / dudoso / no) |
| `quality_metrics.csv` | Métricas por dimensión: completitud, unicidad, validez, consistencia |
| `scorecard.csv` | Cada control: umbral, severidad, acción, PASS/FAIL |
| `data_contract.json` | Qué se garantiza al notebook 02: esquema, propósito, calidad |
| `quality_summary.json` | Decisión del lote + decisiones pendientes para el 02 |
| `run_manifest.json` | Fuente, hash, entorno y decisión: cómo reproducir la ejecución |

## Estructura de carpetas

| Ruta | Contenido |
|---|---|
| `content/data/raw/hotels.csv` | Fuente original. **Nunca se modifica**. Se descarga sola si falta |
| `notebooks/` | Los notebooks, numerados |
| `content/outputs/<notebook>/` | Lo que genera cada notebook |
| `requirements.txt` | Dependencias |

## Datos

| | |
|---|---|
| **Fuente** | Antonio, de Almeida y Nunes (2019). *Hotel booking demand datasets*. Data in Brief 22, 41–49 |
| **DOI** | https://doi.org/10.1016/j.dib.2018.11.126 |
| **Licencia** | CC BY 4.0 |
| **Copia usada** | H1 (Resort) + H2 (City) unidos con la columna `hotel` — [TidyTuesday 2020-02-11](https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-02-11/hotels.csv) |
| **SHA-256** | `7c2ae42a7353905ea136e5c2287f17c92c5435826598bfbb8491c6f0c7b1fc06` (lo comprueba el notebook 01) |
| **Tamaño** | 119 390 filas × 32 columnas |

## Reproducibilidad

| | |
|---|---|
| **Python** | Probado con 3.10 y 3.13 |
| **Semilla** | `SEED = 42` en todos los notebooks |
| **Dependencias** | Fijadas en `requirements.txt` |
| **Python 3.14** | Instala numpy 2.3.x en lugar de 2.2.6 (2.2.6 no tiene instalador para 3.14) |
