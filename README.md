# 🏠 House Price Prediction (Excel Dataset)

An end-to-end machine learning project that predicts house sale prices (in INR lakhs) from property features, using a dataset stored in an **Excel workbook**.

## Project structure
```
house-price-prediction/
├── data/house_prices.xlsx          # Dataset (House_Data + Data_Dictionary sheets)
├── House_Price_Prediction.ipynb    # Main notebook (already executed, with outputs)
├── models/house_price_model.pkl    # Trained & tuned model pipeline
├── outputs/predictions.xlsx        # Test-set predictions + model comparison
├── generate_dataset.py             # Script that created the synthetic dataset
├── requirements.txt
└── README.md
```

## Dataset
1,512 rows × 13 columns: Location, Area_sqft, Bedrooms, Bathrooms, Balconies, Floor, Total_Floors, Age_Years, Furnishing, Parking_Spaces, Near_Metro → **Price_Lakhs** (target).

The data is synthetic and intentionally includes **missing values, 12 duplicate rows and 5 price outliers** so the cleaning steps can be practised.

## Workflow
1. Load data from Excel (`pd.read_excel`)
2. Data understanding (info, describe, missing values, duplicates)
3. Cleaning — drop duplicates, remove extreme outliers using IQR on price per sqft
4. EDA — distributions, price by location, area vs price, correlation heatmap
5. Feature engineering — `Floor_Ratio`, `Rooms_Total`, binary `Near_Metro`
6. Leak-free preprocessing pipeline — imputation, scaling, one-hot encoding
7. Train & compare 5 models with 5-fold cross-validation
8. Hyperparameter tuning with `GridSearchCV`
9. Evaluation — actual vs predicted, residuals, feature importance
10. Save model, export predictions to Excel, predict a new house

## Results (test set)
| Model | CV R² | MAE (lakhs) | RMSE (lakhs) | R² |
|---|---|---|---|---|
| **Gradient Boosting (tuned)** | 0.910 | **8.19** | **12.11** | **0.918** |
| Gradient Boosting | 0.905 | 8.23 | 12.24 | 0.916 |
| Random Forest | 0.892 | 9.04 | 13.34 | 0.901 |
| Ridge Regression | 0.883 | 10.65 | 14.67 | 0.880 |
| Linear Regression | 0.883 | 10.68 | 14.68 | 0.880 |
| Decision Tree | 0.806 | 12.00 | 17.01 | 0.839 |

## How to run
```bash
pip install -r requirements.txt
jupyter notebook House_Price_Prediction.ipynb
```
To use your own Excel data, replace `data/house_prices.xlsx` (keep the same column names) and re-run the notebook.

## Next steps
- Log-transform the target (price is right-skewed)
- Try XGBoost / LightGBM
- Deploy as a Streamlit or Flask web app
