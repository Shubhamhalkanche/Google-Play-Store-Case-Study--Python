## Visualizations
- Creating Visualizations for the Analysis

#Distribution of Size
import matplotlib.pyplot as plt
import warnings
warnings.filterwarnings("ignore")
import seaborn as sns
inp1.Size.plot.hist()
plt.show()
inp1.Size.describe()

#distribution of rating
sns.distplot(inp1.Rating, bins=20, color="g")
plt.title("Distribution of app ratings", fontsize=12)
plt.show()

#Analysing the Content Rating column
inp1['Content Rating'].value_counts()

inp1 = inp1[~inp1['Content Rating'].isin(["Adults only 18+","Unrated"])]

#Check the apps belonging to different categories of Content Rating 
inp1['Content Rating'].value_counts().plot.pie()
plt.show()

#We will analyse Content Rating
inp1['Content Rating'].value_counts().plot.barh()
plt.show()

#Size vs Rating

sns.jointplot(inp1.Size, inp1.Rating)
plt.show()

#Will look into Price and Rating trend
sns.jointplot(inp1.Price, inp1.Rating, kind="reg")
plt.show()

#Now, will plot a reg plot for Price and Rating again for only the paid apps.
sns.jointplot("Price", "Rating", data=inp1[inp1.Price>0], kind="reg")
plt.show()

Reviews' vs 'Size' vs 'Price' vs 'Rating'
'Reviews', 'Size', 'Price','Rating'sns.pairplot(inp1[['Reviews', 'Size', 'Price','Rating']])
plt.show()

#Content Rating vs Average Rating 
inp1.groupby(['Content Rating'])['Rating'].mean().plot.bar()

#minimum Rating with respect to each Content category
sns.barplot(data=inp1, x="Content Rating", y="Rating", estimator=np.min)
plt.show()

#Now, will see the spread and analyse the Rating across several categories
plt.figure(figsize=[9,7])
sns.boxplot(inp1['Content Rating'], inp1.Rating)
plt.show()

#Ratings across the 4 most popular Genres
inp1['Genres'].value_counts()

c = ['Tools','Entertainment','Medical','Education']
inp5= inp1[inp1['Genres'].isin(c)]
sns.boxplot(inp5['Genres'],inp1.Rating)

Ratings vs Size vs Content Rating
inp1['Size_Bucket'] = pd.qcut(inp1.Size, [0, 0.2, 0.4, 0.6, 0.8, 1], ["VL","L","M","H","VH"])
pd.pivot_table(data=inp1, index="Content Rating", columns="Size_Bucket", values="Rating")

res = pd.pivot_table(data=inp1,index="Content Rating",columns="Size_Bucket",values="Rating",aggfunc=lambda x: np.quantile(x,0.2))
sns.heatmap(res, cmap = "Greens", annot=True)
plt.show()

Rating vs Month¶
inp1['updated_month'] = pd.to_datetime(inp1['Last Updated']).dt.month
inp1.groupby(['updated_month'])['Rating'].mean()
plt.figure(figsize=[10,5])
inp1.groupby(['updated_month'])['Rating'].mean().plot()
plt.show()

#Content Rating and updated Month with the values set to Installs
pd.pivot_table(data=inp1, values="Installs", index="updated_month", columns="Content Rating", aggfunc=sum)
monthly = pd.pivot_table(data=inp1, values="Installs", index="updated_month", columns="Content Rating", aggfunc=sum)
monthly.plot(kind="bar", stacked="True", figsize=[10,6])
plt.show()



