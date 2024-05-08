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
### Data Cleaning
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv("/content/SAMPLEIDS.csv")
data.head()
```
![307660493-2e6f57eb-a0eb-46c0-80b6-78ef2ff9c3b4](https://github.com/GANESH23012861/exno1/assets/147139861/ffad0c1d-30f0-4327-b2dd-0bf3927c3786)

```python
data = pd.get_dummies(data)
data.isnull().sum()
```
![307660704-b11b71a8-0335-4acf-8e69-555a75bacf24](https://github.com/GANESH23012861/exno1/assets/147139861/a38ff94a-183e-4ebf-95d2-e5c9b4f2b7ac)

```python
columns_with_null = data.columns[data.isnull().any()]
import seaborn as sns
plt.figure(figsize=(10,10))
sns.barplot(columns_with_null)
plt.title("NULL VALUES")
plt.show()
```
![307660899-deddaf55-87f4-42dc-b4ce-280775cc04b5](https://github.com/GANESH23012861/exno1/assets/147139861/ca766ded-dd43-4143-836a-b60c9af446c7)

```python
for column in columns_with_null:
    median = data[column].median()  
    data[column].fillna(median, inplace=True)
data.isnull().sum().sum()
```
![307660942-5636ffde-4bb3-4f4b-979f-f81fe1ee00bd](https://github.com/GANESH23012861/exno1/assets/147139861/9e830453-0f7c-45f2-853d-9f0c0e710249)
### IQR
```python
import pandas as pd
import seaborn as sns
ir = pd.read_csv("/content/iris (1).csv")
ir.head()
```
![307661018-93d4d44c-8a8e-42ba-b50e-0d427a929e41](https://github.com/GANESH23012861/exno1/assets/147139861/358f5a83-59f5-45c7-9cd2-41b1c895fb03)

```python
ir.describe()
```
![307661079-82718575-7497-43ea-b6b0-0c048b061dd6](https://github.com/GANESH23012861/exno1/assets/147139861/c7794747-1744-4bbe-8f3f-e3984cea4364)

```python
sns.boxplot(x='sepal_width',data=ir)
```
![307661160-2a264b0b-1be7-4cb5-993a-edfb54c7369d](https://github.com/GANESH23012861/exno1/assets/147139861/edf802d8-6134-4d5f-b902-1b436fc023e0)
### Z Score
```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```
![307661405-65296f84-d620-42a2-91e9-825f3313e72c](https://github.com/GANESH23012861/exno1/assets/147139861/ca7cb9d3-2118-42f4-a662-ce12b34f3820)

```python
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```

```python
iqr = q3-q1
iqr
```
![307661484-b9d6b692-7f29-4303-8e22-335186cf6ae3](https://github.com/GANESH23012861/exno1/assets/147139861/8b6d11d2-d804-4392-8dbc-8439821cc77f)

```python
low = q1 - 1.5*iqr
low
```
![307661531-3f341bea-42c2-4cbd-928a-9e1fa576cfaf](https://github.com/GANESH23012861/exno1/assets/147139861/c92b6ed5-6ae2-4ade-a0d2-61c62ca88a8a)

```python
high = q3 + 1.5*iqr
high
```
![307661569-ae80602f-3344-443c-a723-d5cef7928731](https://github.com/GANESH23012861/exno1/assets/147139861/4f14e20e-a17c-4d9f-a0aa-98583ad578ba)

```python
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![307661642-3e5ce1e1-567e-4253-82bb-192c04024d35](https://github.com/GANESH23012861/exno1/assets/147139861/a62184d6-c313-4d42-8fc9-330e7fa1e449)

```python
z = np.abs(stats.zscore(df['height']))
z
```
![307661670-ef207f0d-fcc0-452e-bbd3-5f3c48a03515](https://github.com/GANESH23012861/exno1/assets/147139861/b7ffea06-bca0-43b9-a63b-5f7679b0924b)

# Result
Thus the outliers are detected and removed in the given file and the final data set is saved into the file.
