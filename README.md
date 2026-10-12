# Food Delivery Time Prediction and Analysis Using Predictive Analytics

**B.Tech 7th Semester — Predictive Analytics CA3**

## Problem Statement

Food delivery time can depend on distance, traffic, weather, vehicle conditions and other order details. This project uses historical delivery data to predict delivery time in minutes. It is a regression problem.

## Objective

To follow the KDD (Knowledge Discovery in Databases) process, compare three regression algorithms, evaluate their performance and estimate delivery time for a new order.

## Dataset

- **Records:** 41,953 rows and 20 columns.
- **Date range:** 11 February 2022 to 6 April 2022.
- **Original dataset:** `dataset/India-Food-Delivery-Time-Prediction.txt`
- **Clean CSV:** `data/food_delivery.csv`
- **Target variable:** `Time_taken(min)`

The original `.txt` file contains JSON data and is preserved unchanged. The dataset includes delivery person details, restaurant and delivery location coordinates, weather, traffic, vehicle information, order details and delivery time.

The notebook loads the original dataset and performs data cleaning during execution. The clean CSV is included separately in the project.

## Methodology

The project follows these predictive analytics stages:

1. **Data Understanding:** Inspect the dataset, columns, missing values and summary statistics.
2. **Data Cleaning:** Standardize text values, correct inconsistent spelling and convert columns to suitable data types.
3. **Feature Engineering:** Calculate straight-line delivery distance using the Haversine formula and create order-time features.
4. **Exploratory Data Analysis:** Use graphs to explore delivery times by traffic, weather, vehicle type and distance.
5. **Data Partitioning:** Split orders chronologically into training, validation and testing sets.
6. **Data Preprocessing:** Handle missing values, scale numerical features and encode categorical features using transformations fitted on training data only.
7. **Model Building:** Train three regression algorithms.
8. **Model Evaluation:** Compare prediction errors and select a model using validation RMSE.
9. **Interpretation:** Examine feature importance and make a sample delivery-time prediction.

The chronological split contains 24,041 training records, 9,061 validation records and 8,851 test records.

Pickup time and record identifiers are excluded from model inputs. The `multiple_deliveries` feature is also excluded because its availability at prediction time is unclear. The prediction is intended to be made before pickup.

## Models Used

1. **Linear Regression** — establishes a simple baseline for prediction.
2. **Decision Tree Regressor** — learns decision rules from the data.
3. **Random Forest Regressor** — combines multiple decision trees to make predictions.

All three models are evaluated using the same test set.

## Evaluation Metrics

- **MAE (Mean Absolute Error):** Average absolute prediction error, in minutes.
- **MSE (Mean Squared Error):** Average squared prediction error.
- **RMSE (Root Mean Squared Error):** Square root of MSE, expressed in minutes.
- **MAPE (Mean Absolute Percentage Error):** Average absolute error as a percentage.

Lower values generally indicate better prediction performance.

### Results

The following results are from the current saved notebook run.

| Model | MAE | MSE | RMSE | MAPE |
|---|---:|---:|---:|---:|
| Linear Regression | 4.920 | 38.321 | 6.190 | 21.579% |
| Decision Tree | 3.521 | 19.997 | 4.472 | 15.128% |
| Random Forest | **3.356** | **17.567** | **4.191** | **14.410%** |

Random Forest achieved the lowest validation RMSE and the lowest test errors among the three models in this run. Results can vary slightly across software environments.

## Project Structure

```text
food-delivery-time-prediction/
├── dataset/
│   └── India-Food-Delivery-Time-Prediction.txt
├── data/
│   └── food_delivery.csv
├── notebooks/
│   └── Food_Delivery_Time_Prediction.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## How to Run

Use **Python 3.11**. Open PowerShell in the project folder and run:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m ipykernel install --user --name food-delivery-ca3 --display-name "Python (Food Delivery CA3)"
.\.venv\Scripts\python.exe -m notebook notebooks/Food_Delivery_Time_Prediction.ipynb
```

In the notebook, select the **Python (Food Delivery CA3)** kernel and choose **Restart Kernel and Run All Cells**.

In VS Code, open the notebook and select the `.venv` Python environment as the kernel. Run the cells in order to regenerate the graphs, model-comparison results, feature-importance output and sample prediction.

The project uses the supplied dataset and does not require an external data download. Model training may take a few minutes depending on the computer.

## Conclusion

This project demonstrates an end-to-end predictive analytics workflow for food delivery time estimation. Three regression algorithms are trained and compared using MAE, MSE, RMSE and MAPE. In the current saved run, Random Forest performs best among the three models.

The sample prediction is an estimate rather than a guaranteed arrival time. The calculated distance is straight-line distance, not actual road distance, which is one limitation of the project.
