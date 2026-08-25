# ANA/SNIRH Normalized Series

Long-format hydrometeorological series derived from XLSX reports published by Peru's Autoridad Nacional del Agua (ANA) through SNIRH. The files support reproducible, selective downloads from [ANA-SNIRH Spatial Station Finder](https://jamilramirez.shinyapps.io/ANA_SNIRH_WEB/).

This is an independent derived-data repository. It is not an official ANA product.

## Repository contents

Each ANA/SNIRH `IDConfig` is stored independently:

```text
series_long/
└── <CodigoUH>_<basin>/
    └── IDConfig_<id>.rds
```

The basin folder is descriptive. `id_config` inside the RDS file is the stable series identifier used by the application.

## RDS schema

Each file contains an R `data.table`/`data.frame` in long format with these fields:

| Field | Meaning |
|---|---|
| `series_id` | Composite series identifier |
| `station_id` | Composite physical-station identifier |
| `id_config` | ANA/SNIRH series configuration identifier |
| `codigo_estacion` | ANA station code |
| `nombre_estacion` | Station name |
| `tipo_dato` | Hydrometeorological data type |
| `variable` | Variable reported by ANA/SNIRH |
| `unidad` | Source measurement unit |
| `fecha` | Observation date |
| `hora` | Source observation time |
| `datetime` | Combined observation date and time |
| `valor` | Reported numeric value |
| `expected_obs_day` | Expected observations per day for the source frequency |

Read a file in R with:

```r
series <- readRDS(
  "series_long/0144_Cuenca_Mauri/IDConfig_1227.rds"
)
```

## Normalization scope

Normalization standardizes report structure and identifiers; it does not fill missing observations or merge different `IDConfig` series. Source dates, times, values, units, and expected daily frequency remain explicit so downstream users can apply their own quality and completeness criteria.

The preserved source XLSX reports are available in [ANA-SNIRH-Official-Reports](https://github.com/JamilRamirez/ANA-SNIRH-Official-Reports). Use the [official ANA/SNIRH basin viewer](https://snirh.ana.gob.pe/VisorPorCuenca/) to consult the latest information published by ANA.

## Data rights and attribution

ANA/SNIRH is the source publisher of the underlying observations and reports. No repository-wide open-data license is asserted here for this derived publication because an explicit license for the source SNIRH downloads has not been established by this project. Users should verify ANA's current terms, cite ANA/SNIRH as the data source, and describe any further transformations they perform.

## Update policy

The repository is intended to be replaced from a complete, verified pipeline publication rather than edited file by file. Updates are planned monthly and should remain synchronized with the Web catalog and official-report archive.

Maintained by [Jamil Ramirez](https://jamilramirez.github.io/).
