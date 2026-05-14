# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
~~~
heights.py:

import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt


df = pd.read_csv('heights.csv')
print(df.head(),"\n")

df.info()
print()

print(df.describe(),"\n")

df.isnull()
print(df.isnull().sum())
print()

df_fill_0 = df.fillna(0)
print(df_fill_0,"\n")

df_ffill = df.ffill()
print(df_ffill,"\n")

df_bfill = df.bfill()
print(df_bfill,"\n")

df['height'] = df['height'].fillna(df['height'].mean())
print(df,"\n")

df_dropna = df.dropna()
print(df_dropna,"\n")

sns.boxplot(x=df['height'])
plt.show()
print()

Q1 = df['height'].quantile(0.25)
Q3 = df['height'].quantile(0.75)
IQR = Q3 - Q1
print("IQR:", IQR,"\n")

outliers_iqr = df[
    (df['height'] < (Q1 - 1.5 * IQR)) |
    (df['height'] > (Q3 + 1.5 * IQR))
]
print(outliers_iqr,"\n")

ir_cleaned = df[
    ~((df['height'] < (Q1 - 1.5 * IQR)) |
      (df['height'] > (Q3 + 1.5 * IQR)))
]
print(ir_cleaned,"\n")

df_z = df['height']

z_scores = np.abs(stats.zscore(df_z))
print(z_scores,"\n")

threshold = 3
outliers_z = df_z[z_scores > threshold]
print("Outliers:",outliers_z,"\n")
     
df_z_cleaned = df_z[z_scores <= threshold]
print(df_z_cleaned,"\n")
~~~

<img width="909" height="708" alt="image" src="https://github.com/user-attachments/assets/f859784a-5b6c-40f5-818c-9d4f91785b03" />

~~~
data.head(4)
~~~

<img width="886" height="175" alt="image" src="https://github.com/user-attachments/assets/a4a653f8-f36b-4154-9e87-821c6489ed53" />

~~~
data.tail(7)
~~~

<img width="923" height="269" alt="image" src="https://github.com/user-attachments/assets/ac7a915b-afd7-4b79-8e06-eb0c87f068ab" />

~~~
data.isnull()
~~~

<img width="792" height="707" alt="image" src="https://github.com/user-attachments/assets/29e5c511-2c71-448b-933b-b6c0a679634f" />

~~~
data.notnull()
~~~

<img width="781" height="717" alt="image" src="https://github.com/user-attachments/assets/230e7f9f-d990-4207-9a41-8b03082d87a6" />

~~~
data.isnull().sum()
~~~

<img width="161" height="293" alt="image" src="https://github.com/user-attachments/assets/9b103c9b-5c82-4560-92da-94f846853e3e" />

~~~
data.isnull().any()
~~~

<img width="227" height="284" alt="image" src="https://github.com/user-attachments/assets/4e70075b-b19c-40c1-9866-0d3a2d6b19c6" />

~~~
data.dropna(axis=1)
~~~

<img width="319" height="718" alt="image" src="https://github.com/user-attachments/assets/bc6633b1-748b-45e0-9494-9b1930ee43e7" />

~~~
data.dropna(axis=0)
~~~

<img width="921" height="453" alt="image" src="https://github.com/user-attachments/assets/72431084-125c-462b-8d7b-368f65175bed" />

~~~
data.fillna(0)
~~~

<img width="935" height="719" alt="image" src="https://github.com/user-attachments/assets/b4a48728-e34b-43f2-8fa7-40f3794c811c" />

~~~
data.ffill()
~~~

<img width="928" height="712" alt="image" src="https://github.com/user-attachments/assets/263f85ce-382e-4d0d-b5c5-8589ccac900a" />

~~~
data.bfill()
~~~

<img width="926" height="716" alt="image" src="https://github.com/user-attachments/assets/9e7bed96-93bc-4aa8-85c5-8324a0f92019" />

~~~
data.fillna({'REGNO':0, 'NAME':'PRAVEEN'})
~~~

<img width="921" height="701" alt="image" src="https://github.com/user-attachments/assets/d119f1c1-47d2-4b55-ab9d-eb192e15ab7f" />

~~~
ir=pd.read_csv("iris.csv") 
ir
~~~

<img width="554" height="441" alt="image" src="https://github.com/user-attachments/assets/71f09d52-767d-4d1f-a28e-8414aa102074" />

~~~
ir.describe()
~~~

<img width="499" height="305" alt="image" src="https://github.com/user-attachments/assets/d7cdbe7c-53ea-40f1-ac1f-015893ef2356" />


~~~
import seaborn as sns 
sns.boxplot(x="sepal_width",data=ir)
~~~

<img width="716" height="583" alt="image" src="https://github.com/user-attachments/assets/46823bae-3719-4865-8e56-3ef4a4965709" />

~~~
q1=ir.sepal_width.quantile(0.25)
q3=ir.sepal_width.quantile(0.75)
iqr=q3-q1 
print(iqr)
~~~

<img width="333" height="132" alt="image" src="https://github.com/user-attachments/assets/d3dd7ac9-b420-48f8-98ee-f79744621dd2" />

~~~
rid=ir[((ir.sepal_width<(q1-1.5*iqr))|(ir.sepal_width>(q3+1.5*iqr)))]
rid['sepal_width']
~~~

<img width="346" height="118" alt="image" src="https://github.com/user-attachments/assets/5249fef6-26ce-4b6e-9e07-6a6ca9908928" />

~~~
rid=ir[~((ir.sepal_width<(q1-1.5*iqr))|(ir.sepal_width>(q3+1.5*iqr)))]
rid
~~~

<img width="563" height="438" alt="image" src="https://github.com/user-attachments/assets/33ab03d9-2eec-4b7e-9416-ac9009ded168" />

~~~
rid=ir[((ir.sepal_width>(q1-1.5*iqr))&(ir.sepal_width<(q3+1.5*iqr)))] 
rid['sepal_width']
~~~

<img width="479" height="254" alt="image" src="https://github.com/user-attachments/assets/969f2889-6248-4c40-b770-decad294197d" />

~~~
import numpy as np 
import scipy.stats as stats
z=np.abs(stats.zscore(ir.sepal_width))
z
~~~

<img width="488" height="261" alt="image" src="https://github.com/user-attachments/assets/ed75a7ab-03e8-4187-a1f5-33b3e3b46e2f" />


# Result
Thus the program is executed successfully.
