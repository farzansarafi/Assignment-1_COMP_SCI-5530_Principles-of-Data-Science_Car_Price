
Project Report: Used Car Price Prediction

1. Project Objective

The primary objective of this project was to build a predictive model to estimate the price of used cars based on various features such as car specifications, age, mileage, and other relevant attributes. The goal was to provide insights into factors influencing car prices and to develop a reliable model for prediction.

2. Methodology

 2.1 Data Loading and Initial Inspection

The project began by loading the dataset into a pandas DataFrame. An initial inspection was performed to understand the structure of the data and identify any immediate issues.

 2.2 Data Cleaning

Several data cleaning steps were performed to ensure data quality:
- **Missing Values**: Missing values in the 'Mileage', 'Engine', 'Power', and 'Seats' columns were handled by dropping the corresponding rows. The 'New_Price' column, which had a large number of missing values and was not central to the current analysis, was dropped entirely.
- **Unit Removal and Type Conversion**:
    - The 'Mileage' column, originally containing units like 'kmpl' or 'km/kg', was cleaned by removing these units and converting the data type to float. A conversion factor (1.4) was applied to 'km/kg' entries to standardize them to 'kmpl' equivalents.
    - The 'Engine' column had ' CC' units, which were removed, and the column was converted to integer type.
    - The 'Power' column contained ' bhp' units and 'null bhp' strings. These were removed, and the column was converted to float type.

 2.3 Feature Engineering

Two new features were engineered to enhance the model's predictive capability:
- **Car_Age**: Calculated by subtracting the 'Year' of manufacture from the current year (2025). This provides a direct measure of the car's age.
- **Engine_Liters**: Derived by dividing the 'Engine' capacity (in CC) by 1000, converting it to liters for easier interpretation.

 2.4 Data Transformation and Selection

- The original `df` was used to calculate `average_price_fuel_type` and `average_price_transmission`.
- A new DataFrame `df_manipulated` was created, selecting relevant columns for modeling: 'Name', 'Price', 'Car_Age', 'Fuel_Type_Petrol', 'Transmission_Manual', 'Engine', 'Kilometers_Driven'.
- The 'Kilometers_Driven' column was renamed to 'KMs_Driven' for consistency.
- `df_manipulated` was sorted by 'Price' in descending order.

3. Key Findings from Exploratory Data Analysis (EDA)

Visualizations and summary statistics revealed several insights:
- **Average Price by Fuel Type**: Cars with Diesel/Other fuel types generally had a higher average price compared to Petrol cars. (Average Price for Diesel/Other: 12.96, Petrol: 5.77).
- **Average Price by Transmission Type**: Automatic transmission cars commanded significantly higher average prices than manual transmission cars. (Average Price for Automatic: 19.91, Manual: 5.43).
- **Distribution of Car Age**: A histogram showed the distribution of car ages in the dataset, indicating a prevalence of cars in certain age ranges.
- **Average Price by Car Age**: A bar plot illustrated an inverse relationship between car age and average price, with newer cars generally being more expensive and prices decreasing as cars get older.

4. Model Training and Evaluation

 4.1 Data Splitting

The `df_manipulated` DataFrame was split into features (X) and target (y), where 'Price' was the target variable. The data was then divided into training (80%) and testing (20%) sets using `train_test_split` with `random_state=42` for reproducibility.

 4.2 Model Selection and Training

A Linear Regression model was chosen for its simplicity and interpretability. The 'Name' column was dropped from the feature sets (`X_train` and `X_test`) before training, as it is categorical and would require further encoding not covered in this iteration, and is generally not directly used in linear regression for numerical prediction.

The `LinearRegression` model was initialized and trained on the `X_train_model` and `y_train` datasets.

 4.3 Model Performance

After training, the model's performance was evaluated on the test set using standard regression metrics:
- **Mean Absolute Error (MAE)**: 4.54
- **Mean Squared Error (MSE)**: 52.98
- **R-squared (R2)**: 0.62

The MAE indicates that, on average, the model's predictions deviate by approximately 4.54 units (Lakhs) from the actual car prices. The R-squared value of 0.62 suggests that the model explains about 62% of the variance in the car prices, which is a reasonably good fit for this type of data.

 4.4 Actual vs. Predicted Prices Visualization

A scatter plot comparing actual and predicted prices showed a positive correlation, indicating that the model generally predicts higher prices for cars that are actually more expensive. The presence of a perfect prediction line helped visualize the model's deviation from ideal predictions.

5. Conclusion and Next Steps

This project successfully developed a Linear Regression model capable of predicting used car prices with a reasonable level of accuracy (R2 of 0.62). The EDA provided valuable insights into the key drivers of car prices, such as fuel type, transmission, and car age.

**Potential Next Steps**:
- **Feature Engineering Enhancement**: Explore more advanced feature engineering, such as interaction terms or polynomial features, to capture non-linear relationships.
- **Advanced Models**: Experiment with more sophisticated regression algorithms (e.g., Random Forest, Gradient Boosting, XGBoost) that might capture complex patterns better.
- **Categorical Feature Encoding**: Implement one-hot encoding or other techniques for categorical features (like 'Name' or 'Location') if they are deemed important for prediction.
- **Outlier Detection and Handling**: Further investigate and handle outliers in numerical features, which can significantly impact linear models.
- **Cross-validation**: Implement cross-validation techniques to ensure the model's robustness and prevent overfitting.


 Data Analysis Key Findings
*   The Linear Regression model for used car price prediction achieved an R-squared value of 0.62, indicating it explains 62% of the variance in car prices.
*   The model's Mean Absolute Error (MAE) was $4.54 Lakhs, meaning predictions were, on average, off by this amount from actual prices.
*   Exploratory Data Analysis revealed that cars with Diesel/Other fuel types had a significantly higher average price ($12.96 Lakhs) compared to Petrol cars ($5.77 Lakhs).
*   Automatic transmission cars commanded a much higher average price ($19.91 Lakhs) than manual transmission cars ($5.43 Lakhs).
*   A clear inverse relationship was observed between car age and average price, with newer cars generally being more expensive.

 Insights or Next Steps
*   Enhance model accuracy by exploring advanced feature engineering techniques (e.g., interaction terms, polynomial features) and implementing more sophisticated machine learning models such as Random Forest or XGBoost.
*   Improve model robustness and generalizability by performing outlier detection and handling, implementing cross-validation, and thoroughly evaluating the impact of encoding additional categorical features like 'Name' or 'Location'.

