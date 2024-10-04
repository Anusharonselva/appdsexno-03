# AppDSExno-03

**AIM:**

To Implement Recommendation Systems using the suitable data sets.

**ALGORITHM:**

STEP 1: Load the necessary Datasets.

STEP 2: Include the necessary python library.

STEP 3: Use Fuzzy library for handling text data.

STEP 4: Perform Data Preprocessing Steps.

STEP 5: Standardize column names for merging.

STEP 6: Apply fuzzy matching to find similar text data between datasets.

STEP 7: Perform Data transformation between datasets.

STEP 8: Define a recommendation score using the features of the datasets.

STEP 9: Sort the data by recommendation score.

STEP 10: Export the results to a CSV file.


**CODING & OUTPUT**
```
 import pandas as pd
import numpy as np
pip install pandas numpy scikit-learn fuzzywuzzy python-Levenshtein
```
![Screenshot 2024-10-04 092715](https://github.com/user-attachments/assets/fd21d259-2256-4569-9079-216198f49e40)

```
df =  pd.read_csv('/content/emobile.csv')
df.head()
```
![Screenshot 2024-10-04 092812](https://github.com/user-attachments/assets/2c467c87-c3b2-4ccb-8249-e1b769962258)

```
dx = pd.read_csv('/content/maxmobile.csv')
dx.head()
```
![Screenshot 2024-10-04 092932](https://github.com/user-attachments/assets/e054ded5-99d4-40dd-85ef-2f251165c92d)
```
df.drop_duplicates(inplace=True)
dx.drop_duplicates(inplace=True)
df.columns=['Product_id','Product_Name','Rating','Review_Count']
dx.columns=['Product_id','Product_Name','Rating','Review_Count']
def match_products(name,choices,limit=1):
  results=process.extract(name,choices,limit=limit)
  return results[0][0] if results else None
dx['Matched_Product']= dx['Product_Name'].apply(lambda x: match_products(x,df['Product_Name'].tolist()))
merged_df = pd.merge(df,dx,left_on='Product_Name',right_on='Matched_Product',how='inner',suffixes=('_ds1','_ds2'))
```
```
merged_df
```
![Screenshot 2024-10-04 093122](https://github.com/user-attachments/assets/f944bf5a-0464-4254-a1ad-ea81aecf55e2)
```
merged_df.columns
```
![Screenshot 2024-10-04 093159](https://github.com/user-attachments/assets/450f5f36-8ba6-453d-a5e2-8f958174e808)
```
x = merged_df['Review_Count_ds1'] + merged_df['Review_Count_ds2']
merged_df['Combined_Rating']=(merged_df['Rating_ds1']*merged_df['Review_Count_ds1']+
                             merged_df['Rating_ds2']*merged_df['Review_Count_ds2'])/x
merged_df['Recommendation_score']=0.7*merged_df['Combined_Rating']+0.3*merged_df['Rating_ds1']
```
```
merged_df.head()
```
![Screenshot 2024-10-04 093310](https://github.com/user-attachments/assets/a935ffb2-e55b-477b-93be-a1997e60e579)
```
best_products = merged_df.sort_values(by='Recommendation_score',ascending=False)
```
```
print(best_products[['Matched_Product','Combined_Rating','Recommendation_score']].head(10))
```
![Screenshot 2024-10-04 093551](https://github.com/user-attachments/assets/fe3ffa4e-c8a9-4656-9d19-c0f2852dc58c)
```
rp=pd.read_csv("/content/best_recommended_products.csv")
```
```
rp.head()
```
![Screenshot 2024-10-04 093709](https://github.com/user-attachments/assets/0d4d2c4b-2f01-48de-9ebf-53b66e115055)

**RESULT**
Thus, the Implementation of the Recommendation System for the given dataset is completed successfully.

