# Data Sources

The notebook reads raw data from this `data/` folder. **None of the data files are committed to the repo** — download each from the source below and place it in the structure shown.

All datasets are published under the Open Government Licence v3.0. Files were downloaded in **March 2026**; URLs may change, so verify each link before downloading.

## Required folder structure

```
data/
├── Census data/
│   ├── TS017-2021-1-filtered-2026-03-30T15_36_20Z.csv
│   ├── TS041-2021-3-filtered-2026-03-31T12_29_48Z.csv
│   ├── TS044-2021-1-filtered-2026-03-30T15_35_49Z.csv
│   ├── TS054-2021-1-filtered-2026-03-30T15_35_18Z.csv
│   ├── TS066-2021-1-filtered-2026-03-30T15_36_57Z.csv
│   └── census2021-ts007a-lsoa.csv
├── Deprivation data/
│   └── File_7_-_All_IoD2019_Scores__Ranks__Deciles_and_Population_Denominators_3.csv
├── Electricity data/
│   └── LSOA_domestic_elec_2010-2024.xlsx
├── FIT data/
│   ├── Feed-in Tariff installation report part 1_0.xlsx
│   ├── Feed-in Tariff installation report part 2_0.xlsx
│   └── Feed-in Tariff installation report part 3_0.xlsx
└── Shapefiles/
    ├── LSOA_2011_EW_BFC_V3.shp
    ├── LSOA_2011_EW_BFC_V3.shx
    ├── LSOA_2011_EW_BFC_V3.dbf
    └── LSOA_2011_EW_BFC_V3.prj
```

## Sources

1. Census 2021 LSOA tables (TS007A, TS017, TS041, TS044, TS054, TS066)
Source: ONS / Nomisweb — https://www.nomisweb.co.uk/sources/census_2021_bulk
Folder: Census data/


2. IMD 2019, File 7 — Scores, Ranks, Deciles and Population Denominators
Source: gov.uk — https://www.gov.uk/government/statistics/english-indices-of-deprivation-2019
Folder: Deprivation data/


3. Sub-national domestic electricity consumption, LSOA, 2010–2024
Source: DESNZ — https://www.gov.uk/government/collections/sub-national-electricity-consumption-data
Folder: Electricity data/


4. Feed-in Tariff Installation Register
Source: Ofgem — https://www.ofgem.gov.uk/feed-tariffs-fit/contacts-guidance-and-resources/public-reports-and-data-fit/installation-reports?facet_case_publication_type=1616
Folder: FIT data/


5. LSOA 2011 boundaries (BFC, England and Wales, V3)
Source: ONS Open Geography Portal — https://geoportal.statistics.gov.uk/
Folder: Shapefiles/
