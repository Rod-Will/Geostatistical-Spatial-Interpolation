```markdown
# Geostatistical Spatial Interpolation Workflow

This repository contains a complete workflow for geostatistical spatial interpolation applied to geothermal gradient data within Colombia. The script performs data pre-processing, variogram analysis, multiple spatial interpolation methods, and extensive visualization. All outputs—including fitted variogram metrics, cross-validation (CV) metrics, interpolated grids, and plots—are automatically saved to organized output folders.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Repository Structure](#repository-structure)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Workflow Details](#workflow-details)
- [Output Examples](#output-examples)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## Overview

This repository implements a geostatistical spatial interpolation workflow that:
- Loads and cleans geospatial data (removing outliers using the IQR method).
- Computes the experimental variogram and fits theoretical models (spherical, exponential, and gaussian).
- Performs 5-fold cross-validation using various kriging-based interpolation methods:
  - **Ordinary Kriging (OK)**
  - **Simple Kriging (SK)**
  - **Universal Kriging with AI detrending (UK_AI)**
  - **Universal Kriging with linear drift (UK_linear)**
  - **Universal Kriging with quadratic drift (UK_quadratic)**
- Generates a prediction grid within the Colombia boundary and applies the interpolation methods.
- Visualizes the results with maps, scatter plots, histograms, and comparison plots.
- Saves all results (CSV files and PNG images) in a structured output directory.

---

## Features

- **Data Preparation:** Loads input data and a Colombia shapefile, then removes outliers from the target variable.
- **Variogram Analysis:** Computes experimental variograms and fits three theoretical models.
- **Cross-Validation:** Implements 5-fold CV to evaluate multiple spatial interpolation methods using RMSE, MAE, and R².
- **Spatial Prediction:** Generates a prediction grid, applies interpolation, and masks the results using the Colombia boundary.
- **Visualization:** Creates various plots including:
  - Data location scatter plots
  - Variogram plots with fitted theoretical models
  - Dual-axis CV metric comparison plots
  - Observed vs. predicted scatter plots per model
  - Final spatial interpolation maps and histograms
- **Output Management:** Organizes outputs in dedicated folders for models, plots, and results.

---

## Repository Structure

```plaintext
├── Data/
│   ├── data_pre_norm.csv      # Input dataset (a subset of data for testing)
│   └── COL_adm0.shp           # Colombia boundary shapefile
├── Output_03/
│   ├── models/                # (Optional) Saved model objects
│   ├── plots/                 # Generated plots (PNG format)
│   └── results/               # CSV files with variogram fitting metrics, CV metrics, and interpolated values
├── spatial_interpolation.py   # Main script implementing the workflow
└── README.md                  # This file
```

---

## Requirements

- **Python:** 3.x  
- **Libraries:**
  - `numpy`
  - `pandas`
  - `geopandas`
  - `matplotlib`
  - `gstools`
  - `pykrige`
  - `scikit-learn`
  - `shapely`
  - `scipy`

---

## Installation

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/your_username/geostatistical-interpolation.git
   cd geostatistical-interpolation
   ```

2. **Install Dependencies:**

   You can install the required Python packages via pip:

   ```bash
   pip install numpy pandas geopandas matplotlib gstools pykrige scikit-learn shapely scipy
   ```

---

## Usage

1. **Prepare Your Data:**
   - Place your input dataset (`data_pre_norm.csv`) and the Colombia boundary shapefile (`COL_adm0.shp`) in the `Data/` directory.

2. **Run the Script:**

   Execute the main Python script:

   ```bash
   python spatial_interpolation.py
   ```

3. **Review Outputs:**
   - All outputs (models, plots, and CSV files) are saved in the `Output_03/` directory.
   - Inspect the generated plots in the `Output_03/plots/` folder and review the metrics in the `Output_03/results/` folder.

---

## Workflow Details

The script follows these major steps:

1. **Setup Output Folders:**  
   Automatically creates directories to store models, plots, and results.

2. **Data Loading and Pre-processing:**  
   Loads the first 500 rows of the dataset and the Colombia boundary shapefile. Outliers in the target variable ("Apparent Geothermal Gradient (°C/Km)") are removed using the IQR method.

3. **Variogram Analysis:**  
   - Computes pairwise distances and semivariance.
   - Bins the experimental variogram for smoothing.
   - Fits three theoretical models (spherical, exponential, gaussian) using optimization.

4. **5-Fold Cross-Validation:**  
   Evaluates five spatial interpolation methods:
   - **Ordinary Kriging (OK)**
   - **Simple Kriging (SK)**
   - **Universal Kriging with AI detrending (UK_AI)**
   - **Universal Kriging with linear drift (UK_linear)**
   - **Universal Kriging with quadratic drift (UK_quadratic)**
   
   For each method, RMSE, MAE, and R² are computed and visualized using:
   - Dual-axis bar/line plots for CV metrics.
   - Scatter plots comparing observed vs. predicted values.

5. **Full-Dataset Spatial Interpolation:**  
   - Generates a prediction grid based on the Colombia boundary.
   - Applies each interpolation method over the entire dataset.
   - Saves the interpolated values to a CSV file.

6. **Visualization:**  
   - Masks the interpolated grids to the Colombia boundary.
   - Produces final scatter maps and histograms for the best-performing model.
   - Generates spatial maps and histograms for each interpolation method with a consistent color scale.

7. **Output:**  
   - Prints CV metrics and identifies the best spatial interpolation model based on the lowest RMSE.

---

## Output Examples

- **Data Location Plot:** Shows raw data points overlaid on the Colombia boundary.
- **Variogram Plot:** Displays the experimental variogram along with the fitted theoretical models.
- **CV Metrics Plot:** Dual-axis plot comparing RMSE, MAE, and R² across different methods.
- **Final Spatial Map and Histogram:** Illustrates the spatial interpolation (e.g., using UK_linear) with a scatter map and a colored histogram.
- **Method-Specific Maps:** Spatial interpolation maps and histograms for each of the five methods.

All these outputs are saved in the `Output_03/plots/` and `Output_03/results/` directories.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

---

## Acknowledgements

This project leverages several powerful open-source libraries for geospatial analysis and spatial statistics. Special thanks to the developers and maintainers of:
- [gstools](https://github.com/GeoStat-Framework/gstools)
- [pykrige](https://github.com/GeoStat-Framework/pykrige)
- [geopandas](https://geopandas.org/)
- [scikit-learn](https://scikit-learn.org/)

Your contributions make projects like this possible!

```

Happy Interpolating!
```
