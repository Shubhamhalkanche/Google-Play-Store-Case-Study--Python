## Importing the Dataset
import pandas as pd <br />
import numpy as np <br />
inp0 = pd.read_csv("googleplaystore_v2.csv")

## Data Handling and Cleaning
inp0.info() <br />
inp0.isnull().sum()

**Handling missing values for rating** <br />
inp1 = inp0[~inp0.Rating.isnull()]

#### Drop the rows having null values in the Rating field
inp1 = inp0[~inp0.Rating.isnull()] <br />
inp1.shape <br />
inp1.Rating.isnull().sum() 

#### Check whether any null present/not
inp1.isnull().sum()

#### Inspect the nulls in the Android Version column
inp1[inp1['Android Ver'].isnull()]

#### Dropping the row having shifted values
inp1.loc[10472,:] <br />
inp1[(inp1['Android Ver'].isnull() & (inp1.Category == "1.9"))] <br />
inp1 = inp1[~(inp1['Android Ver'].isnull() & (inp1.Category == "1.9"))] <br />
Check the nulls again in Android version column to cross-verify  
inp1[inp1['Android Ver'].isnull()]

## Imputing Missing Values
Check the most common value in the Android version column <br />
inp1['Android Ver'].value_counts() <br />

Fill up the nulls in the Android Version column with the above value <br />
inp1['Android Ver'] = inp1['Android Ver'].fillna(inp1['Android Ver'].mode()[0]) <br />
inp1['Android Ver'].isnull().sum() <br />
inp1.isnull().sum() <br />

#Replace the nulls in the Current version column with the above value <br />
inp1['Current Ver'] = inp1['Current Ver'].fillna(inp1['Current Ver'].mode()[0]) <br />

To Check the most common value in the Current version column again  <br />
inp1['Current Ver'].value_counts()  <br />
inp1.dtypes <br />
Analyse the Price column <br />
inp1.Price.value_counts() <br />


