```python
import os
import pandas as pd
import numpy as np
os.chdir('/users/mohammadawais/desktop')
```


```python
os.getcwd()
```




    '/Users/mohammadawais/Desktop'




```python
import json
import seaborn as sns
import matplotlib.pyplot as plt
import json
import csv
```


```python
from scipy.stats import skew
from scipy.stats import kurtosis 
```


```python
df=pd.read_json('data.json',lines=True)

```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>item_id</th>
      <th>waist</th>
      <th>size</th>
      <th>quality</th>
      <th>cup size</th>
      <th>hips</th>
      <th>bra size</th>
      <th>category</th>
      <th>bust</th>
      <th>height</th>
      <th>user_name</th>
      <th>length</th>
      <th>fit</th>
      <th>user_id</th>
      <th>shoe size</th>
      <th>shoe width</th>
      <th>review_summary</th>
      <th>review_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>123373</td>
      <td>29.0</td>
      <td>7</td>
      <td>5.0</td>
      <td>d</td>
      <td>38.0</td>
      <td>34.0</td>
      <td>new</td>
      <td>36</td>
      <td>5ft 6in</td>
      <td>Emily</td>
      <td>just right</td>
      <td>small</td>
      <td>991571</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>123373</td>
      <td>31.0</td>
      <td>13</td>
      <td>3.0</td>
      <td>b</td>
      <td>30.0</td>
      <td>36.0</td>
      <td>new</td>
      <td>NaN</td>
      <td>5ft 2in</td>
      <td>sydneybraden2001</td>
      <td>just right</td>
      <td>small</td>
      <td>587883</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>123373</td>
      <td>30.0</td>
      <td>7</td>
      <td>2.0</td>
      <td>b</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>new</td>
      <td>NaN</td>
      <td>5ft 7in</td>
      <td>Ugggh</td>
      <td>slightly long</td>
      <td>small</td>
      <td>395665</td>
      <td>9.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>123373</td>
      <td>NaN</td>
      <td>21</td>
      <td>5.0</td>
      <td>dd/e</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>new</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>alexmeyer626</td>
      <td>just right</td>
      <td>fit</td>
      <td>875643</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>123373</td>
      <td>NaN</td>
      <td>18</td>
      <td>5.0</td>
      <td>b</td>
      <td>NaN</td>
      <td>36.0</td>
      <td>new</td>
      <td>NaN</td>
      <td>5ft 2in</td>
      <td>dberrones1</td>
      <td>slightly long</td>
      <td>small</td>
      <td>944840</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.to_csv('data.csv')

```

# Investigation of Dataset


```python
df=pd.read_csv('data.csv')
```

    /opt/anaconda3/lib/python3.7/site-packages/IPython/core/interactiveshell.py:3063: DtypeWarning: Columns (9) have mixed types.Specify dtype option on import or set low_memory=False.
      interactivity=interactivity, compiler=compiler, result=result)



```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>item_id</th>
      <th>waist</th>
      <th>size</th>
      <th>quality</th>
      <th>cup size</th>
      <th>hips</th>
      <th>bra size</th>
      <th>category</th>
      <th>bust</th>
      <th>height</th>
      <th>user_name</th>
      <th>length</th>
      <th>fit</th>
      <th>user_id</th>
      <th>shoe size</th>
      <th>shoe width</th>
      <th>review_summary</th>
      <th>review_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>123373</td>
      <td>29.0</td>
      <td>7</td>
      <td>5.0</td>
      <td>d</td>
      <td>38.0</td>
      <td>34.0</td>
      <td>new</td>
      <td>36</td>
      <td>5ft 6in</td>
      <td>Emily</td>
      <td>just right</td>
      <td>small</td>
      <td>991571</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>123373</td>
      <td>31.0</td>
      <td>13</td>
      <td>3.0</td>
      <td>b</td>
      <td>30.0</td>
      <td>36.0</td>
      <td>new</td>
      <td>NaN</td>
      <td>5ft 2in</td>
      <td>sydneybraden2001</td>
      <td>just right</td>
      <td>small</td>
      <td>587883</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>123373</td>
      <td>30.0</td>
      <td>7</td>
      <td>2.0</td>
      <td>b</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>new</td>
      <td>NaN</td>
      <td>5ft 7in</td>
      <td>Ugggh</td>
      <td>slightly long</td>
      <td>small</td>
      <td>395665</td>
      <td>9.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>123373</td>
      <td>NaN</td>
      <td>21</td>
      <td>5.0</td>
      <td>dd/e</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>new</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>alexmeyer626</td>
      <td>just right</td>
      <td>fit</td>
      <td>875643</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>123373</td>
      <td>NaN</td>
      <td>18</td>
      <td>5.0</td>
      <td>b</td>
      <td>NaN</td>
      <td>36.0</td>
      <td>new</td>
      <td>NaN</td>
      <td>5ft 2in</td>
      <td>dberrones1</td>
      <td>slightly long</td>
      <td>small</td>
      <td>944840</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.shape
```




    (82790, 19)




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 82790 entries, 0 to 82789
    Data columns (total 19 columns):
     #   Column          Non-Null Count  Dtype  
    ---  ------          --------------  -----  
     0   Unnamed: 0      82790 non-null  int64  
     1   item_id         82790 non-null  int64  
     2   waist           2882 non-null   float64
     3   size            82790 non-null  int64  
     4   quality         82722 non-null  float64
     5   cup size        76535 non-null  object 
     6   hips            56064 non-null  float64
     7   bra size        76772 non-null  float64
     8   category        82790 non-null  object 
     9   bust            11854 non-null  object 
     10  height          81683 non-null  object 
     11  user_name       82790 non-null  object 
     12  length          82755 non-null  object 
     13  fit             82790 non-null  object 
     14  user_id         82790 non-null  int64  
     15  shoe size       27915 non-null  float64
     16  shoe width      18607 non-null  object 
     17  review_summary  76058 non-null  object 
     18  review_text     76058 non-null  object 
    dtypes: float64(5), int64(4), object(10)
    memory usage: 12.0+ MB



```python
def missing_values(df):
    total=df.isnull().sum().sort_values(ascending=False)
    percent = round(df.isnull().sum().sort_values(ascending = False)/len(df)*100,4)
    return pd.concat([total, percent], axis=1, keys=['Total','Percent'])
missing_values(df)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total</th>
      <th>Percent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>waist</th>
      <td>79908</td>
      <td>96.5189</td>
    </tr>
    <tr>
      <th>bust</th>
      <td>70936</td>
      <td>85.6818</td>
    </tr>
    <tr>
      <th>shoe width</th>
      <td>64183</td>
      <td>77.5251</td>
    </tr>
    <tr>
      <th>shoe size</th>
      <td>54875</td>
      <td>66.2822</td>
    </tr>
    <tr>
      <th>hips</th>
      <td>26726</td>
      <td>32.2817</td>
    </tr>
    <tr>
      <th>review_summary</th>
      <td>6732</td>
      <td>8.1314</td>
    </tr>
    <tr>
      <th>review_text</th>
      <td>6732</td>
      <td>8.1314</td>
    </tr>
    <tr>
      <th>cup size</th>
      <td>6255</td>
      <td>7.5553</td>
    </tr>
    <tr>
      <th>bra size</th>
      <td>6018</td>
      <td>7.2690</td>
    </tr>
    <tr>
      <th>height</th>
      <td>1107</td>
      <td>1.3371</td>
    </tr>
    <tr>
      <th>quality</th>
      <td>68</td>
      <td>0.0821</td>
    </tr>
    <tr>
      <th>length</th>
      <td>35</td>
      <td>0.0423</td>
    </tr>
    <tr>
      <th>user_name</th>
      <td>0</td>
      <td>0.0000</td>
    </tr>
    <tr>
      <th>category</th>
      <td>0</td>
      <td>0.0000</td>
    </tr>
    <tr>
      <th>fit</th>
      <td>0</td>
      <td>0.0000</td>
    </tr>
    <tr>
      <th>size</th>
      <td>0</td>
      <td>0.0000</td>
    </tr>
    <tr>
      <th>user_id</th>
      <td>0</td>
      <td>0.0000</td>
    </tr>
    <tr>
      <th>item_id</th>
      <td>0</td>
      <td>0.0000</td>
    </tr>
    <tr>
      <th>Unnamed: 0</th>
      <td>0</td>
      <td>0.0000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>item_id</th>
      <th>waist</th>
      <th>size</th>
      <th>quality</th>
      <th>hips</th>
      <th>bra size</th>
      <th>user_id</th>
      <th>shoe size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>82790.00000</td>
      <td>82790.000000</td>
      <td>2882.000000</td>
      <td>82790.000000</td>
      <td>82722.000000</td>
      <td>56064.000000</td>
      <td>76772.000000</td>
      <td>82790.000000</td>
      <td>27915.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>41394.50000</td>
      <td>469325.229170</td>
      <td>31.319223</td>
      <td>12.661602</td>
      <td>3.949058</td>
      <td>40.358501</td>
      <td>35.972125</td>
      <td>498849.564718</td>
      <td>8.145818</td>
    </tr>
    <tr>
      <th>std</th>
      <td>23899.55873</td>
      <td>213999.803314</td>
      <td>5.302849</td>
      <td>8.271952</td>
      <td>0.992783</td>
      <td>5.827166</td>
      <td>3.224907</td>
      <td>286356.969459</td>
      <td>1.336109</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.00000</td>
      <td>123373.000000</td>
      <td>20.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>30.000000</td>
      <td>28.000000</td>
      <td>6.000000</td>
      <td>5.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>20697.25000</td>
      <td>314980.000000</td>
      <td>28.000000</td>
      <td>8.000000</td>
      <td>3.000000</td>
      <td>36.000000</td>
      <td>34.000000</td>
      <td>252897.750000</td>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>41394.50000</td>
      <td>454030.000000</td>
      <td>30.000000</td>
      <td>12.000000</td>
      <td>4.000000</td>
      <td>39.000000</td>
      <td>36.000000</td>
      <td>497913.500000</td>
      <td>8.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>62091.75000</td>
      <td>658440.000000</td>
      <td>34.000000</td>
      <td>15.000000</td>
      <td>5.000000</td>
      <td>43.000000</td>
      <td>38.000000</td>
      <td>744745.250000</td>
      <td>9.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>82789.00000</td>
      <td>807722.000000</td>
      <td>50.000000</td>
      <td>38.000000</td>
      <td>5.000000</td>
      <td>60.000000</td>
      <td>48.000000</td>
      <td>999972.000000</td>
      <td>38.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.isnull().sum()
```




    Unnamed: 0            0
    item_id               0
    waist             79908
    size                  0
    quality              68
    cup size           6255
    hips              26726
    bra size           6018
    category              0
    bust              70936
    height             1107
    user_name             0
    length               35
    fit                   0
    user_id               0
    shoe size         54875
    shoe width        64183
    review_summary     6732
    review_text        6732
    dtype: int64




```python
df.corr()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>item_id</th>
      <th>waist</th>
      <th>size</th>
      <th>quality</th>
      <th>hips</th>
      <th>bra size</th>
      <th>user_id</th>
      <th>shoe size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Unnamed: 0</th>
      <td>1.000000</td>
      <td>0.990350</td>
      <td>0.017770</td>
      <td>0.003858</td>
      <td>0.009108</td>
      <td>0.003133</td>
      <td>-0.009065</td>
      <td>0.007197</td>
      <td>0.021591</td>
    </tr>
    <tr>
      <th>item_id</th>
      <td>0.990350</td>
      <td>1.000000</td>
      <td>0.023007</td>
      <td>0.004712</td>
      <td>0.011850</td>
      <td>0.006440</td>
      <td>-0.005902</td>
      <td>0.007144</td>
      <td>0.021842</td>
    </tr>
    <tr>
      <th>waist</th>
      <td>0.017770</td>
      <td>0.023007</td>
      <td>1.000000</td>
      <td>0.846494</td>
      <td>0.015710</td>
      <td>0.832980</td>
      <td>0.761668</td>
      <td>-0.011112</td>
      <td>0.315472</td>
    </tr>
    <tr>
      <th>size</th>
      <td>0.003858</td>
      <td>0.004712</td>
      <td>0.846494</td>
      <td>1.000000</td>
      <td>-0.024556</td>
      <td>0.747257</td>
      <td>0.788460</td>
      <td>-0.005214</td>
      <td>0.447805</td>
    </tr>
    <tr>
      <th>quality</th>
      <td>0.009108</td>
      <td>0.011850</td>
      <td>0.015710</td>
      <td>-0.024556</td>
      <td>1.000000</td>
      <td>-0.017317</td>
      <td>-0.019930</td>
      <td>0.004547</td>
      <td>-0.025066</td>
    </tr>
    <tr>
      <th>hips</th>
      <td>0.003133</td>
      <td>0.006440</td>
      <td>0.832980</td>
      <td>0.747257</td>
      <td>-0.017317</td>
      <td>1.000000</td>
      <td>0.671034</td>
      <td>-0.006886</td>
      <td>0.417403</td>
    </tr>
    <tr>
      <th>bra size</th>
      <td>-0.009065</td>
      <td>-0.005902</td>
      <td>0.761668</td>
      <td>0.788460</td>
      <td>-0.019930</td>
      <td>0.671034</td>
      <td>1.000000</td>
      <td>-0.000769</td>
      <td>0.415777</td>
    </tr>
    <tr>
      <th>user_id</th>
      <td>0.007197</td>
      <td>0.007144</td>
      <td>-0.011112</td>
      <td>-0.005214</td>
      <td>0.004547</td>
      <td>-0.006886</td>
      <td>-0.000769</td>
      <td>1.000000</td>
      <td>0.005364</td>
    </tr>
    <tr>
      <th>shoe size</th>
      <td>0.021591</td>
      <td>0.021842</td>
      <td>0.315472</td>
      <td>0.447805</td>
      <td>-0.025066</td>
      <td>0.417403</td>
      <td>0.415777</td>
      <td>0.005364</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
a=df.groupby(by=['item_id'])
a.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>item_id</th>
      <th>waist</th>
      <th>size</th>
      <th>quality</th>
      <th>cup size</th>
      <th>hips</th>
      <th>bra size</th>
      <th>category</th>
      <th>bust</th>
      <th>height</th>
      <th>user_name</th>
      <th>length</th>
      <th>fit</th>
      <th>user_id</th>
      <th>shoe size</th>
      <th>shoe width</th>
      <th>review_summary</th>
      <th>review_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>123373</td>
      <td>29.0</td>
      <td>7</td>
      <td>5.0</td>
      <td>d</td>
      <td>38.0</td>
      <td>34.0</td>
      <td>new</td>
      <td>36</td>
      <td>5ft 6in</td>
      <td>Emily</td>
      <td>just right</td>
      <td>small</td>
      <td>991571</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>123373</td>
      <td>31.0</td>
      <td>13</td>
      <td>3.0</td>
      <td>b</td>
      <td>30.0</td>
      <td>36.0</td>
      <td>new</td>
      <td>NaN</td>
      <td>5ft 2in</td>
      <td>sydneybraden2001</td>
      <td>just right</td>
      <td>small</td>
      <td>587883</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>123373</td>
      <td>30.0</td>
      <td>7</td>
      <td>2.0</td>
      <td>b</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>new</td>
      <td>NaN</td>
      <td>5ft 7in</td>
      <td>Ugggh</td>
      <td>slightly long</td>
      <td>small</td>
      <td>395665</td>
      <td>9.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>123373</td>
      <td>NaN</td>
      <td>21</td>
      <td>5.0</td>
      <td>dd/e</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>new</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>alexmeyer626</td>
      <td>just right</td>
      <td>fit</td>
      <td>875643</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>123373</td>
      <td>NaN</td>
      <td>18</td>
      <td>5.0</td>
      <td>b</td>
      <td>NaN</td>
      <td>36.0</td>
      <td>new</td>
      <td>NaN</td>
      <td>5ft 2in</td>
      <td>dberrones1</td>
      <td>slightly long</td>
      <td>small</td>
      <td>944840</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>82743</th>
      <td>82743</td>
      <td>807722</td>
      <td>NaN</td>
      <td>4</td>
      <td>5.0</td>
      <td>a</td>
      <td>NaN</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>NaN</td>
      <td>5ft</td>
      <td>Susan</td>
      <td>just right</td>
      <td>fit</td>
      <td>711738</td>
      <td>7.0</td>
      <td>NaN</td>
      <td>I bought this on Friday a</td>
      <td>I bought this on Friday and got it today.  It ...</td>
    </tr>
    <tr>
      <th>82744</th>
      <td>82744</td>
      <td>807722</td>
      <td>NaN</td>
      <td>12</td>
      <td>3.0</td>
      <td>d</td>
      <td>NaN</td>
      <td>42.0</td>
      <td>outerwear</td>
      <td>NaN</td>
      <td>5ft 5in</td>
      <td>cinternet5</td>
      <td>just right</td>
      <td>fit</td>
      <td>574877</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I like the jacket. Howeve</td>
      <td>I like the jacket. However, the quality and ma...</td>
    </tr>
    <tr>
      <th>82745</th>
      <td>82745</td>
      <td>807722</td>
      <td>NaN</td>
      <td>12</td>
      <td>5.0</td>
      <td>b</td>
      <td>37.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>NaN</td>
      <td>5ft 6in</td>
      <td>Siddie</td>
      <td>just right</td>
      <td>fit</td>
      <td>348195</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A great jacket, helps acc</td>
      <td>A great jacket, helps accentuate small breasts...</td>
    </tr>
    <tr>
      <th>82746</th>
      <td>82746</td>
      <td>807722</td>
      <td>NaN</td>
      <td>8</td>
      <td>2.0</td>
      <td>c</td>
      <td>38.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>NaN</td>
      <td>5ft 8in</td>
      <td>candyb32</td>
      <td>just right</td>
      <td>small</td>
      <td>516900</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>This feels like a sweatsh</td>
      <td>This feels like a sweatshirt. It isn't a jacke...</td>
    </tr>
    <tr>
      <th>82747</th>
      <td>82747</td>
      <td>807722</td>
      <td>NaN</td>
      <td>12</td>
      <td>3.0</td>
      <td>b</td>
      <td>38.0</td>
      <td>36.0</td>
      <td>outerwear</td>
      <td>34</td>
      <td>5ft 11in</td>
      <td>Kelly</td>
      <td>just right</td>
      <td>fit</td>
      <td>415686</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I really like the look of</td>
      <td>I really like the look of this jacket. The fab...</td>
    </tr>
  </tbody>
</table>
<p>4509 rows × 19 columns</p>
</div>




```python
b=df.groupby(df['user_id']).user_id.count()
b
```




    user_id
    6         1
    46        1
    55        1
    66        4
    104       2
             ..
    999864    1
    999887    2
    999888    1
    999923    3
    999972    3
    Name: user_id, Length: 47958, dtype: int64




```python
print(df.skew())

```

    Unnamed: 0    0.000000
    item_id      -0.120644
    waist         0.993061
    size          1.128301
    quality      -0.676777
    hips          0.969187
    bra size      0.901004
    user_id       0.008201
    shoe size     0.436713
    dtype: float64



```python
print(df.kurtosis())
```

    Unnamed: 0   -1.200000
    item_id      -1.215909
    waist         0.836624
    size          0.760010
    quality      -0.167085
    hips          0.848464
    bra size      1.039445
    user_id      -1.182436
    shoe size     8.448820
    dtype: float64



```python
most_no_of_items = df.groupby(by='item_id')['item_id'].count().sort_values(ascending=False)

print(most_no_of_items.head())
print('total no of items',most_no_of_items.count())
```

    item_id
    539980    2008
    668696    1555
    397005    1506
    175771    1438
    407134    1437
    Name: item_id, dtype: int64
    total no of items 1378



```python
most_active_user=df.groupby(by='user_id')['user_id'].count().sort_values(ascending=False)
print(most_active_user.head())
print('total no of users',most_active_user.count())
```

    user_id
    754084    27
    684924    25
    207153    23
    305119    22
    669884    22
    Name: user_id, dtype: int64
    total no of users 47958


# Exploratory Data Analysis


```python
df.columns
```




    Index(['Unnamed: 0', 'item_id', 'waist', 'size', 'quality', 'cup size', 'hips',
           'bra size', 'category', 'bust', 'height', 'user_name', 'length', 'fit',
           'user_id', 'shoe size', 'shoe width', 'review_summary', 'review_text'],
          dtype='object')




```python
sns.heatmap(df.isnull(),yticklabels=False,cbar=False,cmap='viridis')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x105f05ed0>




![png](output_24_1.png)



```python
df.waist.hist()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x105f288d0>




![png](output_25_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='cup size',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x105f18c10>




![png](output_26_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='bra size',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20b01b90>




![png](output_27_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='category',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20b1dcd0>




![png](output_28_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='length',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x105f362d0>




![png](output_29_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20b40290>




![png](output_30_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='quality',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20af5ad0>




![png](output_31_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='size',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20b612d0>




![png](output_32_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='waist',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20b61390>




![png](output_33_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='hips',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20bb2890>




![png](output_34_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='bust',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20bcdf10>




![png](output_35_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='height',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20bee950>




![png](output_36_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='shoe size',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20bae950>




![png](output_37_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='shoe width',data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20c55f90>




![png](output_38_1.png)



```python
sns.set_style('darkgrid')
sns.countplot(x='quality',hue='fit',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20c70cd0>




![png](output_39_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='quality',hue='length',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20c86250>




![png](output_40_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='length',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20ca4250>




![png](output_41_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='category',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20cb92d0>




![png](output_42_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='bra size',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20cb5710>




![png](output_43_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='size',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20cd2450>




![png](output_44_1.png)



```python
df.columns
```




    Index(['Unnamed: 0', 'item_id', 'waist', 'size', 'quality', 'cup size', 'hips',
           'bra size', 'category', 'bust', 'height', 'user_name', 'length', 'fit',
           'user_id', 'shoe size', 'shoe width', 'review_summary', 'review_text'],
          dtype='object')




```python
sns.distplot(df['waist'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20cdbad0>




![png](output_46_1.png)



```python
sns.distplot(df['size'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20d46b10>




![png](output_47_1.png)



```python
sns.distplot(df['quality'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20d66550>




![png](output_48_1.png)



```python
sns.distplot(df['hips'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20d860d0>




![png](output_49_1.png)



```python
sns.distplot(df['bra size'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20daef90>




![png](output_50_1.png)



```python
sns.distplot(df['shoe size'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20dc0f10>




![png](output_51_1.png)



```python
df.columns
```




    Index(['Unnamed: 0', 'item_id', 'waist', 'size', 'quality', 'cup size', 'hips',
           'bra size', 'category', 'bust', 'height', 'user_name', 'length', 'fit',
           'user_id', 'shoe size', 'shoe width', 'review_summary', 'review_text'],
          dtype='object')




```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='size',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20dde750>




![png](output_53_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='quality',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20dae590>




![png](output_54_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='waist',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20e4ee50>




![png](output_55_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='cup size',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20e4ddd0>




![png](output_56_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='hips',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20e45c90>




![png](output_57_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='bra size',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20ed07d0>




![png](output_58_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='category',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20ee2ed0>




![png](output_59_1.png)



```python
sns.set_style('whitegrid')
sns.countplot(x='fit',hue='bust',data=df,palette='RdBu_r')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20ef4090>




![png](output_60_1.png)



```python
sns.set_style('darkgrid')
sns.countplot(x='fit',hue='length',data=df,palette='rainbow')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20f18510>




![png](output_61_1.png)



```python
df['size'].hist(bins=10,color='darkred',alpha=0.3)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20fa4d50>




![png](output_62_1.png)



```python
df.columns
```




    Index(['Unnamed: 0', 'item_id', 'waist', 'size', 'quality', 'cup size', 'hips',
           'bra size', 'category', 'bust', 'height', 'user_name', 'length', 'fit',
           'user_id', 'shoe size', 'shoe width', 'review_summary', 'review_text'],
          dtype='object')



# Outlier Detection


```python
plt.figure(figsize=(12, 7))
sns.boxplot(x='waist',data=df,palette='winter')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20f2d610>




![png](output_65_1.png)



```python
plt.figure(figsize=(12, 7))
sns.boxplot(x='size',data=df,palette='winter')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20fae5d0>




![png](output_66_1.png)



```python
plt.figure(figsize=(12, 7))
sns.boxplot(x='hips',data=df,palette='winter')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20fa65d0>




![png](output_67_1.png)



```python
plt.figure(figsize=(12, 7))
sns.boxplot(x='bra size',data=df,palette='winter')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20ff4f50>




![png](output_68_1.png)



```python
plt.figure(figsize=(12, 7))
sns.boxplot(x='shoe size',data=df,palette='winter')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a20fcae10>




![png](output_69_1.png)



```python
sns.set_style("whitegrid");
sns.FacetGrid(df, hue="fit", size=4).map(plt.scatter, "waist", "quality").add_legend();
plt.show()
```

    /opt/anaconda3/lib/python3.7/site-packages/seaborn/axisgrid.py:243: UserWarning: The `size` parameter has been renamed to `height`; please update your code.
      warnings.warn(msg, UserWarning)



![png](output_70_1.png)



```python
df.boxplot(column='waist',by='fit')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a21028bd0>




![png](output_71_1.png)



```python
df.boxplot(column='quality',by='fit')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a21033990>




![png](output_72_1.png)



```python
df.boxplot(column='hips',by='fit')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a21038190>




![png](output_73_1.png)



```python
df.boxplot(column='bra size',by='fit')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a210542d0>




![png](output_74_1.png)


# Preprocessing


```python
df.drop(columns=['waist'],inplace=True,axis=1)
# more than 96% of the data are missing and may 4 % of data has high correlation with the size,hips and bra size
#working further with only 4% of data may create inconsistency in the model it is a best to drop this variable
```


```python
df['quality'].fillna(value=4,inplace=True)
# mean is about 3.96 thus, filling with 4
```


```python
df['cup size'].fillna(value='c',inplace=True)
# since cup size is the most common size occured 17500 times
```


```python
df['hips'].fillna(value=40,inplace=True)
# filling with the mean, since distribution is normal and has skewness of .96 and kurtosis of .84
```


```python
df['length'].fillna(value='just right',inplace=True)
# since 'just right' is the mode of the length variable and hence occured more than 60000 times
```


```python
df.drop(columns=['height'],axis=1,inplace=True)
# dropping height
```


```python
df['bra size'].fillna(value=36,inplace=True)
# since the distribuition is normal and has skewness .90 and kurtosis 1.03 having mean 35.96, thus filling with 36
```


```python
df['review_text'].fillna(value='',inplace=True)
df['review_summary'].fillna(value='',inplace=True)
#filling with blank
```


```python
df.drop(columns=['bust'],inplace=True,axis=1)
# approx 86% of data are missing
```


```python
df.drop(columns=['shoe width'],inplace=True,axis=1)
# approx 78% of data are missing
```


```python
df.drop(columns=['shoe size'],inplace=True,axis=1)
# 66% of data are missing
```


```python
df.drop(columns=['Unnamed: 0'],inplace=True,axis=1)
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>item_id</th>
      <th>size</th>
      <th>quality</th>
      <th>cup size</th>
      <th>hips</th>
      <th>bra size</th>
      <th>category</th>
      <th>user_name</th>
      <th>length</th>
      <th>fit</th>
      <th>user_id</th>
      <th>review_summary</th>
      <th>review_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>123373</td>
      <td>7</td>
      <td>5.0</td>
      <td>d</td>
      <td>38.0</td>
      <td>34.0</td>
      <td>new</td>
      <td>Emily</td>
      <td>just right</td>
      <td>small</td>
      <td>991571</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>1</th>
      <td>123373</td>
      <td>13</td>
      <td>3.0</td>
      <td>b</td>
      <td>30.0</td>
      <td>36.0</td>
      <td>new</td>
      <td>sydneybraden2001</td>
      <td>just right</td>
      <td>small</td>
      <td>587883</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>123373</td>
      <td>7</td>
      <td>2.0</td>
      <td>b</td>
      <td>40.0</td>
      <td>32.0</td>
      <td>new</td>
      <td>Ugggh</td>
      <td>slightly long</td>
      <td>small</td>
      <td>395665</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>3</th>
      <td>123373</td>
      <td>21</td>
      <td>5.0</td>
      <td>dd/e</td>
      <td>40.0</td>
      <td>36.0</td>
      <td>new</td>
      <td>alexmeyer626</td>
      <td>just right</td>
      <td>fit</td>
      <td>875643</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>4</th>
      <td>123373</td>
      <td>18</td>
      <td>5.0</td>
      <td>b</td>
      <td>40.0</td>
      <td>36.0</td>
      <td>new</td>
      <td>dberrones1</td>
      <td>slightly long</td>
      <td>small</td>
      <td>944840</td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>item_id</th>
      <th>size</th>
      <th>quality</th>
      <th>cup size</th>
      <th>hips</th>
      <th>bra size</th>
      <th>category</th>
      <th>user_name</th>
      <th>length</th>
      <th>fit</th>
      <th>user_id</th>
      <th>review_summary</th>
      <th>review_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>82780</th>
      <td>807722</td>
      <td>12</td>
      <td>4.0</td>
      <td>ddd/f</td>
      <td>40.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>ollylollie</td>
      <td>just right</td>
      <td>fit</td>
      <td>417852</td>
      <td>stretchy, light weight, c</td>
      <td>stretchy, light weight, comfy</td>
    </tr>
    <tr>
      <th>82781</th>
      <td>807722</td>
      <td>12</td>
      <td>5.0</td>
      <td>dd/e</td>
      <td>40.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>charlotte</td>
      <td>just right</td>
      <td>small</td>
      <td>11806</td>
      <td>This looks so cute over d</td>
      <td>This looks so cute over dresses! I bought both...</td>
    </tr>
    <tr>
      <th>82782</th>
      <td>807722</td>
      <td>8</td>
      <td>3.0</td>
      <td>c</td>
      <td>37.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>Maayan</td>
      <td>just right</td>
      <td>fit</td>
      <td>972740</td>
      <td>Material was more causal</td>
      <td>Material was more causal than I expected, but ...</td>
    </tr>
    <tr>
      <th>82783</th>
      <td>807722</td>
      <td>4</td>
      <td>5.0</td>
      <td>b</td>
      <td>34.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>helenag9</td>
      <td>just right</td>
      <td>fit</td>
      <td>432480</td>
      <td>I was surprised by the ve</td>
      <td>I was surprised by the very good quality of th...</td>
    </tr>
    <tr>
      <th>82784</th>
      <td>807722</td>
      <td>4</td>
      <td>3.0</td>
      <td>a</td>
      <td>35.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>ciwheeles</td>
      <td>just right</td>
      <td>large</td>
      <td>317420</td>
      <td>It ran a little big, and</td>
      <td>It ran a little big, and I'm not crazy about t...</td>
    </tr>
    <tr>
      <th>82785</th>
      <td>807722</td>
      <td>8</td>
      <td>4.0</td>
      <td>b</td>
      <td>40.0</td>
      <td>36.0</td>
      <td>outerwear</td>
      <td>Jennifer</td>
      <td>just right</td>
      <td>fit</td>
      <td>727820</td>
      <td>Cute jacket!</td>
      <td>Cute jacket!</td>
    </tr>
    <tr>
      <th>82786</th>
      <td>807722</td>
      <td>12</td>
      <td>5.0</td>
      <td>ddd/f</td>
      <td>40.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>Kelli</td>
      <td>slightly long</td>
      <td>small</td>
      <td>197040</td>
      <td>It's a beautiful jacket.</td>
      <td>It's a beautiful jacket. I love how it's knit ...</td>
    </tr>
    <tr>
      <th>82787</th>
      <td>807722</td>
      <td>12</td>
      <td>5.0</td>
      <td>dddd/g</td>
      <td>36.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>elacount</td>
      <td>just right</td>
      <td>fit</td>
      <td>102493</td>
      <td>I love this blazer. It is</td>
      <td>I love this blazer. It is a great office piece...</td>
    </tr>
    <tr>
      <th>82788</th>
      <td>807722</td>
      <td>12</td>
      <td>4.0</td>
      <td>c</td>
      <td>40.0</td>
      <td>36.0</td>
      <td>outerwear</td>
      <td>jennaklinner</td>
      <td>just right</td>
      <td>fit</td>
      <td>756491</td>
      <td>I love this blazer!! I wo</td>
      <td>I love this blazer!! I wore it yesterday and g...</td>
    </tr>
    <tr>
      <th>82789</th>
      <td>807722</td>
      <td>4</td>
      <td>4.0</td>
      <td>d</td>
      <td>39.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>maireadsteadman</td>
      <td>just right</td>
      <td>fit</td>
      <td>78305</td>
      <td>I love this piece. I'm re</td>
      <td>I love this piece. I'm really happy with it!</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.drop(columns=['review_summary'],inplace=True,axis=1)
# since review_summary and review_text have both the same meaning but review_text describes the product more though,
# dropping the review_summary variable
```


```python
df.tail(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>item_id</th>
      <th>size</th>
      <th>quality</th>
      <th>cup size</th>
      <th>hips</th>
      <th>bra size</th>
      <th>category</th>
      <th>user_name</th>
      <th>length</th>
      <th>fit</th>
      <th>user_id</th>
      <th>review_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>82780</th>
      <td>807722</td>
      <td>12</td>
      <td>4.0</td>
      <td>ddd/f</td>
      <td>40.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>ollylollie</td>
      <td>just right</td>
      <td>fit</td>
      <td>417852</td>
      <td>stretchy, light weight, comfy</td>
    </tr>
    <tr>
      <th>82781</th>
      <td>807722</td>
      <td>12</td>
      <td>5.0</td>
      <td>dd/e</td>
      <td>40.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>charlotte</td>
      <td>just right</td>
      <td>small</td>
      <td>11806</td>
      <td>This looks so cute over dresses! I bought both...</td>
    </tr>
    <tr>
      <th>82782</th>
      <td>807722</td>
      <td>8</td>
      <td>3.0</td>
      <td>c</td>
      <td>37.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>Maayan</td>
      <td>just right</td>
      <td>fit</td>
      <td>972740</td>
      <td>Material was more causal than I expected, but ...</td>
    </tr>
    <tr>
      <th>82783</th>
      <td>807722</td>
      <td>4</td>
      <td>5.0</td>
      <td>b</td>
      <td>34.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>helenag9</td>
      <td>just right</td>
      <td>fit</td>
      <td>432480</td>
      <td>I was surprised by the very good quality of th...</td>
    </tr>
    <tr>
      <th>82784</th>
      <td>807722</td>
      <td>4</td>
      <td>3.0</td>
      <td>a</td>
      <td>35.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>ciwheeles</td>
      <td>just right</td>
      <td>large</td>
      <td>317420</td>
      <td>It ran a little big, and I'm not crazy about t...</td>
    </tr>
    <tr>
      <th>82785</th>
      <td>807722</td>
      <td>8</td>
      <td>4.0</td>
      <td>b</td>
      <td>40.0</td>
      <td>36.0</td>
      <td>outerwear</td>
      <td>Jennifer</td>
      <td>just right</td>
      <td>fit</td>
      <td>727820</td>
      <td>Cute jacket!</td>
    </tr>
    <tr>
      <th>82786</th>
      <td>807722</td>
      <td>12</td>
      <td>5.0</td>
      <td>ddd/f</td>
      <td>40.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>Kelli</td>
      <td>slightly long</td>
      <td>small</td>
      <td>197040</td>
      <td>It's a beautiful jacket. I love how it's knit ...</td>
    </tr>
    <tr>
      <th>82787</th>
      <td>807722</td>
      <td>12</td>
      <td>5.0</td>
      <td>dddd/g</td>
      <td>36.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>elacount</td>
      <td>just right</td>
      <td>fit</td>
      <td>102493</td>
      <td>I love this blazer. It is a great office piece...</td>
    </tr>
    <tr>
      <th>82788</th>
      <td>807722</td>
      <td>12</td>
      <td>4.0</td>
      <td>c</td>
      <td>40.0</td>
      <td>36.0</td>
      <td>outerwear</td>
      <td>jennaklinner</td>
      <td>just right</td>
      <td>fit</td>
      <td>756491</td>
      <td>I love this blazer!! I wore it yesterday and g...</td>
    </tr>
    <tr>
      <th>82789</th>
      <td>807722</td>
      <td>4</td>
      <td>4.0</td>
      <td>d</td>
      <td>39.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>maireadsteadman</td>
      <td>just right</td>
      <td>fit</td>
      <td>78305</td>
      <td>I love this piece. I'm really happy with it!</td>
    </tr>
  </tbody>
</table>
</div>




```python
# user_id is unique id and we don't need the user_name variable all the mapping would took place through user_id
df.drop(columns=['user_name'],inplace=True,axis=1)
```


```python
df.tail(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>item_id</th>
      <th>size</th>
      <th>quality</th>
      <th>cup size</th>
      <th>hips</th>
      <th>bra size</th>
      <th>category</th>
      <th>length</th>
      <th>fit</th>
      <th>user_id</th>
      <th>review_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>82780</th>
      <td>807722</td>
      <td>12</td>
      <td>4.0</td>
      <td>ddd/f</td>
      <td>40.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>just right</td>
      <td>fit</td>
      <td>417852</td>
      <td>stretchy, light weight, comfy</td>
    </tr>
    <tr>
      <th>82781</th>
      <td>807722</td>
      <td>12</td>
      <td>5.0</td>
      <td>dd/e</td>
      <td>40.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>just right</td>
      <td>small</td>
      <td>11806</td>
      <td>This looks so cute over dresses! I bought both...</td>
    </tr>
    <tr>
      <th>82782</th>
      <td>807722</td>
      <td>8</td>
      <td>3.0</td>
      <td>c</td>
      <td>37.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>just right</td>
      <td>fit</td>
      <td>972740</td>
      <td>Material was more causal than I expected, but ...</td>
    </tr>
    <tr>
      <th>82783</th>
      <td>807722</td>
      <td>4</td>
      <td>5.0</td>
      <td>b</td>
      <td>34.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>just right</td>
      <td>fit</td>
      <td>432480</td>
      <td>I was surprised by the very good quality of th...</td>
    </tr>
    <tr>
      <th>82784</th>
      <td>807722</td>
      <td>4</td>
      <td>3.0</td>
      <td>a</td>
      <td>35.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>just right</td>
      <td>large</td>
      <td>317420</td>
      <td>It ran a little big, and I'm not crazy about t...</td>
    </tr>
    <tr>
      <th>82785</th>
      <td>807722</td>
      <td>8</td>
      <td>4.0</td>
      <td>b</td>
      <td>40.0</td>
      <td>36.0</td>
      <td>outerwear</td>
      <td>just right</td>
      <td>fit</td>
      <td>727820</td>
      <td>Cute jacket!</td>
    </tr>
    <tr>
      <th>82786</th>
      <td>807722</td>
      <td>12</td>
      <td>5.0</td>
      <td>ddd/f</td>
      <td>40.0</td>
      <td>34.0</td>
      <td>outerwear</td>
      <td>slightly long</td>
      <td>small</td>
      <td>197040</td>
      <td>It's a beautiful jacket. I love how it's knit ...</td>
    </tr>
    <tr>
      <th>82787</th>
      <td>807722</td>
      <td>12</td>
      <td>5.0</td>
      <td>dddd/g</td>
      <td>36.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>just right</td>
      <td>fit</td>
      <td>102493</td>
      <td>I love this blazer. It is a great office piece...</td>
    </tr>
    <tr>
      <th>82788</th>
      <td>807722</td>
      <td>12</td>
      <td>4.0</td>
      <td>c</td>
      <td>40.0</td>
      <td>36.0</td>
      <td>outerwear</td>
      <td>just right</td>
      <td>fit</td>
      <td>756491</td>
      <td>I love this blazer!! I wore it yesterday and g...</td>
    </tr>
    <tr>
      <th>82789</th>
      <td>807722</td>
      <td>4</td>
      <td>4.0</td>
      <td>d</td>
      <td>39.0</td>
      <td>32.0</td>
      <td>outerwear</td>
      <td>just right</td>
      <td>fit</td>
      <td>78305</td>
      <td>I love this piece. I'm really happy with it!</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

 # Recommendation System using K-Nearest Neighbor & Content Based

## Recommending existing user based on the best fit garments


```python
# Creating Pivot Table
```


```python
pivot_table=df.pivot_table(index='item_id',columns='user_id',values=['size','quality','category','fit']).fillna(0)
```


```python
pivot_table.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="10" halign="left">quality</th>
      <th>...</th>
      <th colspan="10" halign="left">size</th>
    </tr>
    <tr>
      <th>user_id</th>
      <th>6</th>
      <th>46</th>
      <th>55</th>
      <th>66</th>
      <th>104</th>
      <th>111</th>
      <th>117</th>
      <th>129</th>
      <th>132</th>
      <th>209</th>
      <th>...</th>
      <th>999764</th>
      <th>999812</th>
      <th>999816</th>
      <th>999839</th>
      <th>999843</th>
      <th>999864</th>
      <th>999887</th>
      <th>999888</th>
      <th>999923</th>
      <th>999972</th>
    </tr>
    <tr>
      <th>item_id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>123373</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>124024</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>124124</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>124761</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>125353</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 95916 columns</p>
</div>




```python
# csr vector
```


```python
from scipy.sparse import csr_matrix as csr_m
csr=csr_m(pivot_table.values)

```


```python
print(csr)
```

      (0, 231)	5.0
      (0, 585)	4.0
      (0, 839)	5.0
      (0, 1000)	4.0
      (0, 1290)	4.0
      (0, 1799)	3.0
      (0, 1952)	5.0
      (0, 1996)	5.0
      (0, 2762)	5.0
      (0, 3708)	4.0
      (0, 5443)	1.0
      (0, 5567)	5.0
      (0, 6094)	4.0
      (0, 6153)	5.0
      (0, 6327)	4.0
      (0, 7729)	5.0
      (0, 7755)	4.0
      (0, 9804)	4.0
      (0, 12932)	5.0
      (0, 13425)	4.0
      (0, 15820)	1.0
      (0, 19037)	2.0
      (0, 20337)	5.0
      (0, 23240)	5.0
      (0, 24540)	5.0
      :	:
      (1377, 68085)	12.0
      (1377, 68766)	4.0
      (1377, 70371)	8.0
      (1377, 70568)	12.0
      (1377, 70837)	4.0
      (1377, 70901)	12.0
      (1377, 72845)	8.0
      (1377, 74394)	8.0
      (1377, 75661)	12.0
      (1377, 76348)	12.0
      (1377, 78493)	8.0
      (1377, 82248)	4.0
      (1377, 83049)	8.0
      (1377, 83990)	8.0
      (1377, 84435)	12.0
      (1377, 85017)	12.0
      (1377, 86926)	12.0
      (1377, 89115)	4.0
      (1377, 89549)	8.0
      (1377, 89840)	12.0
      (1377, 91459)	8.0
      (1377, 92047)	4.0
      (1377, 93146)	4.0
      (1377, 94627)	8.0
      (1377, 94751)	8.0



```python
# Using unsupervised Nearest Neighbor and cosine similarity to calculate the similarity distance and using NN for
# recommendation
```


```python
from sklearn.neighbors import NearestNeighbors as nn
model=nn(metric='cosine',algorithm='brute')
model.fit(csr)

```




    NearestNeighbors(algorithm='brute', leaf_size=30, metric='cosine',
                     metric_params=None, n_jobs=None, n_neighbors=5, p=2,
                     radius=1.0)




```python
pivot_table.shape
```




    (1378, 95916)




```python
# Generating a random item_id and recommending the best recommendation to the user based on the similarity of the items.
```


```python
querry_index=np.random.choice(pivot_table.shape[0])
print(querry_index)
```

    1004



```python
distances,indices=model.kneighbors(pivot_table.iloc[querry_index,:].values.reshape(1,-1),n_neighbors=11)
```


```python
for i in range(0,len(distances.flatten())):
    if i==0:
        print('recommendation for item_id {0}:\n'.format(pivot_table.index[querry_index]))
    else:
        print('{0}: item_id {1}: with distance of {2}:'.format(i,pivot_table.index[indices.flatten()[i]],distances.flatten()[i]))
```

    recommendation for item_id 622207:
    
    1: item_id 660757: with distance of 0.884590873011383:
    2: item_id 576008: with distance of 1.0:
    3: item_id 579357: with distance of 1.0:
    4: item_id 578438: with distance of 1.0:
    5: item_id 577999: with distance of 1.0:
    6: item_id 577901: with distance of 1.0:
    7: item_id 577742: with distance of 1.0:
    8: item_id 577164: with distance of 1.0:
    9: item_id 576586: with distance of 1.0:
    10: item_id 580635: with distance of 1.0:


# Recommending New User With No Existing Record Based on The most Popular in the DataBase


```python
def new_user(item_id):
    if item_id==0 or item_id=='':
        print(most_no_of_items.head())

        
```


```python
item_id=''
new_user(item_id)
```

    item_id
    539980    2008
    668696    1555
    397005    1506
    175771    1438
    407134    1437
    Name: item_id, dtype: int64



```python

```
