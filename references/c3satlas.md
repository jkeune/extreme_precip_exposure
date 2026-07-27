# C3S Atlas Precipitation Projections

The **Copernicus Interactive Climate Atlas** is developed by the Copernicus Climate Change Service (C3S), operated by ECMWF on behalf of the European Commission. It provides an interactive web application and a gridded dataset for exploring observed and projected changes in a wide range of climate variables across Europe and the globe.

---

## Dataset: Multi-origin C3S Atlas

**Full name**: Gridded dataset underpinning the Copernicus Interactive Climate Atlas  
**CDS identifier**: `multi-origin-c3s-atlas`  
**Coverage**: Global/European, multiple time periods  
**Source**: [cds.climate.copernicus.eu/datasets/multi-origin-c3s-atlas](https://cds.climate.copernicus.eu/datasets/multi-origin-c3s-atlas)

The dataset bundles pre-processed climate indices derived from multiple sources (observations and model ensembles) and is the underlying data store for the C3S Interactive Climate Atlas web application. In this book, the EURO-CORDEX subset is used.

**Data citation**: {cite}`c3s2024atlas`

---

## EURO-CORDEX ensemble

This book uses the **EURO-CORDEX** component of the C3S Atlas dataset (`origin: cordex_eur_11`, `domain: euro_cordex`), which is a coordinated ensemble of regional climate model (RCM) simulations dynamically downscaling ERA-Interim-driven global climate models over Europe.

| Property | Value |
|---|---|
| **Spatial resolution** | 0.11° (~12.5 km) |
| **Coordinate system** | WGS84 (EPSG:4326) |
| **Historical period** | 1970–2005 |
| **Projection period** | 2006–2100 |
| **Scenarios** | RCP 2.6, RCP 4.5, RCP 8.5 |
| **Bias adjustment** | No bias adjustment |

Each ensemble member is identified by a unique combination of global climate model (GCM) driver and regional climate model (RCM). Downloading all available members for a given scenario and variable yields a multi-model ensemble that captures the range of plausible future climates.

---

## Variable used in this book

**Variable**: Monthly maximum of daily precipitation (`monthly_maximum_1_day_precipitation`, also referred to as **Rx1day**)

Rx1day is the highest single-day precipitation total observed within a calendar month. Annual maxima of this quantity are the standard input for extreme-value analysis (GEV fitting and return-period estimation). Using monthly maxima rather than raw daily values reduces storage requirements while preserving the statistical information needed for block-maxima approaches.

| Property | Value |
|---|---|
| **Short name** | Rx1day |
| **Units** | mm day⁻¹ |
| **Temporal aggregation** | Monthly maximum of daily precipitation |
| **Downloaded period (historical)** | 1970–2005 |
| **Downloaded period (projections)** | 2006–2100 |

---

## RCP scenarios

Three Representative Concentration Pathways (RCPs) are used, representing a range of greenhouse-gas emission trajectories:

| Scenario | Description |
|---|---|
| **RCP 2.6** | Strong mitigation; radiative forcing stabilises at ~2.6 W m⁻² by 2100 |
| **RCP 4.5** | Intermediate mitigation; stabilises at ~4.5 W m⁻² by 2100 |
| **RCP 8.5** | High-emission baseline; reaches ~8.5 W m⁻² by 2100 |

Using all three scenarios is essential for characterising scenario uncertainty — the spread between RCPs grows substantially in the second half of the 21st century.

---

## How the data are used in this book

The downloaded NetCDF files are processed by the [How-To Guide on Projections of Precipitation](../how-to-guides/precipitation_c3satlas.ipynb), which:

1. Clips the global/European grid to the bounding box of the target NUTS2 region.
2. Extracts the monthly Rx1day values for every grid point inside the region boundary.
3. Computes **annual maxima** (block maxima) per model–grid-point combination.
4. Saves the results to CSV files used by the tutorials.

```{admonition} Data access
:class: note
The data are freely available from the [Copernicus Climate Data Store](https://cds.climate.copernicus.eu/datasets/multi-origin-c3s-atlas). A free CDS account and the `cdsapi` Python package are required. See the [How-To Guide](../how-to-guides/precipitation_c3satlas.ipynb) for step-by-step download instructions.
```
