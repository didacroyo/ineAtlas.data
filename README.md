# ineAtlas.data <img src="icon/logo_data.png" align="right" height="278" />

`ineAtlas.data` is the data repository accompanying the [`ineAtlas`](https://github.com/didacroyo/ineAtlas) REST API and R package. It contains processed and standardized data from the Spanish Statistical Office (Instituto Nacional de Estadística, INE) _Atlas de Distribución de Renta de los Hogares_, which provides socioeconomic indicators at the municipal, district, and census tract level for Spain.

This is a fork of [`pablogguz/ineAtlas.data`](https://github.com/pablogguz/ineAtlas.data) maintained by [@didacroyo](https://github.com/didacroyo). It is kept in sync with upstream when INE publishes new data.

## Data structure

All files are `.zip` archives. Tabular datasets compress a CSV inside the ZIP; geometries compress a GeoPackage (`.gpkg`) file.

```
data/
├── income/
│   ├── income_municipality.zip
│   ├── income_district.zip
│   └── income_tract.zip
├── income_sources/
│   ├── income_sources_municipality.zip
│   ├── income_sources_district.zip
│   └── income_sources_tract.zip
├── demographics/
│   ├── demographics_municipality.zip
│   ├── demographics_district.zip
│   └── demographics_tract.zip
├── distribution_sex/
│   ├── distribution_sex_municipality.zip
│   ├── distribution_sex_district.zip
│   └── distribution_sex_tract.zip
├── distribution_sex_age/
│   ├── distribution_sex_age_municipality.zip
│   ├── distribution_sex_age_district.zip
│   └── distribution_sex_age_tract.zip
├── distribution_sex_nationality/
│   ├── distribution_sex_nationality_municipality.zip
│   ├── distribution_sex_nationality_district.zip
│   └── distribution_sex_nationality_tract.zip
├── gini_p80p20/
│   ├── gini_p80p20_municipality.zip
│   ├── gini_p80p20_district.zip
│   └── gini_p80p20_tract.zip
├── census_2021/
│   ├── census_2021_municipality.zip
│   ├── census_2021_district.zip
│   └── census_2021_tract.zip
└── geometries/
    ├── census_tracts_2015.gpkg.zip
    ├── census_tracts_2016.gpkg.zip
    ├── census_tracts_2017.gpkg.zip
    ├── census_tracts_2018.gpkg.zip
    ├── census_tracts_2019.gpkg.zip
    ├── census_tracts_2020.gpkg.zip
    ├── census_tracts_2021.gpkg.zip
    ├── census_tracts_2022.gpkg.zip
    └── census_tracts_2023.gpkg.zip
```

## Data coverage

| Dataset | Years | Geographic levels |
|---------|-------|-------------------|
| `income` | 2015–2023 | municipality, district, tract |
| `income_sources` | 2015–2023 | municipality, district, tract |
| `demographics` | 2015–2023 | municipality, district, tract |
| `distribution_sex` | 2015–2023 | municipality, district, tract |
| `distribution_sex_age` | 2015–2023 | municipality, district, tract |
| `distribution_sex_nationality` | 2015–2023 | municipality, district, tract |
| `gini_p80p20` | 2015–2023 | municipality, district, tract |
| `census_2021` | 2021 (fixed) | municipality, district, tract |
| `geometries` | 2015–2023 | tract (MULTIPOLYGON, EPSG:25830) |

Tract-level tabular datasets contain ~37,072 rows per year (333,648 rows total across 9 years). The geometry files contain ~36,462 features each.

## Syncing with upstream

When `pablogguz/ineAtlas.data` publishes new data (typically after INE releases new Atlas data, around October each year):

```bash
cd ~/Projects/lab/ineAtlas.data
git fetch upstream
git merge upstream/main
git push origin main
```

Then update `valid_years` in `R/get_tract_geom.r` and `GEOMETRY_YEAR` defaults in the main repo accordingly, and redeploy.

## Documentation

Full variable codebook is available at [https://pablogguz.github.io/ineAtlas.data](https://pablogguz.github.io/ineAtlas.data) (upstream documentation).

## Changelog

### [0.4.0] - 2025-10-22
- **New data for 2023!** (income, demographics, distribution, gini, geometries)

### [0.3.0] - 2025-04-24
- Re-built data extraction pipeline and corrected minor bugs that caused some data to be missing for some census tracts

### [0.2.0] - 2024-02-11
- Added data from the 2021 Census

### [0.1.0] - 2024-02-11
- Initial release of ineAtlas.data

## References

This repository contains publicly available data from the Spanish Statistical Office (Instituto Nacional de Estadística, INE), available under a Creative Commons Attribution 4.0 International (CC BY 4.0). More information: https://www.ine.es/dyngs/AYU/index.htm?cid=125.

**Spanish Statistical Office** (2024). *Household Income Distribution Atlas*. Retrieved from [https://www.ine.es/en/experimental/atlas/experimental_atlas_en.htm](https://www.ine.es/en/experimental/atlas/experimental_atlas_en.htm). Latest data release: October 29, 2024.

**Spanish Statistical Office** (2023). *Population and Housing Census 2021*. Retrieved from [https://www.ine.es/censos2021/](https://www.ine.es/censos2021/). Latest data release: June 30, 2023.

## Original author

**Pablo García Guzmán** (EBRD) — [`pablogguz/ineAtlas.data`](https://github.com/pablogguz/ineAtlas.data)
