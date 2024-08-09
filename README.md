# Titanic_data_analysis

# PACKAGES
### importing the packages
import numpy as np 
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
import warnings
warnings.filterwarnings("ignore")

# LOADING DATA
### Loading the data
df_titanic = pd.read_csv("titanic.csv")
df_titanic.head()

### Knowing about the data info
df_titanic.info()

### Describing the data
df_titanic.describe()

### Fetching the columns list
df_titanic.columns.to_list()

# INTERPRETTING THE NULL VALUES
### Checking the null values in columns
df_titanic.isnull().sum()

# DROPPING NULL VALUES
### Dropping the columns which are not necessary for us
df = df_titanic.drop(columns = ["Cabin"], axis = 1)

# MANIPULATING WITH DATA
### Finding the mean value of the age
df["Age"].mean()

### Filling the "Age" column with mean value
df["Age"] = df["Age"].fillna(df["Age"].mean())

### Filling the "Fare" column with mean value
df["Fare"] = df["Fare"].fillna(df["Fare"].mean())

### Finding the mode value of "Embarked" column as it is a character filled column
df["Embarked"].mode()[0]

# PLOTTING GRAPHS
### Building the function to draw the plots 
def bar_plot(variable):
    var = df_titanic[variable]
    var_Value = var.value_counts()
    plt.figure(figsize = (9, 3))
    plt.bar(var_Value.index, var_Value.values)
    plt.xlabel("Passengers")
    plt.ylabel("Rate")
    plt.title(variable)
    plt.show()

### Calling the function and plotting the barplots
data1 = ['Survived','Pclass','Sex','Age','SibSp','Parch','Ticket','Fare','Embarked']
for c in data1:
    bar_plot(c)

# DRAWING COUNTPLOTS
### Drawing the countplot over "surviving" people
sns.countplot(data = df_titanic, x = "Survived")

### Drawing the countplot over "Pclass" people
sns.countplot(data = df_titanic, x = "Pclass")

### Drawing the countplot over "Sex" people
sns.countplot(data = df_titanic, x = "Sex")

### Drawing the countplot over "SibSp" people
sns.countplot(data = df_titanic, x = "SibSp")

### Drawing the countplot over "Parch" people
sns.countplot(data = df_titanic, x = "Parch")

### Drawing the countplot over "Embarked" people
sns.countplot(data = df_titanic, x = "Embarked")

### Drawing the countplot over "Age" people
plt.figure(figsize = (20, 5))
sns.countplot(data = df_titanic, x = "Age")

# DRAWING DISTPLOTS
### Drawing the distplot over "Age" people
sns.distplot(df_titanic["Age"])

# BARPLOT
class_fare = df_titanic.pivot_table(index = "Pclass", values = "Fare")
class_fare.plot(kind = "bar")
plt.xlabel("Pclass")
plt.ylabel("Avg. Fare")
plt.xticks(rotation = 0)
plt.show()

class_fare = df_titanic.pivot_table(index = "Pclass", values = "Fare", aggfunc = np.sum)
class_fare.plot(kind = "bar")
plt.xlabel("Pclass")
plt.ylabel("Total Fare")
plt.xticks(rotation = 0)
plt.show()

### Barplot over "Pclass" , "Fare"
sns.barplot(data = df_titanic, x = "Pclass", y = "Fare", hue = "Survived")

### Barplot over "Survivied" , "Fare"
sns.barplot(data = df_titanic, x = "Survived", y = "Fare", hue = "Pclass")

# CORRELATION MATRIX
corr = df[["Survived", "Pclass", "Age", "SibSp", "Parch", "Fare"]].corr()
plt.figure(figsize = (15, 6))
sns.heatmap(corr, annot = True, cmap = "coolwarm")



