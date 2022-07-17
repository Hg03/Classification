```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

|Columns|Description|
|--------|----------|
|id|Unique identifier for each Asteroid|
|name|Name given by NASA|
|est_diameter_min|Minimum estimated diameter in kms.|
|est_diameter_max|Maximum estimated diameter in kms.|
|relative_velocity|Velocity relative to earth|
|miss_distance|Distance in kms. missed|
|orbiting_body|Planet that the asteroid orbits|
|sentry_object|Included in sentry - an automated collision monitoring system|
|absolute_magnitude|Describes intrinsic luminousity|
|hazardous|Boolean feature that shows whether asteroid is harmful or not|



```python
df = pd.read_csv('Dataset/train.csv')   # id(every row has unique value),name(every row has unique value),orbiting_body(every row has value "Earth"),sentry_object(every row has value "False") has no significance

no_sig = ['id','name','orbiting_body','sentry_object'] # Columns that has no signicance
sig_cols = [col for col in df.columns if col not in no_sig] # filtering out significant columns
        
data = df[sig_cols] # data with significant columns
```


```python
feature = data.drop('hazardous',axis = 1)
target = data.hazardous
```


```python
data.head()
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
      <th>est_diameter_min</th>
      <th>est_diameter_max</th>
      <th>relative_velocity</th>
      <th>miss_distance</th>
      <th>absolute_magnitude</th>
      <th>hazardous</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.198271</td>
      <td>2.679415</td>
      <td>13569.249224</td>
      <td>5.483974e+07</td>
      <td>16.73</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.265800</td>
      <td>0.594347</td>
      <td>73588.726663</td>
      <td>6.143813e+07</td>
      <td>20.00</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.722030</td>
      <td>1.614507</td>
      <td>114258.692129</td>
      <td>4.979872e+07</td>
      <td>17.83</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.096506</td>
      <td>0.215794</td>
      <td>24764.303138</td>
      <td>2.543497e+07</td>
      <td>22.20</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.255009</td>
      <td>0.570217</td>
      <td>42737.733765</td>
      <td>4.627557e+07</td>
      <td>20.09</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
#data.isnull.sum()  # --> 0 this dataset has no null values, but still handle missing values for dynamic purpose.
```


```python
# Histogram of features
plt.figure(figsize=(15,20))
plt.suptitle('Hist plots')
j=1
for i in feature.columns:
    plt.subplot(5,1,j)
    sns.histplot(data=feature,x=i,bins = 40,kde=True)
    j+=1
```


    
![png](https://github.com/Hg03/HazardousPredition/blob/main/Images/output_6_0.png)
    



```python
hazard = [['False','True'],list(data.hazardous.value_counts())]
# Pie distribution of target variable
plt.pie(data = hazard[1],labels = hazard[0],explode=(0.1,0.1),x=hazard[1])
```




    ([<matplotlib.patches.Wedge at 0x7eff9e4b21d0>,
      <matplotlib.patches.Wedge at 0x7eff9e4b22f0>],
     [Text(-1.14435144880889, 0.3611921394618034, 'False'),
      Text(1.144351465717513, -0.3611920858908456, 'True')])




    
![png](https://github.com/Hg03/HazardousPredition/blob/main/Images/output_7_1.png)
    



```python
sns.pairplot(data,hue='hazardous')
```




    <seaborn.axisgrid.PairGrid at 0x7eff9e51f4c0>




    
![png](https://github.com/Hg03/HazardousPredition/blob/main/Images/output_8_1.png)
    



```python

```
