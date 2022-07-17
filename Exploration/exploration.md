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


    
![png](output_6_0.png)
    



```python
hazard = [['False','True'],list(data.hazardous.value_counts())]
# Pie distribution of target variable
plt.pie(data = hazard[1],labels = hazard[0],explode=(0.1,0.1),x=hazard[1])
```




    ([<matplotlib.patches.Wedge at 0x7eff9e4b21d0>,
      <matplotlib.patches.Wedge at 0x7eff9e4b22f0>],
     [Text(-1.14435144880889, 0.3611921394618034, 'False'),
      Text(1.144351465717513, -0.3611920858908456, 'True')])




    
![png](output_7_1.png)
    



```python
sns.pairplot(data,hue='hazardous')
```




    <seaborn.axisgrid.PairGrid at 0x7eff9e51f4c0>




    
![png](output_8_1.png)
    



```python

```
