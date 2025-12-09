🌳 CHAID Decision Tree Model on MODIS NDVI Dataset

A complete implementation of CHAID classification using satellite-derived vegetation indices

📌 Project Overview

This project demonstrates how to build a CHAID (Chi-square Automatic Interaction Detection) decision-tree classifier using MODIS satellite NDVI data.
The workflow includes:

Extracting reflectance and NDVI values from JSON (response.json)

Categorizing NDVI values into discrete bins (value_cat)

Defining vegetation health classes (NDVI_class)

Training a CHAID model using the pandas-CHAID library

Interpreting the CHAID split results

Creating visualizations for deeper insight

This repository also includes the finalized Jupyter Notebook:
📄 Final_chaid_Model.ipynb

📂 Dataset

The dataset originates from MODIS (MOD13Q1) satellite collection and includes:

NDVI values

Reflectance bands (Red, NIR, Blue, MIR)

Quality and reliability flags

Time-stamped 9×9 pixel grids

From this, a flattened tabular dataset was created for CHAID modeling.

🔧 Preprocessing Steps

Load the JSON dataset

Extract NDVI values from MODIS "subset" blocks

Convert raw NDVI values into categorical bins:

df["value_cat"] = pd.qcut(df["value"], q=4, labels=["Low", "Medium", "High", "Very High"])


Map NDVI values to vegetation health classes:

df["NDVI_class"] = pd.cut(
    df["value"], 
    bins=[0, 1000, 2000, 3000, 4000],
    labels=["Poor", "Moderate", "Good", "Excellent"]
)

🤖 CHAID Model Implementation

The model uses the pandas-CHAID library:

from CHAID import Tree

tree = Tree.from_pandas_df(
    df, 
    {'value_cat': 'nominal'}, 
    "NDVI_class"
)

tree.print_tree()

🌳 CHAID Tree Output

The final CHAID tree identified value_cat as the only significant predictor of NDVI_class.

([], {'Poor': 1024, 'Good': 96, 'Moderate': 882, 'Excellent': 264, 'missing': 240})
|-- (['High'], {...}, <Invalid Chaid Split>)
|-- (['Low'], {...}, <Invalid Chaid Split>)
|-- (['Medium'], {...}, <Invalid Chaid Split>)
+-- (['Very High'], {...}, <Invalid Chaid Split>)

✔ Interpretation

The model created four terminal nodes, one for each NDVI category.

No further splits were possible (as expected with a single predictor).

Each category maps to distinct vegetation health distributions.

This validates the strong relationship between NDVI value ranges and vegetation condition.

📊 Visualizations

The notebook includes the following visuals:

1. NDVI Category Distribution

Bar chart showing counts of each NDVI bin.

2. NDVI Category vs Vegetation Class (Heatmap)

A chi-square style visualization showing how CHAID relates the two variables.

3. Decision Tree Diagram (GraphViz)

A simple representation of the CHAID tree structure.

🧠 Key Insights

NDVI categories (value_cat) are the primary driver of vegetation class.

CHAID confirms a nearly monotonic relationship between NDVI and vegetation condition.

The model is straightforward due to the nature of the dataset (pre-segmented NDVI bins).

🚀 Technologies Used

Python 3

pandas

numpy

seaborn / matplotlib

pandas-CHAID library

🗂 Repository Structure
│
├── Final_chaid_Model.ipynb        # Complete CHAID model notebook
├── response.json                  # Original MODIS dataset
├── chaid_tree.png                 # Optional generated tree visualization
├── README.md                      # Project documentation

📘 How to Run

Install dependencies:

pip install pandas numpy seaborn matplotlib CHAID


Open the notebook:

jupyter notebook Final_chaid_Model.ipynb


Run all cells to reproduce results.

📢 Author

Varun Kumar Reddy Gujja
Data Analyst & Machine Learning Enthusiast
