# Spatially Robust Multimodal Agricultural Sensing Fusion for European Topsoil SOC Stock Prediction

This repository contains the reproducibility code accompanying the IEEE Transactions on AgriFood Electronics manuscript:

**Spatially Robust Multimodal Agricultural Sensing Fusion for European Topsoil Organic Carbon Stock Prediction**

## Study overview

The workflow integrates:

- Sentinel-1 SAR
- Sentinel-2 multispectral observations
- ERA5-Land environmental variables
- LUCAS soil texture and land cover
- European topsoil soil-organic-carbon-stock (SOCS) target data

The experimental design emphasizes:

- target-leakage control
- 100-km spatial-block cross-validation
- leave-country-out validation
- multimodal ablation
- target-quality sensitivity
- SHAP-based interpretation
- group-aware conformal prediction

## Repository structure

```text
TAFE_SOCS_GitHub_Repository/
├── gee/
│   ├── 01_extract_sentinel1_2018.js
│   ├── 02_extract_sentinel2_2018.js
│   └── 03_extract_era5land_2018.js
├── scripts/
│   ├── 00_merge_sensing_data.py
│   ├── 01_merge_socs_target.py
│   ├── 02_baseline_models.py
│   ├── 03_multimodal_ablation.py
│   ├── 04_cross_country_and_sensitivity.py
│   ├── 05_reliability_analysis.py
│   ├── 06_final_model_shap_conformal.py
│   └── 07_high_confidence_validation.py
├── data/
│   └── README.md
├── results/
│   └── README.md
├── docs/
│   └── REPRODUCIBILITY.md
├── requirements.txt
├── .gitignore
└── CITATION.cff
```

## Data

Raw and derived datasets are **not redistributed in this repository** because several source datasets are governed by their original access or redistribution conditions.

See [`data/README.md`](data/README.md) for expected filenames and source links/citations.

## Reproducing the analysis

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

Run the scripts in numerical order after placing the required datasets in `data/`.

Example:

```bash
python scripts/00_merge_sensing_data.py
python scripts/01_merge_socs_target.py
python scripts/02_baseline_models.py
python scripts/03_multimodal_ablation.py
python scripts/04_cross_country_and_sensitivity.py
python scripts/05_reliability_analysis.py
python scripts/06_final_model_shap_conformal.py
python scripts/07_high_confidence_validation.py
```

The code is organized so that all spatial validation uses geographic groups rather than ordinary random folds for the primary reported results.

## Primary modeling rules

1. `POINT_ID`, coordinates, and country labels are retained for joining or validation only.
2. Bulk-density and coarse-fragment variables used in SOC-stock construction are excluded from the primary predictor set.
3. Missing soil-texture variables are imputed **within each training fold**.
4. Land cover is one-hot encoded using **training-fold categories only**.
5. Spatial blocks are constructed in EPSG:3035 using a 100-km grid.

## Software

Main Python libraries:

- pandas
- numpy
- scikit-learn
- xgboost
- catboost
- pyproj
- matplotlib

Google Earth Engine is used for Sentinel-1, Sentinel-2, and ERA5-Land extraction.

## Citation

Please cite the associated manuscript and the original data sources when using this code.

## License

A software license has not yet been assigned. Select an appropriate open-source license before public release.
