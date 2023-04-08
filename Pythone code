import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn  as sns

app=pd.read_csv("C:/Users/madhu/Downloads/application_data.csv")

### Checking the len of dataset

len(app)

### checking the columns info

app.info()


### checking the duplicate value in dataset

app.duplicated().sum()


### checking the null value in the dataset


app.isnull().sum()


### checking the null value percentage in the dataset which is >50%

null_columns=app.isnull().sum()/app.shape[0]

null_columns[null_columns>0.50].sort_values(ascending=False)


####Approach- Lets drop the columns which have null value more then 50%

dropping_columns=["COMMONAREA_AVG",
"COMMONAREA_MEDI",
"COMMONAREA_MODE",
"NONLIVINGAPARTMENTS_MEDI",
"NONLIVINGAPARTMENTS_AVG",
"NONLIVINGAPARTMENTS_MODE",
"FONDKAPREMONT_MODE",
"LIVINGAPARTMENTS_MEDI",
"LIVINGAPARTMENTS_AVG",
"LIVINGAPARTMENTS_MODE",
"FLOORSMIN_MODE",
"FLOORSMIN_MEDI",
"FLOORSMIN_AVG",
"YEARS_BUILD_MODE",
"YEARS_BUILD_AVG",
"YEARS_BUILD_MEDI",
"OWN_CAR_AGE",
"LANDAREA_AVG",
"LANDAREA_MEDI",
"LANDAREA_MODE",
"BASEMENTAREA_MEDI",
"BASEMENTAREA_AVG",
"BASEMENTAREA_MODE",
"EXT_SOURCE_1",
"NONLIVINGAREA_MODE",
"NONLIVINGAREA_MEDI",
"NONLIVINGAREA_AVG",
"ELEVATORS_MODE",
"ELEVATORS_MEDI",
"ELEVATORS_AVG",
]

app[dropping_columns]

app.drop(columns=dropping_columns,inplace=True)


##### fill null value for categorical columns

categorical=app.select_dtypes(include="object")

#### check the missing value and replace it

categorical.isnull().sum()/categorical.shape[0] ### null value more then 50 we can remove them


### Approach for fill the missing value

categorical.fillna("unknown",inplace=True)


### Finding null value in numerical dataset and find the percentage

numerical=app.select_dtypes(exclude="object")


null=numerical.isnull().sum()/numerical.shape[0]

null[null>0.50].sort_values(ascending=False)


#### Approach towards handling missing value

from sklearn.impute import KNNImputer as kn

imputer=kn(missing_values=np.nan, n_neighbors=5)

data=pd.Dataframe(imputer.fit_transform(numerical),columns=numerical.columns)


#### checking the outlier in the dataset and removing Approach

numerical=app.select_dtypes(exclude="object")


q1=numerical.quantile(0.25)
q3=numerical.quantile(0.75)
iqr=q3-q1
upper_bound=q3+(1.5*iqr)
lower_bound=q1-(1.5*iqr)

col=numerical.columns

new=numerical[(numerical[col]<upper_bound) | (numerical[col]>lower_bound)]


#### checking the data imblance in the dataset

app.TARGET

app["target"]=app["TARGET"].replace({1:"payment_diffi",0:"payer"})

app["target"].value_counts().plot(kind="pie",)


plt.pie(app["target"].value_counts(),labels=app["target"].value_counts(),hu)



#### Find the top 10 correlation in the dataset

### find corellation for target=0

target1=numerical[numerical["TARGET"]==0]

target1.columns

cor=target1.corr()

cor[cor>0.75].unstack().sort_values(ascending=True).head(20)

##### find corellation for target=1

target1=numerical[numerical["TARGET"]==1]

target1.columns

cor=target1.corr()

cor[cor>0.75].unstack().sort_values(ascending=True).head(20)


#### visulization of the dataset to find the insights for recomendation
x=["target"]

sns.barplot(y=app["AMT_CREDIT"],x=app["target"],hue=app["target"])

app.columns


#### marging previous data with app data

prev_df=pd.read_csv("C:/Users/madhu/Downloads/previous_application.csv")

app.rename(columns={"SK_ID_CURR":"sku_id"},inplace=True)

prev_df.rename(columns={"SK_ID_PREV":"sku_id"},inplace=True)

new_df=pd.merge(,app,how="left",on="sku_id")

new_df[new_df["TARGET"]==1]
