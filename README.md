# ICSHM-EO Atrato

**Earth Observation-based Composite Index of Mining Water Security applied to the Atrato River Basin, Colombia**

**Índice Compuesto de Seguridad Hídrica Minera basado en Observación de la Tierra aplicado a la cuenca del río Atrato, Colombia**

---

## English

### Overview
This repository contains the full analytical pipeline, datasets, and figures supporting the paper submitted to the IEEE International Conference on Artificial Intelligence, Computer, Data Sciences and Applications (ACDSA 2027), Rio de Janeiro, Brazil.

The **ICSHM-EO** (Composite Index of Mining Water Security based on Earth Observation) is a reduced satellite-based version of the ICSHM framework, applied as a pilot to the Atrato River Basin, a legally recognized subject of rights under Constitutional Court Sentence T-622/2016 (Colombia).

### Study area
- **Region:** Atrato River Basin, Chocó Department, Colombia
- **Analytical units:** 170 subbasins from HydroBASINS Level 9 (WWF HydroSHEDS)
- **Cartographic units:** 144 subbasins (26 coastal slivers excluded due to geometry degeneration)
- **Reference year:** 2024

### Indicators
| Dimension | Indicator | Source |
|---|---|---|
| D1 – Precipitation stress | Standardized Precipitation Score | CHIRPS v2.0 (1981-2020 baseline, 2024 evaluated) |
| D2 – Water turbidity | NDTI (Normalized Difference Turbidity Index) | Sentinel-2 SR (Jan-Mar 2024, dry season) |
| D4 – Forest loss | Cumulative loss 2018-2024 | Hansen GFC v1.12 |
| D5 – Mining pressure | Mining area (class 30) | MapBiomas Colombia Collection 3 |

### Method summary
- **Normalization:** Min-Max with log(1+x) transformation for D4 and D5 (skewed distributions)
- **Aggregation:** Arithmetic mean with veto rule (τ = 0.20)
- **Weights:** Equal weights (wᵢ = 0.25), justified by OECD (2008) 50% dominance rule
- **Spatial analysis:** Global Moran's I and Local Moran's I (LISA) with KNN weights (k=8), 999 permutations, Benjamini-Hochberg FDR correction (α=0.05)

### Repository structureICSHM-EO-Atrato/
├── data/ # 8 CSVs of indicators + LISA results (gpkg)
├── shapefile/ # 144 subbasins (WGS 84)
├── figures/ # Fig. 3, 4, 6 (PNG 600 dpi + PDF)
├── notebooks/ # Colab notebooks for ICSHM-EO calculation, LISA, D2 consolidation
├── gee_scripts/ # Google Earth Engine scripts (D1, D2, D4, D5, base subbasins)
├── LICENSE # MIT License
└── README.md # This file
### How to reproduce
1. Run the Google Earth Engine scripts in `gee_scripts/` to generate the raw CSVs (D1, D2 chunks, D4, D5) and the subbasin shapefile.
2. Consolidate the D2 chunks with the `06_Consolidar_D2` notebook.
3. Run `01_ICSHM_EO_calculo.ipynb` to compute the composite index and sensitivity/reliability analyses.
4. Run `02_LISA_Moran.ipynb` to compute the spatial autocorrelation and generate the figures.

### Citation
If you use this material, please cite:
> Salas Cuesta, J., Nero, M. A., & Martínez Asprilla, H. (2027). Earth Observation for Water Security in Legally Recognized Rivers: A Framework Proposal for Data-Sparse Territories Applied to the Atrato Basin, Colombia. *Proceedings of the IEEE International Conference on Artificial Intelligence, Computer, Data Sciences and Applications (ACDSA 2027)*, Rio de Janeiro, Brazil.

### License
This work is released under the MIT License. See `LICENSE` for details.

### Contact
- **Corresponding author:** Jhanier Salas Cuesta
- **Email:** jhaniersc@ufmg.br
- **Institution:** PPGAMSA, Instituto de Geociências, Universidade Federal de Minas Gerais (UFMG), Belo Horizonte, Brazil

---

## Español

### Descripción
Este repositorio contiene el pipeline analítico completo, los datasets y las figuras del artículo enviado a la Conferencia Internacional IEEE sobre Inteligencia Artificial, Informática, Ciencias de Datos y Aplicaciones (ACDSA 2027), Río de Janeiro, Brasil.

El **ICSHM-EO** (Índice Compuesto de Seguridad Hídrica Minera basado en Observación de la Tierra) es una versión reducida satelital del marco ICSHM, aplicado como piloto a la cuenca del río Atrato, sujeto de derechos según la Sentencia T-622/2016 de la Corte Constitucional de Colombia.

### Área de estudio
- **Región:** Cuenca del río Atrato, Departamento del Chocó, Colombia
- **Unidades analíticas:** 170 subcuencas HydroBASINS Nivel 9 (WWF HydroSHEDS)
- **Unidades cartográficas:** 144 subcuencas (26 fragmentos costeros excluidos por degeneración geométrica)
- **Año de referencia:** 2024

### Indicadores
| Dimensión | Indicador | Fuente |
|---|---|---|
| D1 – Estrés de precipitación | Standardized Precipitation Score | CHIRPS v2.0 (línea base 1981-2020, evaluado 2024) |
| D2 – Turbidez del agua | NDTI (Normalized Difference Turbidity Index) | Sentinel-2 SR (ene-mar 2024, época seca) |
| D4 – Pérdida forestal | Pérdida acumulada 2018-2024 | Hansen GFC v1.12 |
| D5 – Presión minera | Área minera (clase 30) | MapBiomas Colombia Colección 3 |

### Resumen metodológico
- **Normalización:** Min-Max con transformación log(1+x) para D4 y D5 (distribuciones sesgadas)
- **Agregación:** Media aritmética con regla de veto (τ = 0.20)
- **Pesos:** Iguales (wᵢ = 0.25), justificados por la regla OECD (2008) de dominancia del 50%
- **Análisis espacial:** Moran's I global y Local Moran's I (LISA) con pesos KNN (k=8), 999 permutaciones, corrección FDR de Benjamini-Hochberg (α=0.05)

### Cómo reproducir
1. Ejecutar los scripts de Google Earth Engine en `gee_scripts/` para generar los CSVs base (D1, chunks del D2, D4, D5) y el shapefile de subcuencas.
2. Consolidar los chunks del D2 con el notebook `06_Consolidar_D2`.
3. Ejecutar `01_ICSHM_EO_calculo.ipynb` para calcular el índice compuesto y los análisis de sensibilidad/confiabilidad.
4. Ejecutar `02_LISA_Moran.ipynb` para el análisis de autocorrelación espacial y generar las figuras.

### Cita
Si utiliza este material, por favor cite:
> Salas Cuesta, J., Nero, M. A., & Martínez Asprilla, H. (2027). Earth Observation for Water Security in Legally Recognized Rivers: A Framework Proposal for Data-Sparse Territories Applied to the Atrato Basin, Colombia. *Proceedings of the IEEE International Conference on Artificial Intelligence, Computer, Data Sciences and Applications (ACDSA 2027)*, Río de Janeiro, Brasil.

### Licencia
Este trabajo se distribuye bajo la Licencia MIT. Ver `LICENSE` para más detalles.

### Contacto
- **Autora principal:** Jhanier Salas Cuesta
- **Correo:** jhaniersc@ufmg.br
- **Institución:** PPGAMSA, Instituto de Geociências, Universidade Federal de Minas Gerais (UFMG), Belo Horizonte, Brasil
