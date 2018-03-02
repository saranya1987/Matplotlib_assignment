

PYBER ANALYSIS: 
    • Around (60 – 70) % of the rides are taken by the Urban riders and the maximum average fare comes from them too. 
    • The New opportunity of increasing the drivers in Suburban area will increase the market share of the company. 


```python
#import Dependencies
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np 
import seaborn as sns
```


```python
#read cities csv file
cities_df = pd.read_csv("city_data.csv")
cities_df.head() 
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
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
#read rides csv file
rides_df = pd.read_csv("ride_data.csv") 
rides_df.head()
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>1/16/2016 13:49</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>1/2/2016 18:42</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>1/21/2016 17:35</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>7/31/2016 14:53</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>7/9/2016 4:42</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merging cities and ride csv 
data_merge = pd.merge(rides_df,cities_df, on="city",how="left")
data_merge
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>1/16/2016 13:49</td>
      <td>38.35</td>
      <td>5403689035038</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>1/2/2016 18:42</td>
      <td>17.49</td>
      <td>4036272335942</td>
      <td>35</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>1/21/2016 17:35</td>
      <td>44.18</td>
      <td>3645042422587</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>7/31/2016 14:53</td>
      <td>6.87</td>
      <td>2242596575892</td>
      <td>68</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>7/9/2016 4:42</td>
      <td>6.28</td>
      <td>1543057793673</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>5</th>
      <td>New Jeffrey</td>
      <td>2/22/2016 18:36</td>
      <td>36.01</td>
      <td>9757888452346</td>
      <td>58</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Port Johnstad</td>
      <td>6/7/2016 2:39</td>
      <td>17.15</td>
      <td>4352278259335</td>
      <td>22</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Jacobfort</td>
      <td>9/20/2016 20:58</td>
      <td>22.98</td>
      <td>1500221409082</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Travisville</td>
      <td>1/15/2016 17:32</td>
      <td>27.39</td>
      <td>850152768361</td>
      <td>37</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Sandymouth</td>
      <td>11/16/2016 7:27</td>
      <td>21.61</td>
      <td>2389035050524</td>
      <td>11</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>10</th>
      <td>New Andreamouth</td>
      <td>4/11/2016 7:20</td>
      <td>7.72</td>
      <td>9992929847990</td>
      <td>42</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>11</th>
      <td>New Christine</td>
      <td>9/13/2016 15:06</td>
      <td>24.89</td>
      <td>7918411468537</td>
      <td>22</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Stewartview</td>
      <td>3/29/2016 5:15</td>
      <td>23.88</td>
      <td>6778235889588</td>
      <td>49</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Rodriguezburgh</td>
      <td>9/5/2016 5:20</td>
      <td>4.54</td>
      <td>9650770953139</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>14</th>
      <td>West Sydneyhaven</td>
      <td>8/2/2016 21:18</td>
      <td>12.87</td>
      <td>7994760397230</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Swansonbury</td>
      <td>7/11/2016 18:42</td>
      <td>39.30</td>
      <td>744481862626</td>
      <td>64</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Lisatown</td>
      <td>7/5/2016 18:09</td>
      <td>5.82</td>
      <td>6370359473201</td>
      <td>47</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>17</th>
      <td>East Erin</td>
      <td>11/3/2016 1:03</td>
      <td>7.51</td>
      <td>4744239092530</td>
      <td>43</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Port Martinberg</td>
      <td>1/6/2016 17:11</td>
      <td>8.66</td>
      <td>7298562820881</td>
      <td>44</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Wiseborough</td>
      <td>9/12/2016 18:43</td>
      <td>26.83</td>
      <td>9304728540000</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Edwardsbury</td>
      <td>2/27/2016 3:55</td>
      <td>20.17</td>
      <td>8514523868075</td>
      <td>11</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Jacobfort</td>
      <td>6/12/2016 17:01</td>
      <td>34.47</td>
      <td>4135673527977</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Pamelahaven</td>
      <td>3/26/2016 12:56</td>
      <td>36.43</td>
      <td>3015329826849</td>
      <td>30</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Fosterside</td>
      <td>8/12/2016 11:52</td>
      <td>28.08</td>
      <td>133077693483</td>
      <td>69</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Jacobfort</td>
      <td>9/17/2016 12:38</td>
      <td>38.25</td>
      <td>2182376146051</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>25</th>
      <td>West Sydneyhaven</td>
      <td>8/23/2016 14:49</td>
      <td>36.12</td>
      <td>5885997568611</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>26</th>
      <td>West Alexis</td>
      <td>1/16/2016 0:33</td>
      <td>26.62</td>
      <td>1574788996743</td>
      <td>47</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Carrollfort</td>
      <td>6/24/2016 20:11</td>
      <td>6.45</td>
      <td>1092683495142</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>28</th>
      <td>New David</td>
      <td>1/12/2016 20:48</td>
      <td>38.68</td>
      <td>5229089333754</td>
      <td>31</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Stewartview</td>
      <td>10/15/2016 5:26</td>
      <td>11.74</td>
      <td>8402784599831</td>
      <td>49</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2377</th>
      <td>West Kevintown</td>
      <td>6/15/2016 19:53</td>
      <td>13.50</td>
      <td>9577921579881</td>
      <td>5</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2378</th>
      <td>Matthewside</td>
      <td>2/23/2016 0:43</td>
      <td>40.84</td>
      <td>8665248512368</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2379</th>
      <td>Erikport</td>
      <td>11/26/2016 4:39</td>
      <td>44.21</td>
      <td>9598643212986</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2380</th>
      <td>Kinghaven</td>
      <td>7/23/2016 8:23</td>
      <td>46.08</td>
      <td>8440329717166</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2381</th>
      <td>Hernandezshire</td>
      <td>2/24/2016 17:30</td>
      <td>44.68</td>
      <td>6389115653382</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2382</th>
      <td>Kennethburgh</td>
      <td>1/1/2016 4:31</td>
      <td>33.53</td>
      <td>5149088250183</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2383</th>
      <td>Stevensport</td>
      <td>2/22/2016 2:45</td>
      <td>19.91</td>
      <td>808097865942</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2384</th>
      <td>South Elizabethmouth</td>
      <td>11/23/2016 7:47</td>
      <td>46.39</td>
      <td>1939838068038</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2385</th>
      <td>East Stephen</td>
      <td>7/30/2016 21:25</td>
      <td>35.39</td>
      <td>1107870956099</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2386</th>
      <td>Jacksonfort</td>
      <td>10/1/2016 13:41</td>
      <td>34.17</td>
      <td>7750597960630</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2387</th>
      <td>Kennethburgh</td>
      <td>4/30/2016 20:44</td>
      <td>23.58</td>
      <td>4524301143267</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2388</th>
      <td>Horneland</td>
      <td>3/25/2016 2:05</td>
      <td>20.04</td>
      <td>5729327140644</td>
      <td>8</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2389</th>
      <td>Shelbyhaven</td>
      <td>1/25/2016 1:39</td>
      <td>59.43</td>
      <td>8088329954312</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2390</th>
      <td>Erikport</td>
      <td>8/3/2016 21:19</td>
      <td>47.67</td>
      <td>9201708664049</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2391</th>
      <td>Kennethburgh</td>
      <td>11/19/2016 6:59</td>
      <td>18.37</td>
      <td>5897895798960</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2392</th>
      <td>Jacksonfort</td>
      <td>10/20/2016 16:42</td>
      <td>37.75</td>
      <td>4356781814784</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2393</th>
      <td>South Joseph</td>
      <td>10/15/2016 3:53</td>
      <td>32.50</td>
      <td>2758038144583</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2394</th>
      <td>Matthewside</td>
      <td>5/18/2016 2:00</td>
      <td>48.67</td>
      <td>2049161404256</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2395</th>
      <td>Matthewside</td>
      <td>8/8/2016 14:02</td>
      <td>24.97</td>
      <td>2872494724827</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2396</th>
      <td>South Joseph</td>
      <td>10/28/2016 9:52</td>
      <td>25.34</td>
      <td>6706101910500</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2397</th>
      <td>South Elizabethmouth</td>
      <td>7/19/2016 9:35</td>
      <td>31.09</td>
      <td>2959749591417</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2398</th>
      <td>North Whitney</td>
      <td>11/11/2016 16:24</td>
      <td>22.99</td>
      <td>3454326063039</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2399</th>
      <td>New Johnbury</td>
      <td>8/29/2016 2:36</td>
      <td>18.83</td>
      <td>7368222134792</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2400</th>
      <td>East Leslie</td>
      <td>6/22/2016 7:45</td>
      <td>34.54</td>
      <td>684950063164</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2401</th>
      <td>Kennethburgh</td>
      <td>6/7/2016 11:43</td>
      <td>56.02</td>
      <td>311733202150</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2402</th>
      <td>West Kevintown</td>
      <td>2/10/2016 0:50</td>
      <td>34.69</td>
      <td>9595491362610</td>
      <td>5</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2403</th>
      <td>East Troybury</td>
      <td>3/14/2016 1:55</td>
      <td>38.80</td>
      <td>9205811495606</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2404</th>
      <td>North Whitney</td>
      <td>1/26/2016 1:06</td>
      <td>34.92</td>
      <td>4165974278063</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2405</th>
      <td>South Joseph</td>
      <td>9/28/2016 7:30</td>
      <td>12.55</td>
      <td>4336212615821</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2406</th>
      <td>South Elizabethmouth</td>
      <td>4/21/2016 10:20</td>
      <td>16.50</td>
      <td>5702608059064</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
  </tbody>
</table>
<p>2407 rows × 6 columns</p>
</div>




```python
# Calculating the city type : ride count, average fare and driver count
urban = data_merge[data_merge["type"]=="Urban"]
rural = data_merge[data_merge["type"]=="Rural"]
suburban = data_merge[data_merge["type"]=="Suburban"]

urban_group = urban.groupby(['city'])
urban_ride_count = urban_group['ride_id'].count()
urban_fare_avg = urban_group['fare'].mean()
urban_dri_count = urban_group['driver_count'].mean() 

rural_group = rural.groupby(['city'])
rural_ride_count = rural_group['ride_id'].count()
rural_fare_avg = rural_group['fare'].mean()
rural_dri_count = rural_group['driver_count'].mean() 

suburban_group = suburban.groupby(['city'])
suburban_ride_count = suburban_group['ride_id'].count()
suburban_fare_avg = suburban_group['fare'].mean()
suburban_dri_count = suburban_group['driver_count'].mean() 

```


```python
#set the grid and figure size using seaborn
sns.set_style("whitegrid", {'grid.linestyle': '--'})
paper_rc = {'lines.linewidth': 1, 'lines.markersize': 2}                  
sns.set(rc={'figure.figsize':(7,5)})

# Plotting the scatter plot
plt.scatter(urban_ride_count, urban_fare_avg, s = 5*urban_dri_count, c="coral", alpha=1, edgecolors="black", linewidth=1,label = "Urban")
plt.scatter(suburban_ride_count, suburban_fare_avg, s = 5*suburban_dri_count, c="lightskyblue", alpha=1, edgecolors="black", linewidth=1,label = "Suburban")
plt.scatter(rural_ride_count, rural_fare_avg, s = 10*rural_dri_count, c="gold", alpha=1, edgecolors="black", linewidth=1,label = "Rural")
plt.xlabel("Total Number of Rides(per city)")
plt.ylabel("Average Fare ($)") 
plt.title("Pyber Ride Sharing Data (2016)")
plt.xlim(0,40,10)
plt.ylim(15,55,5)
legend = plt.legend(loc='upper right', title = "City Types", shadow=True)

# Set the fontsize
for label in legend.get_texts():
    label.set_fontsize('small')
    
for label in legend.get_lines():
    label.set_linewidth(1.5)  # the legend line width
plt.show()

```


![png](output_6_0.png)



```python
#Total Fares by city type calculation
city_type_percent = data_merge.groupby(['type']) 
sum_up = city_type_percent['fare'].sum()
count = data_merge['fare'].sum()
Total_Fares = (sum_up/count)*100 
plt.pie(Total_Fares, explode=[0,0,0.06], labels=["Rural","Suburban","Urban"], colors=["gold","lightskyblue","lightcoral"],
        autopct='%1.1f%%', shadow=True, startangle=140)
plt.title("% of Total Fares by City Type")
plt.show() 
```


![png](output_7_0.png)



```python
# Total Rides by city type calculation
ride_type_percent = data_merge.groupby(['type']) 
sum_ride = ride_type_percent['ride_id'].count() 
count_ride = data_merge['driver_count'].count()
Total_ride = (sum_ride/count_ride)*100 
plt.pie(Total_ride, explode=[0,0,0.05], labels=["Rural","Suburban","Urban"], colors=["gold","lightskyblue","lightcoral"],
        autopct='%1.1f%%', shadow=True, startangle=140)
plt.title("% of Total Rides by City Type")
plt.show()
```


![png](output_8_0.png)



```python
# Total Drivers by city type calculation
city_type_percent = cities_df.groupby(['type']) 
sum_it = city_type_percent['driver_count'].sum()
count_it = cities_df['driver_count'].sum()
Total_driver = (sum_it/count_it)*100 
plt.pie(Total_driver, explode=[0,0,0.1], labels=["Rural","Suburban","Urban"], colors=["gold","lightskyblue","lightcoral"],
        autopct='%1.1f%%', shadow=True, startangle=140)
plt.title("% of Total Drivers by City Type")
plt.show()
```


![png](output_9_0.png)

