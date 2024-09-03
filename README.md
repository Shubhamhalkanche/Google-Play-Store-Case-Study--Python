# Google Play Store Data Analysis

## Overview

This project involves an in-depth analysis of Google Play Store app data to extract valuable insights regarding app performance, user engagement, and app market trends. By analyzing the dataset, we aim to uncover key patterns, understand user preferences, and visualize the distribution of app ratings, installs, and other relevant metrics.

## Project Structure
 **Data** : The dataset used in this project is **googleplaystore_v2.csv** , which includes the following columns:
 
- `App`: Name of the app.
- `Category`: Category the app falls under.
- `Rating`: Average user rating of the app (out of 5).
- `Reviews`: Number of user reviews.
- `Installs`: Number of installs (in units, e.g., '1,000+', '10,000+', etc.).
- `Size`: Size of the app in MB.
- `Type`: Paid or Free.
- `Price`: Price of the app (if paid).
- `Content Rating`: Age group the app is suitable for.
- `Genres`: Genres the app belongs to.
- `Last Updated`: Date when the app was last updated.
- `Current Ver`: Current version of the app.
- `Android Ver`: Minimum Android version required for the app.


**notebook** : Jupyter notebook for exploratory data analysis and visualization.
You can dowload the **"Case Study Python Notebook.ipynb"** from [Here](https://github.com/Shubhamhalkanche/Shubhamhalkanche-Google-Play-Store-Case-Study-using-Python/blob/main/Case%20Study%20Python%20Notebook.ipynb
)


**scripts**: Python scripts for various stages of data processing and analysis.
  - `data_preprocessing.py`: Script for loading and cleaning the data.
  - `feature_engineering.py`: Script for adding additional features to the dataset.
  - `visualization.py`: Script for generating visualizations.


**results**: Contains results of the analysis.
  - `Visuals/`: Directory with saved visualizations.
  - `insights.txt`: File with key insights from the analysis.


**Visualizations:** Visualizations are saved in the Visuals directory. 
Examples include:
rating_distribution.png: Distribution of app ratings.
install_vs_rating.png: Relationship between installs and ratings.
category_distribution.png: Distribution of apps across different categories.

**Insights:** Key findings and insights are documented in results/insights.txt.

**Libraries Used:**  This project leverages the following Python libraries:
- Pandas
- NumPy
- Matplotlib
- Seaborn

