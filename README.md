# zomato-analysis
import pandas as pd 
import numpy as np 
import matplotlib.pyplot as plt
import seaborn as sns
plt.style.use('dark_background')

data={'Name':['Indian Accent','Moti Mahal','Farzi Cafe'],'City':['Delhi','Delhi','Delhi'],'Address':['The Lodhi, Lodhi Road, New Delhi','3703, Netaji Subhash Marg, Daryaganj','38/39, Level 1, Block E, Inner Circle, Connaught Place, New Delhi'],'Pincode':[110003,110002,110001],'Rate':[4.5,3.9,4.8],'Cuisines':['North indian','Chinese','North indian'],'Votes':[500 , 700 , 700] }
product_ids=['001','002','003']
df=pd.DataFrame(data,index=product_ids)
df
df.shape 
df.columns
df.Rate.isnull().sum()
df['Rate'].fillna(df['Rate'].mean(),inplace=True)
df['Rate'].isnull().sum()
df['City'].unique()

cuisines=df['Cuisines'].value_counts(ascending=False)

cuisines_lessrate = cuisines[cuisines<2]

def handle_cuisines(value):
    if(value in cuisines_lessrate):
        return 'others'
    else:
        return value
df['Cuisines'] = df['Cuisines'].apply(handle_cuisines)
df['Cuisines'].value_counts()
df.head()

Votes = df['Votes'].value_counts(ascending = False)

votes_lessthan500 = Votes[Votes>500]

def handle_votes(value):
    if(value in votes_lessthan500):
        return 'others'
    else:
        return value
df['Votes'] = df['Votes'].apply(handle_votes)
df['Votes'].value_counts()
df.head()

plt.figure(figsize=(6,6))
ax=sns.countplot(df['Votes'])
plt.show()
