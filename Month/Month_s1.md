

```python
import pandas as pd
import datetime
import numpy as np
```


```python
date_data = '../OMDB_TMDB_Merge/AllData_withOscarWins.csv'
date_df = pd.read_csv(date_data, parse_dates=True)
date_df.head()
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
      <th>Movie</th>
      <th>Release Date_x</th>
      <th>Release Date_y</th>
      <th>Budget</th>
      <th>Revenue</th>
      <th>Box Office</th>
      <th>Genres</th>
      <th>Rating</th>
      <th>Runtime</th>
      <th>Metascore</th>
      <th>IMDb Rating</th>
      <th>Awards</th>
      <th>Production Company</th>
      <th>wins</th>
      <th>nominations</th>
      <th>Win or Nominated</th>
      <th>Oscar Wins</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Capote</td>
      <td>2005-09-30</td>
      <td>03 Feb 2006</td>
      <td>7000000.0</td>
      <td>49084830.0</td>
      <td>28337516.0</td>
      <td>Crime</td>
      <td>R</td>
      <td>114.0</td>
      <td>88.0</td>
      <td>7.4</td>
      <td>W1O, ++58,86</td>
      <td>Sony Pictures Classics</td>
      <td>58.0</td>
      <td>86.0</td>
      <td>W</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>American Hustle</td>
      <td>2013-12-12</td>
      <td>20 Dec 2013</td>
      <td>40000000.0</td>
      <td>251171807.0</td>
      <td>99165609.0</td>
      <td>Drama</td>
      <td>R</td>
      <td>138.0</td>
      <td>90.0</td>
      <td>7.3</td>
      <td>N10O, ++70,208</td>
      <td>Sony Pictures</td>
      <td>70.0</td>
      <td>208.0</td>
      <td>N</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Brokeback Mountain</td>
      <td>2005-09-10</td>
      <td>13 Jan 2006</td>
      <td>14000000.0</td>
      <td>178043761.0</td>
      <td>82970165.0</td>
      <td>Drama</td>
      <td>R</td>
      <td>134.0</td>
      <td>87.0</td>
      <td>7.7</td>
      <td>W3O, ++138,128</td>
      <td>Focus Features</td>
      <td>138.0</td>
      <td>128.0</td>
      <td>W</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Walk the Line</td>
      <td>2005-09-13</td>
      <td>18 Nov 2005</td>
      <td>28000000.0</td>
      <td>186438883.0</td>
      <td>119317827.0</td>
      <td>Drama</td>
      <td>PG-13</td>
      <td>136.0</td>
      <td>72.0</td>
      <td>7.9</td>
      <td>W1O, ++44,46</td>
      <td>20th Century Fox</td>
      <td>44.0</td>
      <td>46.0</td>
      <td>W</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Good Night, and Good Luck.</td>
      <td>2005-09-16</td>
      <td>04 Nov 2005</td>
      <td>7000000.0</td>
      <td>54600000.0</td>
      <td>31500000.0</td>
      <td>Drama</td>
      <td>PG</td>
      <td>93.0</td>
      <td>80.0</td>
      <td>7.5</td>
      <td>N6O, ++38,121</td>
      <td>Warner Independent Pictures</td>
      <td>38.0</td>
      <td>121.0</td>
      <td>N</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Add new column "Award_date"
date_df['Award_date'] = ""
date_df.head()
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
      <th>Movie</th>
      <th>Release Date_x</th>
      <th>Release Date_y</th>
      <th>Budget</th>
      <th>Revenue</th>
      <th>Box Office</th>
      <th>Genres</th>
      <th>Rating</th>
      <th>Runtime</th>
      <th>Metascore</th>
      <th>IMDb Rating</th>
      <th>Awards</th>
      <th>Production Company</th>
      <th>wins</th>
      <th>nominations</th>
      <th>Win or Nominated</th>
      <th>Oscar Wins</th>
      <th>Award_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Capote</td>
      <td>2005-09-30</td>
      <td>03 Feb 2006</td>
      <td>7000000.0</td>
      <td>49084830.0</td>
      <td>28337516.0</td>
      <td>Crime</td>
      <td>R</td>
      <td>114.0</td>
      <td>88.0</td>
      <td>7.4</td>
      <td>W1O, ++58,86</td>
      <td>Sony Pictures Classics</td>
      <td>58.0</td>
      <td>86.0</td>
      <td>W</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>American Hustle</td>
      <td>2013-12-12</td>
      <td>20 Dec 2013</td>
      <td>40000000.0</td>
      <td>251171807.0</td>
      <td>99165609.0</td>
      <td>Drama</td>
      <td>R</td>
      <td>138.0</td>
      <td>90.0</td>
      <td>7.3</td>
      <td>N10O, ++70,208</td>
      <td>Sony Pictures</td>
      <td>70.0</td>
      <td>208.0</td>
      <td>N</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Brokeback Mountain</td>
      <td>2005-09-10</td>
      <td>13 Jan 2006</td>
      <td>14000000.0</td>
      <td>178043761.0</td>
      <td>82970165.0</td>
      <td>Drama</td>
      <td>R</td>
      <td>134.0</td>
      <td>87.0</td>
      <td>7.7</td>
      <td>W3O, ++138,128</td>
      <td>Focus Features</td>
      <td>138.0</td>
      <td>128.0</td>
      <td>W</td>
      <td>3</td>
      <td></td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Walk the Line</td>
      <td>2005-09-13</td>
      <td>18 Nov 2005</td>
      <td>28000000.0</td>
      <td>186438883.0</td>
      <td>119317827.0</td>
      <td>Drama</td>
      <td>PG-13</td>
      <td>136.0</td>
      <td>72.0</td>
      <td>7.9</td>
      <td>W1O, ++44,46</td>
      <td>20th Century Fox</td>
      <td>44.0</td>
      <td>46.0</td>
      <td>W</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Good Night, and Good Luck.</td>
      <td>2005-09-16</td>
      <td>04 Nov 2005</td>
      <td>7000000.0</td>
      <td>54600000.0</td>
      <td>31500000.0</td>
      <td>Drama</td>
      <td>PG</td>
      <td>93.0</td>
      <td>80.0</td>
      <td>7.5</td>
      <td>N6O, ++38,121</td>
      <td>Warner Independent Pictures</td>
      <td>38.0</td>
      <td>121.0</td>
      <td>N</td>
      <td>6</td>
      <td></td>
    </tr>
  </tbody>
</table>
</div>




```python
#New data frame
date_table=date_df[['Movie','Box Office', 'Release Date_x','Award_date', 'Win or Nominated']]
date_table.head()
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
      <th>Movie</th>
      <th>Box Office</th>
      <th>Release Date_x</th>
      <th>Award_date</th>
      <th>Win or Nominated</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capote</td>
      <td>28337516.0</td>
      <td>2005-09-30</td>
      <td></td>
      <td>W</td>
    </tr>
    <tr>
      <th>1</th>
      <td>American Hustle</td>
      <td>99165609.0</td>
      <td>2013-12-12</td>
      <td></td>
      <td>N</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Brokeback Mountain</td>
      <td>82970165.0</td>
      <td>2005-09-10</td>
      <td></td>
      <td>W</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Walk the Line</td>
      <td>119317827.0</td>
      <td>2005-09-13</td>
      <td></td>
      <td>W</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Good Night, and Good Luck.</td>
      <td>31500000.0</td>
      <td>2005-09-16</td>
      <td></td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>




```python
#extract year from "Release Date_x"
date_table['Release Year'] = pd.DatetimeIndex(date_table['Release Date_x']).year
date_table['Release Month'] = pd.DatetimeIndex(date_table['Release Date_x']).month
date_table.head()
```

    /Users/choiwa/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    /Users/choiwa/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      This is separate from the ipykernel package so we can avoid doing imports until





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
      <th>Movie</th>
      <th>Box Office</th>
      <th>Release Date_x</th>
      <th>Award_date</th>
      <th>Win or Nominated</th>
      <th>Release Year</th>
      <th>Release Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capote</td>
      <td>28337516.0</td>
      <td>2005-09-30</td>
      <td></td>
      <td>W</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>American Hustle</td>
      <td>99165609.0</td>
      <td>2013-12-12</td>
      <td></td>
      <td>N</td>
      <td>2013.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Brokeback Mountain</td>
      <td>82970165.0</td>
      <td>2005-09-10</td>
      <td></td>
      <td>W</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Walk the Line</td>
      <td>119317827.0</td>
      <td>2005-09-13</td>
      <td></td>
      <td>W</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Good Night, and Good Luck.</td>
      <td>31500000.0</td>
      <td>2005-09-16</td>
      <td></td>
      <td>N</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Assigning Award Date Value to each year 

bins = [0, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015]
labels = ['2005-02-27', '2006-03-05', '2007-02-25', '2008-02-24', '2009-02-22', '2010-03-07',
          '2011-02-27', '2012-02-26', '2013-02-24', '2014-03-02', '2015-02-22', '2016-02-28']

date_table['Award_date'] = pd.cut(date_table['Release Year'], bins=bins, labels=labels)
date_table
```

    /Users/choiwa/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:7: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      import sys





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
      <th>Movie</th>
      <th>Box Office</th>
      <th>Release Date_x</th>
      <th>Award_date</th>
      <th>Win or Nominated</th>
      <th>Release Year</th>
      <th>Release Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capote</td>
      <td>28337516.0</td>
      <td>2005-09-30</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>American Hustle</td>
      <td>99165609.0</td>
      <td>2013-12-12</td>
      <td>2014-03-02</td>
      <td>N</td>
      <td>2013.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Brokeback Mountain</td>
      <td>82970165.0</td>
      <td>2005-09-10</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Walk the Line</td>
      <td>119317827.0</td>
      <td>2005-09-13</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Good Night, and Good Luck.</td>
      <td>31500000.0</td>
      <td>2005-09-16</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Syriana</td>
      <td>50800000.0</td>
      <td>2005-11-23</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Crash</td>
      <td>55382847.0</td>
      <td>2005-05-06</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Cinderella Man</td>
      <td>61600000.0</td>
      <td>2005-06-02</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>A History of Violence</td>
      <td>31500000.0</td>
      <td>2005-09-23</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Mrs Henderson Presents</td>
      <td>10965943.0</td>
      <td>2005-09-08</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Transamerica</td>
      <td>8713873.0</td>
      <td>2005-12-23</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Pride</td>
      <td>0.0</td>
      <td>2014-09-12</td>
      <td>2015-02-22</td>
      <td>N</td>
      <td>2014.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>North Country</td>
      <td>18324242.0</td>
      <td>2005-02-12</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Junebug</td>
      <td>2416555.0</td>
      <td>2005-08-03</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>The Constant Gardener</td>
      <td>33565375.0</td>
      <td>2005-08-31</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Being George Clooney</td>
      <td>0.0</td>
      <td>2016-02-06</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Little Italy</td>
      <td>0.0</td>
      <td>2018-08-24</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Made in France</td>
      <td>0.0</td>
      <td>2015-10-27</td>
      <td>2016-02-28</td>
      <td>NaN</td>
      <td>2015.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>A John Williams Celebration</td>
      <td>0.0</td>
      <td>2015-06-15</td>
      <td>2016-02-28</td>
      <td>NaN</td>
      <td>2015.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Blood Diamond</td>
      <td>57300000.0</td>
      <td>2006-12-07</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Half Nelson</td>
      <td>2591047.0</td>
      <td>2006-08-11</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Venus</td>
      <td>3261449.0</td>
      <td>2006-09-02</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>The Pursuit of Happyness</td>
      <td>162586036.0</td>
      <td>2006-12-14</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>The Last King of Scotland</td>
      <td>17449410.0</td>
      <td>2006-09-01</td>
      <td>2007-02-25</td>
      <td>W</td>
      <td>2006.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Little Miss Sunshine</td>
      <td>59831476.0</td>
      <td>2006-07-26</td>
      <td>2007-02-25</td>
      <td>W</td>
      <td>2006.0</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Little Children</td>
      <td>5307219.0</td>
      <td>2006-10-06</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Dreamgirls</td>
      <td>103300000.0</td>
      <td>2006-12-25</td>
      <td>2007-02-25</td>
      <td>W</td>
      <td>2006.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>The Departed</td>
      <td>132300000.0</td>
      <td>2006-10-05</td>
      <td>2007-02-25</td>
      <td>W</td>
      <td>2006.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Volver</td>
      <td>12830604.0</td>
      <td>2006-03-16</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Notes on a Scandal</td>
      <td>17400000.0</td>
      <td>2006-12-25</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>12.0</td>
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
    </tr>
    <tr>
      <th>537</th>
      <td>He Got Game</td>
      <td>0.0</td>
      <td>1998-05-01</td>
      <td>2005-02-27</td>
      <td>NaN</td>
      <td>1998.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>538</th>
      <td>Mumford</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>539</th>
      <td>King Richard and the Crusaders</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>540</th>
      <td>...Og det var Danmark</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>541</th>
      <td>La môme aux boutons</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>542</th>
      <td>I'm Not There</td>
      <td>4000000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>543</th>
      <td>A Christmas Eve Conversation with Quentin Tara...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>544</th>
      <td>Julie</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>545</th>
      <td>Rosy-Fingered Dawn: a Film on Terrence Malick</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>546</th>
      <td>Wallace</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>547</th>
      <td>Don't Tell Mom the Babysitter's Dead</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>548</th>
      <td>The Making of 'Sophie Scholl - Die letzten Tage'</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>549</th>
      <td>Siðasti bærinn í dalnum</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>550</th>
      <td>Eddie Murphy: Raw</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>551</th>
      <td>My Country, No More</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>552</th>
      <td>Indigènes: Sur les traces d'indigène</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>553</th>
      <td>The Stig-Helmer Story</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>554</th>
      <td>Flags of our Fathers</td>
      <td>33600000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>555</th>
      <td>Katyn</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>556</th>
      <td>The Betrayal - Nerakhoon</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>557</th>
      <td>The Lady and the Reaper (La dama y la muerte)</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>558</th>
      <td>GasLand</td>
      <td>30846.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>559</th>
      <td>Bandits en automobile - Épisode 2: Hors-la-loi</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>560</th>
      <td>Eros, O Deus do Amor</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>561</th>
      <td>Chico</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>562</th>
      <td>God Is the Bigger Elvis</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>563</th>
      <td>The Fantastic Flying Books of Mr. Morris Lessmore</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>W</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>564</th>
      <td>Jagal Bhaag Hamar</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>565</th>
      <td>Star Trek: Into Darkness</td>
      <td>228756232.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>566</th>
      <td>Theeb</td>
      <td>128430.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>567 rows × 7 columns</p>
</div>




```python
#data cleaning
date_table = date_table.replace('', np.nan)
date_table2 = date_table.dropna()
date_table2.head(30)
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
      <th>Movie</th>
      <th>Box Office</th>
      <th>Release Date_x</th>
      <th>Award_date</th>
      <th>Win or Nominated</th>
      <th>Release Year</th>
      <th>Release Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capote</td>
      <td>28337516.0</td>
      <td>2005-09-30</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>American Hustle</td>
      <td>99165609.0</td>
      <td>2013-12-12</td>
      <td>2014-03-02</td>
      <td>N</td>
      <td>2013.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Brokeback Mountain</td>
      <td>82970165.0</td>
      <td>2005-09-10</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Walk the Line</td>
      <td>119317827.0</td>
      <td>2005-09-13</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Good Night, and Good Luck.</td>
      <td>31500000.0</td>
      <td>2005-09-16</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Syriana</td>
      <td>50800000.0</td>
      <td>2005-11-23</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Crash</td>
      <td>55382847.0</td>
      <td>2005-05-06</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Cinderella Man</td>
      <td>61600000.0</td>
      <td>2005-06-02</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>A History of Violence</td>
      <td>31500000.0</td>
      <td>2005-09-23</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Mrs Henderson Presents</td>
      <td>10965943.0</td>
      <td>2005-09-08</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Transamerica</td>
      <td>8713873.0</td>
      <td>2005-12-23</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Pride</td>
      <td>0.0</td>
      <td>2014-09-12</td>
      <td>2015-02-22</td>
      <td>N</td>
      <td>2014.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>North Country</td>
      <td>18324242.0</td>
      <td>2005-02-12</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Junebug</td>
      <td>2416555.0</td>
      <td>2005-08-03</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>The Constant Gardener</td>
      <td>33565375.0</td>
      <td>2005-08-31</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Blood Diamond</td>
      <td>57300000.0</td>
      <td>2006-12-07</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Half Nelson</td>
      <td>2591047.0</td>
      <td>2006-08-11</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Venus</td>
      <td>3261449.0</td>
      <td>2006-09-02</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>The Pursuit of Happyness</td>
      <td>162586036.0</td>
      <td>2006-12-14</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>The Last King of Scotland</td>
      <td>17449410.0</td>
      <td>2006-09-01</td>
      <td>2007-02-25</td>
      <td>W</td>
      <td>2006.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Little Miss Sunshine</td>
      <td>59831476.0</td>
      <td>2006-07-26</td>
      <td>2007-02-25</td>
      <td>W</td>
      <td>2006.0</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Little Children</td>
      <td>5307219.0</td>
      <td>2006-10-06</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Dreamgirls</td>
      <td>103300000.0</td>
      <td>2006-12-25</td>
      <td>2007-02-25</td>
      <td>W</td>
      <td>2006.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>The Departed</td>
      <td>132300000.0</td>
      <td>2006-10-05</td>
      <td>2007-02-25</td>
      <td>W</td>
      <td>2006.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Volver</td>
      <td>12830604.0</td>
      <td>2006-03-16</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Notes on a Scandal</td>
      <td>17400000.0</td>
      <td>2006-12-25</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>30</th>
      <td>The Queen</td>
      <td>56222759.0</td>
      <td>2006-09-15</td>
      <td>2007-02-25</td>
      <td>W</td>
      <td>2006.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>31</th>
      <td>The Devil Wears Prada</td>
      <td>124700000.0</td>
      <td>2006-06-30</td>
      <td>2007-02-25</td>
      <td>N</td>
      <td>2006.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Babel</td>
      <td>34237104.0</td>
      <td>2006-09-08</td>
      <td>2007-02-25</td>
      <td>W</td>
      <td>2006.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Michael Clayton</td>
      <td>48976323.0</td>
      <td>2007-09-28</td>
      <td>2008-02-24</td>
      <td>W</td>
      <td>2007.0</td>
      <td>9.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
date_table2.dtypes
```




    Movie                 object
    Box Office           float64
    Release Date_x        object
    Award_date          category
    Win or Nominated      object
    Release Year         float64
    Release Month        float64
    dtype: object




```python
#save as a CSV file
date_table2.to_csv('Merge_Date.csv')
```
