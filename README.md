# Marketing-Campaign-Response-Prediction-ML-Classifier-Comparison
A Python/Google Colab project that trains and compares 10 machine learning classifiers to predict customer responses to retail marketing campaigns, validates across monthly datasets, and generates predictions for unlabeled data.

Features


10 ML models trained and compared in a single pipeline
Cross-validation (5-fold) alongside test-set evaluation for robust comparison
Confusion matrix grid visualizing all models at once
Automatic best model selection based on test accuracy
Month-over-month validation — train on January, validate on February, predict March
Unlabeled prediction pipeline — outputs a scored Excel file for March data
Model persistence via joblib for reuse without retraining



🗂️ Dataset Structure

The project uses three monthly Excel files from a retail marketing campaign:

FileRoleLabelsmarketing_campaign_retail_Enero.xlsxTraining✅ Yesmarketing_campaign_retail_Febrero.xlsxValidation✅ Yesmarketing_campaign_retail_Marzo.xlsxPrediction❌ No

Target variable: Response — whether a customer accepted the campaign offer (binary classification).

Key features include: income, year of birth, education, marital status, product spending (wines, fruits, meat, etc.), campaign acceptance history (AcceptedCmp1–5), and complaints.


🤖 Models Compared

ModelLibraryRandom ForestsklearnLogistic RegressionsklearnDecision TreesklearnGradient BoostingsklearnAdaBoostsklearnXGBoostxgboostLightGBMlightgbmSVMsklearnKNNsklearnNaive Bayessklearn


🔧 Pipeline Overview

1. Load January data
       ↓
2. Preprocessing
   - Drop irrelevant columns (Client ID, Dt_Customer, Z_CostContact, Z_Revenue)
   - Median imputation for missing Income values
   - One-Hot Encoding (Education, Marital_Status, campaign flags, Complain)
   - StandardScaler on numeric features
       ↓
3. Train/Test Split (70/30, random_state=42)
       ↓
4. Train all 10 models → rank by Test Accuracy & Cross-Val Accuracy
       ↓
5. Validate best model on February data
       ↓
6. Predict March data (unlabeled) → export scored Excel file
       ↓
7. Save best model as .pkl


📊 Outputs

FileDescriptioncomparacion_modelos.xlsxAccuracy comparison table (Test + CV-5) for all models{best_model}_model.pklSerialized best-performing modeldigital_marketing_campaign_dataset_with_Predictions.xlsxMarch predictions with client ID, income, and probability scores

Visualizations generated:


Bar chart — Test vs Cross-Validation accuracy for all 10 models
Confusion matrix grid — all models side by side



🛠️ Tech Stack


Python 3.x / Google Colab
scikit-learn — preprocessing, models, evaluation
xgboost — gradient boosted trees
lightgbm — fast gradient boosting
pandas, numpy — data handling
matplotlib — visualization
joblib — model serialization



⚙️ Setup & Usage

1. Clone the repository

bashgit clone https://github.com/your-username/your-repo-name.git
cd your-repo-name

2. Install dependencies

bashpip install pandas numpy matplotlib scikit-learn xgboost lightgbm joblib openpyxl

3. Run in Google Colab

Open PRACTICA_ML_Antonio_Flores.ipynb in Google Colab and run all cells in order. You will be prompted to upload the three monthly Excel files at the relevant steps.


📁 Project Structure

├── PRACTICA_ML_Antonio_Flores.ipynb              # Main notebook
├── marketing_campaign_retail_Enero.xlsx           # Training data (upload)
├── marketing_campaign_retail_Febrero.xlsx         # Validation data (upload)
├── marketing_campaign_retail_Marzo.xlsx           # Unlabeled prediction data (upload)
├── {best_model}_model.pkl                         # Saved best model (generated)
├── comparacion_modelos.xlsx                       # Model comparison table (generated)
├── digital_marketing_campaign_dataset_with_Predictions.xlsx  # March predictions (generated)
└── README.md


📌 Notes


The scaler fitted on January training data is reused on February and March to prevent data leakage.
March features are aligned to the training column schema using reindex(fill_value=0) to handle any category mismatches after one-hot encoding.
The best model is selected automatically based on test accuracy; in case of ties, the first ranked model is chosen.



📄 License

This project is for educational purposes.
