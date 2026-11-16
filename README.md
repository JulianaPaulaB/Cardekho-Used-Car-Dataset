# Used-Car Selling Price Prediction
### A Regression Modeling Project Using the Car Details v3 Dataset
 
A data mining project that investigates which vehicle characteristics are associated with used-car selling prices and compares five regression models for estimating those prices.
 
Developed as part of Analytics Application: Finals Dossier One.
 
---
 
## 📌 Project Overview
 
Pricing a used car is difficult because two vehicles that look alike can sell for very different amounts. Age, kilometers driven, fuel type, transmission, engine size, power, and ownership history all play a part, and the effect of each is not obvious from a few listings.
 
This project uses 8,128 used-car records to examine these relationships and to test whether the available vehicle information can be used to estimate a selling price. Five regression models are trained, tested on unseen records, and compared using MAE, RMSE, and R².
 
---
 
## 🎯 Project Objectives
 
- Identify the vehicle characteristics associated with used-car selling prices.
- Support more informed pricing decisions for buyers, sellers, and dealerships.
- Develop a practical approach for estimating used-car selling prices.
- Compare LASSO, Ridge, Elastic Net, Regression Tree, and Random Forest models.
- Evaluate model performance on a separate testing set.
- Save the best model and use it to generate predictions.
---
 
## 📊 Dataset
 
**Source:** Car details v3 (used-car listings, publicly available on Kaggle)
 
| Attribute | Description |
|---|---|
| `name` | Vehicle make and model name |
| `year` | Manufacturing year |
| `selling_price` | Selling price (target variable) |
| `km_driven` | Kilometers driven |
| `fuel` | Fuel type (Diesel, Petrol, CNG, LPG) |
| `seller_type` | Individual, Dealer, or Trustmark Dealer |
| `transmission` | Manual or Automatic |
| `owner` | Ownership history |
| `mileage` | Fuel efficiency |
| `engine` | Engine capacity (CC) |
| `max_power` | Maximum power (bhp) |
| `torque` | Torque (mixed formats and units) |
| `seats` | Seating capacity |
 
The raw file has 8,128 records and 13 attributes.
 
---
 
## 🛠️ Tools and Technologies
 
- **Python** – Data processing and modeling
- **Pandas & NumPy** – Data cleaning and manipulation
- **Scikit-learn** – Preprocessing pipelines, regression models, and evaluation metrics
- **Matplotlib & Seaborn** – Data visualization
- **Joblib** – Saving and loading the best model
- **Jupyter Notebook** – Analysis and model development
---
 
## 📈 Analytical Methodology
 
1. **Business and Data Understanding** – Defined the business context, problem, objectives, assumptions, and success criteria. Inspected the data types, missing values, duplicates, and value ranges.
2. **Exploratory Data Analysis** – Examined price, year, and kilometers distributions, category frequencies, price comparisons across groups, and correlations.
3. **Data Partitioning** – Removed exact duplicates and records that are identical in every modeling feature and in the price, then split the remaining records 80% training (5,525) and 20% testing (1,382) with `random_state=42`.
4. **Data Cleaning** – Standardized text values and converted `mileage`, `engine`, and `max_power` from text to numbers. `name` and `torque` were excluded from the models.
5. **Pipeline and Model Training** – Built one preprocessing pipeline and trained five regression models.
6. **Model Comparison** – Compared the models on the testing set using MAE, RMSE, and R².
7. **Save, Load, and Predict** – Saved the best model, reloaded it, and compared its predictions with the actual prices.
### Preprocessing Pipeline
 
Imputation, scaling, and encoding are fitted on the training records only, and duplicate records are removed before the split, so no information from the testing records is used during training.
 
| Feature Type | Features | Processing |
|---|---|---|
| Numerical | `year`, `km_driven`, `mileage`, `engine`, `max_power`, `seats` | Median imputation, then standardization |
| Categorical | `fuel`, `seller_type`, `transmission`, `owner` | Most-frequent imputation, then one-hot encoding |
 
### Models Compared
 
| Model | Settings |
|---|---|
| LASSO Regression | `alpha=1.0` |
| Ridge Regression | `alpha=1.0` |
| Elastic Net Regression | `alpha=1.0` |
| Regression Tree | `max_depth=10` |
| Random Forest Regression | `n_estimators=100`, `max_depth=15` |
 
---
 
## 🧹 Data Preparation Summary
 
| Step | Result |
|---|---|
| Original records | 8,128 |
| Exact duplicates removed | 1,202 |
| Records identical in all modeling features and price removed | 19 |
| Records remaining | 6,907 |
| Training records | 5,525 |
| Testing records | 1,382 |
| Attributes used for modeling | 10 predictors + 1 target |
 
---
 
## 🏆 Model Results
 
Evaluated on the 1,382 testing records, ordered by RMSE.
 
| Model | MAE | RMSE | R² |
|---|---|---|---|
| **Random Forest** | 74,693 | 133,543 | **0.919** |
| Regression Tree | 87,158 | 158,597 | 0.886 |
| LASSO | 170,697 | 297,063 | 0.601 |
| Ridge | 170,996 | 297,221 | 0.601 |
| Elastic Net | 158,887 | 305,081 | 0.579 |
 
---
 
## 🔍 Key Findings
 
- **Random Forest performed best.** It explained about 91.9% of the variation in selling prices in the testing set.
- **Tree-based models clearly outperformed the linear models.** LASSO, Ridge, and Elastic Net stayed between 0.579 and 0.601 R², and the Random Forest's MAE is less than half of the lowest linear MAE.
- **The three linear models behave similarly.** The choice between a linear and a tree-based model mattered much more than the choice of penalty, which suggests that the price relationships are not well described by straight-line terms.
- **Converting the text specifications to numbers made them usable.** `mileage`, `engine`, and `max_power` were stored as text with units and had to be converted before modeling.
- **Practical meaning.** The Random Forest's average error is roughly 19% of the median selling price in the cleaned dataset (400,000). It can serve as a reference price for comparing listings, not as an exact valuation.
---
 
## 📁 Project Structure
 
```
used-car-price-prediction/
│
├── FinalsDossier1_Binas_JulianaPaula.ipynb
├── Car details v3.csv
├── cleaned_car_details.csv          (created by the notebook)
├── best_car_price_model.pkl         (created by the notebook)
├── requirements.txt
└── README.md
```
 
---
 
## 📓 Notebook Contents
 
| Part | Section |
|---|---|
| 1–2 | Dataset selection and Business Understanding |
| Data Understanding | Data inspection, exploratory analysis, and data quality checks |
| 3 | Data Partitioning |
| 4 | Data Cleaning |
| 5 | Machine Learning Pipeline (5.1 LASSO, 5.2 Ridge, 5.3 Elastic Net, 5.4 Regression Tree, 5.5 Random Forest) |
| 6 | Model Comparison |
| 7 | Save the Best Model |
| 8 | Load the Best Model |
| 9 | Create Predictions from the X_test Data |
| 10 | Show X_test with y_test and the Predictions |
| 11 | Findings and Project Summary |
 
---
 
## 🚀 How to Run the Project Locally
 
### 1. Clone the Repository
```bash
git clone https://github.com/YOUR-USERNAME/used-car-price-prediction.git
```
 
### 2. Navigate to the Project Folder
```bash
cd used-car-price-prediction
```
 
### 3. Install Dependencies
```bash
pip install -r requirements.txt
```
 
### 4. Open the Notebook
```bash
jupyter notebook FinalsDossier1_Binas_JulianaPaula.ipynb
```
 
The first code cell uses Google Colab's `files.upload()`. When running locally, replace it with:
 
```python
df = pd.read_csv("Car details v3.csv")
```
 
Then choose **Restart and Run All**.
 
### requirements.txt
```
pandas
numpy
scikit-learn
matplotlib
seaborn
joblib
jupyter
```
 
---
 
## 💼 Business Relevance
 
Used-car buyers, individual sellers, dealerships, and online listing platforms all need a reasonable reference price. Buyers want to know whether a listed price is fair, sellers need a competitive asking price, and dealerships need to evaluate vehicles before buying them for resale. This project shows how historical listings can support those decisions.
 
---
 
## ⚠️ Limitations
 
- The scores come from a single 80/20 split with fixed hyperparameters. Cross-validation and hyperparameter tuning were not performed, so the results may change with a different split.
- Different listings of the same vehicle model can still have similar features and prices, so some similarity between the training and testing records remains.
- A few vehicles have a `mileage` or `max_power` of 0 in the source data. These were kept as recorded.
- `mileage` combines values in km/l and km/kg, and only the number was kept.
- `name` and `torque` were excluded from the models.
- Vehicle condition, accident history, location, and current demand are not in the dataset.
- The results show associations in historical listings and do not show that any attribute causes a price change.
---
 
## 👩‍💻 Author
 
**Juliana Paula T. Binas**
BS Information Systems – Business Analytics
West Visayas State University
 
Academic Project | Analytics Application: Finals Dossier One
 
*Turning data into insights for smarter pricing decisions.*
 
