

```python
%load_ext sql
```


```python
%sql postgresql://dsi_student:gastudents@dsi.c20gkj5cvu3l.us-east-1.rds.amazonaws.com/titanic
```




    u'Connected: dsi_student@titanic'




```python
import pandas as pd
import numpy as np
%matplotlib inline
import matplotlib.pyplot as plt
```


```python
%%sql

select * from train limit 5;
```

    5 rows affected.





<table>
    <tr>
        <th>index</th>
        <th>PassengerId</th>
        <th>Survived</th>
        <th>Pclass</th>
        <th>Name</th>
        <th>Sex</th>
        <th>Age</th>
        <th>SibSp</th>
        <th>Parch</th>
        <th>Ticket</th>
        <th>Fare</th>
        <th>Cabin</th>
        <th>Embarked</th>
    </tr>
    <tr>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>3</td>
        <td>Braund, Mr. Owen Harris</td>
        <td>male</td>
        <td>22.0</td>
        <td>1</td>
        <td>0</td>
        <td>A/5 21171</td>
        <td>7.25</td>
        <td>None</td>
        <td>S</td>
    </tr>
    <tr>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>1</td>
        <td>Cumings, Mrs. John Bradley (Florence Briggs Thayer)</td>
        <td>female</td>
        <td>38.0</td>
        <td>1</td>
        <td>0</td>
        <td>PC 17599</td>
        <td>71.2833</td>
        <td>C85</td>
        <td>C</td>
    </tr>
    <tr>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>3</td>
        <td>Heikkinen, Miss. Laina</td>
        <td>female</td>
        <td>26.0</td>
        <td>0</td>
        <td>0</td>
        <td>STON/O2. 3101282</td>
        <td>7.925</td>
        <td>None</td>
        <td>S</td>
    </tr>
    <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
        <td>female</td>
        <td>35.0</td>
        <td>1</td>
        <td>0</td>
        <td>113803</td>
        <td>53.1</td>
        <td>C123</td>
        <td>S</td>
    </tr>
    <tr>
        <td>4</td>
        <td>5</td>
        <td>0</td>
        <td>3</td>
        <td>Allen, Mr. William Henry</td>
        <td>male</td>
        <td>35.0</td>
        <td>0</td>
        <td>0</td>
        <td>373450</td>
        <td>8.05</td>
        <td>None</td>
        <td>S</td>
    </tr>
</table>




```python
titanic_train = %%sql select * from train;
titanic_df = titanic_train.DataFrame()
```

    891 rows affected.



```python
titanic_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>None</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>None</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>None</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
# titanic_df[0:50]
titanic_df[titanic_df['Cabin'] == 'G6']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>11</td>
      <td>1</td>
      <td>3</td>
      <td>Sandstrom, Miss. Marguerite Rut</td>
      <td>female</td>
      <td>4.0</td>
      <td>1</td>
      <td>1</td>
      <td>PP 9549</td>
      <td>16.7000</td>
      <td>G6</td>
      <td>S</td>
    </tr>
    <tr>
      <th>205</th>
      <td>205</td>
      <td>206</td>
      <td>0</td>
      <td>3</td>
      <td>Strom, Miss. Telma Matilda</td>
      <td>female</td>
      <td>2.0</td>
      <td>0</td>
      <td>1</td>
      <td>347054</td>
      <td>10.4625</td>
      <td>G6</td>
      <td>S</td>
    </tr>
    <tr>
      <th>251</th>
      <td>251</td>
      <td>252</td>
      <td>0</td>
      <td>3</td>
      <td>Strom, Mrs. Wilhelm (Elna Matilda Persson)</td>
      <td>female</td>
      <td>29.0</td>
      <td>1</td>
      <td>1</td>
      <td>347054</td>
      <td>10.4625</td>
      <td>G6</td>
      <td>S</td>
    </tr>
    <tr>
      <th>394</th>
      <td>394</td>
      <td>395</td>
      <td>1</td>
      <td>3</td>
      <td>Sandstrom, Mrs. Hjalmar (Agnes Charlotta Bengt...</td>
      <td>female</td>
      <td>24.0</td>
      <td>0</td>
      <td>2</td>
      <td>PP 9549</td>
      <td>16.7000</td>
      <td>G6</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic_df[titanic_df['Ticket'] == 'PP 9549']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>11</td>
      <td>1</td>
      <td>3</td>
      <td>Sandstrom, Miss. Marguerite Rut</td>
      <td>female</td>
      <td>4.0</td>
      <td>1</td>
      <td>1</td>
      <td>PP 9549</td>
      <td>16.7</td>
      <td>G6</td>
      <td>S</td>
    </tr>
    <tr>
      <th>394</th>
      <td>394</td>
      <td>395</td>
      <td>1</td>
      <td>3</td>
      <td>Sandstrom, Mrs. Hjalmar (Agnes Charlotta Bengt...</td>
      <td>female</td>
      <td>24.0</td>
      <td>0</td>
      <td>2</td>
      <td>PP 9549</td>
      <td>16.7</td>
      <td>G6</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
#titanic_df[titanic_df['Cabin'] == re.compile]
titanic_df[titanic_df['Name'].str.contains("Sandstrom")]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>11</td>
      <td>1</td>
      <td>3</td>
      <td>Sandstrom, Miss. Marguerite Rut</td>
      <td>female</td>
      <td>4.0</td>
      <td>1</td>
      <td>1</td>
      <td>PP 9549</td>
      <td>16.7</td>
      <td>G6</td>
      <td>S</td>
    </tr>
    <tr>
      <th>394</th>
      <td>394</td>
      <td>395</td>
      <td>1</td>
      <td>3</td>
      <td>Sandstrom, Mrs. Hjalmar (Agnes Charlotta Bengt...</td>
      <td>female</td>
      <td>24.0</td>
      <td>0</td>
      <td>2</td>
      <td>PP 9549</td>
      <td>16.7</td>
      <td>G6</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic_df['Name'][394]
```




    u'Sandstrom, Mrs. Hjalmar (Agnes Charlotta Bengtsson)'




```python
test = pd.read_csv('test.csv')
```


```python
test.shape
```




    (418, 11)




```python
test[test['Name'].str.contains("Sandstrom")]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PassengerId</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>117</th>
      <td>1009</td>
      <td>3</td>
      <td>Sandstrom, Miss. Beatrice Irene</td>
      <td>female</td>
      <td>1.0</td>
      <td>1</td>
      <td>1</td>
      <td>PP 9549</td>
      <td>16.7</td>
      <td>G6</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
dropped = ['index', 'PassengerId']
df = titanic_df.drop(dropped, 1)
```


```python
df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>None</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>None</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>None</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



### Check for null values


```python
df.Age.isnull().value_counts()
```




    False    714
    True     177
    Name: Age, dtype: int64




```python
# will need to find a way to impute age, else will use median
```


```python
df.Embarked.isnull().value_counts()
```




    False    889
    True       2
    Name: Embarked, dtype: int64




```python
# since only two embarked values are missing will fill with majority class
```


```python
df.Embarked.value_counts()
```




    S    644
    C    168
    Q     77
    Name: Embarked, dtype: int64




```python
# Check two missing embarked indexes
df[df.Embarked.isnull() == True]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>61</th>
      <td>1</td>
      <td>1</td>
      <td>Icard, Miss. Amelie</td>
      <td>female</td>
      <td>38.0</td>
      <td>0</td>
      <td>0</td>
      <td>113572</td>
      <td>80.0</td>
      <td>B28</td>
      <td>None</td>
    </tr>
    <tr>
      <th>829</th>
      <td>1</td>
      <td>1</td>
      <td>Stone, Mrs. George Nelson (Martha Evelyn)</td>
      <td>female</td>
      <td>62.0</td>
      <td>0</td>
      <td>0</td>
      <td>113572</td>
      <td>80.0</td>
      <td>B28</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Let's see if the ticket numbers can give us a clue, 
# Search for similar ticket numbers with fuzzy wuzzy
from fuzzywuzzy import fuzz
from fuzzywuzzy import process
```


```python
query = '113572'
choices = df.Ticket

process.extract(query, choices)
```




    [(u'113572', 100),
     (u'113572', 100),
     (u'113792', 83),
     (u'5727', 77),
     (u'11752', 73)]




```python
df[df['Ticket'] == '113792']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>467</th>
      <td>0</td>
      <td>1</td>
      <td>Smart, Mr. John Montgomery</td>
      <td>male</td>
      <td>56.0</td>
      <td>0</td>
      <td>0</td>
      <td>113792</td>
      <td>26.55</td>
      <td>None</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df[df['Ticket'].str.contains('113')]
```


```python
df['Embarked'] = df['Embarked'].fillna('S')
```


```python
df['Embarked'].isnull().value_counts()
```




    False    891
    Name: Embarked, dtype: int64




```python

```


```python
# Check for missing values in Cabin
df.Cabin.isnull().value_counts()
```




    True     687
    False    204
    Name: Cabin, dtype: int64




```python
# We will not really be able to impute Missing cabins and some passengeres were not assigned a cabin 
# so will replace with value for missing
```

## Feature engineering


```python
# Create a family size feature
df['Fsize'] = df['SibSp'] + df['Parch'] + 1
```


```python
# Pull Titles from Name
import re
def titles(string):
    titles = re.search(' ([A-Za-z]+)\.', string)
    # If the title exists, extract and return it.
    if titles:
        return titles.group(1)
    return ""
# Create a new feature Title, containing the titles of passenger names
df['title'] = df['Name'].apply(titles)
```


```python
df.title.value_counts()
```




    Mr          517
    Miss        182
    Mrs         125
    Master       40
    Dr            7
    Rev           6
    Col           2
    Major         2
    Mlle          2
    Countess      1
    Ms            1
    Lady          1
    Jonkheer      1
    Don           1
    Mme           1
    Capt          1
    Sir           1
    Name: title, dtype: int64




```python
df['title'][df['title'] == 'Mlle'] = 'Miss'
```

    /anaconda/lib/python2.7/site-packages/ipykernel/__main__.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      if __name__ == '__main__':



```python
df['title'][df['title'] == 'Countess'] = 'Lady'
```

    /anaconda/lib/python2.7/site-packages/ipykernel/__main__.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      if __name__ == '__main__':



```python
df['title'][df['title'] == 'Mme'] = 'Ms'
```

    /anaconda/lib/python2.7/site-packages/ipykernel/__main__.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      if __name__ == '__main__':



```python
male_hon = ['Major', 'Col','Jonkheer','Don','Capt']
for i in male_hon:
    df['title'][df['title'] == i] = 'MHon'
```

    /anaconda/lib/python2.7/site-packages/ipykernel/__main__.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      app.launch_new_instance()



```python
df[df['title'] == 'Dr']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Fsize</th>
      <th>title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>245</th>
      <td>0</td>
      <td>1</td>
      <td>Minahan, Dr. William Edward</td>
      <td>male</td>
      <td>44.0</td>
      <td>2</td>
      <td>0</td>
      <td>19928</td>
      <td>90.0000</td>
      <td>C78</td>
      <td>Q</td>
      <td>3</td>
      <td>Dr</td>
    </tr>
    <tr>
      <th>317</th>
      <td>0</td>
      <td>2</td>
      <td>Moraweck, Dr. Ernest</td>
      <td>male</td>
      <td>54.0</td>
      <td>0</td>
      <td>0</td>
      <td>29011</td>
      <td>14.0000</td>
      <td>None</td>
      <td>S</td>
      <td>1</td>
      <td>Dr</td>
    </tr>
    <tr>
      <th>398</th>
      <td>0</td>
      <td>2</td>
      <td>Pain, Dr. Alfred</td>
      <td>male</td>
      <td>23.0</td>
      <td>0</td>
      <td>0</td>
      <td>244278</td>
      <td>10.5000</td>
      <td>None</td>
      <td>S</td>
      <td>1</td>
      <td>Dr</td>
    </tr>
    <tr>
      <th>632</th>
      <td>1</td>
      <td>1</td>
      <td>Stahelin-Maeglin, Dr. Max</td>
      <td>male</td>
      <td>32.0</td>
      <td>0</td>
      <td>0</td>
      <td>13214</td>
      <td>30.5000</td>
      <td>B50</td>
      <td>C</td>
      <td>1</td>
      <td>Dr</td>
    </tr>
    <tr>
      <th>660</th>
      <td>1</td>
      <td>1</td>
      <td>Frauenthal, Dr. Henry William</td>
      <td>male</td>
      <td>50.0</td>
      <td>2</td>
      <td>0</td>
      <td>PC 17611</td>
      <td>133.6500</td>
      <td>None</td>
      <td>S</td>
      <td>3</td>
      <td>Dr</td>
    </tr>
    <tr>
      <th>766</th>
      <td>0</td>
      <td>1</td>
      <td>Brewe, Dr. Arthur Jackson</td>
      <td>male</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>112379</td>
      <td>39.6000</td>
      <td>None</td>
      <td>C</td>
      <td>1</td>
      <td>Dr</td>
    </tr>
    <tr>
      <th>796</th>
      <td>1</td>
      <td>1</td>
      <td>Leader, Dr. Alice (Farnham)</td>
      <td>female</td>
      <td>49.0</td>
      <td>0</td>
      <td>0</td>
      <td>17465</td>
      <td>25.9292</td>
      <td>D17</td>
      <td>S</td>
      <td>1</td>
      <td>Dr</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.title.value_counts()
```




    Mr        517
    Miss      184
    Mrs       125
    Master     40
    MHon        7
    Dr          7
    Rev         6
    Ms          2
    Lady        2
    Sir         1
    Name: title, dtype: int64




```python
# Fill missing cabin values with 'X'
df['Cabin'] = df['Cabin'].fillna('X')
```


```python
# Create a feature for Deck
# Pull deck from Cabin
def deck(string):
    decks = re.search('[A-Za-z]', string)
    # If the deck exists, extract and return it.
    if decks:
        return decks.group(0)
    return ""
# Create a new feature deck
df['deck'] = df['Cabin'].apply(deck)
```


```python
df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Fsize</th>
      <th>title</th>
      <th>deck</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>X</td>
      <td>S</td>
      <td>2</td>
      <td>Mr</td>
      <td>X</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
      <td>2</td>
      <td>Mrs</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>X</td>
      <td>S</td>
      <td>1</td>
      <td>Miss</td>
      <td>X</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
      <td>2</td>
      <td>Mrs</td>
      <td>C</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>X</td>
      <td>S</td>
      <td>1</td>
      <td>Mr</td>
      <td>X</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['deck'][df['Pclass'] == 2].value_counts()
```




    X    168
    F      8
    D      4
    E      4
    Name: deck, dtype: int64




```python
# Surname feature, will try using this feature in decision tree models
names = df['Name'].str.split(',')
surnames = []
for i in names:
    surnames.append(i[0])
df['surname'] = surnames
```


```python
df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Fsize</th>
      <th>title</th>
      <th>deck</th>
      <th>surname</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>X</td>
      <td>S</td>
      <td>2</td>
      <td>Mr</td>
      <td>X</td>
      <td>Braund</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
      <td>2</td>
      <td>Mrs</td>
      <td>C</td>
      <td>Cumings</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>X</td>
      <td>S</td>
      <td>1</td>
      <td>Miss</td>
      <td>X</td>
      <td>Heikkinen</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
      <td>2</td>
      <td>Mrs</td>
      <td>C</td>
      <td>Futrelle</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>X</td>
      <td>S</td>
      <td>1</td>
      <td>Mr</td>
      <td>X</td>
      <td>Allen</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[["Sex", "Survived"]].groupby(['Sex'], as_index=False).mean()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Sex</th>
      <th>Survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>female</td>
      <td>0.742038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>male</td>
      <td>0.188908</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[["Fsize", "Survived"]].groupby(['Fsize'], as_index=False).mean()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Fsize</th>
      <th>Survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.303538</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.552795</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.578431</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.724138</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.200000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>0.136364</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>11</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[df['Fsize'] == 11]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Fsize</th>
      <th>title</th>
      <th>deck</th>
      <th>surname</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>159</th>
      <td>0</td>
      <td>3</td>
      <td>Sage, Master. Thomas Henry</td>
      <td>male</td>
      <td>NaN</td>
      <td>8</td>
      <td>2</td>
      <td>CA. 2343</td>
      <td>69.55</td>
      <td>X</td>
      <td>S</td>
      <td>11</td>
      <td>Master</td>
      <td>X</td>
      <td>Sage</td>
    </tr>
    <tr>
      <th>180</th>
      <td>0</td>
      <td>3</td>
      <td>Sage, Miss. Constance Gladys</td>
      <td>female</td>
      <td>NaN</td>
      <td>8</td>
      <td>2</td>
      <td>CA. 2343</td>
      <td>69.55</td>
      <td>X</td>
      <td>S</td>
      <td>11</td>
      <td>Miss</td>
      <td>X</td>
      <td>Sage</td>
    </tr>
    <tr>
      <th>201</th>
      <td>0</td>
      <td>3</td>
      <td>Sage, Mr. Frederick</td>
      <td>male</td>
      <td>NaN</td>
      <td>8</td>
      <td>2</td>
      <td>CA. 2343</td>
      <td>69.55</td>
      <td>X</td>
      <td>S</td>
      <td>11</td>
      <td>Mr</td>
      <td>X</td>
      <td>Sage</td>
    </tr>
    <tr>
      <th>324</th>
      <td>0</td>
      <td>3</td>
      <td>Sage, Mr. George John Jr</td>
      <td>male</td>
      <td>NaN</td>
      <td>8</td>
      <td>2</td>
      <td>CA. 2343</td>
      <td>69.55</td>
      <td>X</td>
      <td>S</td>
      <td>11</td>
      <td>Mr</td>
      <td>X</td>
      <td>Sage</td>
    </tr>
    <tr>
      <th>792</th>
      <td>0</td>
      <td>3</td>
      <td>Sage, Miss. Stella Anna</td>
      <td>female</td>
      <td>NaN</td>
      <td>8</td>
      <td>2</td>
      <td>CA. 2343</td>
      <td>69.55</td>
      <td>X</td>
      <td>S</td>
      <td>11</td>
      <td>Miss</td>
      <td>X</td>
      <td>Sage</td>
    </tr>
    <tr>
      <th>846</th>
      <td>0</td>
      <td>3</td>
      <td>Sage, Mr. Douglas Bullen</td>
      <td>male</td>
      <td>NaN</td>
      <td>8</td>
      <td>2</td>
      <td>CA. 2343</td>
      <td>69.55</td>
      <td>X</td>
      <td>S</td>
      <td>11</td>
      <td>Mr</td>
      <td>X</td>
      <td>Sage</td>
    </tr>
    <tr>
      <th>863</th>
      <td>0</td>
      <td>3</td>
      <td>Sage, Miss. Dorothy Edith "Dolly"</td>
      <td>female</td>
      <td>NaN</td>
      <td>8</td>
      <td>2</td>
      <td>CA. 2343</td>
      <td>69.55</td>
      <td>X</td>
      <td>S</td>
      <td>11</td>
      <td>Miss</td>
      <td>X</td>
      <td>Sage</td>
    </tr>
  </tbody>
</table>
</div>




```python
test[test['Name'].str.contains('Sage')]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PassengerId</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>188</th>
      <td>1080</td>
      <td>3</td>
      <td>Sage, Miss. Ada</td>
      <td>female</td>
      <td>NaN</td>
      <td>8</td>
      <td>2</td>
      <td>CA. 2343</td>
      <td>69.55</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>342</th>
      <td>1234</td>
      <td>3</td>
      <td>Sage, Mr. John George</td>
      <td>male</td>
      <td>NaN</td>
      <td>1</td>
      <td>9</td>
      <td>CA. 2343</td>
      <td>69.55</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>360</th>
      <td>1252</td>
      <td>3</td>
      <td>Sage, Master. William Henry</td>
      <td>male</td>
      <td>14.5</td>
      <td>8</td>
      <td>2</td>
      <td>CA. 2343</td>
      <td>69.55</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>365</th>
      <td>1257</td>
      <td>3</td>
      <td>Sage, Mrs. John (Annie Bullen)</td>
      <td>female</td>
      <td>NaN</td>
      <td>1</td>
      <td>9</td>
      <td>CA. 2343</td>
      <td>69.55</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
# It appears the fare column may be fare per ticket and not per passenger
# Will try and address that later if time permits
```


```python
df[["Parch", "Survived"]].groupby(['Parch'], as_index=False).mean()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Parch</th>
      <th>Survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0.343658</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0.550847</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>0.600000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>0.200000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[["Pclass", "Survived"]].groupby(['Pclass'], as_index=False).mean()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Pclass</th>
      <th>Survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.629630</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.472826</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.242363</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[["Fsize", "Survived"]].groupby(['Fsize'], as_index=False).mean()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Fsize</th>
      <th>Survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.303538</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.552795</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.578431</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.724138</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.200000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>0.136364</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>11</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[df['Ticket'] == 'F.C.C. 13529']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Fsize</th>
      <th>title</th>
      <th>deck</th>
      <th>surname</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>314</th>
      <td>0</td>
      <td>2</td>
      <td>Hart, Mr. Benjamin</td>
      <td>male</td>
      <td>43.0</td>
      <td>1</td>
      <td>1</td>
      <td>F.C.C. 13529</td>
      <td>26.25</td>
      <td>X</td>
      <td>S</td>
      <td>3</td>
      <td>Mr</td>
      <td>X</td>
      <td>Hart</td>
    </tr>
    <tr>
      <th>440</th>
      <td>1</td>
      <td>2</td>
      <td>Hart, Mrs. Benjamin (Esther Ada Bloomfield)</td>
      <td>female</td>
      <td>45.0</td>
      <td>1</td>
      <td>1</td>
      <td>F.C.C. 13529</td>
      <td>26.25</td>
      <td>X</td>
      <td>S</td>
      <td>3</td>
      <td>Mrs</td>
      <td>X</td>
      <td>Hart</td>
    </tr>
    <tr>
      <th>535</th>
      <td>1</td>
      <td>2</td>
      <td>Hart, Miss. Eva Miriam</td>
      <td>female</td>
      <td>7.0</td>
      <td>0</td>
      <td>2</td>
      <td>F.C.C. 13529</td>
      <td>26.25</td>
      <td>X</td>
      <td>S</td>
      <td>3</td>
      <td>Miss</td>
      <td>X</td>
      <td>Hart</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Impute missing ages
```


```python
pd.pivot_table(df[df['Age'].isnull() == True], index=['Pclass', 'title'], values=['Age'])
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Age</th>
    </tr>
    <tr>
      <th>Pclass</th>
      <th>title</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">1</th>
      <th>Dr</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Miss</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Mr</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Mrs</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2</th>
      <th>Miss</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Mr</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">3</th>
      <th>Master</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Miss</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Mr</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Mrs</th>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Fill missings ages with median for title and pclass
df['Age'].fillna(df.groupby(["title", "Pclass"])["Age"].transform("median"), inplace=True)
```


```python
df['Age'].isnull().value_counts()
```




    False    891
    Name: Age, dtype: int64




```python
df['Age'][df['title'] == 'Dr'][df['Pclass'] == 1]
```




    245    44.0
    632    32.0
    660    50.0
    766    46.5
    796    49.0
    Name: Age, dtype: float64




```python
df['Age'][df['title'] == 'Dr'][df['Pclass'] == 1].median()
```




    46.5



### Lets plot some of our features and Determine how to treat them


```python
import seaborn as sns
```


```python
# Create a list of quantitative data columns
quant = [f for f in df.columns if df.dtypes[f] != 'object']
quant
```




    [u'Survived', u'Pclass', u'Age', u'SibSp', u'Parch', u'Fare', 'Fsize']




```python
hists = ['Age', 'Fare']
```


```python
# Plot Histograms of numerical data columns
sns.set(rc={"figure.figsize": (8, 4)})
for i in hists:
    sns.distplot(df[i])
    plt.xlabel(i)
    plt.ylabel('Count')
    plt.show()
```


![png](output_66_0.png)



![png](output_66_1.png)



```python
df[df['Fare'] > 500]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Fsize</th>
      <th>title</th>
      <th>deck</th>
      <th>surname</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>258</th>
      <td>1</td>
      <td>1</td>
      <td>Ward, Miss. Anna</td>
      <td>female</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>PC 17755</td>
      <td>512.3292</td>
      <td>X</td>
      <td>C</td>
      <td>1</td>
      <td>Miss</td>
      <td>X</td>
      <td>Ward</td>
    </tr>
    <tr>
      <th>679</th>
      <td>1</td>
      <td>1</td>
      <td>Cardeza, Mr. Thomas Drake Martinez</td>
      <td>male</td>
      <td>36.0</td>
      <td>0</td>
      <td>1</td>
      <td>PC 17755</td>
      <td>512.3292</td>
      <td>B51 B53 B55</td>
      <td>C</td>
      <td>2</td>
      <td>Mr</td>
      <td>B</td>
      <td>Cardeza</td>
    </tr>
    <tr>
      <th>737</th>
      <td>1</td>
      <td>1</td>
      <td>Lesurer, Mr. Gustave J</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>PC 17755</td>
      <td>512.3292</td>
      <td>B101</td>
      <td>C</td>
      <td>1</td>
      <td>Mr</td>
      <td>B</td>
      <td>Lesurer</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize=(8,8))
plt.title('Correlation of Features', y=1.05, size=15)
sns.heatmap(df.corr(),linewidths=0.1,vmax=1.0, square=True, linecolor='white', annot=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1130a55d0>




![png](output_68_1.png)



```python
g = sns.pairplot(df[['Survived', 'Pclass', 'Sex', 'Age', 'SibSp','Parch', 'Fare', 'Embarked', 'Fsize', 'title']], \
                 hue='Survived',size=1,diag_kind = 'kde',diag_kws=dict(shade=True),plot_kws=dict(s=10))
g.set(xticklabels=[])
```




    <seaborn.axisgrid.PairGrid at 0x10f838490>




![png](output_69_1.png)



```python
# Standardize Age
```


```python
from sklearn.preprocessing import StandardScaler

std_scale = StandardScaler()
age_df_std = std_scale.fit_transform(df[['Age']])
```


```python
fig, ax = plt.subplots(1,2, figsize=(15,6))
sns.distplot(df['Age'], ax=ax[0], kde=False, color="steelblue", bins=30)
sns.distplot(age_df_std, ax=ax[1], kde=False, color="seagreen", bins=30)
ax[1].set_xlabel('Sklearn');
```


![png](output_72_0.png)



```python
# Standardize Fare
std_scale = StandardScaler()
fare_df_std = std_scale.fit_transform(df[['Fare']])
```


```python
fig, ax = plt.subplots(1,2, figsize=(15,6))
sns.distplot(df['Fare'], ax=ax[0], kde=False, color="steelblue", bins=30)
sns.distplot(fare_df_std, ax=ax[1], kde=False, color="seagreen", bins=30)
ax[1].set_xlabel('Sklearn');
```


![png](output_74_0.png)



```python
df_lr = df.copy()
```


```python
df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Fsize</th>
      <th>title</th>
      <th>deck</th>
      <th>surname</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>X</td>
      <td>S</td>
      <td>2</td>
      <td>Mr</td>
      <td>X</td>
      <td>Braund</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
      <td>2</td>
      <td>Mrs</td>
      <td>C</td>
      <td>Cumings</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>X</td>
      <td>S</td>
      <td>1</td>
      <td>Miss</td>
      <td>X</td>
      <td>Heikkinen</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
      <td>2</td>
      <td>Mrs</td>
      <td>C</td>
      <td>Futrelle</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>X</td>
      <td>S</td>
      <td>1</td>
      <td>Mr</td>
      <td>X</td>
      <td>Allen</td>
    </tr>
  </tbody>
</table>
</div>




```python
lr_drop = ['Name', 'Ticket', 'Cabin', 'surname']
```


```python
df_lr.drop(lr_drop, axis=1, inplace=True)
df_lr.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Fare</th>
      <th>Embarked</th>
      <th>Fsize</th>
      <th>title</th>
      <th>deck</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>S</td>
      <td>2</td>
      <td>Mr</td>
      <td>X</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>C</td>
      <td>2</td>
      <td>Mrs</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>S</td>
      <td>1</td>
      <td>Miss</td>
      <td>X</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>S</td>
      <td>2</td>
      <td>Mrs</td>
      <td>C</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>1</td>
      <td>Mr</td>
      <td>X</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_lr['Sex'] = df_lr['Sex'].apply(lambda x: 1 if x == 'male' else 0)
```


```python
df_lr['Survived'][df_lr['Survived'] == 0].count()*1.0/(df_lr['Survived'][df_lr['Survived'] == 0].count()+\
                                                   df_lr['Survived'][df_lr['Survived'] == 1].count())*1.0
```




    0.61616161616161613




```python
df_lr = pd.get_dummies(df_lr)
df_lr.columns
```




    Index([    u'Survived',       u'Pclass',          u'Sex',          u'Age',
                  u'SibSp',        u'Parch',         u'Fare',        u'Fsize',
             u'Embarked_C',   u'Embarked_Q',   u'Embarked_S',     u'title_Dr',
             u'title_Lady',   u'title_MHon', u'title_Master',   u'title_Miss',
               u'title_Mr',    u'title_Mrs',     u'title_Ms',    u'title_Rev',
              u'title_Sir',       u'deck_A',       u'deck_B',       u'deck_C',
                 u'deck_D',       u'deck_E',       u'deck_F',       u'deck_G',
                 u'deck_T',       u'deck_X'],
          dtype='object')




```python
df_lr.drop(['Embarked_C','title_Mr','deck_X'], axis=1, inplace=True)
df_lr.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Fare</th>
      <th>Fsize</th>
      <th>Embarked_Q</th>
      <th>Embarked_S</th>
      <th>...</th>
      <th>title_Rev</th>
      <th>title_Sir</th>
      <th>deck_A</th>
      <th>deck_B</th>
      <th>deck_C</th>
      <th>deck_D</th>
      <th>deck_E</th>
      <th>deck_F</th>
      <th>deck_G</th>
      <th>deck_T</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>2</td>
      <td>0.0</td>
      <td>1.0</td>
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
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>2</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>1</td>
      <td>0.0</td>
      <td>1.0</td>
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
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>2</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>1</td>
      <td>0.0</td>
      <td>1.0</td>
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
<p>5 rows × 27 columns</p>
</div>




```python
df_lr = pd.concat([df_lr.drop('Pclass',axis=1),pd.get_dummies(df_lr['Pclass'], prefix='Class',drop_first=True)], axis = 1)
```


```python
df_lr = pd.concat([df_lr.drop('SibSp',axis=1),pd.get_dummies(df_lr['SibSp'], prefix='SibSp',drop_first=True)], axis = 1)
```


```python
df_lr = pd.concat([df_lr.drop('Parch',axis=1),pd.get_dummies(df_lr['Parch'], prefix='Parch',drop_first=True)], axis = 1)
```


```python
df_lr = pd.concat([df_lr.drop('Fsize',axis=1),pd.get_dummies(df_lr['Fsize'], prefix='Fsize',drop_first=True)], axis = 1)
```


```python
df_lr.shape
```




    (891, 45)




```python
df_lr['age_std'] = age_df_std
```


```python
df_lr['fare_std'] = fare_df_std
```


```python
df_lr.columns
```




    Index([    u'Survived',          u'Sex',          u'Age',         u'Fare',
             u'Embarked_Q',   u'Embarked_S',     u'title_Dr',   u'title_Lady',
             u'title_MHon', u'title_Master',   u'title_Miss',    u'title_Mrs',
               u'title_Ms',    u'title_Rev',    u'title_Sir',       u'deck_A',
                 u'deck_B',       u'deck_C',       u'deck_D',       u'deck_E',
                 u'deck_F',       u'deck_G',       u'deck_T',      u'Class_2',
                u'Class_3',      u'SibSp_1',      u'SibSp_2',      u'SibSp_3',
                u'SibSp_4',      u'SibSp_5',      u'SibSp_8',      u'Parch_1',
                u'Parch_2',      u'Parch_3',      u'Parch_4',      u'Parch_5',
                u'Parch_6',      u'Fsize_2',      u'Fsize_3',      u'Fsize_4',
                u'Fsize_5',      u'Fsize_6',      u'Fsize_7',      u'Fsize_8',
               u'Fsize_11',      u'age_std',     u'fare_std'],
          dtype='object')




```python
df_lr.drop(['Age','Fare'], axis=1, inplace=True)
```


```python
corr = df_lr.corr(method='pearson', min_periods=1).iloc[:,0]
```


```python
corr = corr[np.argsort(corr, axis=0)[::-1]]
corr = pd.DataFrame(corr)
```


```python
plt.figure(figsize=(6, 0.25*len(corr)))
sns.barplot(data=corr, y=corr.index, x=corr['Survived'], orient='h')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11a133690>




![png](output_94_1.png)



```python
X_lr = df_lr.iloc[:,1:]
y_lr = df_lr['Survived']
```


```python
X_lr.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Sex</th>
      <th>Embarked_Q</th>
      <th>Embarked_S</th>
      <th>title_Dr</th>
      <th>title_Lady</th>
      <th>title_MHon</th>
      <th>title_Master</th>
      <th>title_Miss</th>
      <th>title_Mrs</th>
      <th>title_Ms</th>
      <th>...</th>
      <th>Fsize_2</th>
      <th>Fsize_3</th>
      <th>Fsize_4</th>
      <th>Fsize_5</th>
      <th>Fsize_6</th>
      <th>Fsize_7</th>
      <th>Fsize_8</th>
      <th>Fsize_11</th>
      <th>age_std</th>
      <th>fare_std</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>-0.529702</td>
      <td>-0.502445</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.656200</td>
      <td>0.786845</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
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
      <td>-0.233226</td>
      <td>-0.488854</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.433843</td>
      <td>0.420730</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0.0</td>
      <td>1.0</td>
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
      <td>0.433843</td>
      <td>-0.486337</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 44 columns</p>
</div>




```python

```


```python
# Split training and test
from sklearn.model_selection import train_test_split, cross_val_score

Xlr_train, Xlr_test, ylr_train, ylr_test = train_test_split(X_lr, y_lr, test_size=.30, random_state=42)
```


```python
from sklearn.linear_model import LogisticRegression
```


```python
# fit model
lr = LogisticRegression()
lr_model = lr.fit(Xlr_train, ylr_train)
```


```python
# predictions
ylr_pred = lr_model.predict(Xlr_test)
```


```python
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

acc = accuracy_score(ylr_test, ylr_pred)
```


```python
acc
```




    0.82089552238805974




```python
# conf matrix
lr_cm = confusion_matrix(ylr_test, ylr_pred)
lr_cm = pd.DataFrame(lr_cm, columns=["Survived-N", "Survived-Y"], index=["Survived-N", "Survived-Y"])
lr_cm
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived-N</th>
      <th>Survived-Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Survived-N</th>
      <td>138</td>
      <td>19</td>
    </tr>
    <tr>
      <th>Survived-Y</th>
      <td>29</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




```python
from sklearn.metrics import classification_report

print(classification_report(ylr_test, ylr_pred))
```

                 precision    recall  f1-score   support
    
              0       0.83      0.88      0.85       157
              1       0.81      0.74      0.77       111
    
    avg / total       0.82      0.82      0.82       268
    


Our recall on the positive class is only 74%. Let's tune to see if we can improve and then think about adjusting the threshold so that we increase the recall on the positive class.


```python
cv_lr = cross_val_score(lr, X_lr, y_lr, cv=3)
cv_lr
```




    array([ 0.80808081,  0.82491582,  0.82154882])




```python
cv_lr.mean()
```




    0.81818181818181823




```python
lr_model.get_params()
```




    {'C': 1.0,
     'class_weight': None,
     'dual': False,
     'fit_intercept': True,
     'intercept_scaling': 1,
     'max_iter': 100,
     'multi_class': 'ovr',
     'n_jobs': 1,
     'penalty': 'l2',
     'random_state': None,
     'solver': 'liblinear',
     'tol': 0.0001,
     'verbose': 0,
     'warm_start': False}




```python
from sklearn.model_selection import GridSearchCV
```


```python
lrcv = LogisticRegression(verbose=False)
Cs = [0.0001, 0.001, 0.01, 0.1, .15, .25, .275, .33, 0.5, .66, 0.75, 1.0, 2.5, 5.0, 10.0, 100.0, 1000.0]
penalties = ['l1','l2']

gs = GridSearchCV(lrcv, {'penalty': penalties, 'C': Cs},verbose=False, cv=15)
gs.fit(Xlr_train, ylr_train)
```




    GridSearchCV(cv=15, error_score='raise',
           estimator=LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,
              intercept_scaling=1, max_iter=100, multi_class='ovr', n_jobs=1,
              penalty='l2', random_state=None, solver='liblinear', tol=0.0001,
              verbose=False, warm_start=False),
           fit_params={}, iid=True, n_jobs=1,
           param_grid={'penalty': ['l1', 'l2'], 'C': [0.0001, 0.001, 0.01, 0.1, 0.15, 0.25, 0.275, 0.33, 0.5, 0.66, 0.75, 1.0, 2.5, 5.0, 10.0, 100.0, 1000.0]},
           pre_dispatch='2*n_jobs', refit=True, return_train_score=True,
           scoring=None, verbose=False)




```python
print gs.best_params_
print gs.best_score_
```

    {'penalty': 'l2', 'C': 1.0}
    0.841091492777



```python
lr2 = LogisticRegression(penalty='l2', C=1.0)
lr2_model = lr2.fit(Xlr_train, ylr_train)
```


```python
# predictions
ylr_pred = lr2_model.predict(Xlr_test)
```


```python
acc = accuracy_score(ylr_test, ylr_pred)
acc
```




    0.82089552238805974




```python
# conf matrix
lr_cm = confusion_matrix(ylr_test, ylr_pred)
lr_cm = pd.DataFrame(lr_cm, columns=["Survived_N", "Survived_Y"], index=["Survived_N", "Survived_Y"])
lr_cm
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived_N</th>
      <th>Survived_Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Survived_N</th>
      <td>138</td>
      <td>19</td>
    </tr>
    <tr>
      <th>Survived_Y</th>
      <td>29</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




```python
# lrcv_model.predict_proba(Xlr_test)
```


```python
from sklearn.metrics import roc_curve, auc
import matplotlib.pyplot as plt
plt.style.use('seaborn-white')
%matplotlib inline

Y_score = lr2_model.decision_function(Xlr_test)

FPR = dict()
TPR = dict()
ROC_AUC = dict()

# For class 1, find the area under the curve
FPR[1], TPR[1], _ = roc_curve(ylr_test, Y_score)
ROC_AUC[1] = auc(FPR[1], TPR[1])

# Plot of a ROC curve for class 1 (has_cancer)
plt.figure(figsize=[6,5])
plt.plot(FPR[1], TPR[1], label='ROC curve (area = %0.2f)' % ROC_AUC[1], linewidth=4)
plt.plot([0, 1], [0, 1], 'k--', linewidth=4)
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate', fontsize=18)
plt.ylabel('True Positive Rate', fontsize=18)
plt.title('ROC for predicting Survival', fontsize=18)
plt.legend(loc="lower right")
plt.show()

```


![png](output_118_0.png)



```python
# Lets try to improve our recall on the positive class using the above roc to aim for about 86% recall.
lrcv3 = LogisticRegression(penalty='l2', C=1.0, class_weight={1: 0.95, 0:.30})
lrcv3_model = lrcv3.fit(Xlr_train, ylr_train)
```


```python
# predictions
ylr_pred3 = lrcv3_model.predict(Xlr_test)
```


```python
# conf matrix
lr_cm3 = confusion_matrix(ylr_test, ylr_pred3)
lr_cm3 = pd.DataFrame(lr_cm3, columns=["Survived_N", "Survived_Y"], index=["Survived_N", "Survived_Y"])
lr_cm3
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived_N</th>
      <th>Survived_Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Survived_N</th>
      <td>120</td>
      <td>37</td>
    </tr>
    <tr>
      <th>Survived_Y</th>
      <td>16</td>
      <td>95</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(classification_report(ylr_test, ylr_pred3))
```

                 precision    recall  f1-score   support
    
              0       0.88      0.76      0.82       157
              1       0.72      0.86      0.78       111
    
    avg / total       0.81      0.80      0.80       268
    


### Lets look at Knn


```python
# We will have to rescale our our age feature, we are going to leave out fare
```


```python
df_knn = df_lr.copy()
```


```python
# df_knn.head()
```


```python
# I wonder if it matters if we min max scale from standardized data.
from sklearn.preprocessing import MinMaxScaler
scaler = MinMaxScaler()
age_scaled = scaler.fit_transform(df_knn['age_std'])
df_knn['age_scaled'] = age_scaled
```

    //anaconda/lib/python2.7/site-packages/sklearn/preprocessing/data.py:321: DeprecationWarning: Passing 1d arrays as data is deprecated in 0.17 and will raise ValueError in 0.19. Reshape your data either using X.reshape(-1, 1) if your data has a single feature or X.reshape(1, -1) if it contains a single sample.
      warnings.warn(DEPRECATION_MSG_1D, DeprecationWarning)
    //anaconda/lib/python2.7/site-packages/sklearn/preprocessing/data.py:356: DeprecationWarning: Passing 1d arrays as data is deprecated in 0.17 and will raise ValueError in 0.19. Reshape your data either using X.reshape(-1, 1) if your data has a single feature or X.reshape(1, -1) if it contains a single sample.
      warnings.warn(DEPRECATION_MSG_1D, DeprecationWarning)



```python
df_knn.drop(['age_std', 'fare_std'], axis=1, inplace=True)
```


```python
df_knn.drop(['Embarked_Q', 'Embarked_S'], axis=1, inplace=True)
```


```python
df_knn.columns
```




    Index([    u'Survived',          u'Sex',     u'title_Dr',   u'title_Lady',
             u'title_MHon', u'title_Master',   u'title_Miss',    u'title_Mrs',
               u'title_Ms',    u'title_Rev',    u'title_Sir',       u'deck_A',
                 u'deck_B',       u'deck_C',       u'deck_D',       u'deck_E',
                 u'deck_F',       u'deck_G',       u'deck_T',      u'Class_2',
                u'Class_3',      u'SibSp_1',      u'SibSp_2',      u'SibSp_3',
                u'SibSp_4',      u'SibSp_5',      u'SibSp_8',      u'Parch_1',
                u'Parch_2',      u'Parch_3',      u'Parch_4',      u'Parch_5',
                u'Parch_6',      u'Fsize_2',      u'Fsize_3',      u'Fsize_4',
                u'Fsize_5',      u'Fsize_6',      u'Fsize_7',      u'Fsize_8',
               u'Fsize_11',   u'age_scaled'],
          dtype='object')




```python
df_knn.drop(['deck_A','deck_B','deck_C','deck_D','deck_E','deck_F','deck_G','deck_T'], axis=1, inplace=True)
```


```python
df_knn.drop(['SibSp_1','SibSp_2','SibSp_3','SibSp_4','SibSp_5','SibSp_8'], axis=1, inplace=True)
```


```python
df_knn.drop(['Parch_1','Parch_2','Parch_3','Parch_4','Parch_5','Parch_6'], axis=1, inplace=True)
```


```python
df_knn.drop(['title_Dr','title_Lady','title_MHon', 'title_Master','title_Miss',\
             'title_Mrs','title_Ms','title_Rev','title_Sir'], axis=1, inplace=True)
```


```python
X_knn = df_knn.iloc[:,1:]
y_knn = df_knn['Survived']
```


```python
X_knn.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Sex</th>
      <th>Class_2</th>
      <th>Class_3</th>
      <th>Fsize_2</th>
      <th>Fsize_3</th>
      <th>Fsize_4</th>
      <th>Fsize_5</th>
      <th>Fsize_6</th>
      <th>Fsize_7</th>
      <th>Fsize_8</th>
      <th>Fsize_11</th>
      <th>age_scaled</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.271174</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.472229</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.321438</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.434531</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.434531</td>
    </tr>
  </tbody>
</table>
</div>




```python
Xknn_train, Xknn_test, yknn_train, yknn_test = train_test_split(X_knn, y_knn, test_size=.30, random_state=78)
```


```python
from sklearn.neighbors import KNeighborsClassifier
knn = KNeighborsClassifier(n_neighbors=3, weights='uniform')

knn.fit(Xknn_train,yknn_train)
```




    KNeighborsClassifier(algorithm='auto', leaf_size=30, metric='minkowski',
               metric_params=None, n_jobs=1, n_neighbors=3, p=2,
               weights='uniform')




```python
# Check accuracy
knn_pred = knn.predict(Xknn_test)
accuracy_score(yknn_test, knn_pred)
```




    0.84701492537313428



:P, Reducing our features to four categories brought our accuracy from low 70's to 84.


```python
# Let's gridsearch some parameters for knn
```


```python
K = range(1,11)
wghts = ['uniform','distance']

knn = KNeighborsClassifier()

gs = GridSearchCV(knn, {'n_neighbors': K, 'weights':wghts}, cv=3)
gs.fit(X_knn, y_knn)
```




    GridSearchCV(cv=3, error_score='raise',
           estimator=KNeighborsClassifier(algorithm='auto', leaf_size=30, metric='minkowski',
               metric_params=None, n_jobs=1, n_neighbors=5, p=2,
               weights='uniform'),
           fit_params={}, iid=True, n_jobs=1,
           param_grid={'n_neighbors': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], 'weights': ['uniform', 'distance']},
           pre_dispatch='2*n_jobs', refit=True, return_train_score=True,
           scoring=None, verbose=0)




```python
print gs.best_params_
print gs.best_score_
```

    {'n_neighbors': 4, 'weights': 'uniform'}
    0.814814814815



```python

```


```python
knn = KNeighborsClassifier(n_neighbors=4, weights='uniform')

knn.fit(Xknn_train,yknn_train)
```




    KNeighborsClassifier(algorithm='auto', leaf_size=30, metric='minkowski',
               metric_params=None, n_jobs=1, n_neighbors=4, p=2,
               weights='uniform')




```python
# Check accuracy
knn_pred = knn.predict(Xknn_test)
accuracy_score(yknn_test, knn_pred)
```




    0.81343283582089554



after tuning our model with gridsearch we get a slightly lower accuracy score, possibly due to the fold size and split of the data.


```python
# conf matrix
knn_cm = confusion_matrix(yknn_test, knn_pred)
knn_cm = pd.DataFrame(knn_cm, columns=["Survived_N", "Survived_Y"], index=["Survived_N", "Survived_Y"])
knn_cm
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived_N</th>
      <th>Survived_Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Survived_N</th>
      <td>153</td>
      <td>13</td>
    </tr>
    <tr>
      <th>Survived_Y</th>
      <td>37</td>
      <td>65</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(classification_report(yknn_test, knn_pred))
```

                 precision    recall  f1-score   support
    
              0       0.81      0.92      0.86       166
              1       0.83      0.64      0.72       102
    
    avg / total       0.82      0.81      0.81       268
    



```python
Y_score = knn.predict_proba(Xknn_test)[:,1]


FPR = dict()
TPR = dict()
ROC_AUC = dict()

# For class 1, find the area under the curve
FPR[1], TPR[1], _ = roc_curve(yknn_test, Y_score)
ROC_AUC[1] = auc(FPR[1], TPR[1])

# Plot of a ROC curve for class 1 (has_cancer)
plt.figure(figsize=[6,5])
plt.plot(FPR[1], TPR[1], label='ROC curve (area = %0.2f)' % ROC_AUC[1], linewidth=4)
plt.plot([0, 1], [0, 1], 'k--', linewidth=4)
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate', fontsize=18)
plt.ylabel('True Positive Rate', fontsize=18)
plt.title('Knn - ROC for predicting Survival', fontsize=18)
plt.legend(loc="lower right")
plt.show()
```


![png](output_150_0.png)



```python
# knn does better capturing non-survivors with a 92% recall, but is worse on survivors with a recall of 64, 
# while maintaining a similar accuaracy as log reg
```


```python
# Lets try a decision tree
from sklearn.tree import DecisionTreeClassifier
```


```python
df_tree = df.copy()
```


```python
to_drop = ['Name', 'Ticket', 'Cabin', 'surname']
df_tree.drop(to_drop, axis=1, inplace=True)
df_tree.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Fare</th>
      <th>Embarked</th>
      <th>Fsize</th>
      <th>title</th>
      <th>deck</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>S</td>
      <td>2</td>
      <td>Mr</td>
      <td>X</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>C</td>
      <td>2</td>
      <td>Mrs</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>S</td>
      <td>1</td>
      <td>Miss</td>
      <td>X</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>S</td>
      <td>2</td>
      <td>Mrs</td>
      <td>C</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>1</td>
      <td>Mr</td>
      <td>X</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_tree['Sex'] = df_tree['Sex'].apply(lambda x: 1 if x == 'male' else 0)
```


```python
df_tree = pd.concat([df_tree.drop('Pclass',axis=1),pd.get_dummies(df['Pclass'], prefix='Class')], axis = 1)
df_tree = pd.concat([df_tree.drop('Fsize',axis=1),pd.get_dummies(df['Fsize'], prefix='Fsize')], axis = 1)
```


```python
ytr = df_tree['Survived']
Xtr = pd.get_dummies(df_tree.drop('Survived', axis=1))
Xtr.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Fare</th>
      <th>Class_1</th>
      <th>Class_2</th>
      <th>Class_3</th>
      <th>Fsize_1</th>
      <th>Fsize_2</th>
      <th>...</th>
      <th>title_Sir</th>
      <th>deck_A</th>
      <th>deck_B</th>
      <th>deck_C</th>
      <th>deck_D</th>
      <th>deck_E</th>
      <th>deck_F</th>
      <th>deck_G</th>
      <th>deck_T</th>
      <th>deck_X</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
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
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
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
      <td>1.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
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
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 39 columns</p>
</div>




```python
Xtr_train, Xtr_test, ytr_train, ytr_test = train_test_split(Xtr, ytr, test_size=.30, random_state=42)
```


```python
dt = DecisionTreeClassifier(max_depth = 20) 

dt.fit(Xtr_train, ytr_train)
```




    DecisionTreeClassifier(class_weight=None, criterion='gini', max_depth=20,
                max_features=None, max_leaf_nodes=None,
                min_impurity_split=1e-07, min_samples_leaf=1,
                min_samples_split=2, min_weight_fraction_leaf=0.0,
                presort=False, random_state=None, splitter='best')




```python
feature_importances = pd.DataFrame(dt.feature_importances_,
                                   index = Xtr_train.columns,
                                    columns=['importance'])
feature_importances.sort_values(by='importance', ascending=False)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>importance</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>title_Mr</th>
      <td>0.301381</td>
    </tr>
    <tr>
      <th>Fare</th>
      <td>0.265834</td>
    </tr>
    <tr>
      <th>Age</th>
      <td>0.140920</td>
    </tr>
    <tr>
      <th>Class_3</th>
      <td>0.093943</td>
    </tr>
    <tr>
      <th>title_Rev</th>
      <td>0.024041</td>
    </tr>
    <tr>
      <th>Parch</th>
      <td>0.019571</td>
    </tr>
    <tr>
      <th>deck_E</th>
      <td>0.017983</td>
    </tr>
    <tr>
      <th>Embarked_S</th>
      <td>0.015582</td>
    </tr>
    <tr>
      <th>deck_B</th>
      <td>0.015014</td>
    </tr>
    <tr>
      <th>title_Dr</th>
      <td>0.013680</td>
    </tr>
    <tr>
      <th>Embarked_C</th>
      <td>0.012709</td>
    </tr>
    <tr>
      <th>Fsize_4</th>
      <td>0.011801</td>
    </tr>
    <tr>
      <th>Fsize_5</th>
      <td>0.008725</td>
    </tr>
    <tr>
      <th>deck_X</th>
      <td>0.008162</td>
    </tr>
    <tr>
      <th>deck_C</th>
      <td>0.007443</td>
    </tr>
    <tr>
      <th>Embarked_Q</th>
      <td>0.006782</td>
    </tr>
    <tr>
      <th>Fsize_2</th>
      <td>0.006149</td>
    </tr>
    <tr>
      <th>Class_2</th>
      <td>0.005454</td>
    </tr>
    <tr>
      <th>SibSp</th>
      <td>0.004794</td>
    </tr>
    <tr>
      <th>deck_D</th>
      <td>0.004494</td>
    </tr>
    <tr>
      <th>Fsize_7</th>
      <td>0.003923</td>
    </tr>
    <tr>
      <th>deck_T</th>
      <td>0.003596</td>
    </tr>
    <tr>
      <th>Fsize_1</th>
      <td>0.003596</td>
    </tr>
    <tr>
      <th>Class_1</th>
      <td>0.002865</td>
    </tr>
    <tr>
      <th>Fsize_3</th>
      <td>0.001557</td>
    </tr>
    <tr>
      <th>title_Sir</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>deck_G</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>deck_F</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>deck_A</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>title_Mrs</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>title_Ms</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Fsize_8</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>title_Miss</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>title_Master</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>title_MHon</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>title_Lady</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Fsize_6</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Fsize_11</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Sex</th>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Check accuracy
dt_pred = dt.predict(Xtr_test)
accuracy_score(ytr_test, dt_pred)
```




    0.78358208955223885




```python
K = range(5,31)
wghts = ['balanced', None]

dt = DecisionTreeClassifier()

gs = GridSearchCV(dt, {'max_depth': K, 'class_weight':wghts}, cv=15)
gs.fit(Xtr, ytr)
```




    GridSearchCV(cv=15, error_score='raise',
           estimator=DecisionTreeClassifier(class_weight=None, criterion='gini', max_depth=None,
                max_features=None, max_leaf_nodes=None,
                min_impurity_split=1e-07, min_samples_leaf=1,
                min_samples_split=2, min_weight_fraction_leaf=0.0,
                presort=False, random_state=None, splitter='best'),
           fit_params={}, iid=True, n_jobs=1,
           param_grid={'max_depth': [5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30], 'class_weight': ['balanced', None]},
           pre_dispatch='2*n_jobs', refit=True, return_train_score=True,
           scoring=None, verbose=0)




```python
print gs.best_params_
print gs.best_score_
```

    {'max_depth': 8, 'class_weight': None}
    0.81593714927



```python
# re fit model with max depth 8
dt = DecisionTreeClassifier(max_depth = 8) 

dt.fit(Xtr_train, ytr_train)
```




    DecisionTreeClassifier(class_weight=None, criterion='gini', max_depth=8,
                max_features=None, max_leaf_nodes=None,
                min_impurity_split=1e-07, min_samples_leaf=1,
                min_samples_split=2, min_weight_fraction_leaf=0.0,
                presort=False, random_state=None, splitter='best')




```python
# Check accuracy
dt_pred = dt.predict(Xtr_test)
accuracy_score(ytr_test, dt_pred)
```




    0.81343283582089554




```python
# get a slightly better acuuracy than before gridsearch
```


```python
# conf matrix
dt_cm = confusion_matrix(ytr_test, dt_pred)
dt_cm = pd.DataFrame(dt_cm, columns=["Survived_N", "Survived_Y"], index=["Survived_N", "Survived_Y"])
dt_cm
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived_N</th>
      <th>Survived_Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Survived_N</th>
      <td>136</td>
      <td>21</td>
    </tr>
    <tr>
      <th>Survived_Y</th>
      <td>29</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




```python
# looks pretty much the same as the first logistic regression
# predicted 82 survivors correctly, but missed 29 survivors and also classified 19 non-survivors as survivors.
```


```python
print(classification_report(ytr_test, dt_pred))
```

                 precision    recall  f1-score   support
    
              0       0.82      0.87      0.84       157
              1       0.80      0.74      0.77       111
    
    avg / total       0.81      0.81      0.81       268
    



```python
# Our precision is fairly good, but our recall on class 1 - survival - is a bit lower, 
# missing 26% of of survivors (29)  
```


```python
Y_score = dt.predict_proba(Xtr_test)[:,1]


FPR = dict()
TPR = dict()
ROC_AUC = dict()

# For class 1, find the area under the curve
FPR[1], TPR[1], _ = roc_curve(ytr_test, Y_score)
ROC_AUC[1] = auc(FPR[1], TPR[1])

# Plot of a ROC curve for class 1 (has_cancer)
plt.figure(figsize=[6,5])
plt.plot(FPR[1], TPR[1], label='ROC curve (area = %0.2f)' % ROC_AUC[1], linewidth=4)
plt.plot([0, 1], [0, 1], 'k--', linewidth=4)
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate', fontsize=18)
plt.ylabel('True Positive Rate', fontsize=18)
plt.title('Decision Tree - ROC for predicting Survival', fontsize=18)
plt.legend(loc="lower right")
plt.show()
```


![png](output_171_0.png)



```python
# Lets adjust the decision threshold  
dt2 = DecisionTreeClassifier(max_depth = 8, class_weight={1: 0.1, 0:.9}) 

dt2.fit(Xtr_train, ytr_train)
```




    DecisionTreeClassifier(class_weight={0: 0.9, 1: 0.1}, criterion='gini',
                max_depth=8, max_features=None, max_leaf_nodes=None,
                min_impurity_split=1e-07, min_samples_leaf=1,
                min_samples_split=2, min_weight_fraction_leaf=0.0,
                presort=False, random_state=None, splitter='best')




```python
dt2_pred = dt2.predict(Xtr_test)
accuracy_score(ytr_test, dt2_pred)
```




    0.78358208955223885




```python
# conf matrix
dt2_cm = confusion_matrix(ytr_test, dt2_pred)
dt2_cm = pd.DataFrame(dt2_cm, columns=["P_Survived_N", "P_Survived_Y"], index=["Survived_N", "Survived_Y"])
dt2_cm
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>P_Survived_N</th>
      <th>P_Survived_Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Survived_N</th>
      <td>147</td>
      <td>10</td>
    </tr>
    <tr>
      <th>Survived_Y</th>
      <td>48</td>
      <td>63</td>
    </tr>
  </tbody>
</table>
</div>




```python
dt_cm
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived_N</th>
      <th>Survived_Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Survived_N</th>
      <td>136</td>
      <td>21</td>
    </tr>
    <tr>
      <th>Survived_Y</th>
      <td>29</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>



### We increased the weight of the non-survivor class to be able to identify more people <br> who would likely be at risk in a disastor. The recall on our 0 class is bumped up without too much sacrifice to accuracy.


```python
print(classification_report(ytr_test, dt2_pred))
```

                 precision    recall  f1-score   support
    
              0       0.75      0.94      0.84       157
              1       0.86      0.57      0.68       111
    
    avg / total       0.80      0.78      0.77       268
    



```python
Y_score = dt2.predict_proba(Xtr_test)[:,1]


FPR = dict()
TPR = dict()
ROC_AUC = dict()

# For class 1, find the area under the curve
FPR[1], TPR[1], _ = roc_curve(ytr_test, Y_score)
ROC_AUC[1] = auc(FPR[1], TPR[1])

# Plot of a ROC curve for class 1 (has_cancer)
plt.figure(figsize=[6,5])
plt.plot(FPR[1], TPR[1], label='ROC curve (area = %0.2f)' % ROC_AUC[1], linewidth=4)
plt.plot([0, 1], [0, 1], 'k--', linewidth=4)
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate', fontsize=18)
plt.ylabel('True Positive Rate', fontsize=18)
plt.title('Decision Tree (weighted) - ROC', fontsize=18)
plt.legend(loc="lower right")
plt.show()
```


![png](output_178_0.png)



```python
Y_score = dt2.predict_proba(Xtr_test)[:,1]

FPR = dict()
TPR = dict()
ROC_AUC = dict()

# For class 1, find the area under the curve
FPR[1], TPR[1], _ = roc_curve(ytr_test, Y_score)
ROC_AUC[1] = auc(FPR[1], TPR[1])

# Plot of a ROC curve for class 1 - survival
plt.subplots(figsize=(6,6));
plt.plot(FPR[1], TPR[1], label='CART ROC curve (area = %0.2f)' % ROC_AUC[1], linewidth=4)
plt.plot([0, 1], [0, 1], 'k--', linewidth=4)
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate', fontsize=18)
plt.ylabel('True Positive Rate', fontsize=18)
plt.title('Predicting Survival - ROC', fontsize=18)
plt.legend(loc="lower right")

Y_score = knn.predict_proba(Xknn_test)[:,1]

FPR = dict()
TPR = dict()
ROC_AUC = dict()

FPR[1], TPR[1], _ = roc_curve(yknn_test, Y_score)
ROC_AUC[1] = auc(FPR[1], TPR[1])

plt.plot(FPR[1], TPR[1], label='Knn ROC curve (area = %0.2f)' % ROC_AUC[1], linewidth=4)
plt.plot([0, 1], [0, 1], 'k--', linewidth=4)
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate', fontsize=18)
plt.ylabel('True Positive Rate', fontsize=18)
plt.legend(loc="lower right")

Y_score = lr2_model.decision_function(Xlr_test)

FPR = dict()
TPR = dict()
ROC_AUC = dict()

FPR[1], TPR[1], _ = roc_curve(ylr_test, Y_score)
ROC_AUC[1] = auc(FPR[1], TPR[1])

plt.plot(FPR[1], TPR[1], label='LR ROC curve (area = %0.2f)' % ROC_AUC[1], linewidth=4)
plt.plot([0, 1], [0, 1], 'k--', linewidth=4)
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate', fontsize=18)
plt.ylabel('True Positive Rate', fontsize=18)
plt.legend(loc="lower right")
plt.show()
```


![png](output_179_0.png)


Comparing our ROC curves it looks like we can get a good tradeoff with Knn at a true positive rate of about .85 and a false positive rate of about .15 


```python
# Lets try bagging

from sklearn.ensemble import BaggingClassifier
bagger = BaggingClassifier(dt2, max_samples=1.0)

print "DT Score:\t", cross_val_score(dt2, Xtr, ytr, cv=10, n_jobs=1).mean()
print "Bagging Score:\t", cross_val_score(bagger, Xtr, ytr, cv=10, n_jobs=1).mean()
```

    DT Score:	0.794676256952
    Bagging Score:	0.811594313926



```python
baggerk = BaggingClassifier(knn)

print "Knn Score:\t", cross_val_score(knn, X_knn, y_knn, cv=10, n_jobs=1).mean()
print "Bagging Score:\t", cross_val_score(baggerk, X_knn, y_knn, cv=10, n_jobs=1).mean()
```

    Knn Score:	0.814951481103
    Bagging Score:	0.810470434684



```python
bagger_lr = BaggingClassifier(lr)

print "LR Score:\t", cross_val_score(lr, X_lr, y_lr, cv=10, n_jobs=1).mean()
print "Bagging Score:\t", cross_val_score(bagger_lr, X_lr, y_lr, cv=10, n_jobs=1).mean()
```

    LR Score:	0.832780331404
    Bagging Score:	0.832780331404



```python
# Our decision tree is the only model that benefits from bagging here and only slightly. 
# It perhaps was mildly overfit, while the other two were tuned fairly well already

```

### Report

There was not much difference between each of the classifiers in this case, with just over 80% accuracy for each tuned model. Our Knn model did show a difference in the confusion matrix, having a higher recall for the non-surviving class and a lower recall on the surviving class. Knn predictions captured almost all of the non-survivors but did not capture a high amount of the surviving class.

By adjusting the class weight for a couple of models we were able to slightly increase recall on both the positive and negative class without a big decrease in accuracy. Depending on the implementation and timing one class can be weighted higher than the other to more fully identify either those at risk or those likely to survive.

Bagging only improved our decision tree model and then only slightly. 


```python

```
