# Healthcare Accessibility Analysis in Sub-Saharan African Cities

This repository contains Python scripts to analyze healthcare accessibility across 19 sub-Saharan African cities. The analysis is based on spatial accessibility (SA) metrics, travel time calculations, and relative risk (RR) evaluations between formal and informal urban settlements. Our study combines various data sources, including population datasets, street networks, healthcare facilities, and land-use classifications, to provide a detailed assessment of healthcare access disparities.

## Methods Overview

The code implements a healthcare accessibility model based on travel time to healthcare facilities. Key elements of our methodology, inspired by Levinson and Wu's theory of access assessment, include:
- **Location**: Urban areas in sub-Saharan Africa.
- **Travel Cost**: Measured in travel time (minutes) via isochrone analysis.
- **Healthcare Focus**: All types of healthcare facilities, with a specific analysis on hospitals for comparative purposes.
- **Mode of Transport**: Walking, given its primary role in healthcare access in SSA.
- **Urban Morphology**: Differentiation between formal and informal settlements, as a proxy for socio-economic factors.

The accessibility calculations were performed using transportation network analysis in ESRI ArcGIS Pro 3.2.1, leveraging OpenStreetMap (OSM) data for street networks. Healthcare facility locations were obtained from a geocoded public health facility dataset, while population data were sourced from the WorldPop Constrained UN adjusted dataset.

## Data Sources

The data inputs used in this analysis include:
1. **Land Use and Land Cover (LULC)**: Guzder Williams et al. classification (2023), which categorizes residential areas into formal and informal subdivisions.
2. **Population Data**: WorldPop dataset (2020), with a spatial resolution of 100m, providing a baseline for population estimates.
3. **Street Networks**: OpenStreetMap data, allowing for a detailed street network representation to assess pedestrian travel paths.
4. **Healthcare Facilities**: Maina et al. dataset (2019), containing locations of healthcare facilities across sub-Saharan Africa.

## Code Structure

The code in this repository performs the following tasks:

### 1. Accessibility Analysis
   - **Load Data**: Import population and healthcare facility data, along with land-use classifications.
   - **Travel Time Calculation**: Generate service areas for healthcare facilities for every one-minute interval up to 120 minutes.
   - **Aggregation and Normalization**: Normalize the accessible population in each service area by the total city population.
   - **Uncertainty Calculation**: Adjust walking speed by ±20% to account for intra-urban variations and generate uncertainty intervals around travel time estimates.

### 2. Visualization
   - **Service Area Accessibility Plot**: A time series of accessibility (SA) over time for each city, illustrating the proportion of the population within set travel time thresholds.
   - **Relative Risk (RR) Visualization**: A plot comparing accessibility between formal and informal areas using relative risk (RR) calculations, with uncertainty intervals. An RR > 1 suggests greater accessibility in formal areas, while RR < 1 indicates higher accessibility in informal areas.

### 3. Relative Risk Calculation
   - **RR Calculation**: For each time interval, calculate the relative risk as the ratio of SA in formal areas to SA in informal areas.
   - **Uncertainty Intervals**: Estimate upper and lower RR bounds based on adjusted walking speeds.

## Key Variables and Parameters

- **`time_of_interest`**: Specifies the travel time threshold (e.g., 15, 30, 60 minutes).
- **`uncertainty`**: A ±20% margin used to account for variability in walking speed across urban landscapes.
- **`hospital`**: The healthcare facility category (e.g., hospitals only or all healthcare facilities).

## Usage Instructions

1. **Install Dependencies**: Ensure Python libraries `pandas`, `matplotlib`, and `numpy` are installed.
2. **Prepare Data**: Place CSV files for `population_in_service_area_<hospital>.csv`, `Total_Population.csv`, and other required datasets in the same directory.
3. **Run Code**: Execute the Python scripts in sequence to generate the accessibility and relative risk plots.
4. **View Results**: The output includes time series and relative risk plots, saved to the specified output directory.

## Interpretation of Results

- **Spatial Accessibility (SA)**: Shows the share of the population that can reach healthcare within a given travel time.
- **Relative Risk (RR)**: Quantifies the disparity in accessibility between formal and informal areas. An RR > 1 indicates a higher share of the population in formal areas has access within the specified time, while RR < 1 suggests better access in informal areas.

## Limitations and Considerations

While the dataset used in this study is the best available at this scale, several limitations are noted:
- **Data Quality in Informal Areas**: Population data and road networks may be less accurate in informal settlements.
- **Network Constraints**: OSM data primarily maps motorized roads, so pedestrian paths may be underrepresented.
- **Urban Morphology as a Proxy**: Although urban morphology is a useful indicator of socio-economic differences, it cannot fully capture all factors affecting healthcare accessibility.

## Acknowledgements

This work is based on methodologies from Levinson and Wu's access theory and relies on datasets from Guzder Williams et al. (2023), WorldPop (2020), OpenStreetMap, and Maina et al. (2019).

## References

John Friesen, Stefanos Georganos, Jan Haas et al. Differences in walking access to health-care services between formal and informal areas in 19 sub-Saharan cities, 05 February 2024, PREPRINT (Version 1) available at Research Square [https://doi.org/10.21203/rs.3.rs-3909438/v1]

---

This README provides an overview of the analysis process, data requirements, and interpretation of results for healthcare accessibility in sub-Saharan African cities.
