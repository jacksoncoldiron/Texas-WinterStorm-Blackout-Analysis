Houston Blackout Analysis (February 2021 Winter Storm)
## Overview

This repository contains a spatial analysis of the February 2021 Texas winter storm and its impact on electrical power distribution across the Houston metropolitan area. Using satellite imagery, OpenStreetMap infrastructure data, and socioeconomic census data, this project identifies areas that lost power and examines whether outage impacts were disproportionately experienced across income levels.

The project demonstrates skills in raster and vector data processing, spatial joins, and map visualization using R.

## Repository Structure
EDS223-HW3/
├── README.md                # Project documentation (this file)
├── texas_blackout.qmd       # Quarto document containing full analysis
├── .gitignore               # Prevents data files from being pushed
├── data/                    # Contains input datasets (excluded from GitHub)
│   ├── VNP46A1/             # VIIRS night light imagery
│   ├── gis_osm_buildings_a_free_1.gpkg
│   ├── gis_osm_roads_free_1.gpkg
│   └── ACS_2019_5YR_TRACT_48_TEXAS.gdb
└── outputs/                 # Rendered figures and final PDF (if included)

## Data Access

All datasets used in this analysis are publicly available but are not stored directly in this repository due to size.
To reproduce the analysis:

Download all data files from the sources cited below.

Place them inside the data/ folder using the same directory structure shown above.

Run texas_blackout.qmd to reproduce the results.

## Data Sources and Citations

1. VIIRS Night Lights
NASA (2021). Visible Infrared Imaging Radiometer Suite (VIIRS) Day/Night Band Daily Data Product (VNP46A1), Version 1.
NASA Level-1 and Atmosphere Archive & Distribution System Distributed Active Archive Center (LAADS DAAC), Goddard Space Flight Center.
Tiles used: h08v05 and h08v06, collected on February 7 and February 16, 2021.
Retrieved from: https://ladsweb.modaps.eosdis.nasa.gov

2. Roads
OpenStreetMap contributors (2021). OpenStreetMap Data Extracts — Texas (Road Network).
Geofabrik GmbH, Karlsruhe, Germany.
https://download.geofabrik.de/north-america/us/texas.html

3. Buildings
OpenStreetMap contributors (2021). OpenStreetMap Data Extracts — Texas (Building Footprints).
Geofabrik GmbH, Karlsruhe, Germany.
https://download.geofabrik.de/north-america/us/texas.html

4. Socioeconomic Data
U.S. Census Bureau (2019). American Community Survey (ACS) 2019 5-Year Estimates: Census Tracts for Texas (State FIPS 48).
Retrieved from: https://www.census.gov/programs-surveys/acs

## Analysis Summary

The analysis proceeds in four key stages:

#### Blackout Detection:
VIIRS night-light imagery before (Feb 7) and after (Feb 16, 2021) the storm is compared to identify significant reductions in nighttime radiance (> 200 nW·cm⁻²·sr⁻¹).

#### Highway Exclusion:
Areas within 200 m of highways are excluded to avoid misclassification from reduced vehicle lighting.

#### Residential Impact Estimation:
Residential building footprints from OpenStreetMap are intersected with blackout polygons to estimate the number of homes likely impacted.

#### Socioeconomic Comparison:
Median household income from 2019 ACS census tract data is used to evaluate disparities between tracts that experienced blackouts and those that did not.

## Results Overview

Estimated Homes Impacted: ~r format(n_homes_imp, big.mark=",") homes within Houston metropolitan area

Number of Impacted Census Tracts: r length(impacted_tract_ids)

Median Household Income:

Blackout tracts: $r format(round(income_summary$median[income_summary$blackout == "Blackout"]), big.mark=",")

Non-blackout tracts: $r format(round(income_summary$median[income_summary$blackout == "No Blackout"]), big.mark=",")

The findings suggest that lower-income tracts were disproportionately affected by the 2021 blackout, underscoring the need to consider social vulnerability in energy infrastructure resilience planning.

## Author

Jackson Coldiron
Master of Environmental Data Science (MEDS)
University of California, Santa Barbara
GitHub: @jackson-coldiron

## Acknowledgements

This repository was developed as part of the EDS 223 – Geospatial Analysis course at the Bren School of Environmental Science & Management (UCSB).
Guidance and materials provided by Sam Csik, Julien Brun, Ruth Oliver, Carmen Galaz Garcia, and Max Czapanskiy.

## License

This project is licensed under the MIT License.
See the LICENSE
 file for details.
