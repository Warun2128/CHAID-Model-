# 🌳 CHAID Decision Tree Model for Terrain & Environmental Classification

This project implements a CHAID (Chi-square Automatic Interaction Detector) decision tree model to classify terrain types using complex geospatial, environmental, and vegetation-based data. The workflow includes end-to-end data preprocessing, flattening nested JSON structures, feature transformation, model training, and interpretability using CHAID-based rules.

**## 📌 Project Overview**
This repository demonstrates how to build an interpretable rule-based classification system using the CHAID algorithm, which performs multi-level chi-square-driven splitting. The dataset includes environmental layers such as:
Vegetation indicators (NDVI, EVI, spectral means)
Land Surface Temperature
Soil characteristics
Weather attributes
Topography (elevation, slope, terrain roughness)
The goal is to transform raw satellite-derived JSON data into a structured tabular format and use CHAID to create a clear, transparent classification tree.
**1. Data Preprocessing**
     The project includes several preprocessing stages:
     Parsing complex JSON structures
     Extracting nested fields for vegetation, weather, soil, and topography
     Converting lists and multi-dimensional arrays into usable feature columns
     Cleaning & Feature Engineering
     Handling missing values
     Converting categorical fields to strings (required by CHAID)
     Creating features such as:
     slope_mean
     elevation_mean
     terrain_type
     soil_categories
     Normalized vegetation indicators
     Label Preparation
Encoding the terrain category as the target label
Balancing the dataset where possible
**2. CHAID Model Training**
This project uses a pure-Python CHAID implementation to:
 Build a decision tree using chi-square significance
 Perform multi-level categorical splitting
 Identify most significant predictor variables 
 Generate easy-to-interpret rule-based outputs
** 3. Model Results & Observations**
CHAID selected meaningful, statistically significant predictors
The model primarily split on environmental variables such as:
Vegetation indices
Elevation ranges
Slope values
Soil and terrain descriptors
     Clear rule-based decision structure

The resulting CHAID tree produced readable branches like:

IF elevation_mean > threshold
   AND soil_type = X
      THEN terrain_type = Mountain

✔ Better interpretability than standard decision trees

CHAID handled categorical splitting more naturally and reduced unnecessary branches.

✔ Data imbalance impacted model depth

Some terrain categories had fewer samples, limiting deeper splits.

## 🧪 4. Key Evaluation Metrics
CHAID tree summary printed directly from the model
Class distribution at each node
Significant split p-values
Tree depth and number of branches
These results help understand why the model made certain decisions.

## 📁 5. Repository Structure
📦 CHAID-Model-Project
 ┣ 📜 CHAID_model.ipynb          # Main notebook with full pipeline
 ┣ 📜 sample_data.json           # Example raw dataset (nested JSON)
 ┣ 📜 README.md                  # Project documentation
 ┗ 📂 outputs/
     ┗ 📜 chaid_tree_summary.txt # Generated CHAID tree summary

## 🚀 6. How to Run
Install dependencies
pip install pandas numpy chaid matplotlib

Run the notebook
jupyter notebook CHAID_model.ipynb

## 🔍 7. What I Observed

CHAID successfully handled categorical logic and produced explainable splits.

Only a few features dominated the classification (vegetation + elevation + slope).

Data sparsity and imbalance reduced overall model accuracy.

Despite limitations, the resulting tree provided strong interpretability and clarity.

## 🏁 8. Conclusion

This project demonstrates how CHAID can be used to interpret complex environmental datasets and generate fully transparent decision-making logic. It is especially useful in applications where explainability matters—such as terrain classification, environmental monitoring, and geospatial decision systems.
