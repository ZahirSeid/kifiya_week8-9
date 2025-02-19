# kifiya_week8-9

# Task1

# Fraud Detection Analysis and Data Preprocessing
## Overview

This project aims to analyze and preprocess data for fraud detection based on multiple datasets: Fraud Data, IP Address to Country Data, and Credit Card Transactions Data. The goal is to explore relationships between various features in these datasets, preprocess them for further analysis, and create meaningful insights that can potentially aid in identifying fraudulent activities.
Datasets:

    Fraud Data (Fraud_Data.csv):
        Contains transaction data with user information, purchase details, and fraud labels (class).
    IP Address to Country Data (IpAddress_to_Country.csv):
        Contains mappings of IP address ranges (lower_bound_ip_address, upper_bound_ip_address) to country names.
    Credit Card Transactions Data (CreditCard.csv):
        Contains anonymized transaction data with various numerical features for fraud detection.

## Task Breakdown
### Data Cleaning:

    Fraud Data:
        Missing values were handled by filling them with appropriate values (mode for categorical variables, median for numerical ones).
        Duplicates were removed, and necessary columns were dropped if they contained missing or irrelevant data.

    IP Address to Country Data:
        Missing values for IP address ranges were dropped, and the country column was filled with "unknown" for missing entries.
        Duplicates were removed to ensure clean and accurate data.

    Credit Card Data:
        Missing Time values were converted into a meaningful time representation by calculating the time in days.
        Columns were cleaned to ensure data consistency, and missing values were filled where necessary.

### Exploratory Data Analysis (EDA):

    Fraud Data:
        Various visualizations (histograms, box plots) were created for key features such as purchase_value, age, and class to explore the distribution and identify potential patterns related to fraudulent transactions.
        Time-based features (hour of day, day of week) were derived from purchase_time and analyzed for trends in fraud occurrence.

    IP Address Data:
        The relationship between ip_address and geographical location (from IpAddress_to_Country.csv) was explored to see how location data could aid fraud detection.
        A merge was performed between fraud data and IP address data to map each user's IP address to a specific country.

    Credit Card Data:
        A correlation heatmap was created to understand relationships between numerical features in the credit card data (e.g., Time, V1, V2, etc.).

    Merged Data:
        The Fraud Data and IP Address data were merged using an asof merge to match each user's transaction with the closest lower bound IP address.
        New features such as time_diff were computed to understand the time difference between signup_time and purchase_time and its correlation with fraud occurrence.

### Features Derived

    Fraud Data:
        transaction_count: Count of transactions per user.
        hour_of_day: Extracted hour from purchase_time to analyze fraud patterns based on the time of the day.
        day_of_week: Day of the week extracted from purchase_time to understand weekly fraud patterns.

    Credit Card Data:
        time_in_days: Conversion of the Time feature (in seconds) to days for easier analysis.

### Final Output

    Cleaned and Preprocessed Data:
        Preprocessed_Fraud_Data.csv
        Preprocessed_IpAddress_to_Country.csv
        Preprocessed_Creditcard_Data.csv

    Merged Data:
        merged_data.csv: This file contains merged fraud data with IP address country information for more context in fraud analysis.

## Conclusion

This notebook demonstrates a systematic approach to preprocessing and analyzing fraud detection data. By cleaning and merging relevant datasets, extracting time-based features, and visualizing key aspects, we can identify potential trends and insights useful for fraud detection.




# Task 2 & Task 3
### Fraud Detection Model Training and Explainability

This phase of the project focuses on training machine learning models for fraud detection and explaining their predictions using various interpretability techniques. The models were trained separately on two datasets: Credit Card Transactions Data and Fraud Data (including merged IP address information). 

## Task 2: Model Training
Objective

The goal was to build and evaluate machine learning models that can effectively detect fraudulent transactions in both datasets.
Models Trained

### We trained the following models:

    Logistic Regression
    Random Forest
    Gradient Boosting
    Decision Tree

Each model was trained separately for Credit Card Data and Fraud Data (merged with IP address information).
Evaluation Metrics

### The models were evaluated using:

    Accuracy – Measures overall correctness.
    Precision – Measures how many predicted fraud cases were actually fraud.
    Recall – Measures how many actual fraud cases were correctly detected.
    F1 Score – Harmonic mean of precision and recall.

### Results

#### Credit Card Transactions Data  
| Model                | Accuracy | Precision | Recall | F1 Score |
|----------------------|----------|-----------|--------|----------|
| Logistic Regression | 0.9790    | 0.9906    | 0.9673 | 0.9789   |
| Decision Tree       | 0.9685    | 0.9811    | 0.9557 | 0.9682   |
| Random Forest       | 0.9915    | 0.9987    | 0.9843 | 0.9915   |
| Gradient Boosting   | 0.9864    | 0.9937    | 0.9790 | 0.9863   |

#### Fraud Data (Merged Dataset with IP Address Info)  
| Model                | Accuracy | Precision | Recall | F1 Score |
|----------------------|----------|-----------|--------|----------|
| Logistic Regression | 0.9152    | 0.9234    | 0.9071 | 0.9152   |
| Decision Tree       | 0.8282    | 0.9999    | 0.6594 | 0.7947   |
| Random Forest       | 0.8463    | 0.9952    | 0.6986 | 0.8209   |
| Gradient Boosting   | 0.8936    | 0.9995    | 0.7895 | 0.8822   |


### Model Saving

All trained models were saved for future use:

    Credit Card Models: Stored in saved_models/
    Fraud Detection Models: Stored in fraud_saved_models/


## Task 3: Model Explainability

### Objective

After training the models, we aimed to interpret their predictions to understand how different features contribute to fraud detection.
Methods Used for Explainability

    Feature Importance (for tree-based models like Random Forest & Gradient Boosting)
    SHAP (Shapley Additive Explanations) to understand individual predictions
    LIME (Local Interpretable Model-agnostic Explanations) for black-box models like Logistic Regression

### Key Insights

    Time-based features (such as hour_of_day) played a significant role in fraud detection.
    Transaction amount had a strong correlation with fraud occurrence in the Credit Card dataset.
    IP-based features (from the merged dataset) provided additional fraud detection signals.
    Tree-based models (Random Forest, Gradient Boosting) showed higher performance but needed interpretability techniques to explain predictions.

### Conclusion

    The Random Forest model performed best on the Credit Card data with 99.15% accuracy and high precision (99.87%).
    On the Fraud Data (merged with IP information), Logistic Regression had the best balance of performance and interpretability with 91.52% accuracy.
    Explainability techniques helped in understanding why models made certain predictions, making the system more transparent and reliable.
