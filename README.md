# Socio-Spatial Drivers and Regional Typologies of Domestic Solar PV Adoption in England

Companion repository for the paper *Socio-Spatial Drivers and Regional Typologies of Domestic Solar PV Adoption in England: Integrating Geographically Weighted Regression with Cluster Analysis*.

This project investigates how socio-economic and housing characteristics shape the spatial distribution of domestic rooftop solar PV adoption in England, using Geographically Weighted Regression (GWR) and k-means cluster analysis on Lower Layer Super Output Area (LSOA) data integrated from the UK Feed-in Tariff register, Census 2021, the Index of Multiple Deprivation 2019, and sub-national electricity consumption statistics.

## Authors

- Mennan Guder¹ — *corresponding author* — `mennan.guder@cranfield.ac.uk`
- Abdulrahman Almutairi¹
- Sonali Desai¹ — *repository maintainer* — `s.desai.719@cranfield.ac.uk` / `sonalidesai9697@gmail.com`
- Joel D Souza¹
- William Mensah¹

¹ Cranfield University, Cranfield, Bedfordshire, MK43 0AL, United Kingdom

## Scope

The paper's analytical scope is England. Wales, Scotland, and Northern Ireland are excluded because their deprivation indices (WIMD, SIMD, NIMDM) employ different domain structures, indicators, and reference years, and their small-area geographies (Welsh LSOAs, Scottish Data Zones, Northern Irish Super Output Areas) have incompatible population thresholds and boundaries. Cross-border harmonisation would introduce unacceptable artefacts.

In practice, the FiT register and Census 2021 are first cleaned and merged for England and Wales jointly (since both are published on the LSOA 2011 geography), so descriptive exploratory analysis includes Welsh LSOAs. Welsh LSOAs are then dropped during the spatial-modelling stage when the IMD 2019 merge introduces missing values, so OLS, Moran's I, LISA, GWR, and the cluster analysis are computed for England only (~30,925 LSOAs after data attrition).

## Methodology summary

1. **Data integration** — FiT register (2010–2019) aggregated to LSOA, joined to Census 2021 housing/tenure/economic-activity tables, IMD 2019 domain scores, and sub-national domestic electricity consumption.
2. **Exploratory data analysis** — univariate and bivariate analysis, multicollinearity checks, outlier treatment (winsorisation and log-transform), spatial autocorrelation (Moran's I, LISA).
3. **Global regression** — OLS baseline with Lagrange multiplier diagnostics for spatial dependence.
4. **Geographically Weighted Regression** — adaptive bisquare kernel; bandwidth (284 nearest neighbours) selected via AICc minimisation. Local coefficient estimates and local R² mapped across England.
5. **Cluster analysis** — k-means on standardised GWR coefficient estimates; five clusters interpreted as a heuristic typology of adoption regimes.
6. **Validation** — hierarchical clustering comparison, silhouette analysis, FDR-corrected significance tests, case studies (Peterborough, Solihull, Cornwall).

## Repository structure

```
uk-solar-pv-socio-spatial-analysis/
├── README.md                       this file
├── LICENSE                         Apache 2.0
├── requirements.txt                Python dependencies
├── .gitignore
├── notebooks/
│   └── solar_pv_analysis.ipynb     end-to-end analysis notebook
├── data/
│   └── README.md                   data sources, access instructions, expected layout
└── outputs/                        generated artefacts (gpkg, csv, figures)
    ├── gwr_results_complete.gpkg
    ├── analysis_data_treated.csv
    ├── correlation_pearson.csv
    ├── correlation_spearman.csv
    ├── cluster_coefficient_profiles.csv
    ├── cluster_raw_profiles.csv
    └── policy_recommendations.csv
```

The `data/` folder is **not committed**. See `data/README.md` for the list of source datasets, where to obtain them, and the expected on-disk layout.

## Reproducing the analysis

### 1. Clone the repository

```bash
git clone https://github.com/SonaliDesaiDS/uk-solar-pv-socio-spatial-analysis.git
cd uk-solar-pv-socio-spatial-analysis
```

### 2. Set up the Python environment

Python 3.11 is recommended. Using a virtual environment is strongly advised:

```bash
python -m venv .venv
source .venv/bin/activate          # macOS / Linux
.venv\Scripts\activate             # Windows

pip install -r requirements.txt
```

### 3. Obtain the data

Open `data/README.md` and follow the instructions there. You will need to download:

- The Feed-in Tariff Installation Register (3 Excel files) — Ofgem
- Six Census 2021 LSOA-level tables — ONS / Nomisweb
- Index of Multiple Deprivation 2019, File 7 — gov.uk
- Sub-national domestic electricity consumption (LSOA, 2010–2024) — DESNZ
- LSOA 2011 boundaries (BFC, England and Wales) — ONS Open Geography Portal

All datasets are published under the Open Government Licence v3.0. Place each file in the folder structure described in `data/README.md`.

### 4. Run the notebook

```bash
jupyter lab notebooks/solar_pv_analysis.ipynb
```

Then **Kernel → Restart & Run All**. End-to-end runtime is approximately **30–60 minutes** on a modern laptop, dominated by the GWR fit (~10–15 minutes on ~30,925 LSOAs) and spatial weights matrix construction.

The notebook reads from `../data/` relative to its own location (i.e. the `data/` folder at the repo root) and writes outputs to the working directory; you may want to redirect outputs to `../outputs/` once you have a clean run.

## Key results

A full executed notebook is committed to the repository — open `notebooks/solar_pv_analysis.ipynb` directly in GitHub to view all figures, tables, and printed output without running anything locally. Headline findings are summarised in the paper.

## Software

- `pandas`, `numpy` — data manipulation
- `geopandas`, `mapclassify` — spatial data handling and choropleth classification
- `libpysal`, `esda`, `splot` — spatial weights, Moran's I, LISA
- `spreg` — OLS with spatial diagnostics
- `mgwr` — Geographically Weighted Regression
- `scikit-learn`, `scipy` — k-means, hierarchical clustering, silhouette analysis
- `statsmodels` — multicollinearity diagnostics, FDR correction
- `matplotlib`, `seaborn` — visualisation

Pinned versions are in `requirements.txt`.

## Limitations

The Feed-in Tariff register covers installations from 2010 to 2019 inclusive; post-2019 adoption under the Smart Export Guarantee is not captured. LSOA-level analysis may mask within-area variation. GWR coefficients are correlational, not causal. The five-cluster solution is presented as a heuristic typology rather than a definitive partition; alternative cluster counts produce broadly similar core groupings. The temporal mismatch between FiT data (2010–2019) and predictor snapshots (Census 2021, IMD 2019) is discussed in §3.2.1 of the paper. See the paper's Limitations section for a full discussion.

## License

Code in this repository is released under the Apache License 2.0 — see `LICENSE`.

The underlying datasets are subject to their original licences (predominantly the Open Government Licence v3.0); see `data/README.md` for per-dataset terms.

## Citation

If you use this code or build on this analysis, please cite the paper:

> Guder, M., Almutairi, A., Desai, S., D Souza, J., & Mensah, W. (forthcoming). *Socio-Spatial Drivers and Regional Typologies of Domestic Solar PV Adoption in England: Integrating Geographically Weighted Regression with Cluster Analysis.*

A BibTeX entry will be added once publication details are confirmed.

## Acknowledgements

This research was conducted as part of a term project at Cranfield University. Open data were provided by Ofgem, the Office for National Statistics, the Department for Energy Security and Net Zero, and the UK Data Service. All analysis was conducted using open-source software.

## Contact

For questions about the paper, contact Mennan Guder (`mennan.guder@cranfield.ac.uk`).
For questions about the code or repository, contact Sonali Desai (`s.desai.719@cranfield.ac.uk` or `sonalidesai9697@gmail.com`).
