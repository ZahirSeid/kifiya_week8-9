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
