# Ex No:1 : Data Cleaning Process

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
## Step 1: Reading the Data
```python
import pandas as pd
df = pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![image](https://github.com/user-attachments/assets/609a889a-e0c0-4893-b51a-b0916e727d31)


## Step 2: Getting the Information
```python
df.isnull()
```
![image](https://github.com/user-attachments/assets/057748ab-19fa-48b7-a7ed-8106c15b3c95)

```python
df.notnull()
```
![image](https://github.com/user-attachments/assets/58646408-b585-499d-bcfb-c6fbf71b8b35)

```python
df.dropna(axis=1)
```
![image](https://github.com/user-attachments/assets/4d1dc9a6-f171-4350-a001-5b56978b16ec)

## Step 3: Remove the null values from the data
```python
df.fillna(0)
```
![image](https://github.com/user-attachments/assets/7fb0de16-0ae1-4026-8df1-1edf41256ca3)

```python
df.isnull().any()
```
![image](https://github.com/user-attachments/assets/255e9313-3fce-4878-bd08-58f4e666cec2)

```python
df.fillna({'GENDER':'MALE', 'NAME':'SRI', 'ADDRESS': 'POONAMALEE','M1':98,'M2':87, 'M3':76,'M4':92,'TOTAL':305,'AVG':89})
```
![image](https://github.com/user-attachments/assets/8b80e243-6363-4394-9214-811bab476769)

## Step 4: Save the clean data to the file.
Save the clean data using the code : (inplace = True)
```python
df.fillna({'GENDER':'MALE', 'NAME':'SRI', 'ADDRESS': 'POONAMALEE','M1':98,'M2':87, 'M3':76,'M4':92,'TOTAL':305,'AVG':89}, inplace = True)
```
![Screenshot from 2025-03-07 14-11-27](https://github.com/user-attachments/assets/291e56cf-4bed-4e6c-bd5e-79bf3a4d58df)

## Step 5: Remove Outliers using IQR
To implement this, we are now using another csv file named "iris.csv". Firstly we need to read that file. Also, we must import "Seaborn" library to execute this.
```python
df1 = pd.read_csv("/content/iris.csv")
df1
```
![image](https://github.com/user-attachments/assets/7c7343a5-40a2-4ce7-9e89-b8856ef3f81a)

### To detect the outliers:
The points before the lower bound and after the upper bound in the graph are the outliers.
```python
import seaborn as sns
sns.boxplot(x = 'sepal_width', data=df1)
```
![image](https://github.com/user-attachments/assets/c5e4563d-b11c-430b-85ca-f4ae9c931b4a)

### To remove the outliers:
```python
c1 = df1.sepal_width.quantile(0.25)
c3 = df1.sepal_width.quantile(0.75)
iq = c3-c1
print (iq)
```
![image](https://github.com/user-attachments/assets/ef398979-ecbd-47e8-a0d1-72aa5a780f1f)

```python
delid = df1[~((df1.sepal_width<(c1-1.5*iq))|(df1.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/user-attachments/assets/ef5f96a3-a6ae-47a9-9476-8e3498bd624b)

### The final data without outliers:
```python
sns.boxplot(x='sepal_width',data = delid)
```
![image](https://github.com/user-attachments/assets/d47f7cdb-f177-4d17-ab5b-6c49c35563ca)

## Step 6: Use ZScore to remove outliers
To implement this, we are now using another csv file named "heights.csv". Firstly we need to read that file. Also, we must import "Scipy" and "Numpy" library to execute this.
```python
import numpy as np
import scipy.stats as stats
df2 = pd.read_csv("/content/heights.csv")
df2
```
![image](https://github.com/user-attachments/assets/d873971d-7bd4-4258-b871-7e295c601630)

```python
z = np.abs(stats.zscore(df2['height']))
z
```
![image](https://github.com/user-attachments/assets/e2e84325-b6d2-4657-a419-3c2ce265f249)

```python
res = df2[z<3]
res
```
![image](https://github.com/user-attachments/assets/0e1952e1-2f4a-4acf-9b52-97f7de2b2a02)


# Result
Thus, in the Data cleaning process, we have read the csv file and got the information from it, identified and removed the null values (changed the null values with some default values). Then, we have identified and removed the outliers using the IQR method and the ZScore method using the libraries Pandas, Numpy, Seaborn and Scipy and saved the cleaned data to the file.
