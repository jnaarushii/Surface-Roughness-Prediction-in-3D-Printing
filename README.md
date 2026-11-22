# Surface Roughness Prediction in 3D Printing Using Machine Learning

## Overview

This project develops and evaluates supervised machine learning
regression models to predict the surface roughness of parts manufactured
using Fused Deposition Modelling (FDM).

Surface roughness is an important measure of the surface finish of a
3D-printed component. It can be influenced by printing parameters such
as layer height, wall thickness, infill settings, nozzle temperature,
bed temperature, print speed, material and fan speed.

The project uses recorded FDM process parameters to estimate surface
roughness and compares different regression approaches using standard
evaluation metrics.

## Objectives

- Study the relationship between FDM printing parameters and surface
  roughness.
- Inspect and explore the supplied dataset.
- Preprocess numerical and categorical input variables.
- Implement and compare regression models.
- Evaluate model performance using MAE, RMSE and R².
- Identify the best-performing model for the evaluated test split.

## Input Features

The model uses the following input features:

| Feature              | Description                                            |
|----------------------|--------------------------------------------------------|
| `layer_height`       | Thickness of each deposited layer                      |
| `wall_thickness`     | Wall thickness setting                                 |
| `infill_density`     | Percentage of internal infill                          |
| `infill_pattern`     | Internal infill arrangement, such as grid or honeycomb |
| `nozzle_temperature` | Temperature of the extrusion nozzle                    |
| `bed_temperature`    | Temperature of the build plate                         |
| `print_speed`        | Speed at which material is deposited                   |
| `material`           | Filament material category                             |
| `fan_speed`          | Cooling fan setting                                    |

**Target variable:** `roughness` — measured surface roughness in
micrometres (µm).

The columns `tension_strenght` and `elongation` are excluded from the
model input features.

## Project Workflow

1.  **Dataset loading:** Load the CSV file using Pandas.
2.  **Data inspection:** Check column names, data types, missing values,
    duplicate records and descriptive statistics.
3.  **Exploratory Data Analysis (EDA):**
    - Histogram with a kernel-density curve to examine roughness
      distribution.
    - Box plot to inspect the spread and potential outliers in
      roughness.
    - Correlation heatmap to examine relationships among numerical
      variables.
    - Box plots to compare roughness across infill patterns and
      materials.
4.  **Feature and target selection:** Separate the input features from
    the `roughness` target.
5.  **Train-test split:** Divide the data into training and testing
    sets.
6.  **Preprocessing:**
    - Fill missing numerical values using the training-set median.
    - Fill missing categorical values using the training-set mode.
    - Apply one-hot encoding to categorical variables.
    - Align encoded test columns with training columns.
    - Standardise input arrays for Linear Regression and SVR.
7.  **Model training:** Train the regression models.
8.  **Evaluation:** Compare predictions using MAE, RMSE and R².

## Machine Learning Models

The project implements the following regression approaches:

- **Linear Regression:** Models a linear relationship between the input
  features and the continuous target.
- **Decision Tree Regression:** Splits the feature space into regions
  and predicts a value at each leaf.
- **Random Forest Regression:** Combines predictions from multiple
  decision trees.
- **Support Vector Regression (SVR):** Fits a function while allowing
  errors within an epsilon margin.

The Decision Tree, Random Forest and SVR implementations are custom
implementations in the notebook.

## Evaluation Metrics

- **Mean Absolute Error (MAE):** Mean of the absolute differences
  between actual and predicted roughness values. Lower values are
  better.
- **Root Mean Squared Error (RMSE):** Square root of the mean squared
  prediction error. Lower values are better.
- **R² Score:** Measures predictive fit relative to a mean-value
  baseline. A value closer to 1 indicates a better fit; a negative value
  indicates performance worse than the baseline on the evaluated test
  set.

## Reported Results

For the evaluated test split, the report records the following model
performance:

| Model             |  MAE (µm) | RMSE (µm) |  R² Score |
|-------------------|----------:|----------:|----------:|
| Linear Regression | 31.144977 | 39.842069 |  0.657882 |
| Random Forest     | 37.987674 | 46.375501 |  0.536479 |
| Decision Tree     | 44.280000 | 51.530986 |  0.427693 |
| SVR               | 71.743285 | 83.894102 | -0.516894 |

Linear Regression gives the best performance among the implemented
models for the evaluated test split, based on the lowest MAE and RMSE
and the highest R² score.

## Repository Structure

``` text
.
├── data.csv
├── AI_PROJECT_(006_&_025) (1)(2).ipynb
└── README.md
```

The notebook filename may differ depending on how the project files are
saved.

## Requirements

- Python 3
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn

## How to Run

1.  Place `data.csv` in the same working directory as the notebook.
2.  Install the required libraries.
3.  Open the Jupyter Notebook.
4.  Run the cells in sequence to inspect the data, perform
    preprocessing, train the models and view the evaluation results.

## Limitations and Future Scope

- The model is evaluated using a single train-test split, so results may
  vary with a different split.
- The dataset has limited coverage of printing conditions and does not
  provide external validation across other printers or materials.
- The models produce point predictions without uncertainty estimates.

Possible future improvements include collecting more measurements,
tuning model hyperparameters, comparing with standard library
implementations, adding residual and feature-importance analysis, and
validating the models on other printers and materials.

## Conclusion

This project demonstrates a machine learning workflow for estimating the
surface roughness of FDM-printed parts from their printing parameters.
It includes data inspection, exploratory analysis, preprocessing,
regression model implementation and performance evaluation. Among the
implemented approaches, Linear Regression achieves the strongest
performance on the evaluated test split.
