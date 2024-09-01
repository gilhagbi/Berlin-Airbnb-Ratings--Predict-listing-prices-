

# Berlin-Airbnb-Ratings--Predict-listing-prices
An Evaluation of Berlin Airbnb Properties Based on Host Ratings and More

## Airbnb Berlin Data Preparation Script

This script prepares and cleans a dataset of Airbnb listings in Berlin, transforming and filtering the data to make it suitable for further analysis or modeling.

### 1. Data Download
- **Download CSV File**: The script uses `gdown` to download the Airbnb Berlin dataset from Google Drive and saves it as `Airbnb_Berlin.csv`.

### 2. Data Cleaning and Transformation
- **Date Conversion**: Converts specified columns to datetime format for date-related operations.
  - Columns: `review_date`, `Host Since`, `First Review`, `Last Review`.
  
- **Boolean to Binary Conversion**: Converts boolean columns to binary (1/0) format.
  - Columns: `Is Superhost`, `Is Exact Location`.

- **Postal Code Cleaning**: Cleans and converts the `Postal Code` column to an integer format, removing any non-numeric characters.

- **Host Response Rate Conversion**: Converts `Host Response Rate` from a percentage string to a float value.

- **Column Drop**: Removes unnecessary columns to streamline the dataset.
  - Dropped Columns: `Country`, `Business Travel Ready`, `Is Superhost`, `Is Exact Location`, `Instant Bookable`, `Listing URL`, `Host URL`, `Postal Code`, `Square Feet`.

### 3. Feature Engineering
- **Top 10 Neighbourhoods**: Identifies the top 10 most frequent neighbourhoods and creates a new column `Top10Neighbourhood` to categorize listings.

- **Property Type Hierarchical Mapping**: Maps `Property Type` to higher-level hierarchical categories and creates a new column `Property_Type_groups`.

- **String Conversion**: Converts specified columns to string type for consistency.
  - Columns: `Reviewer Name`, `Listing Name`, `Host Name`, `City`, `Country Code`, `Top10Neighbourhood`, `neighbourhood`, `Neighborhood Group`, `Host Response Time`, `Property Type`, `Property_Type_groups`, `Room Type`.

- **Price Cleaning**: Cleans the `Price` column by removing non-numeric characters and converting it to a float.

- **Handling Negative Values**: Replaces negative values with NaN in specific columns.
  - Columns: `Accommodates`, `Bathrooms`, `Bedrooms`, `Beds`, `Min Nights`.

### 4. Data Preparation for Analysis
- **Panel Data Creation**: Extracts and organizes relevant columns into a DataFrame (`df_panel`) for further analysis.
  - Selected Columns: `Listing ID`, `Listing Name`, `Host ID`, `Host Name`, `Host Since`, `Host Response Time`, `Host Response Rate`, `neighbourhood`, `Neighborhood Group`, `City`, `Country Code`, `Latitude`, `Longitude`, `Property Type`, `Room Type`, `Accommodates`, `Bathrooms`, `Bedrooms`, `Beds`, `Price`, `Guests Included`, `Min Nights`, `Reviews`, `First Review`, `Last Review`, `Overall Rating`, `Accuracy Rating`, `Cleanliness Rating`, `Checkin Rating`, `Communication Rating`, `Location Rating`, `Value Rating`, `Is Superhost_ind`, `Is Exact Location_ind`, `Postal Code_n`, `Top10Neighbourhood`, `Property_Type_groups`.

- **Reviews Data Extraction**: Extracts review-related columns into a separate DataFrame (`df_reviews`).
  - Selected Columns: `Review ID`, `review_date`, `Reviewer ID`, `Reviewer Name`, `Comments`, `Listing ID`, `Listing Name`.

### 5. Data Filtering
- **Filter for Apartments**: Filters the panel DataFrame to include only listings categorized as `Apartment`.

### 6. Saving Data
- **Save as Pickle**: Saves the cleaned and prepared DataFrames (`df_panel`, `df_reviews`) as pickle files for future use.

## Output Files
- `Airbnb_Berlin.pkl`: Pickled version of the entire cleaned DataFrame.
- `df_panel.pkl`: Pickled version of the panel DataFrame focusing on apartments.
- `df_reviews.pkl`: Pickled version of the reviews DataFrame.

## Data Analysis and Visualization Script

### Setup and Imports
1. **Install Packages**:
   - Imports necessary libraries for data processing, visualization, and statistical analysis.

2. **Import Libraries**:
   - Includes `numpy`, `pandas`, `matplotlib`, `seaborn`, `sklearn`, `scipy`, `statsmodels`, and `nltk`.

### Data Loading and Initial Processing
3. **Load Data**:
   - Loads data from a pickle file into `df_panel`.
   - Extracts a subset of columns into `df_eda` for analysis.

4. **Inspect Data**:
   - Prints information about `df_panel` and `df_eda`.

### Data Analysis and Visualization
5. **Export Data Information**:
   - Saves data type information, maximum and minimum values, and missing values to CSV files.

6. **AutoViz Visualization**:
   - Uses AutoViz to create visualizations for `df_eda`.

7. **Count Plots**:
   - Creates count plots for dummy and categorical columns.

8. **Histograms**:
   - Plots histograms for numerical columns and log-transformed price.

9. **Correlation Heatmap**:
   - Computes and visualizes a correlation heatmap for numerical columns.

10. **Scatter Plots**:
    - Creates scatter plots to show the relationship between numerical features and price.

11. **Bar Plots**:
    - Plots average price by categorical features using bar plots.

### Statistical Analysis
12. **Skewness Highlighting**:
    - Highlights skewness in numerical data using custom styling in pandas DataFrame.

## Data Cleansing and Outliers

### Overview
This script performs data cleaning and preparation on a dataset (`df_panel`), focusing on handling missing values, outliers, and feature engineering. It uses various Python libraries to analyze and preprocess the data, ensuring it's ready for further analysis or modeling.

### Script Breakdown

#### 1. Outlier Detection and Treatment
- **Boxplot Visualization**: Visualizes outliers using boxplots.
- **Outlier Summary**: Calculates and saves the count and percentage of outliers for each numerical column.
- **Outlier Capping**: Applies capping to outliers based on the Interquartile Range (IQR) method.
- **Visualization**: Compares distributions and boxplots before and after capping.

#### 2. Handling Missing Values
- **Nulls Matrix**: Visualizes missing data patterns.
- **Missing Value Analysis**: Calculates and displays missing values and their impact on distribution and correlation.
- **Imputation**: Handles missing values for rating columns and fills missing values with specific strategies.
- **Column Removal**: Drops columns with excessive missing values or those not needed.

#### 3. Feature Engineering
- **Binning Numerical Columns**: Bins numerical columns to handle extreme values and outliers.
- **Imputation**: Applies K-Nearest Neighbors (KNN) imputation to fill missing values in numerical columns.
- **Fill Missing Values**: Fills missing values in categorical columns and applies specific handling strategies.

## Feature Engineering

### Setup and Imports
1. **Install Packages**:
   - Uses `pip` to install required libraries.

2. **Imports**:
   - Imports necessary libraries for data processing, visualization, and modeling.

### Data Loading and Initial Processing
3. **Load Data**:
   - Loads data from pickle files into `feature_eng_df` and `reviews_df`.

4. **Clean Data**:
   - Filters `feature_eng_df` to include only positive prices.

### Geographic Information System (GIS) Features
5. **Plot Locations**:
   - Creates a map visualization of property locations using Folium.

6. **Distance Calculation**:
   - Calculates distances from each property to the central point based on latitude and longitude.

7. **Scatter Plot**:
   - Plots distance to the central point versus log-transformed price.

### Neighborhood Features
8. **Neighborhood Ratings**:
   - Computes average location ratings by neighborhood and ranks neighborhoods.

### Date Features
9. **Create Date Features**:
   - Calculates the number of days since key dates and creates indicators for missing values.

10. **Review Metrics**:
    - Calculates the range and ratio of reviews per day.

### Bin Numerical Columns
11. **Bin Columns**:
    - Bins numerical columns to reduce outliers' impact and converts to string format.

### Reviews Processing
12. **Process Reviews**:
    - Analyzes review comments to generate word clouds.
    - Calculates sentiment polarity and creates sentiment labels.

13. **Review Summarization**:
    - Summarizes polarity and sentiment for all comments and the top 5 most recent comments per listing.

## Feature Selection Script

### Overview
This script performs feature selection on a dataset to determine which features are most important for predicting the target variable, `Price`. It utilizes multiple regression models to evaluate the significance of each feature and selects those that meet certain criteria.

### Libraries Used
- **Pandas**: Data manipulation and analysis.
- **NumPy**: Numerical operations.
- **Seaborn**: Data visualization.
- **Scikit-Learn**: Machine learning models and feature selection.

### Script Breakdown

#### 1. Data Loading
- Loads the dataset from `step_4_df.pkl`.

#### 2. Feature Selection
- **Data Preparation**: 
  - Defines the feature matrix `X` and target variable `y`.
  - Encodes string columns using `OrdinalEncoder`.
- **Model F

itting**: 
  - Fits various regression models, including `LinearRegression`, `LassoCV`, `RidgeCV`, and `ElasticNetCV`.
- **Feature Importance**: 
  - Evaluates and visualizes feature importances using model coefficients.

### Outputs
- **Feature Importance Scores**: Saves feature importance scores to CSV files.
- **Visualization**: Generates plots of feature importances for the top 20 features.

## References
- **Airbnb Berlin Dataset**: [Google Drive Link](https://drive.google.com/file/d/1cc5HV0v5GxCuQuj87t8aS0H5IBDGqOZH/view?usp=sharing)

