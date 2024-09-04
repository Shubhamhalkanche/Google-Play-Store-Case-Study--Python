## Visualizations
- **Creating Visualizations for the Analysis**

**import matplotlib.pyplot as plt <br />**
**import warnings <br />**
**warnings.filterwarnings("ignore") <br />**
**import seaborn as sns <br />** <br />

**Distribution of Size :** <br />
inp1.Size.plot.hist() <br />
plt.show() <br />
inp1.Size.describe() <br />

**Distribution of rating :** <br />
sns.distplot(inp1.Rating, bins=20, color="g") <br /> 
plt.title("Distribution of app ratings", fontsize=12) <br />
plt.show() <br />

**Analysing the Content Rating column :** <br />
inp1['Content Rating'].value_counts() <br />
inp1 = inp1[~inp1['Content Rating'].isin(["Adults only 18+","Unrated"])] <br />

**Apps belonging to different categories of Content Rating :** <br />
inp1['Content Rating'].value_counts().plot.pie() <br />
plt.show() <br />

**We will analyse Content Rating :** <br />
inp1['Content Rating'].value_counts().plot.barh() <br />
plt.show() <br />

**Size vs Rating :** <br />
sns.jointplot(inp1.Size, inp1.Rating) <br /> 
plt.show() <br />

**Price vs Rating trend :** <br />
sns.jointplot(inp1.Price, inp1.Rating, kind="reg") <br />
plt.show() <br />

**Price vs Rating for only the paid apps.**  <br />
sns.jointplot("Price", "Rating", data=inp1[inp1.Price>0], kind="reg") <br />
plt.show() <br />

**Reviews' vs 'Size' vs 'Price' vs 'Rating' :** 
sns.pairplot(inp1[['Reviews', 'Size', 'Price','Rating']]) <br />
plt.show() <br />

**Content Rating vs Average Rating :** <br />
inp1.groupby(['Content Rating'])['Rating'].mean().plot.bar() <br />

**Minimum Rating for each Content category :** <br />
sns.barplot(data=inp1, x="Content Rating", y="Rating", estimator=np.min) <br />
plt.show() <br />

**Spread of Ratings across several categories :** <br />
sns.boxplot(inp1['Content Rating'], inp1.Rating) <br />
plt.show() <br />

**Ratings across the 4 most popular Genres :** <br />
inp1['Genres'].value_counts() <br />
c = ['Tools','Entertainment','Medical','Education'] <br />
inp5= inp1[inp1['Genres'].isin(c)] <br />
sns.boxplot(inp5['Genres'],inp1.Rating) <br />

**Ratings vs Size vs Content Rating :** <br />
inp1['Size_Bucket'] = pd.qcut(inp1.Size, [0, 0.2, 0.4, 0.6, 0.8, 1], ["VL","L","M","H","VH"]) <br />
pd.pivot_table(data=inp1, index="Content Rating", columns="Size_Bucket", values="Rating") <br />
res = pd.pivot_table(data=inp1,index="Content Rating",columns="Size_Bucket",values="Rating",aggfunc=lambda x: np.quantile(x,0.2)) <br />
sns.heatmap(res, cmap = "Greens", annot=True) <br />
plt.show() <br />

**Rating vs Month :** <br />
inp1['updated_month'] = pd.to_datetime(inp1['Last Updated']).dt.month <br />
inp1.groupby(['updated_month'])['Rating'].mean() <br />
plt.figure(figsize=[10,5]) <br />
inp1.groupby(['updated_month'])['Rating'].mean().plot() <br />
plt.show() <br />

**Content Rating and updated Month with the values set to Installs :** <br />
pd.pivot_table(data=inp1, values="Installs", index="updated_month", columns="Content Rating", aggfunc=sum) <br />
monthly = pd.pivot_table(data=inp1, values="Installs", index="updated_month", columns="Content Rating", aggfunc=sum)
monthly.plot(kind="bar", stacked="True", figsize=[10,6])
plt.show()



