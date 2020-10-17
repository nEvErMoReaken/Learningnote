
Panda与numpy的不同: `panda`是基于Dataframe数据类型的，而`numpy`是基于ndarray的


```python
import pandas as pd
```

# 1. 创建

pd.DataFrame(data=None,index=None,columns=None,dtype=None,copy=False)


```python
pd.DataFrame([[1,2,3],[3,5,7]])
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>5</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
df = pd.DataFrame([[1,2,3],[3,5,7]],columns=['a','b','c'])
```


```python
df
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
      <th>a</th>
      <th>b</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>5</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.index
```




    RangeIndex(start=0, stop=2, step=1)




```python
type(df)
```




    pandas.core.frame.DataFrame




```python
df.index.values
```




    array([0, 1], dtype=int64)




```python
df.columns.values
```




    array(['a', 'b', 'c'], dtype=object)




```python
df = pd.read_csv('SalesJan2009.csv') #导入一个某超市营业表
```

# 2. 取值 赋值


```python
df.iloc[1,:] #第一行的数据
```




    Transaction_date                   2001/2/9 4:53
    Product                                 Product1
    Price                                       1200
    Payment_Type                                Visa
    Name                                      Betina
    City                Parkville                   
    State                                         MO
    Country                            United States
    Account_Created                    2001/2/9 4:42
    Last_Login                         2001/2/9 7:49
    Latitude                                  39.195
    Longitude                               -94.6819
    Name: 1, dtype: object




```python
df.iloc[1,:]['Price'] #可以加列名 iloc=Integer Location
```




    '1200'




```python
df.loc[1:5,['Price']] #第一行的数据 注意loc 与iolc的区别
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
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1200</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3600</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1200</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[:,'Transaction_date'] #或者直接 df.Transaction_date 或df['Transaction_date']
```




    0        2001/2/9 6:17
    1        2001/2/9 4:53
    2       2001/2/9 13:08
    3       2001/3/9 14:44
    4       2001/4/9 12:56
    5       2001/4/9 13:19
    6       2001/4/9 20:11
    7       2001/2/9 20:09
    8       2001/4/9 13:17
    9       2001/4/9 14:11
    10       2001/5/9 2:42
    11       2001/5/9 5:39
    12       2001/2/9 9:16
    13      2001/5/9 10:08
    14      2001/2/9 14:18
    15       2001/4/9 1:05
    16      2001/5/9 11:37
    17       2001/6/9 5:02
    18       2001/6/9 7:45
    19       2001/2/9 7:35
    20      2001/6/9 12:56
    21      2001/1/9 11:05
    22       2001/5/9 4:10
    23       2001/6/9 7:18
    24       2001/2/9 1:11
    25       2001/1/9 2:24
    26       2001/7/9 8:08
    27       2001/2/9 2:57
    28      2001/1/9 20:21
    29       2001/8/9 0:42
                ...       
    968     2001/2/9 17:24
    969     2001/7/9 18:15
    970     2001/3/9 21:19
    971      2001/4/9 5:13
    972      2001/4/9 9:28
    973      2001/2/9 4:34
    974      1/22/09 11:10
    975     2001/7/9 12:06
    976      1/29/09 13:25
    977       1/27/09 2:57
    978     2001/7/9 13:19
    979      1/23/09 10:04
    980       1/19/09 4:55
    981      1/28/09 22:02
    982     2001/4/9 18:57
    983    2001/12/9 20:31
    984      1/24/09 12:00
    985      1/28/09 11:19
    986     2001/7/9 17:48
    987      1/23/09 12:42
    988     2001/7/9 19:48
    989      1/26/09 11:19
    990     2001/5/9 13:23
    991      1/26/09 13:41
    992      1/20/09 10:42
    993      1/22/09 14:25
    994       1/28/09 5:36
    995      2001/1/9 4:24
    996     2001/8/9 11:55
    997    2001/12/9 21:30
    Name: Transaction_date, Length: 998, dtype: object




```python
df['Price2'] =  df.Price #为表格追加一列
```


```python
df #出现了Price2一列
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
      <th>Transaction_date</th>
      <th>Product</th>
      <th>Price</th>
      <th>Payment_Type</th>
      <th>Name</th>
      <th>City</th>
      <th>State</th>
      <th>Country</th>
      <th>Account_Created</th>
      <th>Last_Login</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Price2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2001/2/9 6:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>carolina</td>
      <td>Basildon</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/2/9 6:00</td>
      <td>2001/2/9 6:08</td>
      <td>51.500000</td>
      <td>-1.116667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2001/2/9 4:53</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Betina</td>
      <td>Parkville</td>
      <td>MO</td>
      <td>United States</td>
      <td>2001/2/9 4:42</td>
      <td>2001/2/9 7:49</td>
      <td>39.195000</td>
      <td>-94.681940</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2001/2/9 13:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Federica e Andrea</td>
      <td>Astoria</td>
      <td>OR</td>
      <td>United States</td>
      <td>2001/1/9 16:21</td>
      <td>2001/3/9 12:32</td>
      <td>46.188060</td>
      <td>-123.830000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2001/3/9 14:44</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Gouya</td>
      <td>Echuca</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>9/25/05 21:13</td>
      <td>2001/3/9 14:22</td>
      <td>-36.133333</td>
      <td>144.750000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2001/4/9 12:56</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Gerd W</td>
      <td>Cahaba Heights</td>
      <td>AL</td>
      <td>United States</td>
      <td>11/15/08 15:47</td>
      <td>2001/4/9 12:45</td>
      <td>33.520560</td>
      <td>-86.802500</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2001/4/9 13:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>LAURENCE</td>
      <td>Mickleton</td>
      <td>NJ</td>
      <td>United States</td>
      <td>9/24/08 15:19</td>
      <td>2001/4/9 13:04</td>
      <td>39.790000</td>
      <td>-75.238060</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2001/4/9 20:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Fleur</td>
      <td>Peoria</td>
      <td>IL</td>
      <td>United States</td>
      <td>2001/3/9 9:38</td>
      <td>2001/4/9 19:45</td>
      <td>40.693610</td>
      <td>-89.588890</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2001/2/9 20:09</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>adam</td>
      <td>Martin</td>
      <td>TN</td>
      <td>United States</td>
      <td>2001/2/9 17:43</td>
      <td>2001/4/9 20:01</td>
      <td>36.343330</td>
      <td>-88.850280</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2001/4/9 13:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Renee Elisabeth</td>
      <td>Tel Aviv</td>
      <td>Tel Aviv</td>
      <td>Israel</td>
      <td>2001/4/9 13:03</td>
      <td>2001/4/9 22:10</td>
      <td>32.066667</td>
      <td>34.766667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2001/4/9 14:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Aidan</td>
      <td>Chatou</td>
      <td>Ile-de-France</td>
      <td>France</td>
      <td>2006/3/8 4:22</td>
      <td>2001/5/9 1:17</td>
      <td>48.883333</td>
      <td>2.150000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2001/5/9 2:42</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Stacy</td>
      <td>New York</td>
      <td>NY</td>
      <td>United States</td>
      <td>2001/5/9 2:23</td>
      <td>2001/5/9 4:59</td>
      <td>40.714170</td>
      <td>-74.006390</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2001/5/9 5:39</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Heidi</td>
      <td>Eindhoven</td>
      <td>Noord-Brabant</td>
      <td>Netherlands</td>
      <td>2001/5/9 4:55</td>
      <td>2001/5/9 8:15</td>
      <td>51.450000</td>
      <td>5.466667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2001/2/9 9:16</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Sean</td>
      <td>Shavano Park</td>
      <td>TX</td>
      <td>United States</td>
      <td>2001/2/9 8:32</td>
      <td>2001/5/9 9:05</td>
      <td>29.423890</td>
      <td>-98.493330</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2001/5/9 10:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Georgia</td>
      <td>Eagle</td>
      <td>ID</td>
      <td>United States</td>
      <td>2011/11/8 15:53</td>
      <td>2001/5/9 10:05</td>
      <td>43.695560</td>
      <td>-116.353060</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2001/2/9 14:18</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Richard</td>
      <td>Riverside</td>
      <td>NJ</td>
      <td>United States</td>
      <td>2012/9/8 12:07</td>
      <td>2001/5/9 11:01</td>
      <td>40.032220</td>
      <td>-74.957780</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2001/4/9 1:05</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Leanne</td>
      <td>Julianstown</td>
      <td>Meath</td>
      <td>Ireland</td>
      <td>2001/4/9 0:00</td>
      <td>2001/5/9 13:36</td>
      <td>53.677222</td>
      <td>-6.319167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2001/5/9 11:37</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Janet</td>
      <td>Ottawa</td>
      <td>Ontario</td>
      <td>Canada</td>
      <td>2001/5/9 9:35</td>
      <td>2001/5/9 19:24</td>
      <td>45.416667</td>
      <td>-75.700000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2001/6/9 5:02</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>barbara</td>
      <td>Hyderabad</td>
      <td>Andhra Pradesh</td>
      <td>India</td>
      <td>2001/6/9 2:41</td>
      <td>2001/6/9 7:52</td>
      <td>17.383333</td>
      <td>78.466667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2001/6/9 7:45</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Sabine</td>
      <td>London</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/6/9 7:00</td>
      <td>2001/6/9 9:17</td>
      <td>51.527210</td>
      <td>0.145590</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2001/2/9 7:35</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Hani</td>
      <td>Salt Lake City</td>
      <td>UT</td>
      <td>United States</td>
      <td>12/30/08 5:44</td>
      <td>2001/6/9 10:52</td>
      <td>40.760830</td>
      <td>-111.890280</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2001/6/9 12:56</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Jeremy</td>
      <td>Manchester</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/6/9 10:58</td>
      <td>2001/6/9 13:31</td>
      <td>53.500000</td>
      <td>-2.216667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2001/1/9 11:05</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Janis</td>
      <td>Ballynora</td>
      <td>Cork</td>
      <td>Ireland</td>
      <td>2012/10/7 12:37</td>
      <td>2001/7/9 1:52</td>
      <td>51.863056</td>
      <td>-8.580000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2001/5/9 4:10</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Nicola</td>
      <td>Roodepoort</td>
      <td>Gauteng</td>
      <td>South Africa</td>
      <td>2001/5/9 2:33</td>
      <td>2001/7/9 5:13</td>
      <td>-26.166667</td>
      <td>27.866667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2001/6/9 7:18</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>asuman</td>
      <td>Chula Vista</td>
      <td>CA</td>
      <td>United States</td>
      <td>2001/6/9 7:07</td>
      <td>2001/7/9 7:08</td>
      <td>32.640000</td>
      <td>-117.083330</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2001/2/9 1:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Lena</td>
      <td>Kuopio</td>
      <td>Ita-Suomen Laani</td>
      <td>Finland</td>
      <td>12/31/08 2:48</td>
      <td>2001/7/9 10:20</td>
      <td>62.900000</td>
      <td>27.683333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2001/1/9 2:24</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Lisa</td>
      <td>Sugar Land</td>
      <td>TX</td>
      <td>United States</td>
      <td>2001/1/9 1:56</td>
      <td>2001/7/9 10:52</td>
      <td>29.619440</td>
      <td>-95.634720</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2001/7/9 8:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Bryan Kerrene</td>
      <td>New York</td>
      <td>NY</td>
      <td>United States</td>
      <td>2001/7/9 7:39</td>
      <td>2001/7/9 12:38</td>
      <td>40.714170</td>
      <td>-74.006390</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2001/2/9 2:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>chris</td>
      <td>London</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/3/8 7:23</td>
      <td>2001/7/9 13:14</td>
      <td>51.527210</td>
      <td>0.145590</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2001/1/9 20:21</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Maxine</td>
      <td>Morton</td>
      <td>IL</td>
      <td>United States</td>
      <td>10/24/08 6:48</td>
      <td>2001/7/9 20:49</td>
      <td>40.612780</td>
      <td>-89.459170</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2001/8/9 0:42</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Family</td>
      <td>Los Gatos</td>
      <td>CA</td>
      <td>United States</td>
      <td>2001/8/9 0:28</td>
      <td>2001/8/9 3:39</td>
      <td>37.226670</td>
      <td>-121.973610</td>
      <td>1200</td>
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
    </tr>
    <tr>
      <th>968</th>
      <td>2001/2/9 17:24</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Diners</td>
      <td>clara</td>
      <td>Perth</td>
      <td>Western Australia</td>
      <td>Australia</td>
      <td>2001/1/9 21:20</td>
      <td>2/27/09 18:43</td>
      <td>-31.933333</td>
      <td>115.833333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>969</th>
      <td>2001/7/9 18:15</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Selma</td>
      <td>Greenville</td>
      <td>TX</td>
      <td>United States</td>
      <td>2001/5/9 18:16</td>
      <td>2/27/09 19:07</td>
      <td>33.138330</td>
      <td>-96.110560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>970</th>
      <td>2001/3/9 21:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Doug and Tina</td>
      <td>Pls Vrds Est</td>
      <td>CA</td>
      <td>United States</td>
      <td>12/24/07 22:59</td>
      <td>2/27/09 21:40</td>
      <td>33.800560</td>
      <td>-118.389170</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>971</th>
      <td>2001/4/9 5:13</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Lauren</td>
      <td>Hradec Kralove</td>
      <td>East Bohemia</td>
      <td>Czech Republic</td>
      <td>2003/5/6 0:51</td>
      <td>2/27/09 23:30</td>
      <td>50.211667</td>
      <td>15.844167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>972</th>
      <td>2001/4/9 9:28</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Jen</td>
      <td>Maidstone</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>7/18/05 14:17</td>
      <td>2/28/09 2:28</td>
      <td>51.266667</td>
      <td>0.516667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>973</th>
      <td>2001/2/9 4:34</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>gladys</td>
      <td>Saint Albans</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/10/6 4:20</td>
      <td>2/28/09 3:43</td>
      <td>51.750000</td>
      <td>-0.333333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>974</th>
      <td>1/22/09 11:10</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Gustavo</td>
      <td>Voluntari</td>
      <td>Bucuresti</td>
      <td>Romania</td>
      <td>7/28/08 11:12</td>
      <td>2/28/09 7:52</td>
      <td>44.466667</td>
      <td>26.133333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>975</th>
      <td>2001/7/9 12:06</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Erica</td>
      <td>Nadur</td>
      <td></td>
      <td>Malta</td>
      <td>3/30/06 2:02</td>
      <td>2/28/09 7:59</td>
      <td>36.037778</td>
      <td>14.294167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>976</th>
      <td>1/29/09 13:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Hale</td>
      <td>Morrison</td>
      <td>CO</td>
      <td>United States</td>
      <td>2011/3/5 18:14</td>
      <td>2/28/09 8:27</td>
      <td>39.653610</td>
      <td>-105.190560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>977</th>
      <td>1/27/09 2:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Rosemary</td>
      <td>Cobham</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/27/09 2:50</td>
      <td>2/28/09 9:22</td>
      <td>51.383333</td>
      <td>0.400000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>978</th>
      <td>2001/7/9 13:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Darian</td>
      <td>Izmir</td>
      <td>Izmir</td>
      <td>Turkey</td>
      <td>8/26/08 7:33</td>
      <td>2/28/09 9:54</td>
      <td>38.407222</td>
      <td>27.150278</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>979</th>
      <td>1/23/09 10:04</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Kevin</td>
      <td>Hollywood</td>
      <td>CA</td>
      <td>United States</td>
      <td>5/30/06 20:25</td>
      <td>2/28/09 9:59</td>
      <td>34.098330</td>
      <td>-118.325830</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>980</th>
      <td>1/19/09 4:55</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Alyssa</td>
      <td>Brighton</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2/19/08 9:27</td>
      <td>2/28/09 10:06</td>
      <td>50.833333</td>
      <td>-0.150000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>981</th>
      <td>1/28/09 22:02</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Hale</td>
      <td>Hawera</td>
      <td>Taranaki</td>
      <td>New Zealand</td>
      <td>1/23/09 22:31</td>
      <td>2/28/09 12:43</td>
      <td>-39.591667</td>
      <td>174.283333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>982</th>
      <td>2001/4/9 18:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>KELI</td>
      <td>Worongary</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>12/23/08 15:17</td>
      <td>2/28/09 14:00</td>
      <td>-28.050000</td>
      <td>153.350000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>983</th>
      <td>2001/12/9 20:31</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Glen</td>
      <td>Atlantida</td>
      <td>Guatemala</td>
      <td>Guatemala</td>
      <td>2001/6/9 16:53</td>
      <td>2/28/09 14:39</td>
      <td>14.650000</td>
      <td>-90.483333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>984</th>
      <td>1/24/09 12:00</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>T</td>
      <td>El Escorial</td>
      <td>Madrid</td>
      <td>Spain</td>
      <td>12/30/08 15:19</td>
      <td>2/28/09 15:17</td>
      <td>40.583333</td>
      <td>-4.116667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>985</th>
      <td>1/28/09 11:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>christal</td>
      <td>Morrison</td>
      <td>CO</td>
      <td>United States</td>
      <td>6/20/04 17:16</td>
      <td>2/28/09 17:18</td>
      <td>39.653610</td>
      <td>-105.190560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>986</th>
      <td>2001/7/9 17:48</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Alex</td>
      <td>Augusta</td>
      <td>GA</td>
      <td>United States</td>
      <td>2006/10/5 20:25</td>
      <td>2/28/09 19:57</td>
      <td>33.517220</td>
      <td>-82.075830</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>987</th>
      <td>1/23/09 12:42</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Anke</td>
      <td>Avalon</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>2003/3/8 17:38</td>
      <td>2/28/09 22:26</td>
      <td>-33.633333</td>
      <td>151.333333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>988</th>
      <td>2001/7/9 19:48</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>TRICIA</td>
      <td>Sydney</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>9/21/08 20:49</td>
      <td>2003/1/9 0:14</td>
      <td>-33.883333</td>
      <td>151.216667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>989</th>
      <td>1/26/09 11:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>smith</td>
      <td>Lahti</td>
      <td>Etela-Suomen Laani</td>
      <td>Finland</td>
      <td>2001/4/9 5:25</td>
      <td>2003/1/9 0:39</td>
      <td>60.966667</td>
      <td>25.666667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>990</th>
      <td>2001/5/9 13:23</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Macy</td>
      <td>Inner City</td>
      <td>Vienna</td>
      <td>Austria</td>
      <td>2001/5/9 11:28</td>
      <td>2003/1/9 2:28</td>
      <td>48.216667</td>
      <td>16.366667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>991</th>
      <td>1/26/09 13:41</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Lesleigh</td>
      <td>Baden</td>
      <td>Aargau</td>
      <td>Switzerland</td>
      <td>10/23/05 9:23</td>
      <td>2003/1/9 3:11</td>
      <td>47.466667</td>
      <td>8.300000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>992</th>
      <td>1/20/09 10:42</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Diners</td>
      <td>esther</td>
      <td>Huddersfield</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/20/09 9:15</td>
      <td>2003/1/9 3:29</td>
      <td>53.650000</td>
      <td>-1.783333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>993</th>
      <td>1/22/09 14:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Hans-Joerg</td>
      <td>Belfast</td>
      <td>Northern Ireland</td>
      <td>United Kingdom</td>
      <td>2011/10/8 12:15</td>
      <td>2003/1/9 3:37</td>
      <td>54.583333</td>
      <td>-5.933333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>994</th>
      <td>1/28/09 5:36</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Christiane</td>
      <td>Black River</td>
      <td>Black River</td>
      <td>Mauritius</td>
      <td>2001/9/9 8:10</td>
      <td>2003/1/9 4:40</td>
      <td>-20.360278</td>
      <td>57.366111</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2001/1/9 4:24</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Amex</td>
      <td>Pamela</td>
      <td>Skaneateles</td>
      <td>NY</td>
      <td>United States</td>
      <td>12/28/08 17:28</td>
      <td>2003/1/9 7:21</td>
      <td>42.946940</td>
      <td>-76.429440</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2001/8/9 11:55</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>julie</td>
      <td>Haverhill</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>11/29/06 13:31</td>
      <td>2003/1/9 7:28</td>
      <td>52.083333</td>
      <td>0.433333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2001/12/9 21:30</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Julia</td>
      <td>Madison</td>
      <td>WI</td>
      <td>United States</td>
      <td>11/17/08 22:24</td>
      <td>2003/1/9 10:14</td>
      <td>43.073060</td>
      <td>-89.401110</td>
      <td>1200</td>
    </tr>
  </tbody>
</table>
<p>998 rows × 13 columns</p>
</div>




```python
df.append(df)# 出现了index不唯一的错误
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
      <th>Transaction_date</th>
      <th>Product</th>
      <th>Price</th>
      <th>Payment_Type</th>
      <th>Name</th>
      <th>City</th>
      <th>State</th>
      <th>Country</th>
      <th>Account_Created</th>
      <th>Last_Login</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Price2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2001/2/9 6:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>carolina</td>
      <td>Basildon</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/2/9 6:00</td>
      <td>2001/2/9 6:08</td>
      <td>51.500000</td>
      <td>-1.116667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2001/2/9 4:53</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Betina</td>
      <td>Parkville</td>
      <td>MO</td>
      <td>United States</td>
      <td>2001/2/9 4:42</td>
      <td>2001/2/9 7:49</td>
      <td>39.195000</td>
      <td>-94.681940</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2001/2/9 13:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Federica e Andrea</td>
      <td>Astoria</td>
      <td>OR</td>
      <td>United States</td>
      <td>2001/1/9 16:21</td>
      <td>2001/3/9 12:32</td>
      <td>46.188060</td>
      <td>-123.830000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2001/3/9 14:44</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Gouya</td>
      <td>Echuca</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>9/25/05 21:13</td>
      <td>2001/3/9 14:22</td>
      <td>-36.133333</td>
      <td>144.750000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2001/4/9 12:56</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Gerd W</td>
      <td>Cahaba Heights</td>
      <td>AL</td>
      <td>United States</td>
      <td>11/15/08 15:47</td>
      <td>2001/4/9 12:45</td>
      <td>33.520560</td>
      <td>-86.802500</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2001/4/9 13:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>LAURENCE</td>
      <td>Mickleton</td>
      <td>NJ</td>
      <td>United States</td>
      <td>9/24/08 15:19</td>
      <td>2001/4/9 13:04</td>
      <td>39.790000</td>
      <td>-75.238060</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2001/4/9 20:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Fleur</td>
      <td>Peoria</td>
      <td>IL</td>
      <td>United States</td>
      <td>2001/3/9 9:38</td>
      <td>2001/4/9 19:45</td>
      <td>40.693610</td>
      <td>-89.588890</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2001/2/9 20:09</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>adam</td>
      <td>Martin</td>
      <td>TN</td>
      <td>United States</td>
      <td>2001/2/9 17:43</td>
      <td>2001/4/9 20:01</td>
      <td>36.343330</td>
      <td>-88.850280</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2001/4/9 13:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Renee Elisabeth</td>
      <td>Tel Aviv</td>
      <td>Tel Aviv</td>
      <td>Israel</td>
      <td>2001/4/9 13:03</td>
      <td>2001/4/9 22:10</td>
      <td>32.066667</td>
      <td>34.766667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2001/4/9 14:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Aidan</td>
      <td>Chatou</td>
      <td>Ile-de-France</td>
      <td>France</td>
      <td>2006/3/8 4:22</td>
      <td>2001/5/9 1:17</td>
      <td>48.883333</td>
      <td>2.150000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2001/5/9 2:42</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Stacy</td>
      <td>New York</td>
      <td>NY</td>
      <td>United States</td>
      <td>2001/5/9 2:23</td>
      <td>2001/5/9 4:59</td>
      <td>40.714170</td>
      <td>-74.006390</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2001/5/9 5:39</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Heidi</td>
      <td>Eindhoven</td>
      <td>Noord-Brabant</td>
      <td>Netherlands</td>
      <td>2001/5/9 4:55</td>
      <td>2001/5/9 8:15</td>
      <td>51.450000</td>
      <td>5.466667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2001/2/9 9:16</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Sean</td>
      <td>Shavano Park</td>
      <td>TX</td>
      <td>United States</td>
      <td>2001/2/9 8:32</td>
      <td>2001/5/9 9:05</td>
      <td>29.423890</td>
      <td>-98.493330</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2001/5/9 10:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Georgia</td>
      <td>Eagle</td>
      <td>ID</td>
      <td>United States</td>
      <td>2011/11/8 15:53</td>
      <td>2001/5/9 10:05</td>
      <td>43.695560</td>
      <td>-116.353060</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2001/2/9 14:18</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Richard</td>
      <td>Riverside</td>
      <td>NJ</td>
      <td>United States</td>
      <td>2012/9/8 12:07</td>
      <td>2001/5/9 11:01</td>
      <td>40.032220</td>
      <td>-74.957780</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2001/4/9 1:05</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Leanne</td>
      <td>Julianstown</td>
      <td>Meath</td>
      <td>Ireland</td>
      <td>2001/4/9 0:00</td>
      <td>2001/5/9 13:36</td>
      <td>53.677222</td>
      <td>-6.319167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2001/5/9 11:37</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Janet</td>
      <td>Ottawa</td>
      <td>Ontario</td>
      <td>Canada</td>
      <td>2001/5/9 9:35</td>
      <td>2001/5/9 19:24</td>
      <td>45.416667</td>
      <td>-75.700000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2001/6/9 5:02</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>barbara</td>
      <td>Hyderabad</td>
      <td>Andhra Pradesh</td>
      <td>India</td>
      <td>2001/6/9 2:41</td>
      <td>2001/6/9 7:52</td>
      <td>17.383333</td>
      <td>78.466667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2001/6/9 7:45</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Sabine</td>
      <td>London</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/6/9 7:00</td>
      <td>2001/6/9 9:17</td>
      <td>51.527210</td>
      <td>0.145590</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2001/2/9 7:35</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Hani</td>
      <td>Salt Lake City</td>
      <td>UT</td>
      <td>United States</td>
      <td>12/30/08 5:44</td>
      <td>2001/6/9 10:52</td>
      <td>40.760830</td>
      <td>-111.890280</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2001/6/9 12:56</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Jeremy</td>
      <td>Manchester</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/6/9 10:58</td>
      <td>2001/6/9 13:31</td>
      <td>53.500000</td>
      <td>-2.216667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2001/1/9 11:05</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Janis</td>
      <td>Ballynora</td>
      <td>Cork</td>
      <td>Ireland</td>
      <td>2012/10/7 12:37</td>
      <td>2001/7/9 1:52</td>
      <td>51.863056</td>
      <td>-8.580000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2001/5/9 4:10</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Nicola</td>
      <td>Roodepoort</td>
      <td>Gauteng</td>
      <td>South Africa</td>
      <td>2001/5/9 2:33</td>
      <td>2001/7/9 5:13</td>
      <td>-26.166667</td>
      <td>27.866667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2001/6/9 7:18</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>asuman</td>
      <td>Chula Vista</td>
      <td>CA</td>
      <td>United States</td>
      <td>2001/6/9 7:07</td>
      <td>2001/7/9 7:08</td>
      <td>32.640000</td>
      <td>-117.083330</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2001/2/9 1:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Lena</td>
      <td>Kuopio</td>
      <td>Ita-Suomen Laani</td>
      <td>Finland</td>
      <td>12/31/08 2:48</td>
      <td>2001/7/9 10:20</td>
      <td>62.900000</td>
      <td>27.683333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2001/1/9 2:24</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Lisa</td>
      <td>Sugar Land</td>
      <td>TX</td>
      <td>United States</td>
      <td>2001/1/9 1:56</td>
      <td>2001/7/9 10:52</td>
      <td>29.619440</td>
      <td>-95.634720</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2001/7/9 8:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Bryan Kerrene</td>
      <td>New York</td>
      <td>NY</td>
      <td>United States</td>
      <td>2001/7/9 7:39</td>
      <td>2001/7/9 12:38</td>
      <td>40.714170</td>
      <td>-74.006390</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2001/2/9 2:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>chris</td>
      <td>London</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/3/8 7:23</td>
      <td>2001/7/9 13:14</td>
      <td>51.527210</td>
      <td>0.145590</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2001/1/9 20:21</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Maxine</td>
      <td>Morton</td>
      <td>IL</td>
      <td>United States</td>
      <td>10/24/08 6:48</td>
      <td>2001/7/9 20:49</td>
      <td>40.612780</td>
      <td>-89.459170</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2001/8/9 0:42</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Family</td>
      <td>Los Gatos</td>
      <td>CA</td>
      <td>United States</td>
      <td>2001/8/9 0:28</td>
      <td>2001/8/9 3:39</td>
      <td>37.226670</td>
      <td>-121.973610</td>
      <td>1200</td>
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
    </tr>
    <tr>
      <th>968</th>
      <td>2001/2/9 17:24</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Diners</td>
      <td>clara</td>
      <td>Perth</td>
      <td>Western Australia</td>
      <td>Australia</td>
      <td>2001/1/9 21:20</td>
      <td>2/27/09 18:43</td>
      <td>-31.933333</td>
      <td>115.833333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>969</th>
      <td>2001/7/9 18:15</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Selma</td>
      <td>Greenville</td>
      <td>TX</td>
      <td>United States</td>
      <td>2001/5/9 18:16</td>
      <td>2/27/09 19:07</td>
      <td>33.138330</td>
      <td>-96.110560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>970</th>
      <td>2001/3/9 21:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Doug and Tina</td>
      <td>Pls Vrds Est</td>
      <td>CA</td>
      <td>United States</td>
      <td>12/24/07 22:59</td>
      <td>2/27/09 21:40</td>
      <td>33.800560</td>
      <td>-118.389170</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>971</th>
      <td>2001/4/9 5:13</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Lauren</td>
      <td>Hradec Kralove</td>
      <td>East Bohemia</td>
      <td>Czech Republic</td>
      <td>2003/5/6 0:51</td>
      <td>2/27/09 23:30</td>
      <td>50.211667</td>
      <td>15.844167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>972</th>
      <td>2001/4/9 9:28</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Jen</td>
      <td>Maidstone</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>7/18/05 14:17</td>
      <td>2/28/09 2:28</td>
      <td>51.266667</td>
      <td>0.516667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>973</th>
      <td>2001/2/9 4:34</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>gladys</td>
      <td>Saint Albans</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/10/6 4:20</td>
      <td>2/28/09 3:43</td>
      <td>51.750000</td>
      <td>-0.333333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>974</th>
      <td>1/22/09 11:10</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Gustavo</td>
      <td>Voluntari</td>
      <td>Bucuresti</td>
      <td>Romania</td>
      <td>7/28/08 11:12</td>
      <td>2/28/09 7:52</td>
      <td>44.466667</td>
      <td>26.133333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>975</th>
      <td>2001/7/9 12:06</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Erica</td>
      <td>Nadur</td>
      <td></td>
      <td>Malta</td>
      <td>3/30/06 2:02</td>
      <td>2/28/09 7:59</td>
      <td>36.037778</td>
      <td>14.294167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>976</th>
      <td>1/29/09 13:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Hale</td>
      <td>Morrison</td>
      <td>CO</td>
      <td>United States</td>
      <td>2011/3/5 18:14</td>
      <td>2/28/09 8:27</td>
      <td>39.653610</td>
      <td>-105.190560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>977</th>
      <td>1/27/09 2:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Rosemary</td>
      <td>Cobham</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/27/09 2:50</td>
      <td>2/28/09 9:22</td>
      <td>51.383333</td>
      <td>0.400000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>978</th>
      <td>2001/7/9 13:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Darian</td>
      <td>Izmir</td>
      <td>Izmir</td>
      <td>Turkey</td>
      <td>8/26/08 7:33</td>
      <td>2/28/09 9:54</td>
      <td>38.407222</td>
      <td>27.150278</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>979</th>
      <td>1/23/09 10:04</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Kevin</td>
      <td>Hollywood</td>
      <td>CA</td>
      <td>United States</td>
      <td>5/30/06 20:25</td>
      <td>2/28/09 9:59</td>
      <td>34.098330</td>
      <td>-118.325830</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>980</th>
      <td>1/19/09 4:55</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Alyssa</td>
      <td>Brighton</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2/19/08 9:27</td>
      <td>2/28/09 10:06</td>
      <td>50.833333</td>
      <td>-0.150000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>981</th>
      <td>1/28/09 22:02</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Hale</td>
      <td>Hawera</td>
      <td>Taranaki</td>
      <td>New Zealand</td>
      <td>1/23/09 22:31</td>
      <td>2/28/09 12:43</td>
      <td>-39.591667</td>
      <td>174.283333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>982</th>
      <td>2001/4/9 18:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>KELI</td>
      <td>Worongary</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>12/23/08 15:17</td>
      <td>2/28/09 14:00</td>
      <td>-28.050000</td>
      <td>153.350000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>983</th>
      <td>2001/12/9 20:31</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Glen</td>
      <td>Atlantida</td>
      <td>Guatemala</td>
      <td>Guatemala</td>
      <td>2001/6/9 16:53</td>
      <td>2/28/09 14:39</td>
      <td>14.650000</td>
      <td>-90.483333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>984</th>
      <td>1/24/09 12:00</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>T</td>
      <td>El Escorial</td>
      <td>Madrid</td>
      <td>Spain</td>
      <td>12/30/08 15:19</td>
      <td>2/28/09 15:17</td>
      <td>40.583333</td>
      <td>-4.116667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>985</th>
      <td>1/28/09 11:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>christal</td>
      <td>Morrison</td>
      <td>CO</td>
      <td>United States</td>
      <td>6/20/04 17:16</td>
      <td>2/28/09 17:18</td>
      <td>39.653610</td>
      <td>-105.190560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>986</th>
      <td>2001/7/9 17:48</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Alex</td>
      <td>Augusta</td>
      <td>GA</td>
      <td>United States</td>
      <td>2006/10/5 20:25</td>
      <td>2/28/09 19:57</td>
      <td>33.517220</td>
      <td>-82.075830</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>987</th>
      <td>1/23/09 12:42</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Anke</td>
      <td>Avalon</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>2003/3/8 17:38</td>
      <td>2/28/09 22:26</td>
      <td>-33.633333</td>
      <td>151.333333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>988</th>
      <td>2001/7/9 19:48</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>TRICIA</td>
      <td>Sydney</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>9/21/08 20:49</td>
      <td>2003/1/9 0:14</td>
      <td>-33.883333</td>
      <td>151.216667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>989</th>
      <td>1/26/09 11:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>smith</td>
      <td>Lahti</td>
      <td>Etela-Suomen Laani</td>
      <td>Finland</td>
      <td>2001/4/9 5:25</td>
      <td>2003/1/9 0:39</td>
      <td>60.966667</td>
      <td>25.666667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>990</th>
      <td>2001/5/9 13:23</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Macy</td>
      <td>Inner City</td>
      <td>Vienna</td>
      <td>Austria</td>
      <td>2001/5/9 11:28</td>
      <td>2003/1/9 2:28</td>
      <td>48.216667</td>
      <td>16.366667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>991</th>
      <td>1/26/09 13:41</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Lesleigh</td>
      <td>Baden</td>
      <td>Aargau</td>
      <td>Switzerland</td>
      <td>10/23/05 9:23</td>
      <td>2003/1/9 3:11</td>
      <td>47.466667</td>
      <td>8.300000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>992</th>
      <td>1/20/09 10:42</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Diners</td>
      <td>esther</td>
      <td>Huddersfield</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/20/09 9:15</td>
      <td>2003/1/9 3:29</td>
      <td>53.650000</td>
      <td>-1.783333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>993</th>
      <td>1/22/09 14:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Hans-Joerg</td>
      <td>Belfast</td>
      <td>Northern Ireland</td>
      <td>United Kingdom</td>
      <td>2011/10/8 12:15</td>
      <td>2003/1/9 3:37</td>
      <td>54.583333</td>
      <td>-5.933333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>994</th>
      <td>1/28/09 5:36</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Christiane</td>
      <td>Black River</td>
      <td>Black River</td>
      <td>Mauritius</td>
      <td>2001/9/9 8:10</td>
      <td>2003/1/9 4:40</td>
      <td>-20.360278</td>
      <td>57.366111</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2001/1/9 4:24</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Amex</td>
      <td>Pamela</td>
      <td>Skaneateles</td>
      <td>NY</td>
      <td>United States</td>
      <td>12/28/08 17:28</td>
      <td>2003/1/9 7:21</td>
      <td>42.946940</td>
      <td>-76.429440</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2001/8/9 11:55</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>julie</td>
      <td>Haverhill</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>11/29/06 13:31</td>
      <td>2003/1/9 7:28</td>
      <td>52.083333</td>
      <td>0.433333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2001/12/9 21:30</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Julia</td>
      <td>Madison</td>
      <td>WI</td>
      <td>United States</td>
      <td>11/17/08 22:24</td>
      <td>2003/1/9 10:14</td>
      <td>43.073060</td>
      <td>-89.401110</td>
      <td>1200</td>
    </tr>
  </tbody>
</table>
<p>1996 rows × 13 columns</p>
</div>




```python
df.append(df,ignore_index=True)# 这样就修复了 或是df.append(df).reset_index()
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
      <th>Transaction_date</th>
      <th>Product</th>
      <th>Price</th>
      <th>Payment_Type</th>
      <th>Name</th>
      <th>City</th>
      <th>State</th>
      <th>Country</th>
      <th>Account_Created</th>
      <th>Last_Login</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Price2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2001/2/9 6:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>carolina</td>
      <td>Basildon</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/2/9 6:00</td>
      <td>2001/2/9 6:08</td>
      <td>51.500000</td>
      <td>-1.116667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2001/2/9 4:53</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Betina</td>
      <td>Parkville</td>
      <td>MO</td>
      <td>United States</td>
      <td>2001/2/9 4:42</td>
      <td>2001/2/9 7:49</td>
      <td>39.195000</td>
      <td>-94.681940</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2001/2/9 13:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Federica e Andrea</td>
      <td>Astoria</td>
      <td>OR</td>
      <td>United States</td>
      <td>2001/1/9 16:21</td>
      <td>2001/3/9 12:32</td>
      <td>46.188060</td>
      <td>-123.830000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2001/3/9 14:44</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Gouya</td>
      <td>Echuca</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>9/25/05 21:13</td>
      <td>2001/3/9 14:22</td>
      <td>-36.133333</td>
      <td>144.750000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2001/4/9 12:56</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Gerd W</td>
      <td>Cahaba Heights</td>
      <td>AL</td>
      <td>United States</td>
      <td>11/15/08 15:47</td>
      <td>2001/4/9 12:45</td>
      <td>33.520560</td>
      <td>-86.802500</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2001/4/9 13:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>LAURENCE</td>
      <td>Mickleton</td>
      <td>NJ</td>
      <td>United States</td>
      <td>9/24/08 15:19</td>
      <td>2001/4/9 13:04</td>
      <td>39.790000</td>
      <td>-75.238060</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2001/4/9 20:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Fleur</td>
      <td>Peoria</td>
      <td>IL</td>
      <td>United States</td>
      <td>2001/3/9 9:38</td>
      <td>2001/4/9 19:45</td>
      <td>40.693610</td>
      <td>-89.588890</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2001/2/9 20:09</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>adam</td>
      <td>Martin</td>
      <td>TN</td>
      <td>United States</td>
      <td>2001/2/9 17:43</td>
      <td>2001/4/9 20:01</td>
      <td>36.343330</td>
      <td>-88.850280</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2001/4/9 13:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Renee Elisabeth</td>
      <td>Tel Aviv</td>
      <td>Tel Aviv</td>
      <td>Israel</td>
      <td>2001/4/9 13:03</td>
      <td>2001/4/9 22:10</td>
      <td>32.066667</td>
      <td>34.766667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2001/4/9 14:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Aidan</td>
      <td>Chatou</td>
      <td>Ile-de-France</td>
      <td>France</td>
      <td>2006/3/8 4:22</td>
      <td>2001/5/9 1:17</td>
      <td>48.883333</td>
      <td>2.150000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2001/5/9 2:42</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Stacy</td>
      <td>New York</td>
      <td>NY</td>
      <td>United States</td>
      <td>2001/5/9 2:23</td>
      <td>2001/5/9 4:59</td>
      <td>40.714170</td>
      <td>-74.006390</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2001/5/9 5:39</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Heidi</td>
      <td>Eindhoven</td>
      <td>Noord-Brabant</td>
      <td>Netherlands</td>
      <td>2001/5/9 4:55</td>
      <td>2001/5/9 8:15</td>
      <td>51.450000</td>
      <td>5.466667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2001/2/9 9:16</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Sean</td>
      <td>Shavano Park</td>
      <td>TX</td>
      <td>United States</td>
      <td>2001/2/9 8:32</td>
      <td>2001/5/9 9:05</td>
      <td>29.423890</td>
      <td>-98.493330</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2001/5/9 10:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Georgia</td>
      <td>Eagle</td>
      <td>ID</td>
      <td>United States</td>
      <td>2011/11/8 15:53</td>
      <td>2001/5/9 10:05</td>
      <td>43.695560</td>
      <td>-116.353060</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2001/2/9 14:18</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Richard</td>
      <td>Riverside</td>
      <td>NJ</td>
      <td>United States</td>
      <td>2012/9/8 12:07</td>
      <td>2001/5/9 11:01</td>
      <td>40.032220</td>
      <td>-74.957780</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2001/4/9 1:05</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Leanne</td>
      <td>Julianstown</td>
      <td>Meath</td>
      <td>Ireland</td>
      <td>2001/4/9 0:00</td>
      <td>2001/5/9 13:36</td>
      <td>53.677222</td>
      <td>-6.319167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2001/5/9 11:37</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Janet</td>
      <td>Ottawa</td>
      <td>Ontario</td>
      <td>Canada</td>
      <td>2001/5/9 9:35</td>
      <td>2001/5/9 19:24</td>
      <td>45.416667</td>
      <td>-75.700000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2001/6/9 5:02</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>barbara</td>
      <td>Hyderabad</td>
      <td>Andhra Pradesh</td>
      <td>India</td>
      <td>2001/6/9 2:41</td>
      <td>2001/6/9 7:52</td>
      <td>17.383333</td>
      <td>78.466667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2001/6/9 7:45</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Sabine</td>
      <td>London</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/6/9 7:00</td>
      <td>2001/6/9 9:17</td>
      <td>51.527210</td>
      <td>0.145590</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2001/2/9 7:35</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Hani</td>
      <td>Salt Lake City</td>
      <td>UT</td>
      <td>United States</td>
      <td>12/30/08 5:44</td>
      <td>2001/6/9 10:52</td>
      <td>40.760830</td>
      <td>-111.890280</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2001/6/9 12:56</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Jeremy</td>
      <td>Manchester</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/6/9 10:58</td>
      <td>2001/6/9 13:31</td>
      <td>53.500000</td>
      <td>-2.216667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2001/1/9 11:05</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Janis</td>
      <td>Ballynora</td>
      <td>Cork</td>
      <td>Ireland</td>
      <td>2012/10/7 12:37</td>
      <td>2001/7/9 1:52</td>
      <td>51.863056</td>
      <td>-8.580000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2001/5/9 4:10</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Nicola</td>
      <td>Roodepoort</td>
      <td>Gauteng</td>
      <td>South Africa</td>
      <td>2001/5/9 2:33</td>
      <td>2001/7/9 5:13</td>
      <td>-26.166667</td>
      <td>27.866667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2001/6/9 7:18</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>asuman</td>
      <td>Chula Vista</td>
      <td>CA</td>
      <td>United States</td>
      <td>2001/6/9 7:07</td>
      <td>2001/7/9 7:08</td>
      <td>32.640000</td>
      <td>-117.083330</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2001/2/9 1:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Lena</td>
      <td>Kuopio</td>
      <td>Ita-Suomen Laani</td>
      <td>Finland</td>
      <td>12/31/08 2:48</td>
      <td>2001/7/9 10:20</td>
      <td>62.900000</td>
      <td>27.683333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2001/1/9 2:24</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Lisa</td>
      <td>Sugar Land</td>
      <td>TX</td>
      <td>United States</td>
      <td>2001/1/9 1:56</td>
      <td>2001/7/9 10:52</td>
      <td>29.619440</td>
      <td>-95.634720</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2001/7/9 8:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Bryan Kerrene</td>
      <td>New York</td>
      <td>NY</td>
      <td>United States</td>
      <td>2001/7/9 7:39</td>
      <td>2001/7/9 12:38</td>
      <td>40.714170</td>
      <td>-74.006390</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2001/2/9 2:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>chris</td>
      <td>London</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/3/8 7:23</td>
      <td>2001/7/9 13:14</td>
      <td>51.527210</td>
      <td>0.145590</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2001/1/9 20:21</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Maxine</td>
      <td>Morton</td>
      <td>IL</td>
      <td>United States</td>
      <td>10/24/08 6:48</td>
      <td>2001/7/9 20:49</td>
      <td>40.612780</td>
      <td>-89.459170</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2001/8/9 0:42</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Family</td>
      <td>Los Gatos</td>
      <td>CA</td>
      <td>United States</td>
      <td>2001/8/9 0:28</td>
      <td>2001/8/9 3:39</td>
      <td>37.226670</td>
      <td>-121.973610</td>
      <td>1200</td>
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
    </tr>
    <tr>
      <th>1966</th>
      <td>2001/2/9 17:24</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Diners</td>
      <td>clara</td>
      <td>Perth</td>
      <td>Western Australia</td>
      <td>Australia</td>
      <td>2001/1/9 21:20</td>
      <td>2/27/09 18:43</td>
      <td>-31.933333</td>
      <td>115.833333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>1967</th>
      <td>2001/7/9 18:15</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Selma</td>
      <td>Greenville</td>
      <td>TX</td>
      <td>United States</td>
      <td>2001/5/9 18:16</td>
      <td>2/27/09 19:07</td>
      <td>33.138330</td>
      <td>-96.110560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1968</th>
      <td>2001/3/9 21:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Doug and Tina</td>
      <td>Pls Vrds Est</td>
      <td>CA</td>
      <td>United States</td>
      <td>12/24/07 22:59</td>
      <td>2/27/09 21:40</td>
      <td>33.800560</td>
      <td>-118.389170</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1969</th>
      <td>2001/4/9 5:13</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Lauren</td>
      <td>Hradec Kralove</td>
      <td>East Bohemia</td>
      <td>Czech Republic</td>
      <td>2003/5/6 0:51</td>
      <td>2/27/09 23:30</td>
      <td>50.211667</td>
      <td>15.844167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1970</th>
      <td>2001/4/9 9:28</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Jen</td>
      <td>Maidstone</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>7/18/05 14:17</td>
      <td>2/28/09 2:28</td>
      <td>51.266667</td>
      <td>0.516667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1971</th>
      <td>2001/2/9 4:34</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>gladys</td>
      <td>Saint Albans</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/10/6 4:20</td>
      <td>2/28/09 3:43</td>
      <td>51.750000</td>
      <td>-0.333333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1972</th>
      <td>1/22/09 11:10</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Gustavo</td>
      <td>Voluntari</td>
      <td>Bucuresti</td>
      <td>Romania</td>
      <td>7/28/08 11:12</td>
      <td>2/28/09 7:52</td>
      <td>44.466667</td>
      <td>26.133333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1973</th>
      <td>2001/7/9 12:06</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Erica</td>
      <td>Nadur</td>
      <td></td>
      <td>Malta</td>
      <td>3/30/06 2:02</td>
      <td>2/28/09 7:59</td>
      <td>36.037778</td>
      <td>14.294167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1974</th>
      <td>1/29/09 13:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Hale</td>
      <td>Morrison</td>
      <td>CO</td>
      <td>United States</td>
      <td>2011/3/5 18:14</td>
      <td>2/28/09 8:27</td>
      <td>39.653610</td>
      <td>-105.190560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1975</th>
      <td>1/27/09 2:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Rosemary</td>
      <td>Cobham</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/27/09 2:50</td>
      <td>2/28/09 9:22</td>
      <td>51.383333</td>
      <td>0.400000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1976</th>
      <td>2001/7/9 13:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Darian</td>
      <td>Izmir</td>
      <td>Izmir</td>
      <td>Turkey</td>
      <td>8/26/08 7:33</td>
      <td>2/28/09 9:54</td>
      <td>38.407222</td>
      <td>27.150278</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1977</th>
      <td>1/23/09 10:04</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Kevin</td>
      <td>Hollywood</td>
      <td>CA</td>
      <td>United States</td>
      <td>5/30/06 20:25</td>
      <td>2/28/09 9:59</td>
      <td>34.098330</td>
      <td>-118.325830</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1978</th>
      <td>1/19/09 4:55</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Alyssa</td>
      <td>Brighton</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2/19/08 9:27</td>
      <td>2/28/09 10:06</td>
      <td>50.833333</td>
      <td>-0.150000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1979</th>
      <td>1/28/09 22:02</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Hale</td>
      <td>Hawera</td>
      <td>Taranaki</td>
      <td>New Zealand</td>
      <td>1/23/09 22:31</td>
      <td>2/28/09 12:43</td>
      <td>-39.591667</td>
      <td>174.283333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1980</th>
      <td>2001/4/9 18:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>KELI</td>
      <td>Worongary</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>12/23/08 15:17</td>
      <td>2/28/09 14:00</td>
      <td>-28.050000</td>
      <td>153.350000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1981</th>
      <td>2001/12/9 20:31</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Glen</td>
      <td>Atlantida</td>
      <td>Guatemala</td>
      <td>Guatemala</td>
      <td>2001/6/9 16:53</td>
      <td>2/28/09 14:39</td>
      <td>14.650000</td>
      <td>-90.483333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1982</th>
      <td>1/24/09 12:00</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>T</td>
      <td>El Escorial</td>
      <td>Madrid</td>
      <td>Spain</td>
      <td>12/30/08 15:19</td>
      <td>2/28/09 15:17</td>
      <td>40.583333</td>
      <td>-4.116667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1983</th>
      <td>1/28/09 11:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>christal</td>
      <td>Morrison</td>
      <td>CO</td>
      <td>United States</td>
      <td>6/20/04 17:16</td>
      <td>2/28/09 17:18</td>
      <td>39.653610</td>
      <td>-105.190560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1984</th>
      <td>2001/7/9 17:48</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Alex</td>
      <td>Augusta</td>
      <td>GA</td>
      <td>United States</td>
      <td>2006/10/5 20:25</td>
      <td>2/28/09 19:57</td>
      <td>33.517220</td>
      <td>-82.075830</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1985</th>
      <td>1/23/09 12:42</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Anke</td>
      <td>Avalon</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>2003/3/8 17:38</td>
      <td>2/28/09 22:26</td>
      <td>-33.633333</td>
      <td>151.333333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>1986</th>
      <td>2001/7/9 19:48</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>TRICIA</td>
      <td>Sydney</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>9/21/08 20:49</td>
      <td>2003/1/9 0:14</td>
      <td>-33.883333</td>
      <td>151.216667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>1987</th>
      <td>1/26/09 11:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>smith</td>
      <td>Lahti</td>
      <td>Etela-Suomen Laani</td>
      <td>Finland</td>
      <td>2001/4/9 5:25</td>
      <td>2003/1/9 0:39</td>
      <td>60.966667</td>
      <td>25.666667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1988</th>
      <td>2001/5/9 13:23</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Macy</td>
      <td>Inner City</td>
      <td>Vienna</td>
      <td>Austria</td>
      <td>2001/5/9 11:28</td>
      <td>2003/1/9 2:28</td>
      <td>48.216667</td>
      <td>16.366667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1989</th>
      <td>1/26/09 13:41</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Lesleigh</td>
      <td>Baden</td>
      <td>Aargau</td>
      <td>Switzerland</td>
      <td>10/23/05 9:23</td>
      <td>2003/1/9 3:11</td>
      <td>47.466667</td>
      <td>8.300000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1990</th>
      <td>1/20/09 10:42</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Diners</td>
      <td>esther</td>
      <td>Huddersfield</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/20/09 9:15</td>
      <td>2003/1/9 3:29</td>
      <td>53.650000</td>
      <td>-1.783333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>1991</th>
      <td>1/22/09 14:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Hans-Joerg</td>
      <td>Belfast</td>
      <td>Northern Ireland</td>
      <td>United Kingdom</td>
      <td>2011/10/8 12:15</td>
      <td>2003/1/9 3:37</td>
      <td>54.583333</td>
      <td>-5.933333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1992</th>
      <td>1/28/09 5:36</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Christiane</td>
      <td>Black River</td>
      <td>Black River</td>
      <td>Mauritius</td>
      <td>2001/9/9 8:10</td>
      <td>2003/1/9 4:40</td>
      <td>-20.360278</td>
      <td>57.366111</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>1993</th>
      <td>2001/1/9 4:24</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Amex</td>
      <td>Pamela</td>
      <td>Skaneateles</td>
      <td>NY</td>
      <td>United States</td>
      <td>12/28/08 17:28</td>
      <td>2003/1/9 7:21</td>
      <td>42.946940</td>
      <td>-76.429440</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>1994</th>
      <td>2001/8/9 11:55</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>julie</td>
      <td>Haverhill</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>11/29/06 13:31</td>
      <td>2003/1/9 7:28</td>
      <td>52.083333</td>
      <td>0.433333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1995</th>
      <td>2001/12/9 21:30</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Julia</td>
      <td>Madison</td>
      <td>WI</td>
      <td>United States</td>
      <td>11/17/08 22:24</td>
      <td>2003/1/9 10:14</td>
      <td>43.073060</td>
      <td>-89.401110</td>
      <td>1200</td>
    </tr>
  </tbody>
</table>
<p>1996 rows × 13 columns</p>
</div>



# 3. 复杂查询


```python
# select * from df where Latitude > 30
df.loc[df.Latitude>30,:]
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
      <th>Transaction_date</th>
      <th>Product</th>
      <th>Price</th>
      <th>Payment_Type</th>
      <th>Name</th>
      <th>City</th>
      <th>State</th>
      <th>Country</th>
      <th>Account_Created</th>
      <th>Last_Login</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Price2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2001/2/9 6:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>carolina</td>
      <td>Basildon</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/2/9 6:00</td>
      <td>2001/2/9 6:08</td>
      <td>51.500000</td>
      <td>-1.116667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2001/2/9 4:53</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Betina</td>
      <td>Parkville</td>
      <td>MO</td>
      <td>United States</td>
      <td>2001/2/9 4:42</td>
      <td>2001/2/9 7:49</td>
      <td>39.195000</td>
      <td>-94.681940</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2001/2/9 13:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Federica e Andrea</td>
      <td>Astoria</td>
      <td>OR</td>
      <td>United States</td>
      <td>2001/1/9 16:21</td>
      <td>2001/3/9 12:32</td>
      <td>46.188060</td>
      <td>-123.830000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2001/4/9 12:56</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Gerd W</td>
      <td>Cahaba Heights</td>
      <td>AL</td>
      <td>United States</td>
      <td>11/15/08 15:47</td>
      <td>2001/4/9 12:45</td>
      <td>33.520560</td>
      <td>-86.802500</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2001/4/9 13:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>LAURENCE</td>
      <td>Mickleton</td>
      <td>NJ</td>
      <td>United States</td>
      <td>9/24/08 15:19</td>
      <td>2001/4/9 13:04</td>
      <td>39.790000</td>
      <td>-75.238060</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2001/4/9 20:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Fleur</td>
      <td>Peoria</td>
      <td>IL</td>
      <td>United States</td>
      <td>2001/3/9 9:38</td>
      <td>2001/4/9 19:45</td>
      <td>40.693610</td>
      <td>-89.588890</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2001/2/9 20:09</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>adam</td>
      <td>Martin</td>
      <td>TN</td>
      <td>United States</td>
      <td>2001/2/9 17:43</td>
      <td>2001/4/9 20:01</td>
      <td>36.343330</td>
      <td>-88.850280</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2001/4/9 13:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Renee Elisabeth</td>
      <td>Tel Aviv</td>
      <td>Tel Aviv</td>
      <td>Israel</td>
      <td>2001/4/9 13:03</td>
      <td>2001/4/9 22:10</td>
      <td>32.066667</td>
      <td>34.766667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2001/4/9 14:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Aidan</td>
      <td>Chatou</td>
      <td>Ile-de-France</td>
      <td>France</td>
      <td>2006/3/8 4:22</td>
      <td>2001/5/9 1:17</td>
      <td>48.883333</td>
      <td>2.150000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2001/5/9 2:42</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Stacy</td>
      <td>New York</td>
      <td>NY</td>
      <td>United States</td>
      <td>2001/5/9 2:23</td>
      <td>2001/5/9 4:59</td>
      <td>40.714170</td>
      <td>-74.006390</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2001/5/9 5:39</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Heidi</td>
      <td>Eindhoven</td>
      <td>Noord-Brabant</td>
      <td>Netherlands</td>
      <td>2001/5/9 4:55</td>
      <td>2001/5/9 8:15</td>
      <td>51.450000</td>
      <td>5.466667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2001/5/9 10:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Georgia</td>
      <td>Eagle</td>
      <td>ID</td>
      <td>United States</td>
      <td>2011/11/8 15:53</td>
      <td>2001/5/9 10:05</td>
      <td>43.695560</td>
      <td>-116.353060</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2001/2/9 14:18</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Richard</td>
      <td>Riverside</td>
      <td>NJ</td>
      <td>United States</td>
      <td>2012/9/8 12:07</td>
      <td>2001/5/9 11:01</td>
      <td>40.032220</td>
      <td>-74.957780</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2001/4/9 1:05</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Leanne</td>
      <td>Julianstown</td>
      <td>Meath</td>
      <td>Ireland</td>
      <td>2001/4/9 0:00</td>
      <td>2001/5/9 13:36</td>
      <td>53.677222</td>
      <td>-6.319167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2001/5/9 11:37</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Janet</td>
      <td>Ottawa</td>
      <td>Ontario</td>
      <td>Canada</td>
      <td>2001/5/9 9:35</td>
      <td>2001/5/9 19:24</td>
      <td>45.416667</td>
      <td>-75.700000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2001/6/9 7:45</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Sabine</td>
      <td>London</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/6/9 7:00</td>
      <td>2001/6/9 9:17</td>
      <td>51.527210</td>
      <td>0.145590</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2001/2/9 7:35</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Hani</td>
      <td>Salt Lake City</td>
      <td>UT</td>
      <td>United States</td>
      <td>12/30/08 5:44</td>
      <td>2001/6/9 10:52</td>
      <td>40.760830</td>
      <td>-111.890280</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2001/6/9 12:56</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Jeremy</td>
      <td>Manchester</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/6/9 10:58</td>
      <td>2001/6/9 13:31</td>
      <td>53.500000</td>
      <td>-2.216667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2001/1/9 11:05</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Janis</td>
      <td>Ballynora</td>
      <td>Cork</td>
      <td>Ireland</td>
      <td>2012/10/7 12:37</td>
      <td>2001/7/9 1:52</td>
      <td>51.863056</td>
      <td>-8.580000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2001/6/9 7:18</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>asuman</td>
      <td>Chula Vista</td>
      <td>CA</td>
      <td>United States</td>
      <td>2001/6/9 7:07</td>
      <td>2001/7/9 7:08</td>
      <td>32.640000</td>
      <td>-117.083330</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2001/2/9 1:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Lena</td>
      <td>Kuopio</td>
      <td>Ita-Suomen Laani</td>
      <td>Finland</td>
      <td>12/31/08 2:48</td>
      <td>2001/7/9 10:20</td>
      <td>62.900000</td>
      <td>27.683333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2001/7/9 8:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Bryan Kerrene</td>
      <td>New York</td>
      <td>NY</td>
      <td>United States</td>
      <td>2001/7/9 7:39</td>
      <td>2001/7/9 12:38</td>
      <td>40.714170</td>
      <td>-74.006390</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2001/2/9 2:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>chris</td>
      <td>London</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/3/8 7:23</td>
      <td>2001/7/9 13:14</td>
      <td>51.527210</td>
      <td>0.145590</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2001/1/9 20:21</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Maxine</td>
      <td>Morton</td>
      <td>IL</td>
      <td>United States</td>
      <td>10/24/08 6:48</td>
      <td>2001/7/9 20:49</td>
      <td>40.612780</td>
      <td>-89.459170</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2001/8/9 0:42</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Family</td>
      <td>Los Gatos</td>
      <td>CA</td>
      <td>United States</td>
      <td>2001/8/9 0:28</td>
      <td>2001/8/9 3:39</td>
      <td>37.226670</td>
      <td>-121.973610</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>30</th>
      <td>2001/8/9 3:56</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Katherine</td>
      <td>New York</td>
      <td>NY</td>
      <td>United States</td>
      <td>2001/8/9 3:33</td>
      <td>2001/8/9 6:19</td>
      <td>40.714170</td>
      <td>-74.006390</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>32</th>
      <td>2001/8/9 1:59</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>SYLVIA</td>
      <td>Vesenaz</td>
      <td>Geneve</td>
      <td>Switzerland</td>
      <td>11/28/07 11:56</td>
      <td>2001/8/9 7:20</td>
      <td>46.233333</td>
      <td>6.200000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>33</th>
      <td>2001/3/9 9:03</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Sheila</td>
      <td>Brooklyn</td>
      <td>NY</td>
      <td>United States</td>
      <td>2001/3/9 8:47</td>
      <td>2001/8/9 10:38</td>
      <td>40.650000</td>
      <td>-73.950000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>34</th>
      <td>2001/5/9 13:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Stephanie</td>
      <td>Badhoevedorp</td>
      <td>Noord-Holland</td>
      <td>Netherlands</td>
      <td>2001/5/9 12:45</td>
      <td>2001/8/9 11:45</td>
      <td>52.333333</td>
      <td>4.783333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>35</th>
      <td>2001/6/9 7:46</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Kelly</td>
      <td>Reston</td>
      <td>VA</td>
      <td>United States</td>
      <td>2001/6/9 7:30</td>
      <td>2001/8/9 12:40</td>
      <td>38.968610</td>
      <td>-77.341390</td>
      <td>1200</td>
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
    </tr>
    <tr>
      <th>960</th>
      <td>1/25/09 11:52</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Gloria Gail</td>
      <td>WalcProduct3ee</td>
      <td>Tyrol</td>
      <td>Austria</td>
      <td>1/25/09 5:03</td>
      <td>2/27/09 5:37</td>
      <td>47.650000</td>
      <td>12.316667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>961</th>
      <td>2001/10/9 4:12</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Gloria Gail</td>
      <td>Foxrock</td>
      <td>Dublin</td>
      <td>Ireland</td>
      <td>2001/7/9 7:39</td>
      <td>2/27/09 6:33</td>
      <td>53.266667</td>
      <td>-6.174167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>962</th>
      <td>2001/10/9 9:32</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Cheryl</td>
      <td>Hilton Head</td>
      <td>SC</td>
      <td>United States</td>
      <td>2001/10/5 21:39</td>
      <td>2/27/09 7:33</td>
      <td>32.216110</td>
      <td>-80.752780</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>963</th>
      <td>1/22/09 12:45</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Frank and Christelle</td>
      <td>Valley Center</td>
      <td>CA</td>
      <td>United States</td>
      <td>1/22/09 10:25</td>
      <td>2/27/09 10:49</td>
      <td>33.218330</td>
      <td>-117.033330</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>964</th>
      <td>2001/6/9 18:11</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Triona</td>
      <td>Swampscott</td>
      <td>MA</td>
      <td>United States</td>
      <td>2006/9/6 8:57</td>
      <td>2/27/09 13:00</td>
      <td>42.470830</td>
      <td>-70.918060</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>965</th>
      <td>1/19/09 5:56</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Allison</td>
      <td>Edinburgh</td>
      <td>Scotland</td>
      <td>United Kingdom</td>
      <td>7/27/08 11:58</td>
      <td>2/27/09 14:35</td>
      <td>55.950000</td>
      <td>-3.200000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>967</th>
      <td>1/14/09 8:38</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>jingyan</td>
      <td>Bristol</td>
      <td>RI</td>
      <td>United States</td>
      <td>2003/12/7 15:14</td>
      <td>2/27/09 17:13</td>
      <td>41.676940</td>
      <td>-71.266670</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>969</th>
      <td>2001/7/9 18:15</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Selma</td>
      <td>Greenville</td>
      <td>TX</td>
      <td>United States</td>
      <td>2001/5/9 18:16</td>
      <td>2/27/09 19:07</td>
      <td>33.138330</td>
      <td>-96.110560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>970</th>
      <td>2001/3/9 21:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Doug and Tina</td>
      <td>Pls Vrds Est</td>
      <td>CA</td>
      <td>United States</td>
      <td>12/24/07 22:59</td>
      <td>2/27/09 21:40</td>
      <td>33.800560</td>
      <td>-118.389170</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>971</th>
      <td>2001/4/9 5:13</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Lauren</td>
      <td>Hradec Kralove</td>
      <td>East Bohemia</td>
      <td>Czech Republic</td>
      <td>2003/5/6 0:51</td>
      <td>2/27/09 23:30</td>
      <td>50.211667</td>
      <td>15.844167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>972</th>
      <td>2001/4/9 9:28</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Jen</td>
      <td>Maidstone</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>7/18/05 14:17</td>
      <td>2/28/09 2:28</td>
      <td>51.266667</td>
      <td>0.516667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>973</th>
      <td>2001/2/9 4:34</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>gladys</td>
      <td>Saint Albans</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/10/6 4:20</td>
      <td>2/28/09 3:43</td>
      <td>51.750000</td>
      <td>-0.333333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>974</th>
      <td>1/22/09 11:10</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Gustavo</td>
      <td>Voluntari</td>
      <td>Bucuresti</td>
      <td>Romania</td>
      <td>7/28/08 11:12</td>
      <td>2/28/09 7:52</td>
      <td>44.466667</td>
      <td>26.133333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>975</th>
      <td>2001/7/9 12:06</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Erica</td>
      <td>Nadur</td>
      <td></td>
      <td>Malta</td>
      <td>3/30/06 2:02</td>
      <td>2/28/09 7:59</td>
      <td>36.037778</td>
      <td>14.294167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>976</th>
      <td>1/29/09 13:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Hale</td>
      <td>Morrison</td>
      <td>CO</td>
      <td>United States</td>
      <td>2011/3/5 18:14</td>
      <td>2/28/09 8:27</td>
      <td>39.653610</td>
      <td>-105.190560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>977</th>
      <td>1/27/09 2:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Rosemary</td>
      <td>Cobham</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/27/09 2:50</td>
      <td>2/28/09 9:22</td>
      <td>51.383333</td>
      <td>0.400000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>978</th>
      <td>2001/7/9 13:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Darian</td>
      <td>Izmir</td>
      <td>Izmir</td>
      <td>Turkey</td>
      <td>8/26/08 7:33</td>
      <td>2/28/09 9:54</td>
      <td>38.407222</td>
      <td>27.150278</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>979</th>
      <td>1/23/09 10:04</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Kevin</td>
      <td>Hollywood</td>
      <td>CA</td>
      <td>United States</td>
      <td>5/30/06 20:25</td>
      <td>2/28/09 9:59</td>
      <td>34.098330</td>
      <td>-118.325830</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>980</th>
      <td>1/19/09 4:55</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Alyssa</td>
      <td>Brighton</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2/19/08 9:27</td>
      <td>2/28/09 10:06</td>
      <td>50.833333</td>
      <td>-0.150000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>984</th>
      <td>1/24/09 12:00</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>T</td>
      <td>El Escorial</td>
      <td>Madrid</td>
      <td>Spain</td>
      <td>12/30/08 15:19</td>
      <td>2/28/09 15:17</td>
      <td>40.583333</td>
      <td>-4.116667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>985</th>
      <td>1/28/09 11:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>christal</td>
      <td>Morrison</td>
      <td>CO</td>
      <td>United States</td>
      <td>6/20/04 17:16</td>
      <td>2/28/09 17:18</td>
      <td>39.653610</td>
      <td>-105.190560</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>986</th>
      <td>2001/7/9 17:48</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Alex</td>
      <td>Augusta</td>
      <td>GA</td>
      <td>United States</td>
      <td>2006/10/5 20:25</td>
      <td>2/28/09 19:57</td>
      <td>33.517220</td>
      <td>-82.075830</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>989</th>
      <td>1/26/09 11:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>smith</td>
      <td>Lahti</td>
      <td>Etela-Suomen Laani</td>
      <td>Finland</td>
      <td>2001/4/9 5:25</td>
      <td>2003/1/9 0:39</td>
      <td>60.966667</td>
      <td>25.666667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>990</th>
      <td>2001/5/9 13:23</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Macy</td>
      <td>Inner City</td>
      <td>Vienna</td>
      <td>Austria</td>
      <td>2001/5/9 11:28</td>
      <td>2003/1/9 2:28</td>
      <td>48.216667</td>
      <td>16.366667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>991</th>
      <td>1/26/09 13:41</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Lesleigh</td>
      <td>Baden</td>
      <td>Aargau</td>
      <td>Switzerland</td>
      <td>10/23/05 9:23</td>
      <td>2003/1/9 3:11</td>
      <td>47.466667</td>
      <td>8.300000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>992</th>
      <td>1/20/09 10:42</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Diners</td>
      <td>esther</td>
      <td>Huddersfield</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/20/09 9:15</td>
      <td>2003/1/9 3:29</td>
      <td>53.650000</td>
      <td>-1.783333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>993</th>
      <td>1/22/09 14:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Hans-Joerg</td>
      <td>Belfast</td>
      <td>Northern Ireland</td>
      <td>United Kingdom</td>
      <td>2011/10/8 12:15</td>
      <td>2003/1/9 3:37</td>
      <td>54.583333</td>
      <td>-5.933333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2001/1/9 4:24</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Amex</td>
      <td>Pamela</td>
      <td>Skaneateles</td>
      <td>NY</td>
      <td>United States</td>
      <td>12/28/08 17:28</td>
      <td>2003/1/9 7:21</td>
      <td>42.946940</td>
      <td>-76.429440</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2001/8/9 11:55</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>julie</td>
      <td>Haverhill</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>11/29/06 13:31</td>
      <td>2003/1/9 7:28</td>
      <td>52.083333</td>
      <td>0.433333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2001/12/9 21:30</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Julia</td>
      <td>Madison</td>
      <td>WI</td>
      <td>United States</td>
      <td>11/17/08 22:24</td>
      <td>2003/1/9 10:14</td>
      <td>43.073060</td>
      <td>-89.401110</td>
      <td>1200</td>
    </tr>
  </tbody>
</table>
<p>864 rows × 13 columns</p>
</div>




```python
df.loc[(df.Latitude>30) & (df.Longitude >0) ,:].reset_index()
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
      <th>index</th>
      <th>Transaction_date</th>
      <th>Product</th>
      <th>Price</th>
      <th>Payment_Type</th>
      <th>Name</th>
      <th>City</th>
      <th>State</th>
      <th>Country</th>
      <th>Account_Created</th>
      <th>Last_Login</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Price2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8</td>
      <td>2001/4/9 13:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Renee Elisabeth</td>
      <td>Tel Aviv</td>
      <td>Tel Aviv</td>
      <td>Israel</td>
      <td>2001/4/9 13:03</td>
      <td>2001/4/9 22:10</td>
      <td>32.066667</td>
      <td>34.766667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
      <td>2001/4/9 14:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Aidan</td>
      <td>Chatou</td>
      <td>Ile-de-France</td>
      <td>France</td>
      <td>2006/3/8 4:22</td>
      <td>2001/5/9 1:17</td>
      <td>48.883333</td>
      <td>2.150000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11</td>
      <td>2001/5/9 5:39</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Heidi</td>
      <td>Eindhoven</td>
      <td>Noord-Brabant</td>
      <td>Netherlands</td>
      <td>2001/5/9 4:55</td>
      <td>2001/5/9 8:15</td>
      <td>51.450000</td>
      <td>5.466667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>3</th>
      <td>18</td>
      <td>2001/6/9 7:45</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Sabine</td>
      <td>London</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/6/9 7:00</td>
      <td>2001/6/9 9:17</td>
      <td>51.527210</td>
      <td>0.145590</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>4</th>
      <td>24</td>
      <td>2001/2/9 1:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Lena</td>
      <td>Kuopio</td>
      <td>Ita-Suomen Laani</td>
      <td>Finland</td>
      <td>12/31/08 2:48</td>
      <td>2001/7/9 10:20</td>
      <td>62.900000</td>
      <td>27.683333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>5</th>
      <td>27</td>
      <td>2001/2/9 2:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>chris</td>
      <td>London</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/3/8 7:23</td>
      <td>2001/7/9 13:14</td>
      <td>51.527210</td>
      <td>0.145590</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>6</th>
      <td>32</td>
      <td>2001/8/9 1:59</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>SYLVIA</td>
      <td>Vesenaz</td>
      <td>Geneve</td>
      <td>Switzerland</td>
      <td>11/28/07 11:56</td>
      <td>2001/8/9 7:20</td>
      <td>46.233333</td>
      <td>6.200000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>7</th>
      <td>34</td>
      <td>2001/5/9 13:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Stephanie</td>
      <td>Badhoevedorp</td>
      <td>Noord-Holland</td>
      <td>Netherlands</td>
      <td>2001/5/9 12:45</td>
      <td>2001/8/9 11:45</td>
      <td>52.333333</td>
      <td>4.783333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>8</th>
      <td>42</td>
      <td>2001/3/9 13:24</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Mehmet Fatih</td>
      <td>Helsingor</td>
      <td>Frederiksborg</td>
      <td>Denmark</td>
      <td>2001/3/9 12:47</td>
      <td>2001/9/9 11:14</td>
      <td>56.033333</td>
      <td>12.616667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>9</th>
      <td>47</td>
      <td>2001/3/9 13:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>simone</td>
      <td>Kobenhavn</td>
      <td>Kobenhavn</td>
      <td>Denmark</td>
      <td>10/31/08 0:31</td>
      <td>2001/10/9 13:24</td>
      <td>55.666667</td>
      <td>12.583333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>10</th>
      <td>56</td>
      <td>2001/11/9 14:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Stephanie</td>
      <td>Brussels</td>
      <td>Brussels (Bruxelles)</td>
      <td>Belgium</td>
      <td>2001/11/9 13:39</td>
      <td>2001/11/9 13:39</td>
      <td>50.833333</td>
      <td>4.333333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>11</th>
      <td>60</td>
      <td>2001/5/9 0:31</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Bonnie</td>
      <td>Saltsjobaden</td>
      <td>Stockholm</td>
      <td>Sweden</td>
      <td>2001/4/9 23:45</td>
      <td>2001/12/9 0:37</td>
      <td>59.283333</td>
      <td>18.300000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>12</th>
      <td>64</td>
      <td>2001/7/9 0:12</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Deirdre</td>
      <td>Lausanne</td>
      <td>Vaud</td>
      <td>Switzerland</td>
      <td>2012/1/8 6:25</td>
      <td>2001/12/9 6:55</td>
      <td>46.533333</td>
      <td>6.666667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>13</th>
      <td>67</td>
      <td>2001/11/9 11:33</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Stefan</td>
      <td>Stavanger</td>
      <td>Rogaland</td>
      <td>Norway</td>
      <td>2001/11/9 9:02</td>
      <td>2001/12/9 10:37</td>
      <td>58.966667</td>
      <td>5.750000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>14</th>
      <td>70</td>
      <td>2001/5/9 13:52</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Tammy</td>
      <td>Morges</td>
      <td>Vaud</td>
      <td>Switzerland</td>
      <td>2001/5/9 5:55</td>
      <td>2001/12/9 14:04</td>
      <td>46.516667</td>
      <td>6.500000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>15</th>
      <td>75</td>
      <td>2001/12/9 13:41</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Eric</td>
      <td>Gasperich</td>
      <td>Luxembourg</td>
      <td>Luxembourg</td>
      <td>2001/12/9 13:16</td>
      <td>1/13/09 1:03</td>
      <td>49.585556</td>
      <td>6.123056</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>16</th>
      <td>77</td>
      <td>1/13/09 5:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Robin</td>
      <td>Milan</td>
      <td>Lombardy</td>
      <td>Italy</td>
      <td>10/15/08 5:31</td>
      <td>1/13/09 5:55</td>
      <td>45.466667</td>
      <td>9.200000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>17</th>
      <td>79</td>
      <td>2001/8/9 13:14</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Dr. Claudia</td>
      <td>Oslo</td>
      <td>Oslo</td>
      <td>Norway</td>
      <td>2001/8/9 12:47</td>
      <td>1/13/09 10:49</td>
      <td>59.916667</td>
      <td>10.750000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>18</th>
      <td>85</td>
      <td>2001/5/9 8:58</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Marcia</td>
      <td>Telgte</td>
      <td>Nordrhein-Westfalen</td>
      <td>Germany</td>
      <td>2009/1/8 3:39</td>
      <td>1/14/09 2:07</td>
      <td>52.333333</td>
      <td>7.900000</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>19</th>
      <td>88</td>
      <td>2001/2/9 12:18</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Alice</td>
      <td>Nakskov</td>
      <td>Storstrom</td>
      <td>Denmark</td>
      <td>2012/5/7 11:37</td>
      <td>1/14/09 4:05</td>
      <td>54.833333</td>
      <td>11.150000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>20</th>
      <td>90</td>
      <td>2001/6/9 17:15</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Andrea</td>
      <td>Bubuieci</td>
      <td>Chisinau</td>
      <td>Moldova</td>
      <td>12/24/08 17:31</td>
      <td>1/14/09 10:27</td>
      <td>46.985000</td>
      <td>28.942500</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>21</th>
      <td>103</td>
      <td>1/15/09 3:43</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Stephanie</td>
      <td>Rouen</td>
      <td>Upper Normandy</td>
      <td>France</td>
      <td>12/26/08 9:01</td>
      <td>1/15/09 5:39</td>
      <td>49.433333</td>
      <td>1.083333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>22</th>
      <td>112</td>
      <td>2001/1/9 5:04</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Regina</td>
      <td>Glimmen</td>
      <td>Groningen</td>
      <td>Netherlands</td>
      <td>12/16/02 4:09</td>
      <td>1/15/09 10:50</td>
      <td>53.133333</td>
      <td>6.633333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>23</th>
      <td>115</td>
      <td>2001/12/9 9:43</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Petra</td>
      <td>Bergen</td>
      <td>Nordrhein-Westfalen</td>
      <td>Germany</td>
      <td>2001/7/9 8:39</td>
      <td>1/15/09 12:14</td>
      <td>51.716667</td>
      <td>6.500000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>24</th>
      <td>123</td>
      <td>2001/7/9 7:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Jocelyn</td>
      <td>Bruxelles</td>
      <td>Brussels (Bruxelles)</td>
      <td>Belgium</td>
      <td>6/30/08 9:33</td>
      <td>1/16/09 8:54</td>
      <td>50.833333</td>
      <td>4.333333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>25</th>
      <td>127</td>
      <td>2001/2/9 0:50</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Sam</td>
      <td>Tesvikiye</td>
      <td>Istanbul</td>
      <td>Turkey</td>
      <td>2001/2/9 0:10</td>
      <td>1/17/09 1:57</td>
      <td>40.616667</td>
      <td>29.066667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>26</th>
      <td>135</td>
      <td>1/17/09 12:59</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Linda</td>
      <td>Den Haag</td>
      <td>Zuid-Holland</td>
      <td>Netherlands</td>
      <td>10/29/08 13:09</td>
      <td>1/17/09 13:07</td>
      <td>52.083333</td>
      <td>4.300000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>27</th>
      <td>139</td>
      <td>2001/1/9 3:51</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>sunny</td>
      <td>Amsterdam</td>
      <td>Noord-Holland</td>
      <td>Netherlands</td>
      <td>9/14/05 22:53</td>
      <td>1/17/09 22:34</td>
      <td>52.350000</td>
      <td>4.916667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>28</th>
      <td>142</td>
      <td>2001/1/9 1:51</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Si</td>
      <td>Holte</td>
      <td>Kobenhavn</td>
      <td>Denmark</td>
      <td>12/14/05 15:46</td>
      <td>1/18/09 4:44</td>
      <td>55.816667</td>
      <td>12.466667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>29</th>
      <td>143</td>
      <td>1/18/09 6:30</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Sherri</td>
      <td>Freienbach</td>
      <td>Schwyz</td>
      <td>Switzerland</td>
      <td>6/22/08 14:10</td>
      <td>1/18/09 6:21</td>
      <td>47.200000</td>
      <td>8.750000</td>
      <td>1200</td>
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
    </tr>
    <tr>
      <th>211</th>
      <td>889</td>
      <td>2001/5/9 15:15</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Amy</td>
      <td>Ashford</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>8/18/05 2:04</td>
      <td>2/24/09 10:35</td>
      <td>51.133333</td>
      <td>0.883333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>212</th>
      <td>891</td>
      <td>1/25/09 9:27</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>erin</td>
      <td>London</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2009/4/6 14:35</td>
      <td>2/24/09 13:37</td>
      <td>51.527210</td>
      <td>0.145590</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>213</th>
      <td>892</td>
      <td>2001/5/9 6:12</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Tracy</td>
      <td>Lucca</td>
      <td>Tuscany</td>
      <td>Italy</td>
      <td>2001/4/9 6:19</td>
      <td>2/24/09 13:56</td>
      <td>43.833333</td>
      <td>10.483333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>214</th>
      <td>897</td>
      <td>1/19/09 10:47</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>David</td>
      <td>Stavenger</td>
      <td>Rogaland</td>
      <td>Norway</td>
      <td>1/13/09 13:53</td>
      <td>2/25/09 0:40</td>
      <td>58.966667</td>
      <td>5.750000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>215</th>
      <td>898</td>
      <td>2001/8/9 2:49</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Caroline</td>
      <td>Begnins</td>
      <td>Vaud</td>
      <td>Switzerland</td>
      <td>2001/7/9 4:14</td>
      <td>2/25/09 1:37</td>
      <td>46.433333</td>
      <td>6.250000</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>216</th>
      <td>900</td>
      <td>2001/11/9 0:15</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Chris</td>
      <td>Den Haag</td>
      <td>Zuid-Holland</td>
      <td>Netherlands</td>
      <td>2005/7/7 4:07</td>
      <td>2/25/09 4:04</td>
      <td>52.083333</td>
      <td>4.300000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>217</th>
      <td>901</td>
      <td>1/16/09 5:12</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Karen</td>
      <td>Berikon</td>
      <td>Aargau</td>
      <td>Switzerland</td>
      <td>10/19/07 12:31</td>
      <td>2/25/09 5:12</td>
      <td>47.350000</td>
      <td>8.383333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>218</th>
      <td>905</td>
      <td>1/23/09 5:52</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Tary</td>
      <td>Zug</td>
      <td>Zug</td>
      <td>Switzerland</td>
      <td>1/23/09 1:22</td>
      <td>2/25/09 9:40</td>
      <td>47.166667</td>
      <td>8.516667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>219</th>
      <td>909</td>
      <td>1/22/09 12:56</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Laleh</td>
      <td>Aasgaardstrand</td>
      <td>Vestfold</td>
      <td>Norway</td>
      <td>1/20/09 13:13</td>
      <td>2/25/09 12:03</td>
      <td>59.348889</td>
      <td>10.467500</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>220</th>
      <td>910</td>
      <td>1/16/09 13:35</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Michael</td>
      <td>Milano</td>
      <td>Lombardy</td>
      <td>Italy</td>
      <td>1/16/09 12:43</td>
      <td>2/25/09 13:59</td>
      <td>45.466667</td>
      <td>9.200000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>221</th>
      <td>911</td>
      <td>1/13/09 9:26</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Kerry</td>
      <td>Anieres</td>
      <td>Geneve</td>
      <td>Switzerland</td>
      <td>1/24/06 13:15</td>
      <td>2/25/09 14:05</td>
      <td>46.283333</td>
      <td>6.216667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>222</th>
      <td>917</td>
      <td>1/28/09 14:09</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>giovanna</td>
      <td>Pruszkow</td>
      <td>Mazowieckie</td>
      <td>Poland</td>
      <td>1/28/09 13:40</td>
      <td>2/25/09 16:19</td>
      <td>52.166667</td>
      <td>20.833333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>223</th>
      <td>921</td>
      <td>1/26/09 22:45</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Anjan</td>
      <td>Tokyo</td>
      <td>Tokyo</td>
      <td>Japan</td>
      <td>5/15/08 19:33</td>
      <td>2/25/09 17:34</td>
      <td>35.685000</td>
      <td>139.751389</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>224</th>
      <td>925</td>
      <td>2001/2/9 4:21</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Elaine</td>
      <td>Tranby</td>
      <td>Buskerud</td>
      <td>Norway</td>
      <td>7/30/07 11:42</td>
      <td>2/26/09 3:18</td>
      <td>59.816667</td>
      <td>10.250000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>225</th>
      <td>932</td>
      <td>1/17/09 7:56</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Diners</td>
      <td>Michel</td>
      <td>Lipari</td>
      <td>Sicilia</td>
      <td>Italy</td>
      <td>1/17/09 7:25</td>
      <td>2/26/09 7:32</td>
      <td>38.466667</td>
      <td>14.950000</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>226</th>
      <td>933</td>
      <td>1/17/09 7:58</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Diners</td>
      <td>natalie</td>
      <td>Lipari</td>
      <td>Sicilia</td>
      <td>Italy</td>
      <td>1/17/09 7:25</td>
      <td>2/26/09 7:32</td>
      <td>38.466667</td>
      <td>14.950000</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>227</th>
      <td>934</td>
      <td>1/18/09 4:32</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>jure</td>
      <td>Lipari</td>
      <td>Sicilia</td>
      <td>Italy</td>
      <td>1/17/09 7:25</td>
      <td>2/26/09 7:32</td>
      <td>38.466667</td>
      <td>14.950000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>228</th>
      <td>948</td>
      <td>1/31/09 4:50</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Detlev</td>
      <td>Taby</td>
      <td>Stockholm</td>
      <td>Sweden</td>
      <td>2001/12/9 1:03</td>
      <td>2/26/09 13:12</td>
      <td>59.500000</td>
      <td>18.050000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>229</th>
      <td>958</td>
      <td>1/22/09 3:57</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Parth</td>
      <td>Oegstgeest</td>
      <td>Zuid-Holland</td>
      <td>Netherlands</td>
      <td>1/20/09 14:36</td>
      <td>2/27/09 1:59</td>
      <td>52.183333</td>
      <td>4.466667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>230</th>
      <td>960</td>
      <td>1/25/09 11:52</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Gloria Gail</td>
      <td>WalcProduct3ee</td>
      <td>Tyrol</td>
      <td>Austria</td>
      <td>1/25/09 5:03</td>
      <td>2/27/09 5:37</td>
      <td>47.650000</td>
      <td>12.316667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>231</th>
      <td>971</td>
      <td>2001/4/9 5:13</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Lauren</td>
      <td>Hradec Kralove</td>
      <td>East Bohemia</td>
      <td>Czech Republic</td>
      <td>2003/5/6 0:51</td>
      <td>2/27/09 23:30</td>
      <td>50.211667</td>
      <td>15.844167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>232</th>
      <td>972</td>
      <td>2001/4/9 9:28</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Jen</td>
      <td>Maidstone</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>7/18/05 14:17</td>
      <td>2/28/09 2:28</td>
      <td>51.266667</td>
      <td>0.516667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>233</th>
      <td>974</td>
      <td>1/22/09 11:10</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Gustavo</td>
      <td>Voluntari</td>
      <td>Bucuresti</td>
      <td>Romania</td>
      <td>7/28/08 11:12</td>
      <td>2/28/09 7:52</td>
      <td>44.466667</td>
      <td>26.133333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>234</th>
      <td>975</td>
      <td>2001/7/9 12:06</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Erica</td>
      <td>Nadur</td>
      <td></td>
      <td>Malta</td>
      <td>3/30/06 2:02</td>
      <td>2/28/09 7:59</td>
      <td>36.037778</td>
      <td>14.294167</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>235</th>
      <td>977</td>
      <td>1/27/09 2:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Rosemary</td>
      <td>Cobham</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/27/09 2:50</td>
      <td>2/28/09 9:22</td>
      <td>51.383333</td>
      <td>0.400000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>236</th>
      <td>978</td>
      <td>2001/7/9 13:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Darian</td>
      <td>Izmir</td>
      <td>Izmir</td>
      <td>Turkey</td>
      <td>8/26/08 7:33</td>
      <td>2/28/09 9:54</td>
      <td>38.407222</td>
      <td>27.150278</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>237</th>
      <td>989</td>
      <td>1/26/09 11:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>smith</td>
      <td>Lahti</td>
      <td>Etela-Suomen Laani</td>
      <td>Finland</td>
      <td>2001/4/9 5:25</td>
      <td>2003/1/9 0:39</td>
      <td>60.966667</td>
      <td>25.666667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>238</th>
      <td>990</td>
      <td>2001/5/9 13:23</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Macy</td>
      <td>Inner City</td>
      <td>Vienna</td>
      <td>Austria</td>
      <td>2001/5/9 11:28</td>
      <td>2003/1/9 2:28</td>
      <td>48.216667</td>
      <td>16.366667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>239</th>
      <td>991</td>
      <td>1/26/09 13:41</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Lesleigh</td>
      <td>Baden</td>
      <td>Aargau</td>
      <td>Switzerland</td>
      <td>10/23/05 9:23</td>
      <td>2003/1/9 3:11</td>
      <td>47.466667</td>
      <td>8.300000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>240</th>
      <td>996</td>
      <td>2001/8/9 11:55</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>julie</td>
      <td>Haverhill</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>11/29/06 13:31</td>
      <td>2003/1/9 7:28</td>
      <td>52.083333</td>
      <td>0.433333</td>
      <td>1200</td>
    </tr>
  </tbody>
</table>
<p>241 rows × 14 columns</p>
</div>




```python
# 3.2 where Country like 'Aus%'
df.loc[df.Country.str.startswith('Aus')]
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
      <th>Transaction_date</th>
      <th>Product</th>
      <th>Price</th>
      <th>Payment_Type</th>
      <th>Name</th>
      <th>City</th>
      <th>State</th>
      <th>Country</th>
      <th>Account_Created</th>
      <th>Last_Login</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Price2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>2001/3/9 14:44</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Gouya</td>
      <td>Echuca</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>9/25/05 21:13</td>
      <td>2001/3/9 14:22</td>
      <td>-36.133333</td>
      <td>144.750000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>36</th>
      <td>2001/5/9 20:00</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>James</td>
      <td>Burpengary</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>2012/10/8 19:53</td>
      <td>2001/8/9 17:58</td>
      <td>-27.166667</td>
      <td>152.950000</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>51</th>
      <td>2001/6/9 1:20</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Frank</td>
      <td>Melbourne</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>2001/2/9 17:51</td>
      <td>2001/10/9 18:27</td>
      <td>-37.816667</td>
      <td>144.966667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>55</th>
      <td>2001/11/9 2:04</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>chris</td>
      <td>Gold Coast</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>2001/11/9 0:33</td>
      <td>2001/11/9 2:11</td>
      <td>-28.000000</td>
      <td>153.433333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>120</th>
      <td>2001/12/9 1:37</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>IMAN</td>
      <td>Brisbane</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>2001/12/9 1:26</td>
      <td>1/15/09 17:54</td>
      <td>-27.500000</td>
      <td>153.016667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>186</th>
      <td>2001/4/9 1:38</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>jeremy</td>
      <td>Charlestown</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>7/15/08 21:04</td>
      <td>1/20/09 1:08</td>
      <td>-32.950000</td>
      <td>151.666667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>199</th>
      <td>1/20/09 3:51</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Elizabeth</td>
      <td>The Grange</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>2011/12/8 3:34</td>
      <td>1/20/09 13:11</td>
      <td>-24.816667</td>
      <td>152.416667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>205</th>
      <td>2001/9/9 14:51</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Bob</td>
      <td>Sydney</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>2001/7/9 18:15</td>
      <td>1/21/09 0:29</td>
      <td>-33.883333</td>
      <td>151.216667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>207</th>
      <td>1/16/09 18:36</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Elizabeth</td>
      <td>Wollongong</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>2011/1/8 16:32</td>
      <td>1/21/09 1:49</td>
      <td>-34.433333</td>
      <td>150.883333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>215</th>
      <td>2001/2/9 2:28</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Morgan</td>
      <td>Coomera</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>2005/3/8 4:14</td>
      <td>1/21/09 16:37</td>
      <td>-27.883333</td>
      <td>153.300000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>223</th>
      <td>2001/11/9 22:22</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>STEPHANIE</td>
      <td>Mona Vale</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>12/30/08 17:48</td>
      <td>1/21/09 22:33</td>
      <td>-33.666667</td>
      <td>151.300000</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>251</th>
      <td>1/16/09 1:51</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Angela</td>
      <td>Vienna</td>
      <td>Vienna</td>
      <td>Austria</td>
      <td>1/16/09 1:38</td>
      <td>1/24/09 5:39</td>
      <td>48.200000</td>
      <td>16.366667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>280</th>
      <td>1/24/09 8:21</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>corina</td>
      <td>Neustift am Walde</td>
      <td>Vienna</td>
      <td>Austria</td>
      <td>7/19/05 12:42</td>
      <td>1/25/09 14:22</td>
      <td>48.250000</td>
      <td>16.300000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>281</th>
      <td>1/24/09 8:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>manon</td>
      <td>Neustift am Walde</td>
      <td>Vienna</td>
      <td>Austria</td>
      <td>7/19/05 12:42</td>
      <td>1/25/09 14:22</td>
      <td>48.250000</td>
      <td>16.300000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>326</th>
      <td>2001/7/9 10:03</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Emma</td>
      <td>Sydney</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>2012/1/8 6:09</td>
      <td>1/27/09 20:18</td>
      <td>-33.883333</td>
      <td>151.216667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>327</th>
      <td>1/18/09 3:46</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Marina</td>
      <td>Nerang</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>1/18/09 0:54</td>
      <td>1/27/09 23:52</td>
      <td>-27.983333</td>
      <td>153.333333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>389</th>
      <td>2001/1/9 8:09</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Nicole</td>
      <td>South Melbourne</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>12/30/08 0:55</td>
      <td>1/31/09 5:40</td>
      <td>-37.833333</td>
      <td>144.966667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>437</th>
      <td>1/30/09 17:33</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>nina</td>
      <td>Warwick</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>1/25/09 22:36</td>
      <td>2002/2/9 6:13</td>
      <td>-28.233333</td>
      <td>152.016667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>525</th>
      <td>2001/4/9 16:59</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Amy</td>
      <td>Parramatta</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>2001/3/9 22:35</td>
      <td>2002/5/9 22:44</td>
      <td>-33.816667</td>
      <td>151.000000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>527</th>
      <td>2001/6/9 5:10</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Astrid</td>
      <td>Altlengbach</td>
      <td>Lower Austria</td>
      <td>Austria</td>
      <td>6/24/08 0:49</td>
      <td>2002/6/9 0:37</td>
      <td>48.150000</td>
      <td>15.916667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>546</th>
      <td>2001/2/9 22:44</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>eva</td>
      <td>Gisborne</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>2012/3/6 15:36</td>
      <td>2002/6/9 20:03</td>
      <td>-37.483333</td>
      <td>144.583333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>562</th>
      <td>1/26/09 20:18</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>John</td>
      <td>Griffith</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>1/15/07 20:37</td>
      <td>2002/7/9 18:04</td>
      <td>-34.283333</td>
      <td>146.033333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>598</th>
      <td>2001/8/9 23:40</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Jacob</td>
      <td>Lindfield</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>2001/8/9 17:52</td>
      <td>2002/9/9 18:31</td>
      <td>-33.783333</td>
      <td>151.166667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>605</th>
      <td>1/24/09 18:30</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Ruangrote</td>
      <td>Melbourne</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>7/17/08 5:19</td>
      <td>2002/10/9 2:12</td>
      <td>-37.816667</td>
      <td>144.966667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>633</th>
      <td>1/14/09 6:35</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Eric</td>
      <td>Melbourne</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>7/25/08 7:02</td>
      <td>2002/11/9 2:05</td>
      <td>-37.816667</td>
      <td>144.966667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>635</th>
      <td>1/31/09 23:09</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Dawn</td>
      <td>Vaucluse</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>9/13/04 22:55</td>
      <td>2002/11/9 3:09</td>
      <td>-33.866667</td>
      <td>151.283333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>636</th>
      <td>1/21/09 14:34</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Tamara</td>
      <td>Klosterneuburg</td>
      <td>Lower Austria</td>
      <td>Austria</td>
      <td>1/21/09 14:12</td>
      <td>2002/11/9 3:19</td>
      <td>48.300000</td>
      <td>16.316667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>643</th>
      <td>1/24/09 3:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Michelle</td>
      <td>Lyndoch</td>
      <td>South Australia</td>
      <td>Australia</td>
      <td>9/26/08 19:23</td>
      <td>2002/11/9 15:05</td>
      <td>-34.616667</td>
      <td>138.883333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>652</th>
      <td>2001/12/9 23:35</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Lisa</td>
      <td>Perth</td>
      <td>Western Australia</td>
      <td>Australia</td>
      <td>2005/8/6 23:41</td>
      <td>2002/12/9 3:46</td>
      <td>-31.933333</td>
      <td>115.833333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>662</th>
      <td>2001/1/9 21:40</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Tina</td>
      <td>Anglesea</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>10/20/08 18:27</td>
      <td>2002/12/9 14:58</td>
      <td>-38.416667</td>
      <td>144.166667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>668</th>
      <td>1/22/09 14:32</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Sara</td>
      <td>Perth City</td>
      <td>Western Australia</td>
      <td>Australia</td>
      <td>2009/5/8 7:18</td>
      <td>2/13/09 3:50</td>
      <td>-31.933333</td>
      <td>115.833333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>677</th>
      <td>1/23/09 5:14</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Ellen Walton</td>
      <td>Melbourne</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>12/16/07 17:05</td>
      <td>2/13/09 15:28</td>
      <td>-37.816667</td>
      <td>144.966667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>703</th>
      <td>2001/3/9 14:17</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Kees en Valesca</td>
      <td>Scamander</td>
      <td>Tasmania</td>
      <td>Australia</td>
      <td>2001/3/9 13:53</td>
      <td>2/14/09 20:11</td>
      <td>-41.465000</td>
      <td>148.257222</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>707</th>
      <td>2001/4/9 17:34</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Dean</td>
      <td>Rockingham</td>
      <td>Western Australia</td>
      <td>Australia</td>
      <td>10/20/07 19:09</td>
      <td>2/15/09 2:14</td>
      <td>-32.283333</td>
      <td>115.716667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>746</th>
      <td>1/19/09 1:52</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Kirsten</td>
      <td>Melbourne</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>4/24/07 4:36</td>
      <td>2/17/09 1:20</td>
      <td>-37.816667</td>
      <td>144.966667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>774</th>
      <td>1/14/09 0:03</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Piret</td>
      <td>Bunbury</td>
      <td>Western Australia</td>
      <td>Australia</td>
      <td>6/16/08 18:22</td>
      <td>2/17/09 19:31</td>
      <td>-33.333333</td>
      <td>115.633333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>791</th>
      <td>1/20/09 13:54</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Elisabeth</td>
      <td>Birkdale</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>12/20/05 23:05</td>
      <td>2/18/09 23:07</td>
      <td>-27.483333</td>
      <td>153.216667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>792</th>
      <td>1/23/09 21:35</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Ann</td>
      <td>Brisbane</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>4/21/07 19:33</td>
      <td>2/18/09 23:12</td>
      <td>-27.500000</td>
      <td>153.016667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>893</th>
      <td>2001/6/9 2:41</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Polyxene</td>
      <td>Perth</td>
      <td>Western Australia</td>
      <td>Australia</td>
      <td>11/20/05 23:46</td>
      <td>2/24/09 16:04</td>
      <td>-31.933333</td>
      <td>115.833333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>960</th>
      <td>1/25/09 11:52</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Gloria Gail</td>
      <td>WalcProduct3ee</td>
      <td>Tyrol</td>
      <td>Austria</td>
      <td>1/25/09 5:03</td>
      <td>2/27/09 5:37</td>
      <td>47.650000</td>
      <td>12.316667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>968</th>
      <td>2001/2/9 17:24</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Diners</td>
      <td>clara</td>
      <td>Perth</td>
      <td>Western Australia</td>
      <td>Australia</td>
      <td>2001/1/9 21:20</td>
      <td>2/27/09 18:43</td>
      <td>-31.933333</td>
      <td>115.833333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>982</th>
      <td>2001/4/9 18:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>KELI</td>
      <td>Worongary</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>12/23/08 15:17</td>
      <td>2/28/09 14:00</td>
      <td>-28.050000</td>
      <td>153.350000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>987</th>
      <td>1/23/09 12:42</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Anke</td>
      <td>Avalon</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>2003/3/8 17:38</td>
      <td>2/28/09 22:26</td>
      <td>-33.633333</td>
      <td>151.333333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>988</th>
      <td>2001/7/9 19:48</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>TRICIA</td>
      <td>Sydney</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>9/21/08 20:49</td>
      <td>2003/1/9 0:14</td>
      <td>-33.883333</td>
      <td>151.216667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>990</th>
      <td>2001/5/9 13:23</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Macy</td>
      <td>Inner City</td>
      <td>Vienna</td>
      <td>Austria</td>
      <td>2001/5/9 11:28</td>
      <td>2003/1/9 2:28</td>
      <td>48.216667</td>
      <td>16.366667</td>
      <td>1200</td>
    </tr>
  </tbody>
</table>
</div>



## 3.1 Series.str 包含的常用方法
```
startwith
endwith
contains
upper
lower
find #找第一个目标字符串出现的下标
split
strip #去空格
replace
slice(0,12)#切片
match#正则匹配
extract#提取正则中的组到每一列
```


```python
df.City = df.City.str.strip() #去空格，格式化数据
```


```python
df.City
```




    0            Basildon
    1           Parkville
    2             Astoria
    3              Echuca
    4      Cahaba Heights
    5           Mickleton
    6              Peoria
    7              Martin
    8            Tel Aviv
    9              Chatou
    10           New York
    11          Eindhoven
    12       Shavano Park
    13              Eagle
    14          Riverside
    15        Julianstown
    16             Ottawa
    17          Hyderabad
    18             London
    19     Salt Lake City
    20         Manchester
    21          Ballynora
    22         Roodepoort
    23        Chula Vista
    24             Kuopio
    25         Sugar Land
    26           New York
    27             London
    28             Morton
    29          Los Gatos
                ...      
    968             Perth
    969        Greenville
    970      Pls Vrds Est
    971    Hradec Kralove
    972         Maidstone
    973      Saint Albans
    974         Voluntari
    975             Nadur
    976          Morrison
    977            Cobham
    978             Izmir
    979         Hollywood
    980          Brighton
    981            Hawera
    982         Worongary
    983         Atlantida
    984       El Escorial
    985          Morrison
    986           Augusta
    987            Avalon
    988            Sydney
    989             Lahti
    990        Inner City
    991             Baden
    992      Huddersfield
    993           Belfast
    994       Black River
    995       Skaneateles
    996         Haverhill
    997           Madison
    Name: City, Length: 998, dtype: object




```python
import locale

#将Price去逗号，再转为int形式
df.Price = df.Price.str.replace(',','')

df.Price = df.Price.apply(locate.atoi) #df.apply() 对每一行都运行参数
```


```python
# order by 排序
df.sort_values('Price',ascending=False)
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
      <th>Transaction_date</th>
      <th>Product</th>
      <th>Price</th>
      <th>Payment_Type</th>
      <th>Name</th>
      <th>City</th>
      <th>State</th>
      <th>Country</th>
      <th>Account_Created</th>
      <th>Last_Login</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Price2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>477</th>
      <td>1/30/09 7:42</td>
      <td>Product1</td>
      <td>250</td>
      <td>Visa</td>
      <td>Tabatha</td>
      <td>Altadena</td>
      <td>CA</td>
      <td>United States</td>
      <td>12/28/08 14:42</td>
      <td>2002/3/9 18:09</td>
      <td>34.189720</td>
      <td>-118.130280</td>
      <td>250</td>
    </tr>
    <tr>
      <th>294</th>
      <td>1/21/09 11:28</td>
      <td>Product1</td>
      <td>800</td>
      <td>Amex</td>
      <td>Heloise</td>
      <td>Arlington</td>
      <td>VA</td>
      <td>United States</td>
      <td>9/25/05 20:26</td>
      <td>1/26/09 6:23</td>
      <td>38.890280</td>
      <td>-77.084440</td>
      <td>800</td>
    </tr>
    <tr>
      <th>0</th>
      <td>2001/2/9 6:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>carolina</td>
      <td>Basildon</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2001/2/9 6:00</td>
      <td>2001/2/9 6:08</td>
      <td>51.500000</td>
      <td>-1.116667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>627</th>
      <td>2001/8/9 12:46</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Trine Marie</td>
      <td>Orillia</td>
      <td>Ontario</td>
      <td>Canada</td>
      <td>12/16/08 22:57</td>
      <td>2002/10/9 22:11</td>
      <td>44.600000</td>
      <td>-79.416667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>628</th>
      <td>1/29/09 16:07</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Kim</td>
      <td>Paris</td>
      <td>Ile-de-France</td>
      <td>France</td>
      <td>1/29/09 15:45</td>
      <td>2002/10/9 22:24</td>
      <td>48.866667</td>
      <td>2.333333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>629</th>
      <td>1/29/09 13:41</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>John</td>
      <td>San Jose</td>
      <td>CA</td>
      <td>United States</td>
      <td>1/14/04 21:59</td>
      <td>2002/10/9 23:58</td>
      <td>37.339440</td>
      <td>-121.893890</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>630</th>
      <td>2001/8/9 6:29</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Rich</td>
      <td>Ingelheim-Mitte</td>
      <td>Rhineland-Palatinate</td>
      <td>Germany</td>
      <td>3/24/06 6:21</td>
      <td>2002/10/9 23:59</td>
      <td>49.983333</td>
      <td>8.066667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>631</th>
      <td>2001/4/9 12:53</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Kayla</td>
      <td>Leamington Spa</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>2012/11/8 7:35</td>
      <td>2002/11/9 0:04</td>
      <td>52.300000</td>
      <td>-1.533333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>632</th>
      <td>1/14/09 12:55</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Richard and Comfort</td>
      <td>Regensdorf</td>
      <td>Zurich</td>
      <td>Switzerland</td>
      <td>2001/11/9 10:36</td>
      <td>2002/11/9 1:58</td>
      <td>47.433333</td>
      <td>8.466667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>633</th>
      <td>1/14/09 6:35</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Eric</td>
      <td>Melbourne</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>7/25/08 7:02</td>
      <td>2002/11/9 2:05</td>
      <td>-37.816667</td>
      <td>144.966667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>634</th>
      <td>1/27/09 13:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Melissa</td>
      <td>Geneve</td>
      <td>Geneve</td>
      <td>Switzerland</td>
      <td>2005/9/8 8:50</td>
      <td>2002/11/9 2:19</td>
      <td>46.200000</td>
      <td>6.166667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>635</th>
      <td>1/31/09 23:09</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Dawn</td>
      <td>Vaucluse</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>9/13/04 22:55</td>
      <td>2002/11/9 3:09</td>
      <td>-33.866667</td>
      <td>151.283333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>636</th>
      <td>1/21/09 14:34</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Tamara</td>
      <td>Klosterneuburg</td>
      <td>Lower Austria</td>
      <td>Austria</td>
      <td>1/21/09 14:12</td>
      <td>2002/11/9 3:19</td>
      <td>48.300000</td>
      <td>16.316667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>637</th>
      <td>1/16/09 8:28</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Ashley</td>
      <td>Rancho Cordova</td>
      <td>CA</td>
      <td>United States</td>
      <td>2001/9/9 12:13</td>
      <td>2002/11/9 8:34</td>
      <td>38.589170</td>
      <td>-121.301670</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>638</th>
      <td>2001/11/9 9:55</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>familly</td>
      <td>Creemore</td>
      <td>Ontario</td>
      <td>Canada</td>
      <td>2001/10/9 7:14</td>
      <td>2002/11/9 8:45</td>
      <td>44.316667</td>
      <td>-80.100000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>639</th>
      <td>2001/8/9 2:46</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Ken</td>
      <td>Sidcup</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>11/26/07 16:44</td>
      <td>2002/11/9 11:00</td>
      <td>51.416667</td>
      <td>0.116667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>640</th>
      <td>1/26/09 7:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Tori</td>
      <td>Minneapolis</td>
      <td>MN</td>
      <td>United States</td>
      <td>11/22/08 21:06</td>
      <td>2002/11/9 11:35</td>
      <td>44.980000</td>
      <td>-93.263610</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>642</th>
      <td>2001/9/9 8:35</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Precious</td>
      <td>Edmonton</td>
      <td>Alberta</td>
      <td>Canada</td>
      <td>2001/8/9 14:14</td>
      <td>2002/11/9 14:26</td>
      <td>53.550000</td>
      <td>-113.500000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>643</th>
      <td>1/24/09 3:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Michelle</td>
      <td>Lyndoch</td>
      <td>South Australia</td>
      <td>Australia</td>
      <td>9/26/08 19:23</td>
      <td>2002/11/9 15:05</td>
      <td>-34.616667</td>
      <td>138.883333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>644</th>
      <td>1/26/09 8:45</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Paula</td>
      <td>Larchmont</td>
      <td>NY</td>
      <td>United States</td>
      <td>2/15/06 17:21</td>
      <td>2002/11/9 17:12</td>
      <td>40.927780</td>
      <td>-73.752220</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>645</th>
      <td>1/23/09 10:45</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Stephanie</td>
      <td>Saint Charles</td>
      <td>IL</td>
      <td>United States</td>
      <td>1/23/09 8:46</td>
      <td>2002/11/9 17:57</td>
      <td>41.914170</td>
      <td>-88.308610</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>646</th>
      <td>1/28/09 8:50</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>kemp</td>
      <td>Brentwood</td>
      <td>TN</td>
      <td>United States</td>
      <td>1/28/09 8:42</td>
      <td>2002/11/9 18:41</td>
      <td>36.033060</td>
      <td>-86.782780</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>648</th>
      <td>2001/9/9 20:25</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Mona</td>
      <td>Kelowna</td>
      <td>British Columbia</td>
      <td>Canada</td>
      <td>2001/9/9 14:20</td>
      <td>2002/11/9 20:19</td>
      <td>49.900000</td>
      <td>-119.483333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>649</th>
      <td>1/15/09 21:53</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Caroline</td>
      <td>Toronto</td>
      <td>Ontario</td>
      <td>Canada</td>
      <td>2001/1/9 18:01</td>
      <td>2002/11/9 21:01</td>
      <td>43.666667</td>
      <td>-79.416667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>650</th>
      <td>2001/12/9 0:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Andrea</td>
      <td>Brondby Strand</td>
      <td>Kobenhavn</td>
      <td>Denmark</td>
      <td>2001/7/9 23:40</td>
      <td>2002/11/9 22:23</td>
      <td>55.616667</td>
      <td>12.350000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>651</th>
      <td>1/25/09 10:32</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Pilar</td>
      <td>Florence</td>
      <td>Tuscany</td>
      <td>Italy</td>
      <td>1/23/09 4:46</td>
      <td>2002/12/9 2:22</td>
      <td>43.766667</td>
      <td>11.250000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>626</th>
      <td>1/28/09 16:17</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Zoe</td>
      <td>Coventry</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/28/09 15:59</td>
      <td>2002/10/9 19:55</td>
      <td>52.416667</td>
      <td>-1.550000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>625</th>
      <td>1/19/09 11:05</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Bertrand</td>
      <td>North Caldwell</td>
      <td>NJ</td>
      <td>United States</td>
      <td>2010/3/8 5:55</td>
      <td>2002/10/9 18:16</td>
      <td>40.839720</td>
      <td>-74.276940</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>624</th>
      <td>2001/2/9 14:14</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Aaron</td>
      <td>Reading</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>11/16/08 15:49</td>
      <td>2002/10/9 16:38</td>
      <td>51.433333</td>
      <td>-1.000000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>623</th>
      <td>1/29/09 15:03</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Mary</td>
      <td>Auckland</td>
      <td>Auckland</td>
      <td>New Zealand</td>
      <td>2002/9/6 11:14</td>
      <td>2002/10/9 16:31</td>
      <td>-36.866667</td>
      <td>174.766667</td>
      <td>1200</td>
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
    </tr>
    <tr>
      <th>727</th>
      <td>1/19/09 4:23</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>don</td>
      <td>Cagliari</td>
      <td>Sardinia</td>
      <td>Italy</td>
      <td>1/13/08 11:41</td>
      <td>2/16/09 0:22</td>
      <td>39.216667</td>
      <td>9.116667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>868</th>
      <td>2001/6/9 20:39</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Christiane</td>
      <td>Mission</td>
      <td>British Columbia</td>
      <td>Canada</td>
      <td>2001/6/9 9:44</td>
      <td>2/23/09 8:55</td>
      <td>49.133333</td>
      <td>-122.300000</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>867</th>
      <td>2001/8/9 11:14</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Liz</td>
      <td>Langnau</td>
      <td>Zurich</td>
      <td>Switzerland</td>
      <td>2001/7/9 10:25</td>
      <td>2/23/09 7:17</td>
      <td>47.283333</td>
      <td>8.533333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>372</th>
      <td>1/29/09 10:09</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Jacqui</td>
      <td>Scottsdale</td>
      <td>AZ</td>
      <td>United States</td>
      <td>1/29/09 9:59</td>
      <td>1/29/09 12:58</td>
      <td>33.509170</td>
      <td>-111.898330</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>863</th>
      <td>1/15/09 15:56</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Charmain</td>
      <td>Cartersburg</td>
      <td>IN</td>
      <td>United States</td>
      <td>2001/2/8 10:51</td>
      <td>2/23/09 6:24</td>
      <td>39.698610</td>
      <td>-86.463610</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>620</th>
      <td>1/24/09 13:54</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Meredith</td>
      <td>Kloten</td>
      <td>Zurich</td>
      <td>Switzerland</td>
      <td>1/24/09 12:30</td>
      <td>2002/10/9 13:47</td>
      <td>47.450000</td>
      <td>8.583333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>901</th>
      <td>1/16/09 5:12</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Karen</td>
      <td>Berikon</td>
      <td>Aargau</td>
      <td>Switzerland</td>
      <td>10/19/07 12:31</td>
      <td>2/25/09 5:12</td>
      <td>47.350000</td>
      <td>8.383333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>290</th>
      <td>1/26/09 3:49</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Jane</td>
      <td>Biot</td>
      <td>Provence-Alpes-Cote d'Azur</td>
      <td>France</td>
      <td>2003/1/8 0:00</td>
      <td>1/26/09 3:18</td>
      <td>43.633333</td>
      <td>7.100000</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>546</th>
      <td>2001/2/9 22:44</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>eva</td>
      <td>Gisborne</td>
      <td>Victoria</td>
      <td>Australia</td>
      <td>2012/3/6 15:36</td>
      <td>2002/6/9 20:03</td>
      <td>-37.483333</td>
      <td>144.583333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>857</th>
      <td>2001/12/9 10:08</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Judy</td>
      <td>Washington</td>
      <td>DC</td>
      <td>United States</td>
      <td>5/31/08 12:03</td>
      <td>2/22/09 18:58</td>
      <td>38.895000</td>
      <td>-77.036670</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>752</th>
      <td>1/27/09 3:45</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>minjeong</td>
      <td>Bern</td>
      <td>Bern</td>
      <td>Switzerland</td>
      <td>1/27/09 2:39</td>
      <td>2/17/09 3:44</td>
      <td>46.916667</td>
      <td>7.466667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>195</th>
      <td>2001/7/9 6:11</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Tiffany</td>
      <td>Paris</td>
      <td>Ile-de-France</td>
      <td>France</td>
      <td>2001/7/9 5:30</td>
      <td>1/20/09 11:22</td>
      <td>48.866667</td>
      <td>2.333333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>755</th>
      <td>1/24/09 17:18</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Charlotte</td>
      <td>Sterling</td>
      <td>VA</td>
      <td>United States</td>
      <td>2/15/08 15:34</td>
      <td>2/17/09 6:26</td>
      <td>39.006110</td>
      <td>-77.428890</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>312</th>
      <td>1/20/09 7:08</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Miye</td>
      <td>Downingtown</td>
      <td>PA</td>
      <td>United States</td>
      <td>1/19/09 8:06</td>
      <td>1/27/09 6:38</td>
      <td>40.006390</td>
      <td>-75.703610</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>505</th>
      <td>1/25/09 16:11</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>scott</td>
      <td>Rogers</td>
      <td>AR</td>
      <td>United States</td>
      <td>1/25/09 15:55</td>
      <td>2002/5/9 0:20</td>
      <td>36.331940</td>
      <td>-94.118330</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>912</th>
      <td>1/25/09 11:35</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Mastercard</td>
      <td>Anita</td>
      <td>Fresno</td>
      <td>TX</td>
      <td>United States</td>
      <td>1/24/09 9:24</td>
      <td>2/25/09 14:22</td>
      <td>29.538610</td>
      <td>-95.447220</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2001/1/9 4:24</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Amex</td>
      <td>Pamela</td>
      <td>Skaneateles</td>
      <td>NY</td>
      <td>United States</td>
      <td>12/28/08 17:28</td>
      <td>2003/1/9 7:21</td>
      <td>42.946940</td>
      <td>-76.429440</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>434</th>
      <td>1/14/09 10:32</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Mastercard</td>
      <td>Diana</td>
      <td>Campinas</td>
      <td>Sao Paulo</td>
      <td>Brazil</td>
      <td>2011/5/8 7:03</td>
      <td>2002/2/9 5:54</td>
      <td>-22.900000</td>
      <td>-47.083333</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>511</th>
      <td>1/25/09 1:53</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Michael</td>
      <td>Pietermaritzburg</td>
      <td>KwaZulu-Natal</td>
      <td>South Africa</td>
      <td>1/24/09 12:52</td>
      <td>2002/5/9 4:37</td>
      <td>-29.616667</td>
      <td>30.383333</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>206</th>
      <td>1/16/09 2:41</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Kristyn</td>
      <td>Kearns</td>
      <td>UT</td>
      <td>United States</td>
      <td>1/15/09 18:01</td>
      <td>1/21/09 1:02</td>
      <td>40.660000</td>
      <td>-111.995560</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>814</th>
      <td>2001/12/9 5:50</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Mastercard</td>
      <td>Brona</td>
      <td>Den Haag</td>
      <td>Zuid-Holland</td>
      <td>Netherlands</td>
      <td>2001/4/5 12:43</td>
      <td>2/20/09 0:24</td>
      <td>52.083333</td>
      <td>4.300000</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>493</th>
      <td>2001/11/9 4:29</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Hans</td>
      <td>Knoxville</td>
      <td>TN</td>
      <td>United States</td>
      <td>8/28/08 6:20</td>
      <td>2002/4/9 12:17</td>
      <td>35.960560</td>
      <td>-83.920830</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>244</th>
      <td>2001/5/9 2:57</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Marion</td>
      <td>Rennes</td>
      <td>Brittany</td>
      <td>France</td>
      <td>12/29/08 3:16</td>
      <td>1/23/09 7:29</td>
      <td>48.083333</td>
      <td>-1.683333</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>932</th>
      <td>1/17/09 7:56</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Diners</td>
      <td>Michel</td>
      <td>Lipari</td>
      <td>Sicilia</td>
      <td>Italy</td>
      <td>1/17/09 7:25</td>
      <td>2/26/09 7:32</td>
      <td>38.466667</td>
      <td>14.950000</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>963</th>
      <td>1/22/09 12:45</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Frank and Christelle</td>
      <td>Valley Center</td>
      <td>CA</td>
      <td>United States</td>
      <td>1/22/09 10:25</td>
      <td>2/27/09 10:49</td>
      <td>33.218330</td>
      <td>-117.033330</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>933</th>
      <td>1/17/09 7:58</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Diners</td>
      <td>natalie</td>
      <td>Lipari</td>
      <td>Sicilia</td>
      <td>Italy</td>
      <td>1/17/09 7:25</td>
      <td>2/26/09 7:32</td>
      <td>38.466667</td>
      <td>14.950000</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>544</th>
      <td>1/15/09 10:16</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Karin</td>
      <td>Olive Branch</td>
      <td>MS</td>
      <td>United States</td>
      <td>2001/12/9 17:41</td>
      <td>2002/6/9 18:48</td>
      <td>34.961670</td>
      <td>-89.829440</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>189</th>
      <td>1/20/09 5:24</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Mastercard</td>
      <td>Amanda</td>
      <td>Shreveport</td>
      <td>LA</td>
      <td>United States</td>
      <td>1/20/09 5:13</td>
      <td>1/20/09 7:15</td>
      <td>32.525000</td>
      <td>-93.750000</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>150</th>
      <td>1/18/09 13:26</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Mastercard</td>
      <td>Julianne</td>
      <td>Navan</td>
      <td>Meath</td>
      <td>Ireland</td>
      <td>1/18/09 12:20</td>
      <td>1/18/09 12:20</td>
      <td>53.652778</td>
      <td>-6.681389</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>558</th>
      <td>1/28/09 18:00</td>
      <td>Product1</td>
      <td>13000</td>
      <td>Visa</td>
      <td>sandhya</td>
      <td>Centennial</td>
      <td>CO</td>
      <td>United States</td>
      <td>2012/2/6 23:24</td>
      <td>2002/7/9 15:18</td>
      <td>39.579170</td>
      <td>-104.876390</td>
      <td>13,000</td>
    </tr>
  </tbody>
</table>
<p>998 rows × 13 columns</p>
</div>




```python
df.sort_values(['Price','City'],ascending=[False,True]) # 先按price 再按City排 先正序 后倒序
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
      <th>Transaction_date</th>
      <th>Product</th>
      <th>Price</th>
      <th>Payment_Type</th>
      <th>Name</th>
      <th>City</th>
      <th>State</th>
      <th>Country</th>
      <th>Account_Created</th>
      <th>Last_Login</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Price2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>558</th>
      <td>1/28/09 18:00</td>
      <td>Product1</td>
      <td>13000</td>
      <td>Visa</td>
      <td>sandhya</td>
      <td>Centennial</td>
      <td>CO</td>
      <td>United States</td>
      <td>2012/2/6 23:24</td>
      <td>2002/7/9 15:18</td>
      <td>39.579170</td>
      <td>-104.876390</td>
      <td>13,000</td>
    </tr>
    <tr>
      <th>434</th>
      <td>1/14/09 10:32</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Mastercard</td>
      <td>Diana</td>
      <td>Campinas</td>
      <td>Sao Paulo</td>
      <td>Brazil</td>
      <td>2011/5/8 7:03</td>
      <td>2002/2/9 5:54</td>
      <td>-22.900000</td>
      <td>-47.083333</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>814</th>
      <td>2001/12/9 5:50</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Mastercard</td>
      <td>Brona</td>
      <td>Den Haag</td>
      <td>Zuid-Holland</td>
      <td>Netherlands</td>
      <td>2001/4/5 12:43</td>
      <td>2/20/09 0:24</td>
      <td>52.083333</td>
      <td>4.300000</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>912</th>
      <td>1/25/09 11:35</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Mastercard</td>
      <td>Anita</td>
      <td>Fresno</td>
      <td>TX</td>
      <td>United States</td>
      <td>1/24/09 9:24</td>
      <td>2/25/09 14:22</td>
      <td>29.538610</td>
      <td>-95.447220</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>206</th>
      <td>1/16/09 2:41</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Kristyn</td>
      <td>Kearns</td>
      <td>UT</td>
      <td>United States</td>
      <td>1/15/09 18:01</td>
      <td>1/21/09 1:02</td>
      <td>40.660000</td>
      <td>-111.995560</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>493</th>
      <td>2001/11/9 4:29</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Hans</td>
      <td>Knoxville</td>
      <td>TN</td>
      <td>United States</td>
      <td>8/28/08 6:20</td>
      <td>2002/4/9 12:17</td>
      <td>35.960560</td>
      <td>-83.920830</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>932</th>
      <td>1/17/09 7:56</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Diners</td>
      <td>Michel</td>
      <td>Lipari</td>
      <td>Sicilia</td>
      <td>Italy</td>
      <td>1/17/09 7:25</td>
      <td>2/26/09 7:32</td>
      <td>38.466667</td>
      <td>14.950000</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>933</th>
      <td>1/17/09 7:58</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Diners</td>
      <td>natalie</td>
      <td>Lipari</td>
      <td>Sicilia</td>
      <td>Italy</td>
      <td>1/17/09 7:25</td>
      <td>2/26/09 7:32</td>
      <td>38.466667</td>
      <td>14.950000</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>150</th>
      <td>1/18/09 13:26</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Mastercard</td>
      <td>Julianne</td>
      <td>Navan</td>
      <td>Meath</td>
      <td>Ireland</td>
      <td>1/18/09 12:20</td>
      <td>1/18/09 12:20</td>
      <td>53.652778</td>
      <td>-6.681389</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>544</th>
      <td>1/15/09 10:16</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Karin</td>
      <td>Olive Branch</td>
      <td>MS</td>
      <td>United States</td>
      <td>2001/12/9 17:41</td>
      <td>2002/6/9 18:48</td>
      <td>34.961670</td>
      <td>-89.829440</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>511</th>
      <td>1/25/09 1:53</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Michael</td>
      <td>Pietermaritzburg</td>
      <td>KwaZulu-Natal</td>
      <td>South Africa</td>
      <td>1/24/09 12:52</td>
      <td>2002/5/9 4:37</td>
      <td>-29.616667</td>
      <td>30.383333</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>244</th>
      <td>2001/5/9 2:57</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Marion</td>
      <td>Rennes</td>
      <td>Brittany</td>
      <td>France</td>
      <td>12/29/08 3:16</td>
      <td>1/23/09 7:29</td>
      <td>48.083333</td>
      <td>-1.683333</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>505</th>
      <td>1/25/09 16:11</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>scott</td>
      <td>Rogers</td>
      <td>AR</td>
      <td>United States</td>
      <td>1/25/09 15:55</td>
      <td>2002/5/9 0:20</td>
      <td>36.331940</td>
      <td>-94.118330</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>189</th>
      <td>1/20/09 5:24</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Mastercard</td>
      <td>Amanda</td>
      <td>Shreveport</td>
      <td>LA</td>
      <td>United States</td>
      <td>1/20/09 5:13</td>
      <td>1/20/09 7:15</td>
      <td>32.525000</td>
      <td>-93.750000</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2001/1/9 4:24</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Amex</td>
      <td>Pamela</td>
      <td>Skaneateles</td>
      <td>NY</td>
      <td>United States</td>
      <td>12/28/08 17:28</td>
      <td>2003/1/9 7:21</td>
      <td>42.946940</td>
      <td>-76.429440</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>963</th>
      <td>1/22/09 12:45</td>
      <td>Product3</td>
      <td>7500</td>
      <td>Visa</td>
      <td>Frank and Christelle</td>
      <td>Valley Center</td>
      <td>CA</td>
      <td>United States</td>
      <td>1/22/09 10:25</td>
      <td>2/27/09 10:49</td>
      <td>33.218330</td>
      <td>-117.033330</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>563</th>
      <td>1/25/09 17:58</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>carol</td>
      <td>Ann Arbor</td>
      <td>MI</td>
      <td>United States</td>
      <td>2007/5/8 9:20</td>
      <td>2002/7/9 18:51</td>
      <td>42.270830</td>
      <td>-83.726390</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>894</th>
      <td>1/27/09 14:42</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Jean</td>
      <td>Arlington</td>
      <td>VA</td>
      <td>United States</td>
      <td>2001/8/9 11:01</td>
      <td>2/24/09 16:38</td>
      <td>38.890280</td>
      <td>-77.084440</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>987</th>
      <td>1/23/09 12:42</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Anke</td>
      <td>Avalon</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>2003/3/8 17:38</td>
      <td>2/28/09 22:26</td>
      <td>-33.633333</td>
      <td>151.333333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>799</th>
      <td>1/30/09 6:18</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Louise</td>
      <td>Balgach</td>
      <td>St Gallen</td>
      <td>Switzerland</td>
      <td>1/14/06 2:40</td>
      <td>2/19/09 7:10</td>
      <td>47.416667</td>
      <td>9.600000</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>523</th>
      <td>2001/8/9 19:29</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>PATRICK</td>
      <td>Ban Khlong Sip</td>
      <td>Krung Thep</td>
      <td>Thailand</td>
      <td>2001/8/9 0:01</td>
      <td>2002/5/9 21:22</td>
      <td>13.916667</td>
      <td>100.816667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>898</th>
      <td>2001/8/9 2:49</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Caroline</td>
      <td>Begnins</td>
      <td>Vaud</td>
      <td>Switzerland</td>
      <td>2001/7/9 4:14</td>
      <td>2/25/09 1:37</td>
      <td>46.433333</td>
      <td>6.250000</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>432</th>
      <td>2001/12/9 10:05</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Amex</td>
      <td>Pamela</td>
      <td>Bellinzona</td>
      <td>Ticino</td>
      <td>Switzerland</td>
      <td>2009/3/7 13:23</td>
      <td>2002/2/9 5:16</td>
      <td>46.200000</td>
      <td>9.016667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>901</th>
      <td>1/16/09 5:12</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Karen</td>
      <td>Berikon</td>
      <td>Aargau</td>
      <td>Switzerland</td>
      <td>10/19/07 12:31</td>
      <td>2/25/09 5:12</td>
      <td>47.350000</td>
      <td>8.383333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>752</th>
      <td>1/27/09 3:45</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>minjeong</td>
      <td>Bern</td>
      <td>Bern</td>
      <td>Switzerland</td>
      <td>1/27/09 2:39</td>
      <td>2/17/09 3:44</td>
      <td>46.916667</td>
      <td>7.466667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>175</th>
      <td>1/14/09 5:20</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Kristen</td>
      <td>Binningen</td>
      <td>Basel-Country</td>
      <td>Switzerland</td>
      <td>2001/12/9 13:31</td>
      <td>1/19/09 13:07</td>
      <td>47.533333</td>
      <td>7.566667</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>290</th>
      <td>1/26/09 3:49</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Mastercard</td>
      <td>Jane</td>
      <td>Biot</td>
      <td>Provence-Alpes-Cote d'Azur</td>
      <td>France</td>
      <td>2003/1/8 0:00</td>
      <td>1/26/09 3:18</td>
      <td>43.633333</td>
      <td>7.100000</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>994</th>
      <td>1/28/09 5:36</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Christiane</td>
      <td>Black River</td>
      <td>Black River</td>
      <td>Mauritius</td>
      <td>2001/9/9 8:10</td>
      <td>2003/1/9 4:40</td>
      <td>-20.360278</td>
      <td>57.366111</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>172</th>
      <td>2001/8/9 11:55</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Caren</td>
      <td>Braunschweig</td>
      <td>Lower Saxony</td>
      <td>Germany</td>
      <td>2001/3/9 12:39</td>
      <td>1/19/09 8:31</td>
      <td>52.266667</td>
      <td>10.533333</td>
      <td>3600</td>
    </tr>
    <tr>
      <th>573</th>
      <td>1/26/09 1:44</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Geraldine</td>
      <td>Brussels</td>
      <td>Brussels (Bruxelles)</td>
      <td>Belgium</td>
      <td>1/31/08 13:28</td>
      <td>2002/8/9 14:39</td>
      <td>50.833333</td>
      <td>4.333333</td>
      <td>3600</td>
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
    </tr>
    <tr>
      <th>410</th>
      <td>2001/7/9 13:49</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>megan</td>
      <td>West Hills</td>
      <td>CA</td>
      <td>United States</td>
      <td>2001/7/9 12:36</td>
      <td>2002/1/9 8:20</td>
      <td>34.201110</td>
      <td>-118.597220</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>138</th>
      <td>1/17/09 16:22</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Chad</td>
      <td>West Orange</td>
      <td>NJ</td>
      <td>United States</td>
      <td>1/17/09 15:22</td>
      <td>1/17/09 18:42</td>
      <td>40.798610</td>
      <td>-74.239440</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>710</th>
      <td>1/25/09 17:48</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>olla</td>
      <td>Westminster</td>
      <td>CO</td>
      <td>United States</td>
      <td>1/24/09 23:48</td>
      <td>2/15/09 8:08</td>
      <td>39.836670</td>
      <td>-105.036670</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>391</th>
      <td>1/31/09 7:22</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Monica</td>
      <td>Weston</td>
      <td>CT</td>
      <td>United States</td>
      <td>2/29/08 17:34</td>
      <td>1/31/09 6:43</td>
      <td>41.200830</td>
      <td>-73.381110</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>575</th>
      <td>1/24/09 21:26</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Olivia</td>
      <td>Wheaton</td>
      <td>IL</td>
      <td>United States</td>
      <td>2005/8/8 16:02</td>
      <td>2002/8/9 16:00</td>
      <td>41.866110</td>
      <td>-88.106940</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>287</th>
      <td>2001/9/9 10:22</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>HELIDA</td>
      <td>White House</td>
      <td>TN</td>
      <td>United States</td>
      <td>2001/5/9 14:49</td>
      <td>1/25/09 19:35</td>
      <td>36.470280</td>
      <td>-86.651390</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>187</th>
      <td>1/20/09 3:11</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Randy</td>
      <td>Wigan</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/20/09 3:02</td>
      <td>1/20/09 3:06</td>
      <td>53.533333</td>
      <td>-2.616667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>782</th>
      <td>1/19/09 14:06</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Elisabeth</td>
      <td>Wilmington</td>
      <td>NC</td>
      <td>United States</td>
      <td>1/19/09 12:41</td>
      <td>2/18/09 8:18</td>
      <td>34.225560</td>
      <td>-77.945000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>874</th>
      <td>1/21/09 7:31</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Beatrice</td>
      <td>Wilmington</td>
      <td>DE</td>
      <td>United States</td>
      <td>3/25/08 13:23</td>
      <td>2/23/09 16:29</td>
      <td>39.745830</td>
      <td>-75.546940</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>236</th>
      <td>1/20/09 8:51</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Marie</td>
      <td>Winchester</td>
      <td>MA</td>
      <td>United States</td>
      <td>7/23/08 14:59</td>
      <td>1/22/09 18:08</td>
      <td>42.452220</td>
      <td>-71.137500</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>162</th>
      <td>1/13/09 20:59</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Andrew</td>
      <td>Winnipeg</td>
      <td>Manitoba</td>
      <td>Canada</td>
      <td>1/13/09 16:44</td>
      <td>1/18/09 19:17</td>
      <td>49.883333</td>
      <td>-97.166667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>228</th>
      <td>2001/12/9 9:23</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Jacob</td>
      <td>Winter Haven</td>
      <td>FL</td>
      <td>United States</td>
      <td>2001/10/9 14:55</td>
      <td>1/22/09 7:59</td>
      <td>28.021940</td>
      <td>-81.733060</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>936</th>
      <td>2001/11/9 8:41</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Juliann</td>
      <td>Winter Spgs</td>
      <td>FL</td>
      <td>United States</td>
      <td>2001/8/8 7:24</td>
      <td>2/26/09 8:17</td>
      <td>28.698610</td>
      <td>-81.308330</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>600</th>
      <td>1/14/09 13:23</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>eugenia</td>
      <td>Wisconsin Rapids</td>
      <td>WI</td>
      <td>United States</td>
      <td>11/15/08 13:57</td>
      <td>2002/9/9 18:44</td>
      <td>44.383610</td>
      <td>-89.817220</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>207</th>
      <td>1/16/09 18:36</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Elizabeth</td>
      <td>Wollongong</td>
      <td>New South Wales</td>
      <td>Australia</td>
      <td>2011/1/8 16:32</td>
      <td>1/21/09 1:49</td>
      <td>-34.433333</td>
      <td>150.883333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>678</th>
      <td>1/14/09 16:02</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Jessica</td>
      <td>Woodland Hills</td>
      <td>CA</td>
      <td>United States</td>
      <td>1/14/09 14:53</td>
      <td>2/13/09 16:45</td>
      <td>34.168330</td>
      <td>-118.605000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>66</th>
      <td>2001/8/9 15:16</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Dottie</td>
      <td>Woodsboro</td>
      <td>MD</td>
      <td>United States</td>
      <td>2001/8/9 14:56</td>
      <td>2001/12/9 9:29</td>
      <td>39.533060</td>
      <td>-77.315000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>748</th>
      <td>1/25/09 7:29</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Howard</td>
      <td>Worcester</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/22/09 14:02</td>
      <td>2/17/09 3:00</td>
      <td>52.200000</td>
      <td>-2.200000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>982</th>
      <td>2001/4/9 18:57</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>KELI</td>
      <td>Worongary</td>
      <td>Queensland</td>
      <td>Australia</td>
      <td>12/23/08 15:17</td>
      <td>2/28/09 14:00</td>
      <td>-28.050000</td>
      <td>153.350000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>156</th>
      <td>2001/4/9 23:48</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Diners</td>
      <td>Sarka</td>
      <td>Yellowknife</td>
      <td>Northwest Territories</td>
      <td>Canada</td>
      <td>2001/4/9 22:41</td>
      <td>1/18/09 16:17</td>
      <td>62.450000</td>
      <td>-114.350000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>680</th>
      <td>2001/8/9 20:52</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Pam and Rob</td>
      <td>Yorba Linda</td>
      <td>CA</td>
      <td>United States</td>
      <td>11/18/08 20:03</td>
      <td>2/13/09 19:32</td>
      <td>33.888610</td>
      <td>-117.812220</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>129</th>
      <td>1/15/09 10:24</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Grace</td>
      <td>York</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>1/13/09 12:30</td>
      <td>1/17/09 4:42</td>
      <td>53.966667</td>
      <td>-1.083333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>469</th>
      <td>1/24/09 10:23</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>DD</td>
      <td>York</td>
      <td>England</td>
      <td>United Kingdom</td>
      <td>8/19/08 12:58</td>
      <td>2002/3/9 12:57</td>
      <td>53.966667</td>
      <td>-1.083333</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>530</th>
      <td>1/19/09 3:19</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>TG</td>
      <td>Zagore</td>
      <td>Stara Zagora</td>
      <td>Bulgaria</td>
      <td>11/20/08 3:00</td>
      <td>2002/6/9 4:19</td>
      <td>42.350000</td>
      <td>25.666667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>169</th>
      <td>2001/3/9 9:54</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Sylvia</td>
      <td>Zekeriyakoy</td>
      <td>Istanbul</td>
      <td>Turkey</td>
      <td>12/29/08 10:38</td>
      <td>1/19/09 7:37</td>
      <td>41.198056</td>
      <td>29.030278</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>905</th>
      <td>1/23/09 5:52</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Amex</td>
      <td>Tary</td>
      <td>Zug</td>
      <td>Zug</td>
      <td>Switzerland</td>
      <td>1/23/09 1:22</td>
      <td>2/25/09 9:40</td>
      <td>47.166667</td>
      <td>8.516667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>798</th>
      <td>1/21/09 11:56</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Katrin</td>
      <td>Zumikon</td>
      <td>Zurich</td>
      <td>Switzerland</td>
      <td>3/21/06 13:30</td>
      <td>2/19/09 7:05</td>
      <td>47.333333</td>
      <td>8.616667</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>515</th>
      <td>1/25/09 8:50</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Shane</td>
      <td>Zurich</td>
      <td>Zurich</td>
      <td>Switzerland</td>
      <td>1/24/09 12:23</td>
      <td>2002/5/9 11:07</td>
      <td>47.366667</td>
      <td>8.550000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>294</th>
      <td>1/21/09 11:28</td>
      <td>Product1</td>
      <td>800</td>
      <td>Amex</td>
      <td>Heloise</td>
      <td>Arlington</td>
      <td>VA</td>
      <td>United States</td>
      <td>9/25/05 20:26</td>
      <td>1/26/09 6:23</td>
      <td>38.890280</td>
      <td>-77.084440</td>
      <td>800</td>
    </tr>
    <tr>
      <th>477</th>
      <td>1/30/09 7:42</td>
      <td>Product1</td>
      <td>250</td>
      <td>Visa</td>
      <td>Tabatha</td>
      <td>Altadena</td>
      <td>CA</td>
      <td>United States</td>
      <td>12/28/08 14:42</td>
      <td>2002/3/9 18:09</td>
      <td>34.189720</td>
      <td>-118.130280</td>
      <td>250</td>
    </tr>
  </tbody>
</table>
<p>998 rows × 13 columns</p>
</div>




```python
#groupby
df.groupby(df.Country).mean().sort_values('Price',ascending=False) #按平均值分类 再排序
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
      <th>Price</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mauritius</th>
      <td>3600.000000</td>
      <td>-20.360278</td>
      <td>57.366111</td>
    </tr>
    <tr>
      <th>Russia</th>
      <td>3600.000000</td>
      <td>55.628333</td>
      <td>37.660833</td>
    </tr>
    <tr>
      <th>Italy</th>
      <td>2520.000000</td>
      <td>42.895556</td>
      <td>11.368889</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>2460.000000</td>
      <td>-20.486944</td>
      <td>-46.100333</td>
    </tr>
    <tr>
      <th>South Africa</th>
      <td>2460.000000</td>
      <td>-27.538222</td>
      <td>29.150778</td>
    </tr>
    <tr>
      <th>Thailand</th>
      <td>2400.000000</td>
      <td>10.900000</td>
      <td>99.608333</td>
    </tr>
    <tr>
      <th>Malta</th>
      <td>2400.000000</td>
      <td>35.979028</td>
      <td>14.368333</td>
    </tr>
    <tr>
      <th>Switzerland</th>
      <td>2133.333333</td>
      <td>46.846296</td>
      <td>7.526852</td>
    </tr>
    <tr>
      <th>Netherlands</th>
      <td>2031.818182</td>
      <td>52.241667</td>
      <td>4.870455</td>
    </tr>
    <tr>
      <th>United Arab Emirates</th>
      <td>2000.000000</td>
      <td>25.107130</td>
      <td>55.117037</td>
    </tr>
    <tr>
      <th>Czech Republic</th>
      <td>2000.000000</td>
      <td>50.142778</td>
      <td>14.898056</td>
    </tr>
    <tr>
      <th>France</th>
      <td>1966.666667</td>
      <td>47.174691</td>
      <td>4.074691</td>
    </tr>
    <tr>
      <th>Sweden</th>
      <td>1753.846154</td>
      <td>59.428205</td>
      <td>17.692308</td>
    </tr>
    <tr>
      <th>Australia</th>
      <td>1705.263158</td>
      <td>-33.028465</td>
      <td>144.039225</td>
    </tr>
    <tr>
      <th>Germany</th>
      <td>1680.000000</td>
      <td>50.322000</td>
      <td>9.614667</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>1642.105263</td>
      <td>48.280482</td>
      <td>-99.206360</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>1619.870410</td>
      <td>37.510644</td>
      <td>-93.057584</td>
    </tr>
    <tr>
      <th>Austria</th>
      <td>1542.857143</td>
      <td>48.145238</td>
      <td>15.697619</td>
    </tr>
    <tr>
      <th>Belgium</th>
      <td>1500.000000</td>
      <td>50.835417</td>
      <td>4.325000</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>1440.000000</td>
      <td>52.371276</td>
      <td>-1.307689</td>
    </tr>
    <tr>
      <th>Ireland</th>
      <td>1426.530612</td>
      <td>52.923997</td>
      <td>-7.132545</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>1400.000000</td>
      <td>40.227269</td>
      <td>-1.922523</td>
    </tr>
    <tr>
      <th>Norway</th>
      <td>1350.000000</td>
      <td>59.776944</td>
      <td>8.537483</td>
    </tr>
    <tr>
      <th>Moldova</th>
      <td>1200.000000</td>
      <td>46.985000</td>
      <td>28.942500</td>
    </tr>
    <tr>
      <th>Monaco</th>
      <td>1200.000000</td>
      <td>43.733333</td>
      <td>7.416667</td>
    </tr>
    <tr>
      <th>New Zealand</th>
      <td>1200.000000</td>
      <td>-37.651389</td>
      <td>174.558333</td>
    </tr>
    <tr>
      <th>The Bahamas</th>
      <td>1200.000000</td>
      <td>25.791667</td>
      <td>-78.058333</td>
    </tr>
    <tr>
      <th>Philippines</th>
      <td>1200.000000</td>
      <td>8.008611</td>
      <td>124.654583</td>
    </tr>
    <tr>
      <th>Turkey</th>
      <td>1200.000000</td>
      <td>40.590648</td>
      <td>28.702546</td>
    </tr>
    <tr>
      <th>Romania</th>
      <td>1200.000000</td>
      <td>44.466667</td>
      <td>26.133333</td>
    </tr>
    <tr>
      <th>Ukraine</th>
      <td>1200.000000</td>
      <td>50.516667</td>
      <td>30.250000</td>
    </tr>
    <tr>
      <th>South Korea</th>
      <td>1200.000000</td>
      <td>37.533333</td>
      <td>127.116667</td>
    </tr>
    <tr>
      <th>Poland</th>
      <td>1200.000000</td>
      <td>53.258333</td>
      <td>19.750000</td>
    </tr>
    <tr>
      <th>Argentina</th>
      <td>1200.000000</td>
      <td>-37.150000</td>
      <td>-58.483333</td>
    </tr>
    <tr>
      <th>Malaysia</th>
      <td>1200.000000</td>
      <td>3.166667</td>
      <td>101.700000</td>
    </tr>
    <tr>
      <th>Luxembourg</th>
      <td>1200.000000</td>
      <td>49.585556</td>
      <td>6.123056</td>
    </tr>
    <tr>
      <th>Bahrain</th>
      <td>1200.000000</td>
      <td>26.217222</td>
      <td>50.540556</td>
    </tr>
    <tr>
      <th>Bermuda</th>
      <td>1200.000000</td>
      <td>32.294167</td>
      <td>-64.783889</td>
    </tr>
    <tr>
      <th>Bulgaria</th>
      <td>1200.000000</td>
      <td>42.350000</td>
      <td>25.666667</td>
    </tr>
    <tr>
      <th>Cayman Isls</th>
      <td>1200.000000</td>
      <td>19.300000</td>
      <td>-81.383333</td>
    </tr>
    <tr>
      <th>China</th>
      <td>1200.000000</td>
      <td>22.250000</td>
      <td>112.783333</td>
    </tr>
    <tr>
      <th>Costa Rica</th>
      <td>1200.000000</td>
      <td>10.033333</td>
      <td>-84.150000</td>
    </tr>
    <tr>
      <th>Denmark</th>
      <td>1200.000000</td>
      <td>55.655667</td>
      <td>12.110037</td>
    </tr>
    <tr>
      <th>Dominican Republic</th>
      <td>1200.000000</td>
      <td>18.466667</td>
      <td>-69.900000</td>
    </tr>
    <tr>
      <th>Finland</th>
      <td>1200.000000</td>
      <td>61.933333</td>
      <td>26.675000</td>
    </tr>
    <tr>
      <th>Greece</th>
      <td>1200.000000</td>
      <td>37.983333</td>
      <td>23.733333</td>
    </tr>
    <tr>
      <th>Guatemala</th>
      <td>1200.000000</td>
      <td>14.650000</td>
      <td>-90.483333</td>
    </tr>
    <tr>
      <th>Hong Kong</th>
      <td>1200.000000</td>
      <td>22.283333</td>
      <td>114.150000</td>
    </tr>
    <tr>
      <th>Hungary</th>
      <td>1200.000000</td>
      <td>47.255556</td>
      <td>19.277778</td>
    </tr>
    <tr>
      <th>Iceland</th>
      <td>1200.000000</td>
      <td>63.850000</td>
      <td>-21.366667</td>
    </tr>
    <tr>
      <th>India</th>
      <td>1200.000000</td>
      <td>22.925000</td>
      <td>77.750000</td>
    </tr>
    <tr>
      <th>Israel</th>
      <td>1200.000000</td>
      <td>32.066667</td>
      <td>34.766667</td>
    </tr>
    <tr>
      <th>Japan</th>
      <td>1200.000000</td>
      <td>35.659167</td>
      <td>139.700694</td>
    </tr>
    <tr>
      <th>Kuwait</th>
      <td>1200.000000</td>
      <td>29.289167</td>
      <td>48.050000</td>
    </tr>
    <tr>
      <th>Latvia</th>
      <td>1200.000000</td>
      <td>57.033333</td>
      <td>24.100000</td>
    </tr>
    <tr>
      <th>Jersey</th>
      <td>1200.000000</td>
      <td>49.200000</td>
      <td>-2.033333</td>
    </tr>
  </tbody>
</table>
</div>




```python
# join on
df2 = pd.DataFrame([['MO',0],['OR',1],['AL',2]],columns=['State','v']) #构建一个新表
df2
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
      <th>State</th>
      <th>v</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MO</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>OR</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AL</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df2,df,on='State',how='left')
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
      <th>State</th>
      <th>v</th>
      <th>Transaction_date</th>
      <th>Product</th>
      <th>Price</th>
      <th>Payment_Type</th>
      <th>Name</th>
      <th>City</th>
      <th>Country</th>
      <th>Account_Created</th>
      <th>Last_Login</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Price2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MO</td>
      <td>0</td>
      <td>2001/2/9 4:53</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Betina</td>
      <td>Parkville</td>
      <td>United States</td>
      <td>2001/2/9 4:42</td>
      <td>2001/2/9 7:49</td>
      <td>39.19500</td>
      <td>-94.68194</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>OR</td>
      <td>1</td>
      <td>2001/2/9 13:08</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Mastercard</td>
      <td>Federica e Andrea</td>
      <td>Astoria</td>
      <td>United States</td>
      <td>2001/1/9 16:21</td>
      <td>2001/3/9 12:32</td>
      <td>46.18806</td>
      <td>-123.83000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>OR</td>
      <td>1</td>
      <td>1/17/09 7:23</td>
      <td>Product1</td>
      <td>1200</td>
      <td>Visa</td>
      <td>Georgina</td>
      <td>Portland</td>
      <td>United States</td>
      <td>11/28/07 10:05</td>
      <td>1/24/09 8:54</td>
      <td>45.52361</td>
      <td>-122.67500</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>3</th>
      <td>AL</td>
      <td>2</td>
      <td>2001/4/9 12:56</td>
      <td>Product2</td>
      <td>3600</td>
      <td>Visa</td>
      <td>Gerd W</td>
      <td>Cahaba Heights</td>
      <td>United States</td>
      <td>11/15/08 15:47</td>
      <td>2001/4/9 12:45</td>
      <td>33.52056</td>
      <td>-86.80250</td>
      <td>3600</td>
    </tr>
  </tbody>
</table>
</div>


