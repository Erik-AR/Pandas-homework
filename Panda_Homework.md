
# Trends
### Heroes of Pymoli is mostly played by male players (80%). Male players also spend more money and buy more Items.
### Players seems to buy and spend the most in the age from 17 to 36 more than 200 USD per age group with a peak around 25 to 29, more than 600USD.
### Most profitable item is the "Retribution Axe" it is also one of the most purchased despite an high average price compared to other items in the list of popular items


```python
#import dependencies
import pandas as pd
import numpy as np
#Create Path for json file and printing head to see if correct
json_path = pd.read_json("purchase_data.json")
json_path.head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
##number of total individual (unique) players 
total_players= json_path['SN'].nunique()
total_players

```




    573




```python
# * Number of Unique Items

unique_items = json_path['Item ID'].nunique()
unique_items

```




    183




```python
# * Average Purchase Price

avg_price = json_path['Price'].mean()
round(avg_price, 2)


```




    2.93




```python
# * Total Number of Purchases
total_purchase = json_path['Item Name'].count()
total_purchase

                          
```




    780




```python
# * Total Revenue
totPrice = json_path['Price'].sum()
round(totPrice, 2)


```




    2286.33




```python
#Presenting the numbers above in table
# **Purchasing Analysis (Total)**

# * Number of Unique Items
# * Average Purchase Price
# * Total Number of Purchases
# * Total Revenue

columns = ['Unique Items', 'Avg Purchase Price', 'Total Number of Purchase', 'Total revenue']
purchase_analysis_df = pd. DataFrame(columns = columns)
purchase_analysis_df ['Unique Items'] = [unique_items]
purchase_analysis_df ['Total Number of Purchase'] = [total_purchase]
purchase_analysis_df ['Total revenue'] = [totPrice]
purchase_analysis_df ['Avg Purchase Price'] = [avg_price] 

purchase_analysis_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unique Items</th>
      <th>Avg Purchase Price</th>
      <th>Total Number of Purchase</th>
      <th>Total revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>2.931192</td>
      <td>780</td>
      <td>2286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python

# **Gender Demographics**

grouped_gender_df = json_path.groupby("Gender").count()
grouped_gender_df['SN']



```




    Gender
    Female                   136
    Male                     633
    Other / Non-Disclosed     11
    Name: SN, dtype: int64




```python
# * Percentage and Count of Male Players
total_males = json_path[json_path["Gender"]=="Male"]["SN"].nunique()
male_percent = (total_males/total_players)*100
round(male_percent, 2)
```




    81.15




```python
total_males
```




    465




```python

# * Percentage and Count of Female Players
total_females = json_path[json_path["Gender"]=="Female"]["SN"].nunique()
female_percent = (total_females/total_players)*100
round(female_percent, 2 )
```




    17.45




```python
total_females
```




    100




```python
# * Percentage and Count of Other / Non-Di
total_other = json_path[json_path["Gender"]=="Other / Non-Disclosed"]["SN"].nunique()
other_percent = total_other/total_players*100
round(other_percent,2)
```




    1.4




```python
total_other
```




    8




```python
#Create overview

columns = ['Number', 'Percentage','Total Players']
gender_df = pd. DataFrame(columns = columns)
gender_df ['Number'] = [total_males, total_females, total_other]
gender_df ['Percentage']= [male_percent, female_percent, other_percent]

# gender_df ['Total Players'] = [total_players]
gender_df                            
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number</th>
      <th>Percentage</th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>465</td>
      <td>81.151832</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>100</td>
      <td>17.452007</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>1.396161</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
#   * Purchase Count
#   * Average Purchase Price
# Creating a group based off of the bins



age = json_path["Age"].max()
# age
bins = np.arange(0,49,4)
bins
groups = ['4 to 7', '8 to 12', '13 to 16', '17 to 20', '21 to 24', '25 to 28', '29 to 32', '33 to 36', '37 to 40', '41 to 44', '45 to 48', '49 to 52']
# groups
json_path["age_groups"] = pd.cut(json_path["Age"], bins, labels=groups)
json_path.head()


```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>age_groups</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>41 to 44</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>25 to 28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>37 to 40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>25 to 28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>25 to 28</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Total Purchase Value placed in age groups
age_price = pd.DataFrame(json_path.groupby(["age_groups"])["Price"].sum().reset_index(name = "Total Purchase Value"))
age_price
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age_groups</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4 to 7</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8 to 12</td>
      <td>61.34</td>
    </tr>
    <tr>
      <th>2</th>
      <td>13 to 16</td>
      <td>81.25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17 to 20</td>
      <td>238.89</td>
    </tr>
    <tr>
      <th>4</th>
      <td>21 to 24</td>
      <td>468.03</td>
    </tr>
    <tr>
      <th>5</th>
      <td>25 to 28</td>
      <td>696.09</td>
    </tr>
    <tr>
      <th>6</th>
      <td>29 to 32</td>
      <td>309.37</td>
    </tr>
    <tr>
      <th>7</th>
      <td>33 to 36</td>
      <td>202.09</td>
    </tr>
    <tr>
      <th>8</th>
      <td>37 to 40</td>
      <td>113.28</td>
    </tr>
    <tr>
      <th>9</th>
      <td>41 to 44</td>
      <td>107.35</td>
    </tr>
    <tr>
      <th>10</th>
      <td>45 to 48</td>
      <td>5.92</td>
    </tr>
    <tr>
      <th>11</th>
      <td>49 to 52</td>
      <td>2.72</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Total Purchase Count placed in age groups
age_count = pd.DataFrame(json_path.groupby(["age_groups"])["Price"].count().reset_index(name = "Purchase count"))
age_count
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age_groups</th>
      <th>Purchase count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4 to 7</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8 to 12</td>
      <td>22</td>
    </tr>
    <tr>
      <th>2</th>
      <td>13 to 16</td>
      <td>24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17 to 20</td>
      <td>87</td>
    </tr>
    <tr>
      <th>4</th>
      <td>21 to 24</td>
      <td>161</td>
    </tr>
    <tr>
      <th>5</th>
      <td>25 to 28</td>
      <td>238</td>
    </tr>
    <tr>
      <th>6</th>
      <td>29 to 32</td>
      <td>104</td>
    </tr>
    <tr>
      <th>7</th>
      <td>33 to 36</td>
      <td>66</td>
    </tr>
    <tr>
      <th>8</th>
      <td>37 to 40</td>
      <td>38</td>
    </tr>
    <tr>
      <th>9</th>
      <td>41 to 44</td>
      <td>37</td>
    </tr>
    <tr>
      <th>10</th>
      <td>45 to 48</td>
      <td>2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>49 to 52</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



#Normalized totals

Normalized_totals = json_path.groupby(["age_groups"])["Price"].sum() / json_path.groupby(["age_groups"])["SN"].nunique()
round(Normalized_totals,2)



```python
# * Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
#   * SN
#   * Purchase Count
#   * Average Purchase Price
#   * Total Purchase Value

#Create dataframes
top_spenders = pd.DataFrame(json_path.groupby('SN')["Price"].sum().sort_values(ascending = False).head(5)).reset_index()     
top_spender_count = pd.DataFrame(json_path[json_path['SN'].isin(top_spender['SN'])].groupby('SN')['SN'].count().reset_index(name = 'Purchase Count'))

```


```python
#present dataframe
columns = ['SN', 'Gender', 'Purchase Count', 'Avg Purchase Price']
top_spender_df = pd. DataFrame(columns = columns)
top_spender_df ['SN'] = top_spenders['SN']
top_spender_df ['Gender'] = json_path['Gender']
top_spender_df ['Purchase Value'] = top_spenders['Price']
top_spender_df ['Purchase Count'] = top_spenders_count ['Purchase Count']
top_spender_df ['Avg Purchase Price'] = top_spender_df['Purchase Value']/top_spender_df['Purchase Count']
top_spender_df

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Gender</th>
      <th>Purchase Count</th>
      <th>Avg Purchase Price</th>
      <th>Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Undirrala66</td>
      <td>Male</td>
      <td>3</td>
      <td>5.686667</td>
      <td>17.06</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Saedue76</td>
      <td>Male</td>
      <td>3</td>
      <td>4.520000</td>
      <td>13.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mindimnya67</td>
      <td>Male</td>
      <td>4</td>
      <td>3.185000</td>
      <td>12.74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Haellysu29</td>
      <td>Male</td>
      <td>4</td>
      <td>3.182500</td>
      <td>12.73</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Eoda93</td>
      <td>Male</td>
      <td>5</td>
      <td>2.316000</td>
      <td>11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Identify the 5 most profitable items by total purchase value, then list (in a table):
#   * Item ID
#   * Item Name
#   * Purchase Count
#   * Item Price
#   * Total Purchase Value



# top_item
df_players_count = pd.DataFrame(json_path.groupby(["Item ID","Item Name","Price"])["Item ID"].count().sort_values(ascending = False).head(5).reset_index(name = "Purchase Count"))
df_players_count



```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Purchase Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>84</td>
      <td>Arcane Gem</td>
      <td>2.23</td>
      <td>11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>39</td>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>2.35</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2</th>
      <td>31</td>
      <td>Trickster</td>
      <td>2.07</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>34</td>
      <td>Retribution Axe</td>
      <td>4.14</td>
      <td>9</td>
    </tr>
    <tr>
      <th>4</th>
      <td>175</td>
      <td>Woeful Adamantite Claymore</td>
      <td>1.24</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most profitable Items
profitable_item = pd.DataFrame(json_path.groupby(["Item ID","Item Name","Price"])["Price"].sum().sort_values(ascending = False).head(5).reset_index(name = "Total Value"))
profitable_item
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Total Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>34</td>
      <td>Retribution Axe</td>
      <td>4.14</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>1</th>
      <td>115</td>
      <td>Spectral Diamond Doomblade</td>
      <td>4.25</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>32</td>
      <td>Orenmir</td>
      <td>4.95</td>
      <td>29.70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>103</td>
      <td>Singed Scalpel</td>
      <td>4.87</td>
      <td>29.22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>107</td>
      <td>Splitter, Foe Of Subtlety</td>
      <td>3.61</td>
      <td>28.88</td>
    </tr>
  </tbody>
</table>
</div>


