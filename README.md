# Ex-08-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.

```
Developed by: S Adithya Chowdary.
Register no: 212221230100.
```
# CODE
~~~
#loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
~~~
~~~
#removing unnecessary data variables
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()
~~~
~~~
#detecting and removing outliers in current numeric data
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
~~~
~~~
#data visualization
#line plots
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
~~~
~~~
#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
~~~
~~~
#Histogram
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
~~~
~~~
#count plot
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
~~~
~~~
#Barplot 
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
~~~
~~~
#KDE plot
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
~~~
~~~
#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
~~~
~~~
#point plot
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
~~~
~~~
#Pie Chart
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
~~~
~~~
#HeatMap
df4=df.copy()

#encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])

#scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

#Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
~~~
# OUPUT:
![image](https://user-images.githubusercontent.com/93427248/205423103-b0304d8f-9e10-4512-ad70-623ab27847b2.png)

![image](https://user-images.githubusercontent.com/93427248/205423135-74339e6b-762d-412c-b07c-529f01dca4b4.png)

![image](https://user-images.githubusercontent.com/93427248/205423153-f6c7da36-5efb-45f7-9fdc-5db9b8814a83.png)

![image](https://user-images.githubusercontent.com/93427248/205423173-0e92010d-8071-43e5-bb8a-7b8bed2b3f81.png)

![image](https://user-images.githubusercontent.com/93427248/205423188-39176c1d-72c2-45f2-9c11-2ab3f0ea0e9d.png)

![image](https://user-images.githubusercontent.com/93427248/205423230-0647f189-c7a1-4688-a390-27fd2e85eb88.png)

![image](https://user-images.githubusercontent.com/93427248/205423247-6d48f2c8-1fe6-4a12-a550-dc23d10b60e3.png)

![image](https://user-images.githubusercontent.com/93427248/205423281-5bd95887-dd1f-42e0-99ae-6daa6842bc77.png)

![image](https://user-images.githubusercontent.com/93427248/205423401-2a510422-88c2-4a56-9df9-79fd353cad8e.png)

![image](https://user-images.githubusercontent.com/93427248/205423537-f1048652-43fc-40ae-909b-20d2428b5d97.png)

![image](https://user-images.githubusercontent.com/93427248/205423640-2becefe1-9206-4854-8ecb-22bfe2fb5b3b.png)

![image](https://user-images.githubusercontent.com/93427248/205423704-9994b449-da27-4ad6-85a8-bbf8d79daf4b.png)

![image](https://user-images.githubusercontent.com/93427248/205423791-b3c00db8-3186-4ae1-97d2-d747d5b20824.png)

![image](https://user-images.githubusercontent.com/93427248/205423886-ce05142b-805f-4319-b7c5-aa452c6e3b46.png)

![image](https://user-images.githubusercontent.com/93427248/205423920-92d53848-f4e3-4a5e-984c-272a2c7ce686.png)

![image](https://user-images.githubusercontent.com/93427248/205423934-4333b3a8-240b-4d13-bc73-646da1ed4cfa.png)

![image](https://user-images.githubusercontent.com/93427248/205423956-e398f32e-f549-4ff3-bf15-f5d08407d335.png)

![image](https://user-images.githubusercontent.com/93427248/205423965-0e9bf3bf-7e09-4835-9357-862479e3d98a.png)

![image](https://user-images.githubusercontent.com/93427248/205423986-bb8a757e-d0e9-411c-ae74-54555c106406.png)

![image](https://user-images.githubusercontent.com/93427248/205423997-4a704b4f-c9ea-4bfa-8388-42de7a44f16a.png)

![image](https://user-images.githubusercontent.com/93427248/205424026-27774569-de57-4514-8318-cef305a8e04f.png)

![image](https://user-images.githubusercontent.com/93427248/205424047-5ade4cdc-31a1-43c9-8e54-c432df93eb8f.png)

![image](https://user-images.githubusercontent.com/93427248/205424064-cb198dae-d73c-4865-8de5-079792bb73dc.png)

![image](https://user-images.githubusercontent.com/93427248/205424074-b52e4a1b-c279-4303-b587-080930ce2caa.png)

![image](https://user-images.githubusercontent.com/93427248/205424097-7bd0af9b-cf0e-4447-8050-c77362e57004.png)

![image](https://user-images.githubusercontent.com/93427248/205424112-10b6fdac-4653-499b-98d0-339d017f8c36.png)

# Result:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file.
