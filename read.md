## Importing the Dataset
import pandas as pd <br />
import numpy as np <br />
inp0 = pd.read_csv("googleplaystore_v2.csv")

## Data Handling and Cleaning
- **To clean and preprocess the data to handle missing values and inconsistencies:** <br />

inp0.info() <br />
inp0.isnull().sum()

**Handling missing values for rating**  <br />
inp1 = inp0[~inp0.Rating.isnull()]

**To drop the rows having null values in the Rating field**  <br />
inp1 = inp0[~inp0.Rating.isnull()] <br />
inp1.shape <br />
inp1.Rating.isnull().sum() 

**Checking whether any null value present/not**  <br />
inp1.isnull().sum()

**Inspecting the nulls in the Android Version column**  <br />
inp1[inp1['Android Ver'].isnull()]

**Dropping the row having shifted values**  <br />
inp1.loc[10472,:] <br />
inp1[(inp1['Android Ver'].isnull() & (inp1.Category == "1.9"))] <br />
inp1 = inp1[~(inp1['Android Ver'].isnull() & (inp1.Category == "1.9"))] <br />
**Checking the nulls again in Android version column to cross-verify**   <br />
inp1[inp1['Android Ver'].isnull()]

## Imputing Missing Values
**To check the most common value in the Android version column** <br />
inp1['Android Ver'].value_counts() <br />

**Filling up the nulls in the Android Version column with the above value** <br />
inp1['Android Ver'] = inp1['Android Ver'].fillna(inp1['Android Ver'].mode()[0]) <br />
inp1['Android Ver'].isnull().sum() <br />
inp1.isnull().sum() <br />

**Replacing the nulls in the Current version column with the above value** <br />
inp1['Current Ver'] = inp1['Current Ver'].fillna(inp1['Current Ver'].mode()[0]) <br />

**To Check the most common value in the Current version column again**  <br />
inp1['Current Ver'].value_counts()  <br />
inp1.dtypes <br />

**Analysis of Price column**  <br />
inp1.Price.value_counts() <br />
inp1.Price = inp1.Price.apply(lambda x: 0 if x=="0" else float(x[1:]))  <br />
inp1.Price.dtype  <br />

**Analysis of Reviews column** <br />
inp1.Reviews.value_counts() <br />
#Change the dtype of this column <br />
inp1.Reviews = inp1.Reviews.astype("int32") <br />
inp1.Reviews.describe() <br />

**Analysis of Installs Column** <br />
inp1.Installs.head() <br />
def clean_installs(val): <br />
    return int(val.replace(",","").replace("+","")) <br />
type(clean_installs("3,000+")) <br />
inp1.Installs = inp1.Installs.apply(clean_installs) <br />
inp1.Installs.describe() <br />

## Sanity Checks
**Number of Reviews is less than or equal to the number of Installs.** <br />
inp1[(inp1.Reviews > inp1.Installs)] <br />
inp1 = inp1[inp1.Reviews <= inp1.Installs] <br />
**Free Apps shouldn’t have a price greater than 0.** <br />
inp1[(inp1.Type == "Free") & (inp1.Price>0)] <br />




