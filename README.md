## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:

STEP 1:Read the given Data.

STEP 2:Clean the Data Set using Data Cleaning Process.

STEP 3:Apply Feature Encoding for the feature in the data set.

STEP 4:Apply Feature Transformation for the feature in the data set.

STEP 5:Save the data to the file.


# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
```
import pandas as pd
df=pd.read_csv('/content/Encoding Data.csv')
df
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/b1339b0e-66ca-4a4e-a4c9-5de685b34fdb)

# Ordinal Encoding
```
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
pm=['Hot','Warm','Cold']
e1=OrdinalEncoder(categories=[pm])
e1.fit_transform(df[["ord_2"]])
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/46d9700d-3b04-4984-aaad-371b8eeb85f3)

```
df['bo2']=e1.fit_transform(df[["ord_2"]])
df
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/435c0c9c-778f-42a9-9fc4-44820dff2fdc)

# Label Encoder
```
le=LabelEncoder()
dfc=df.copy()
dfc['ord_2']=le.fit_transform(dfc['ord_2'])
dfc
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/16134e42-d50f-4acb-90ee-63bb3257c508)

# OneHot Encoder
```
from sklearn.preprocessing import OneHotEncoder
ohe=OneHotEncoder(sparse=False)
df2=df.copy()
enc=pd.DataFrame(ohe.fit_transform(df2[['nom_0']]))
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/edd808f1-e9df-4027-9de2-260c13c4b1a4)

```
df2=pd.concat([df2,enc],axis=1)
df2
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/e11d000c-1bec-4ca3-8e3c-b7f92c6b26b6)

```
pd.get_dummies(df2,columns=["nom_0"])
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/e077a61f-aea7-443e-84f0-e8689b22f7e5)

# Binary Encoder
```
pip install --upgrade category_encoders
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/cd98f351-d7a0-4300-8d45-95dcb5a756ba)

```
from category_encoders import BinaryEncoder
df=pd.read_csv("/content/data.csv")
df
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/96530562-9fd4-4d2b-80fd-e37e1e4a0d50)

```
be=BinaryEncoder()
nd=be.fit_transform(df['Ord_2'])
dfb=pd.concat([df,nd],axis=1)
dfb
```

![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/5b3da487-5553-44b2-a0da-13949fb94a43)


# Target Encoder
```
from category_encoders import TargetEncoder
te=TargetEncoder()
cc=df.copy()
new=te.fit_transform(X=cc["City"],y=cc["Target"])
cc=pd.concat([cc,new],axis=1)
cc
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/bdd88b6c-9710-400c-842e-69b6c3794fbc)


# Data Transformation
```
import pandas as pd
from scipy import stats
import numpy as np
df=pd.read_csv('/content/Data_to_Transform.csv')
df
```

![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/a22f2b02-0400-4158-92d5-793559d6f405)

```
df.skew()
```

![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/9dcd3777-40df-46e9-835c-0b96906b1933)

```
np.log(df["Highly Positive Skew"])
```

![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/dac20945-36ab-487e-8f6b-e59bbddb5203)

```
np.reciprocal(df["Moderate Positive Skew"])

```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/7635c17a-9dcd-432e-9999-00a8e4b9d03a)

```
np.sqrt(df["Highly Positive Skew"])
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/57079a37-320b-451d-bc2e-29cb90a43e3f)

```
np.square(df["Highly Positive Skew"])
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/6597d7be-eb2d-4584-bb6a-0b770ad5f771)

```
df["Highly Positive Skew_boxcox"],parameters=stats.boxcox(df["Highly Positive Skew"])
df
```

![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/83d8c747-0f0d-4f86-adf1-5946c066a026)

```
df["Moderate Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Moderate Negative Skew"])
df.skew()
```

![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/89f55267-e6ef-46fd-9ff9-2dae83cb2656)



```
df["Highly Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Highly Negative Skew"])
df.skew()
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/f7709441-bc85-4ae0-b3bd-bf8436582a93)

```
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal')
df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])
df
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/6de3342c-a336-4eec-9fe0-03ef236dd3b4)

```
import seaborn as sns
import statsmodels.api as sm
import matplotlib.pyplot as plt
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/f5d79540-0443-4450-863d-c6d5fc9f8ae5)

```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
plt.show()
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/5d540607-354b-4e30-85f1-2afea6c5811c)

```
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/65404c46-639a-4fb9-91e2-302510cfb953)

```
df["Highly Negative Skew_1"]=qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df["Highly Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/661706dd-59fd-43c9-b456-3d4b20c5e36d)

```
sm.qqplot(df['Highly Negative Skew_1'],line='45')
plt.show()
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/7a6dd5cf-db80-4e13-b756-1a6e00f1a334)

```
dt=pd.read_csv("/content/titanic_dataset.csv")
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
dt["Age_1"]=qt.fit_transform(dt[["Age"]])
sm.qqplot(dt['Age'],line='45')
plt.show()
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/7d3feb2c-fa3e-446a-a8be-a930125396c4)

```
sm.qqplot(dt['Age_1'],line='45')
plt.show()
```
![image](https://github.com/sanjaythiyagarajan/EXNO-3-DS/assets/119409242/395eab02-cfe8-483d-8e37-d4001c5a7b23)


      
# RESULT:
      Finally, perform Feature Encoding and Transformation process is executed successfully.
       
