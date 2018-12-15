

```python
%matplotlib notebook
```


```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
from matplotlib.ticker import FuncFormatter
```


```python
month_box_data = '../Month/Merge_Date.csv'
month_box = pd.read_csv(month_box_data, parse_dates=True)
month_box.head()
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
      <td>0</td>
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
      <td>1</td>
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
      <td>2</td>
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
      <td>3</td>
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
      <td>4</td>
      <td>Good Night, and Good Luck.</td>
      <td>31500000.0</td>
      <td>2005-09-16</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>9.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#categorize ranges of days
bins = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
labels = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'July', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']

month_box['Release Month'] = pd.cut(month_box['Release Month'], bins=bins, labels=labels)
month_box.head()
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
      <td>0</td>
      <td>Capote</td>
      <td>28337516.0</td>
      <td>2005-09-30</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>Sep</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>American Hustle</td>
      <td>99165609.0</td>
      <td>2013-12-12</td>
      <td>2014-03-02</td>
      <td>N</td>
      <td>2013.0</td>
      <td>Dec</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Brokeback Mountain</td>
      <td>82970165.0</td>
      <td>2005-09-10</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>Sep</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Walk the Line</td>
      <td>119317827.0</td>
      <td>2005-09-13</td>
      <td>2006-03-05</td>
      <td>W</td>
      <td>2005.0</td>
      <td>Sep</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Good Night, and Good Luck.</td>
      <td>31500000.0</td>
      <td>2005-09-16</td>
      <td>2006-03-05</td>
      <td>N</td>
      <td>2005.0</td>
      <td>Sep</td>
    </tr>
  </tbody>
</table>
</div>




```python
winner = month_box[month_box["Win or Nominated"] == "W"]
April_df = winner[winner['Release Month'] == 'Apr'] 
#Taxi to the Dark Side : Worldwide:$294,309, less than 1 million, no show
#Music by Prudence is short documentary, no Box office
winner_count = winner.groupby(["Release Month"]).count()["Win or Nominated"]
winner_box_sum = winner.groupby('Release Month')["Box Office"].sum().reset_index()
winner_box_sum['Box Office'] = winner_box_sum['Box Office'] / 1000000  #cover to Million
April_df
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
      <th>205</th>
      <td>253</td>
      <td>Taxi to the Dark Side</td>
      <td>0.0</td>
      <td>2007-04-30</td>
      <td>2008-02-24</td>
      <td>W</td>
      <td>2007.0</td>
      <td>Apr</td>
    </tr>
    <tr>
      <th>257</th>
      <td>317</td>
      <td>Music by Prudence</td>
      <td>0.0</td>
      <td>2010-04-01</td>
      <td>2011-02-27</td>
      <td>W</td>
      <td>2010.0</td>
      <td>Apr</td>
    </tr>
  </tbody>
</table>
</div>




```python
winner_box_mean = winner.groupby('Release Month')["Box Office"].mean().reset_index()
winner_box_mean['Box Office'] = winner_box_mean['Box Office'] / 1000000  #cover to Million
winner_box_mean
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
      <th>Release Month</th>
      <th>Box Office</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jan</td>
      <td>6.105753</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Feb</td>
      <td>39.625670</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mar</td>
      <td>113.493071</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Apr</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>May</td>
      <td>121.441022</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Jun</td>
      <td>117.262879</td>
    </tr>
    <tr>
      <th>6</th>
      <td>July</td>
      <td>100.387470</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Aug</td>
      <td>89.706071</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Sep</td>
      <td>55.661957</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Oct</td>
      <td>53.864344</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Nov</td>
      <td>87.993737</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Dec</td>
      <td>104.363655</td>
    </tr>
  </tbody>
</table>
</div>




```python
nominate = month_box[month_box["Win or Nominated"] == "N"]
nominate_count = nominate.groupby(["Release Month"]).count()["Win or Nominated"]
nominate_box_sum = nominate.groupby('Release Month')["Box Office"].sum().reset_index()
nominate_box_sum['Box Office'] = nominate_box_sum['Box Office'] / 1000000  #cover to Million
nominate_count
```




    Release Month
    Jan     21
    Feb     14
    Mar     13
    Apr     15
    May     21
    Jun     27
    July    14
    Aug     18
    Sep     48
    Oct     39
    Nov     28
    Dec     43
    Name: Win or Nominated, dtype: int64




```python
nominate_box_mean = nominate.groupby('Release Month')["Box Office"].mean().reset_index()
nominate_box_mean['Box Office'] = nominate_box_mean['Box Office'] / 1000000  #cover to Million
nominate_box_mean
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
      <th>Release Month</th>
      <th>Box Office</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jan</td>
      <td>7.733621</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Feb</td>
      <td>14.419626</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mar</td>
      <td>68.811342</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Apr</td>
      <td>113.974892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>May</td>
      <td>70.330679</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Jun</td>
      <td>126.301013</td>
    </tr>
    <tr>
      <th>6</th>
      <td>July</td>
      <td>110.172893</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Aug</td>
      <td>37.757970</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Sep</td>
      <td>23.629141</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Oct</td>
      <td>26.299758</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Nov</td>
      <td>52.973624</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Dec</td>
      <td>75.926077</td>
    </tr>
  </tbody>
</table>
</div>




```python
N = 12
avg_winner_value = winner_box_mean['Box Office']
avg_nominate_value = nominate_box_mean['Box Office']
avg_total_value = avg_winner_value + avg_nominate_value
ind = np.arange(N) 
width = 0.3 
w_a = plt.bar(ind, avg_winner_value, width, label='Winner', color='lightblue')
n_a = plt.bar(ind + width, avg_nominate_value, width, label='Nominate', color='gold')
total_a = plt.bar(ind + width*2, avg_total_value, width, label='Nominate', color='coral')
plt.xticks(ind + width / 2, ('Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'July', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'))

```


    <IPython.core.display.Javascript object>



<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA1oAAALaCAYAAAAoZSLyAAAAAXNSR0IArs4c6QAAQABJREFUeAHs3Qu8ZXPdP/DfmJmYkWvuoUahNBQpt1x6YlBoqEeiQqKL9AipSWV0oaTiUY8kD7mli2sqtxSVUErExFSEDHIdzOQy9n99V8/a/33O7HPOnH3W2Wfvtd/r9dqz917X3+/9W/vM+uzfWmuPq2VDMhAgQIAAAQIECBAgQIBAaQKLlbYmKyJAgAABAgQIECBAgACBXEDQsiMQIECAAAECBAgQIECgZAFBq2RQqyNAgAABAgQIECBAgICgZR8gQIAAAQIECBAgQIBAyQKCVsmgVkeAAAECBAgQIECAAAFByz5AgAABAgQIECBAgACBkgUErZJBrY4AAQIECBAgQIAAAQKCln2AAAECBAgQIECAAAECJQsIWiWDWh0BAgQIECBAgAABAgQELfsAAQIECBAgQIAAAQIEShYQtEoGtToCBAgQIECAAAECBAgIWvYBAgQIECBAgAABAgQIlCwgaJUManUECBAgQIAAAQIECBAQtOwDBAgQIECAAAECBAgQKFlA0CoZ1OoIECBAgAABAgQIECAgaNkHCBAgQIAAAQIECBAgULKAoFUyqNURIECAAAECBAgQIEBA0LIPECBAgAABAgQIECBAoGQBQatkUKsjQIAAAQIECBAgQICAoGUfIECAAAECBAgQIECAQMkCglbJoFZHgAABAgQIECBAgAABQcs+QIAAAQIECBAgQIAAgZIFBK2SQa2OAAECBAgQIECAAAECgpZ9gAABAgQIECBAgAABAiULCFolg1odAQIECBAgQIAAAQIEBC37AAECBAgQIECAAAECBEoWELRKBrU6AgQIECBAgAABAgQICFr2AQIECBAgQIAAAQIECJQsIGiVDGp1BAgQIECAAAECBAgQELTsAwQIECBAgAABAgQIEChZQNAqGdTqCBAgQIAAAQIECBAgIGjZBwgQIECAAAECBAgQIFCygKBVMqjVESBAgAABAgQIECBAQNCyDxAgQIAAAQIECBAgQKBkAUGrZFCrI0CAAAECBAgQIECAgKBlHyBAgAABAgQIECBAgEDJAoJWyaBWR4AAAQIECBAgQIAAAUHLPkCAAAECBAgQIECAAIGSBQStkkGtjgABAgQIECBAgAABAoKWfYAAAQIECBAgQIAAAQIlCwhaJYNaHQECBAgQIECAAAECBAQt+wABAgQIECBAgAABAgRKFhC0Sga1OgIECBAgQIAAAQIECAha9gECBAgQIECAAAECBAiULCBolQxqdQQIECBAgAABAgQIEBC07AMECBAgQIAAAQIECBAoWUDQKhnU6ggQIECAAAECBAgQICBo2QcIECBAgAABAgQIECBQsoCgVTKo1REgQIAAAQIECBAgQEDQsg8QIECAAAECBAgQIECgZAFBq2RQqyNAgAABAgQIECBAgICgZR8gQIAAAQIECBAgQIBAyQKCVsmgVkeAAAECBAgQIECAAAFByz5AgAABAgQIECBAgACBkgUErZJBrY4AAQIECBAgQIAAAQKCln2AAAECBAgQIECAAAECJQsIWiWDWh0BAgQIECBAgAABAgQELfsAAQIECBAgQIAAAQIEShYQtEoGtToCBAgQIECAAAECBAgIWvYBAgQIECBAgAABAgQIlCwgaJUManUECBAgQIAAAQIECBAQtOwDBAgQIECAAAECBAgQKFlA0CoZ1OoIECBAgAABAgQIECAgaNkHCBAgQIAAAQIECBAgULKAoFUyqNURIECAAAECBAgQIEBA0LIPECBAgAABAgQIECBAoGQBQatkUKsjQIAAAQIECBAgQICAoGUfIECgqcC4cePShRde2HSakaMrwL6v7z777JOmT5/ed2TF3730pS9Nxx9//IC1vOuuu1LsJzfddNOA83T7hD//+c9p0003TUsssUR6zWte09XVaVaX/uN6oU27uhEVnkALAoJWC2gWIdAtAt/85jfTUkstlZ577rl6kZ988sk0ceLEtOWWW9bHxYtf/vKX+YHbHXfckY+fM2dO2nHHHfvM0wlvnnnmmbTCCiukz3/+802Lc8wxx+TTY74FCxakeP+KV7wiTZo0KS2//PL5gdtpp53WdNkY+Ytf/CJ3mDp1ar5844zLLrtsOv300xtHjcrr0bDfZptt0sEHHzzi8hY+yy23XPrXv/7VZ3033HBDbhcBoMzhhBNOaIv7zJkz8/LvsMMOCxX/2GOPzaeFY5lD7E+xX43lcO+996YXvOAF+edkLMvRf9tHHnlkWnLJJdPtt9+efvazn/WfnL+PEB77W/F40YtelKL9br755qbzlz3y2muvTW9+85tTfB4iEK6//vrpK1/5ykJ/O5rVpf+4NdZY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B6brrrsuXXHFFem5557LfxPqqaee6rPk/vvvn+bMmVN/nHzyyX2m77nnnummm25Kl156af6I1xG2DAQIECBAgAABAgQIVE/A72gN0aYRjBqH0047LUXP1o033pi22mqr+qT4faVVVlml/r7xxaxZs/JwFWFtk002ySedcsopabPNNst7x9Zdd93G2b0mQIAAAQIECBAgQKDLBQStYTbg448/ni+x/PLL91ny7LPPTmeddVZaeeWV04477piOPPLI/HTDmOk3v/lNfrpgEbJi3KabbpqPu/baa1OzoPX000+neBRD/Gp3DPFDevHolqEoa/HcLeVuVs6iDsVzs3m6YVxR/uK5G8o8UBmLOhTPA83XDeOLOhTP3VDmgcpY1KF4Hmi+bhhf1KF47oYyNytjUf7iudk83TKuqEPx3C3lblbOog7Fc7N5umVcUYfiuVvK3b+cRfmL5/7Tq/i+l+ra7vYbV8uGdm+0W7cXVG9961tTXG/1y1/+sl6N6J2aMmVK3qP1pz/9Kc2YMSO9/OUvz081jJmOPvrodPrpp6c77rijvky8WGedddK+++6bz99nQvZm5syZ6aijjuo/Op1zzjkpes8MBAgQIECAAAECBEYqMG/evBSXuERnwtJLLz3S1Vm+QUCPVgPGUC8//OEPp5tvvjn96le/6jNrXJ9VDFOnTk1rr7122njjjdPvf//7tNFGG+WT4iYZ/YcIbs3Gx3wR1g455JD6ItGjtcYaa+TXh3XThyC+JYlr27bbbrs0ceLEen268UVV6lKVesQ+pC6d+UnSLp3XLtqk89okSqRdOq9dqtQmi6pbnDW1qPObb9EFBK1FtDrooIPSxRdfnK655pq0+uqrD7pUhKsIFbNnz86DVly79cADDyy0zD//+c/8VMOFJmQjFl988fzRf1qstxsDS7eWu79/vK9KXapSjyq1ibqEQGcOVfm8VKUesZeoi8/KaApUaf8ayinqahgdAXcdHMI1ep2iJ+v8889PV111VX6K4BCLpFtvvTX/lmrVVVfNZ42bXkR37A033FBf9Prrr8/Hbb755vVxXhAgQIAAAQIECBAgUA0BPVpDtGPc2j2ui7rooovym1vcf//9+RLxe1iTJk1Kf/3rX1PcCOPNb35zWmGFFdJtt92WDj300LThhhumLbbYIp/3la98Zdphhx1SnGJY3Pb9gAMOSDvttFPTG2EMUSSTCRAgQIAAAQIECBDocAE9WkM00EknnZT3PMWPEkcPVfH43ve+ly/5ghe8IP3sZz9L22+/fR6aPvKRj+TXUV155ZVp/Pjx9bVHGFt//fXzadOmTUsbbLBBOvPMM+vTvSBAgAABAgQIECBAoDoCerSGaMuhbsoYN6iIHzUeaojbwcft3w0ECBAgQIAAAQIECFRfQI9W9dtYDQkQIECAAAECBAgQaLOAoNVmcJsjQIAAAQIECBAgQKD6AoJW9dtYDQkQIECAAAECBAgQaLOAoNVmcJsjQIAAAQIECBAgQKD6AoJW9dtYDQkQIECAAAECBAgQaLOAoNVmcJsjQIAAAQIECBAgQKD6AoJW9dtYDQkQIECAAAECBAgQaLOA39FqM7jNESBAgMAQAjN3HWKGQSbPvGCQiSYRIECAAIH2CejRap+1LREgQIAAAQIECBAg0CMCglaPNLRqEiBAgAABAgQIECDQPgFBq33WtkSAAAECBAgQIECAQI8ICFo90tCqSYAAAQIECBAgQIBA+wQErfZZ2xIBAgQIECBAgAABAj0iIGj1SEOrJgECBAgQIECAAAEC7RMQtNpnbUsECBAgQIAAAQIECPSIgKDVIw2tmgQIECBAgAABAgQItE9A0GqftS0RIECAAAECBAgQINAjAoJWjzS0ahIgQIAAAQIECBAg0D4BQat91rZEgAABAgQIECBAgECPCAhaPdLQqkmAAAECBAgQIECAQPsEBK32WdsSAQIECBAgQIAAAQI9IiBo9UhDqyYBAgQIECBAgAABAu0TELTaZ21LBAgQIECAAAECBAj0iICg1SMNrZoECBAgQIAAAQIECLRPQNBqn7UtESBAgAABAgQIECDQIwKCVo80tGoSIECAAAECBAgQINA+AUGrfda2RIAAAQIECBAgQIBAjwgIWj3S0KpJgAABAgQIECBAgED7BASt9lnbEgECBAgQIECAAAECPSIgaPVIQ6smAQIECBAgQIAAAQLtExC02mdtSwQIECBAgAABAgQI9IiAoNUjDa2aBAgQIECAAAECBAi0T0DQap+1LREgQIAAAQIECBAg0CMCglaPNLRqEiBAgAABAgQIECDQPgFBq33WtkSAAAECBAgQIECAQI8ICFo90tCqSYAAAQIECBAgQIBA+wQErfZZ2xIBAgQIECBAgAABAj0iIGj1SEOrJgECBAgQIECAAAEC7RMQtNpnbUsECBAgQIAAAQIECPSIgKDVIw2tmgQIECBAgAABAgQItE9A0GqftS0RIECAAAECBAgQINAjAoJWjzS0ahIgQIAAAQIECBAg0D4BQat91rZEgAABAgQIECBAgECPCAhaPdLQqkmAAAECBAgQIECAQPsEBK32WdsSAQIECBAgQIAAAQI9IiBo9UhDqyYBAgQIECBAgAABAu0TELTaZ21LBAgQIECAAAECBAj0iICg1SMNrZoECBAgQIAAAQIECLRPQNBqn7UtESBAgAABAgQIECDQIwKCVo80tGoSIECAAAECBAgQINA+AUGrfda2RIAAAQIECBAgQIBAjwgIWj3S0KpJgAABAgQIECBAgED7BASt9lnbEgECBAgQIECAAAECPSIgaPVIQ6smAQIECBAgQIAAAQLtExC02mdtSwQIECBAgAABAgQI9IiAoNUjDa2aBAgQIECAAAECBAi0T0DQap+1LREgQIAAAQIECBAg0CMCglaPNLRqEiBAgAABAgQIECDQPgFBq33WtkSAAAECBAgQIECAQI8ICFo90tCqSYAAAQIECBAgQIBA+wQErfZZ2xIBAgQIECBAgAABAj0iIGj1SEOrJgECBAgQIECAAAEC7RMQtNpnbUsECBAgQIAAAQIECPSIgKDVIw2tmgQIECBAgAABAgQItE9A0GqftS0RIECAAAECBAgQINAjAoJWjzS0ahIgQIAAAQIECBAg0D4BQat91rZEgAABAgQIECBAgECPCAhaPdLQqkmAAAECBAgQIECAQPsEBK32WdsSAQIECBAgQIAAAQI9IiBo9UhDqyYBAgQIECBAgAABAu0TELTaZ21LBAgQIECAAAECBAj0iICg1SMNrZoECBAgQIAAAQIECLRPQNBqn7UtESBAgAABAgQIECDQIwKCVo80tGoSIECAAAECBAgQINA+AUGrfda2RIAAAQIECBAgQIBAjwgIWj3S0KpJgAABAgQIECBAgED7BASt9lnbEgECBAgQIECAAAECPSIgaPVIQ6smAQIECBAgQIAAAQLtExC02mdtSwQIECBAgAABAgQI9IiAoNUjDa2aBAgQIECAAAECBAi0T2BC+zZlSwQIECBAoMcEZu7aeoVnXtD6spYkQIAAgTEX0KM15k2gAAQIECBAgAABAgQIVE1A0Kpai6oPAQIECBAgQIAAAQJjLiBojXkTKAABAgQIECBAgAABAlUTELSq1qLqQ4AAAQIECBAgQIDAmAsIWmPeBApAgAABAgQIECBAgEDVBAStqrWo+hAgQIAAAQIECBAgMOYCgtaYN4ECECBAgAABAgQIECBQNQFBq2otqj4ECBAgQIAAAQIECIy5gKA15k2gAAQIECBAgAABAgQIVE1A0Kpai6oPAQIECBAgQIAAAQJjLiBojXkTKAABAgQIECBAgAABAlUTELSq1qLqQ4AAAQIECBAgQIDAmAsIWmPeBApAgAABAgQIECBAgEDVBAStqrWo+hAgQIAAAQIECBAgMOYCgtaYN4ECECBAgAABAgQIECBQNQFBq2otqj4ECBAgQIAAAQIECIy5gKA15k2gAAQIECBAgAABAgQIVE1A0Kpai6oPAQIECBAgQIAAAQJjLiBoDdEExxxzTHrd616XllpqqbTSSiul6dOnp9tvv73PUk8//XQ66KCD0gorrJCWXHLJtMsuu6R77723zzx333132nnnnfPpMd9HPvKR9Mwzz/SZxxsCBAgQIECAAAECBKohIGgN0Y5XX311OvDAA9N1112XrrjiivTcc8+ladOmpaeeeqq+5MEHH5wuuOCCdO6556Zf/epX6cknn0w77bRTWrBgQT5PPL/lLW/Jl4npMd95552XDj300Po6vCBAgAABAgQIECBAoDoCE6pTldGpyaWXXtpnxaeddlres3XjjTemrbbaKj3++OPp1FNPTWeeeWbadttt83nPOuustMYaa6Qrr7wybb/99unyyy9Pt912W7rnnnvSaqutls/zla98Je2zzz7pC1/4Qlp66aX7bMMbAgQIECBAgAABAgS6W0DQGmb7RbCKYfnll8+fI3A9++yzeS9XPiL7J8LU1KlT07XXXpsHrd/85jf5+yJkxXwRwOKUw1j+jW98Y7Fo/TmmxaMY5s6dm7+MbcWjW4airMVzt5S7WTmLOhTPzebphnFF+YvnbijzQGUs6lA8DzRfN4wv6lA8d0OZBypjUYfieaD5Bhy/2MQBJw05oeS/j0Udiucht99/hg6pS1H+4rl/MbvpfVGH4rmbyt6/rEUdiuf+07vpfVGH4rmbyt5Y1qL8xXPjtKq+7qW6trsNx9Wyod0b7dbtBdVb3/rW9Oijj6Zf/vKXeTXOOeectO+++/YJRTEhTi+cMmVKOvnkk9MBBxyQ7rrrrrxnq7Huiy++eDr99NPTO9/5zsbR+euZM2emo446aqHxsb3JkycvNN4IAgQIECBAgAABAsMVmDdvXtpzzz3zs7ScZTVcvcHn16M1uE+fqR/+8IfTzTffnF+H1WdCkzcRysaNG1ef0vi6GNl/nmJ8PM+YMSMdcsgh9VHRoxWnI0aA66YPQXxLEte2bbfddmnixBF8S12XGLsXValLVeoRe4K6jN3nYbAtj7hdjtlrsNUPPm3G2YNPH+bUqtRlxPUYpttozq4uo6nb+rqr0i5VqcdwWrI4a2o4y5h30QQErUVzyu8qePHFF6drrrkmrb766vWlVllllfzugdHLtdxyy9XHP/jgg2nzzTfP38c8119/fX1avIj548O88sor9xlfvInernj0HyKsdGNg6dZy9/eP91WpS1XqUaU2UZcQyIbnR3B69Ch9odPy56XD6tJyPf7dMh31r7p0VHPUC1OVdqlKPeoNM8iLqKthdATcdXAI1+h1ip6s888/P1111VX56YCNi7z2ta/ND7yj16YY5syZk/70pz/Vg9Zmm22Wv4/xxRA3yIggFcsbCBAgQIAAAQIECBColoAerSHaM27tHtdFXXTRRflvad1///35Essss0yaNGlSiuf99tsvv1X7i170ovwmGYcddlhaf/3163chjNP91ltvvfTud787ffnLX06PPPJIinn233//rjoNcAgqkwkQIECAAAECBAgQ+D8BQWuIXeGkk07K59hmm236zBm3eY/bs8fwta99LU2YMCHtvvvuaf78+elNb3pTOj27ycX48ePz6fH84x//OH3oQx9KW2yxRR7Q4qLD4447Lp/uHwIECBAgQIAAAQIEqiUgaA3RnnHq4FDDEksskU488cT8MdC8a665ZrrkkksGmmw8AQIECBAgQIAAAQIVEnCNVoUaU1UIECBAgAABAgQIEOgMAUGrM9pBKQgQIECAAAECBAgQqJCAoFWhxlQVAgQIECBAgAABAgQ6Q0DQ6ox2UAoCBAgQIECAAAECBCokIGhVqDFVhQABAgQIECBAgACBzhAQtDqjHZSCAAECBAgQIECAAIEKCQhaFWpMVSFAgAABAgQIECBAoDMEBK3OaAelIECAAAECBAgQIECgQgKCVoUaU1UIECBAgAABAgQIEOgMAUGrM9pBKQgQIECAAAECBAgQqJCAoFWhxlQVAgQIECBAgAABAgQ6Q2BCZxRDKQgQIEBgRAIzd2198ZkXtL6sJQkQIECAAIGmAnq0mrIYSYAAAQIECBAgQIAAgdYFBK3W7SxJgAABAgQIECBAgACBpgKCVlMWIwkQIECAAAECBAgQINC6gKDVup0lCRAgQIAAAQIECBAg0FRA0GrKYiQBAgQIECBAgAABAgRaFxC0WrezJAECBAgQIECAAAECBJoKCFpNWYwkQIAAAQIECBAgQIBA6wKCVut2liRAgAABAgQIECBAgEBTAUGrKYuRBAgQIECAAAECBAgQaF1A0GrdzpIECBAgQIAAAQIECBBoKiBoNWUxkgABAgQIECBAgAABAq0LCFqt21mSAAECBAgQIECAAAECTQUEraYsRhIgQIAAAQIECBAgQKB1AUGrdTtLEiBAgAABAgQIECBAoKmAoNWUxUgCBAgQIECAAAECBAi0LiBotW5nSQIECBAgQIAAAQIECDQVELSashhJgAABAgQIECBAgACB1gUErdbtLEmAAAECBAgQIECAAIGmAoJWUxYjCRAgQIAAAQIECBAg0LqAoNW6nSUJECBAgAABAgQIECDQVGBC07FGEiBAYDCBmbsONnXwaTMvGHy6qQQIECBAgACBCgjo0apAI6oCAQIECBAgQIAAAQKdJSBodVZ7KA0BAgQIECBAgAABAhUQELQq0IiqQIAAAQIECBAgQIBAZwm4Rquz2kNpCBAgQIAAAQIEulnAdczd3Hqlll2PVqmcVkaAAAECBAgQIECAAIGUBC17AQECBAgQIECAAAECBEoWELRKBrU6AgQIECBAgAABAgQICFr2AQIECBAgQIAAAQIECJQsIGiVDGp1BAgQIECAAAECBAgQELTsAwQIECBAgAABAgQIEChZQNAqGdTqCBAgQIAAAQIECBAgIGjZBwgQIECAAAECBAgQIFCygKBVMqjVESBAgAABAgQIECBAQNCyDxAgQIAAAQIECBAgQKBkAUGrZFCrI0CAAAECBAgQIECAgKBlHyBAgAABAgQIECBAgEDJAoJWyaBWR4AAAQIECBAgQIAAAUHLPkCAAAECBAgQIECAAIGSBQStkkGtjgABAgQIECBAgAABAoKWfYAAAQIECBAgQIAAAQIlCwhaJYNaHQECBAgQIECAAAECBAQt+wABAgQIECBAgAABAgRKFhC0Sga1OgIECBAgQIAAAQIECAha9gECBAgQIECAAAECBAiULCBolQxqdQQIECBAgAABAgQIEBC07AMECBAgQIAAAQIECBAoWUDQKhnU6ggQIECAAAECBAgQICBo2QcIECBAgAABAgQIECBQsoCgVTKo1REgQIAAAQIECBAgQEDQsg8QIECAAAECBAgQIECgZAFBq2RQqyNAgAABAgQIECBAgICgZR8gQIAAAQIECBAgQIBAyQKCVsmgVkeAAAECBAgQIECAAAFByz5AgAABAgQIECBAgACBkgUErZJBrY4AAQIECBAgQIAAAQKCln2AAAECBAgQIECAAAECJQsIWiWDWh0BAgQIECBAgAABAgQELfsAAQIECBAgQIAAAQIEShYQtEoGtToCBAgQIECAAAECBAgIWvYBAgQIECBAgAABAgQIlCwgaJUManUECBAgQIAAAQIECBAQtOwDBAgQIECAAAECBAgQKFlA0CoZ1OoIECBAgAABAgQIECAgaNkHCBAgQIAAAQIECBAgULKAoFUyqNURIECAAAECBAgQIEBA0LIPECBAgAABAgQIECBAoGQBQatkUKsjQIAAAQIECBAgQICAoGUfIECAAAECBAgQIECAQMkCglbJoFZHgAABAgQIECBAgAABQcs+QIAAAQIECBAgQIAAgZIFBK2SQa2OAAECBAgQIECAAAECgpZ9gAABAgQIECBAgAABAiULCFolg1odAQIECBAgQIAAAQIEBC37AAECBAgQIECAAAECBEoWmFDy+jpmdU8//XS64YYb0l133ZXmzZuXVlxxxbThhhumKVOmdEwZFYQAAQIECBAgQIAAgWoKVC5oXXvttenEE09MF154YXrmmWfSsssumyZNmpQeeeSRFOFrrbXWSgcccED6wAc+kJZaaqlqtqpaESBAgAABAgQIECAwpgKVOnXwrW99a3r729+eXvziF6fLLrssPfHEE+nhhx9O9957b96rNXv27PSpT30q/exnP0vrrLNOuuKKK8YU38YJECBAgAABAgQIEKimQKV6tKZNm5Z+8IMfpBe84AVNWyt6s+Kx9957p1tvvTXdd999TeczkgABAgQIECBAgAABAiMRqFTQOvDAAxfZ4lWvelWKh4EAAQIECBAgQIAAAQJlC1QqaDXDieu0HnzwwfT888/3mbzmmmv2ee8NAQIECBAgQIAAAQIEyhKobNCK67He+973prg5RuNQq9XSuHHj0oIFCxpHe02AAAECBAgQIECAAIHSBCobtPbZZ580YcKEdMkll6RVV101D1elqVkRAQIECBAgQIAAAQIEBhGobNC66aab0o033phe8YpXDFJ9kwgQIECAAAECBAgQIFC+QKVu797Is95666WHHnqocZTXBAgQIECAAAECBAgQaItAZYPWl770pXT44YenX/ziF/lvac2dOzc1PtqiayMECBAgQIAAAQIECPSkQGVPHdx2223zBn3Tm97Up2HdDKMPhzcECBAgQIAAAQIECIyCQGV7tH7+85+neFx11VV9HsW44Vhec801aeedd06rrbZaflONCy+8sM/iceONuJNh42PTTTftM8/TTz+dDjrooLTCCiukJZdcMu2yyy7p3nvv7TOPNwQIECBAgAABAgQIVEOgsj1aW2+9dWkt9NRTT6VXv/rVad99901ve9vbmq53hx12SKeddlp92gte8IL663hx8MEHpx/96Efp3HPPTS960YvSoYcemnbaaaf8hh3jx4/vM683BAgQIECAAAECBAh0t0Blg1Y0y2OPPZZOPfXUNGvWrLy3KW6QEb+ttcwyywyr1XbccccUj8GGxRdfPK2yyipNZ3n88cfzcpx55pmpOKXxrLPOSmussUa68sor0/bbb990OSMJECBAgAABAgQIEOhOgcoGrd/97nd5gJk0aVJ6/etfn+LarK9+9avpC1/4Qrr88svTRhttVGqLxU03VlpppbTsssum6E2L7cT7GOI2888++2yaNm1afZtxGuLUqVPzH1RuFrTiVMN4FEPcyCOGWE88umUoylo8d0u5m5WzqEPx3GyebhhXlL94bqnMi01sabF8oRL336IOxXPrhRr7JYs6FM/DLlGHtEmUu6hD8awuwxb49wI+K03hiv2qeG46U5eMLOpQPHdJsZsWs6hD8dx0pi4YWZS/eG6pyB3093hRyj+iui7KBnp4nnFZAKlVsf5bbrllevnLX55OOeWU/IeLo47PPfdcet/73pf+9re/pbjuqpUhrsO64IIL0vTp0+uLf+9730svfOEL00te8pJ05513pk9/+tP5tiJgRU/XOeeck5922BicYuEIXlOmTEknn3xyfV3Fi5kzZ6ajjjqqeFt/jnVNnjy5/t4LAgQIECBAgAABAq0KzJs3L+25554pzsBaeumlW12N5ZoIVLpHqzFkRd0nTJiQ3/J94403bkLR+qh3vOMd9YWjlyrWH6Hrxz/+cdptt93q0/q/KO6A2H98vJ8xY0Y65JBD6pOiRytONYxw1k0fgviW5IorrkjbbbddmjhxBL0gdYmxe1GVupRSj2P2ar0hZpzd+rL9liylLv3WOVZvR1yXDmmT8FOXhr2oQ9plxG3SUKWxfqkuY90CzbdflXYppR4d8rlv3lILjy3Omlp4ijEjFahs0Iowcvfdd6dXvOIVfYzuueeetNRSS/UZV/abVVddNQ9as2fPzlcd124988wz6dFHH03LLbdcfXMPPvhg2nzzzevvG19ET1g8+g8RVroxsHRrufv7x/uq1GVE9Xh+BKevjkLgHlFdmjXyGI5ruS4d1iYj+qyoy7/3QJ+VQT+JLX9WBl3r2ExUl7FxH2yrI2qTDvwbNlRdB5tuWusClb29e/Qy7bfffilO64twFbdSjzv+xamD73znO1sXW4QlH3744XybEbhieO1rX5sfnEfPTjHMmTMn/elPfxowaBXzeSZAgAABAgQIECBAoPsEKtujddxxx+V3GnzPe96TXy8VTRPfTnzwgx9MX/ziF4fVUk8++WT6y1/+Ul8mrsO66aab0vLLL58/4nqquO17BKu77rorffKTn8x/L2vXXXfNl4m7HEboi1u6x63dY7nDDjssrb/++vW7ENZX7gUBAgQIECBAgAABAl0vUNmgFb9jdcIJJ6Rjjjkm/fWvf83vOhg3x2jlRhJxB8M3vvGN9cYurp3ae++900knnZRuueWWdMYZZ+S3k4+wFfNGT1rjKYpf+9rX8mvEdt999zR//vz0pje9KZ1++unJb2jVWb0gQIAAAQIECBAgUBmBygatooUiWEXP0UiGbbbZJg9qA63jsssuG2hSffwSSyyRTjzxxPxRH+kFAQIECBAgQIAAAQKVFKhU0Io7/EUvUdwIY7C7/UVLnn/++ZVsUJUiQIAAAQIECBAgQGDsBSoVtOJaqPidqxjitYEAAQIECBAgQIAAAQJjIVCpoHXaaafVDRtf10d6QYAAAQIECBAgQIAAgTYIVPb27m2wswkCBAgQIECAAAECBAg0FahUj9aGG25YP3WwaW0bRv7+979veOclAQIECBAgQIAAAQIEyhOoVNCaPn16eTLWRIAAAQIECBAgQIAAgRYFKhW0jjzyyBYZLEaAAAECBAgQIECAAIHyBFyjVZ6lNREgQIAAAQIECBAgQCAXqFSP1nLLLbfI12g98sgjdgECBAgQIECAAAECBAiMikClgtbxxx8/KkhWSoAAAQIECBAgQIAAgeEIVCpo7b333sOpu3kJECBAgAABAgQIECAwKgKVClpz585NSy+9dA4VrwcbivkGm8c0AgQIECBAgAABAgQItCJQqaAV12jNmTMnrbTSSmnZZZdter1WrVbLxy9YsKAVL8sQIECAAAECBAgQIEBgSIFKBa2rrroqLb/88nmlf/7znw9ZeTMQIECAAAECBAh0gMDMXVsvxMwLWl/WkgRGUaBSQWvrrbeuUzW+ro/0ggABAgQIECBAgAABAm0QqFTQCq+77757kdjWXHPNRZrPTAQIECBAgAABAgQIEBiuQOWC1pQpU+oGcT1WDOPGjeszLt67RqtO4gUBAgQIECBAgAABAiULVC5oRYhaffXV0z777JN23nnnNGFC5apY8i5gdQQIECBAgAABAgQIlC1QuRRy7733pu985zvp9NNPT9/85jfTu971rrTffvulV77ylWXbWR8BAgQIECBAgAABAgSaCizWdGwXj1xllVXSxz/+8TRr1qz0wx/+MD366KNpk002SZtuumk65ZRT0vPPP9/FtVN0AgQIECBAgAABAgS6QaByQasR/Q1veEM69dRT0+zZs9PkyZPTBz7wgfTYY481zuI1AQIECBAgQIAAAQIESheodNC69tpr0/ve9760zjrrpCeffDJ94xvfyH/IuHRFKyRAgAABAgQIECBAgECDQOWu0ZozZ04644wz0mmnnZafNrjXXnulCFyvetWrGqrtJQECBAgQIECAAAECBEZPoHJB6yUveUlabbXV0t5775122WWXNHHixPxW7jfffHMfxQ022KDPe28IECBAgAABAgQIECBQlkDlgtZzzz2X/2jx5z73ufT5z38+dyp+T6tA8ztahYRnAgQIECBAgAABAgRGQ6ByQevOO+8cDSfrJECAAAECBAgQIECAwCILVC5oxamDBgIECBAgQIAAAQIECIylQKXuOnj33XcPy/If//jHsOY3MwECBAgQIECAAAECBBZFoFJB63Wve13af//90w033DBg3R9//PH8h4unTp2azj///AHnM4EAAQIECBAgQIAAAQKtClTq1MFZs2alo48+Ou2www753QY33njj/A6ESyyxRH6r99tuuy3deuutKcZ/+ctfTjvuuGOrbpYjQIAAAQIECBAgQIDAgAKV6tFafvnl03HHHZfuu+++dNJJJ+U/VPzQQw+l2bNn5wDxm1o33nhj+vWvfy1kDbhLmECAAAECBAgQIECAwEgFKtWjVWBED9Zuu+2WP4pxngkQIECAAAECBAgQINAugUr1aLULzXYIECBAgAABAgQIECAwmICgNZiOaQQIECBAgAABAgQIEGhBQNBqAc0iBAgQIECAAAECBAgQGExA0BpMxzQCBAgQIECAAAECBAi0ICBotYBmEQIECAKi7e4AAEAASURBVBAgQIAAAQIECAwmUOmgdeaZZ6Ytttgi/y2tv//977nD8ccfny666KLBTEwjQIAAAQIECBAgQIDAiAQqG7Tid7QOOeSQ9OY3vzk99thjacGCBTnUsssumyJsGQgQIECAAAECBAgQIDBaApUNWieeeGI65ZRT0hFHHJHGjx9f99t4443TLbfcUn/vBQECBAgQIECAAAECBMoWqGzQuvPOO9OGG264kNfiiy+ennrqqYXGG0GAAAECBAgQIECAAIGyBCobtKZMmZJuuummhZx++tOfpvXWW2+h8UYQIECAAAECBAgQIECgLIEJZa2o09bzsY99LB144IHpX//6V6rVaumGG25I3/3ud9MxxxyTvv3tb3dacZWHAAECBAgQIECAAIEKCVQ2aO27777pueeeS4cffniaN29e2nPPPdOLX/zidMIJJ6Q99tijQk2oKgQIECBAoA0CM3dtfSMzL2h9WUsSIECgSwUqG7SiPfbff//88dBDD6Xnn38+rbTSSl3aTIpNgAABAgQIECBAgEA3CVQ2aMXNMKJHa+21104rrLBCvU1mz56dJk6cmF760pfWx3lBgAABAqMgcMcyKY2f38KKp7ewjEUIECBAgEBnCVT2Zhj77LNPuvbaaxfSvv7661NMMxAgQIAAAQIECBAgQGC0BCobtP7whz+kLbbYYiG3TTfdtOndCBea0QgCBAgQIECAAAECBAi0KFDZoDVu3Lj0xBNPLMTy+OOPpwULFiw03ggCBAgQIECAAAECBAiUJVDZoLXlllvmt3JvDFXxOm7v/oY3vKEsP+shQIAAAQIECBAgQIDAQgKVvRnGsccem7baaqu07rrrpghdMfzyl79Mc+fOTVddddVCEEYQIECAAAECBAgQIECgLIHK9mitt9566eabb0677757evDBB/PTCN/znvekP//5z2nq1Kll+VkPAQIECBAgQIAAAQIEFhKobI9W1HS11VZLRx999EKVNoIAAQIECBAgQIAAAQKjKVCpoBU9WNFbtdhii+W9WYPBbbDBBoNNNo0AAQIECBAgQIAAAQItC1QqaL3mNa9J999/f1pppZVSvI47D9ZqtYVwYnzjTTIWmsEIAgQIECBAgAABAgQIjECgUkHrzjvvTCuuuGLOEa8NBAgQIECAAAECBAgQGAuBSgWtXXfdNf3sZz9Lyy23XPrOd76TDjvssDR58uSxcLVNAgR6VOD82+e0VvPs5yfGt7akpQgQIECAAIEOFKjUXQdnzZqVnnrqqZz5qKOOSk8++WQHkisSAQIECBAgQIAAAQJVF6hUj1Zcl7XvvvvmP0gc12Ydd9xx6YUvfGHTNvzMZz7TdLyRBAgQIECAAAECBAgQGKlApYLW6aefno488sh0ySWX5DfC+OlPf5omTFi4inEzDEFrpLuO5QkQIECAAAECBAgQGEhg4RQy0JxdMH7ddddN5557bl7SuMV7XK8VdyA0ECBAgAABAgQIECBAoJ0ClbpGa6ONNkqPPvpo7hc9WwOdNthOYNsiQIAAAQIECBAgQKD3BCoVtBpvhvHZz37WzTB6b39WYwIECBAgQIAAAQIdIVCpUwfdDKMj9imFIECAAAECBAgQINDzApUKWm6G0fP7MwACBAgQIECAAAECHSFQqaDlZhgdsU8pBAECFRBo+YeXo+5+fLkCe4AqECBAgMBIBSoVtBoxnn/++ca3XhMgQIAAAQIECBAgQKBtApW6GUaj2g9+8IO02267palTp6b1118/f/3DH/6wcRavCRAgQIAAAQIECBAgMCoClQta0ZP1jne8I3/cdttt6eUvf3laa6210q233pqP22OPPVKtVhsVTCslQIAAAQIECBAgQIBACFTu1MHjjz8+XXnlleniiy9OO+20U59WjnH77rtvOuGEE9LBBx/cZ5o3BAgQIECAAAECBAgQKEugcj1acefBL3/5ywuFrADbZZdd0rHHHptOPfXUsvyshwABAgQIECBAgAABAgsJVC5ozZ49O2277bYLVbQYEdP+8pe/FG89EyBAgAABAgQIECBAoHSByp06OGnSpPTYY4+lNddcsynW3LlzU8xjIECgQgJ3LJPS+PnDr9C504e/TOMSMy9ofOc1AQIECBAgQKAuULmgtdlmm6WTTjopf9Rr2fDiG9/4Rop5DAS6XaDl3znyG0fd3vTKT4AAAQIECHSBQOWC1hFHHJG22Wab9PDDD6fDDjssveIVr8jvMjhr1qz0la98JV100UXp5z//eRc0jSISIECAAAECBAgQINCtApULWptvvnn63ve+lw444IB03nnn9WmX5ZZbLn33u99NW2yxRZ/x3hAgQIAAAQIECBAgQKBMgcoFrcDZdddd0/bbb58uu+yyFDfHiGGdddZJ06ZNS5MnT87f+4cAAQIECBAgQIAAAQKjJVDJoBVYEagicBkIECBAgAABAgQIECDQboHK3d693YC2R4AAAQIECBAgQIAAgf4CglZ/Ee8JECBAgAABAgQIECAwQgFBa4SAFidAgAABAgQIECBAgEB/gcpeo9W/ot4TIECAAIGWBVr9Uew0wh/FbrnAFiRAgACBsRaobI/Wqaee2tT2ueeeSzNmzGg6zUgCBAgQIECAAAECBAiUIVDZoHXooYemt73tbemRRx6pO/35z39Or3/969P3v//9+jgvCBAgQIAAAQIECBAgULZAZYPWH/7wh/TAAw+k9ddfP11xxRXpG9/4Rtpoo43S1KlT00033VS2o/URIECAAAECBAgQIECgLlDZa7SmTJmSrrnmmvTRj3407bDDDmn8+PHpjDPOSHvssUe98l4QIECAAAECBAgQIEBgNAQq26MVWJdcckn67ne/mzbffPO07LLLplNOOSXdd999o+FonQQIECBAgAABAgQIEKgLVDZovf/970+77757Ovzww/OerZtvvjktvvji+amErtGqt78XBAgQIECAAAECBAiMgkBlTx389a9/na6//vr06le/OmdbZZVV0k9+8pP8Wq33vve9eQgbBU+rJECAAAECBAgQIECAQKps0LrxxhvzHqz+bXzggQembbfdtv9o7wkQIECAAAECBAgQIFCaQGWDVpwmGMM///nPdPvtt6dx48alddZZJ6244opp3XXXLQ3QiggQIECAAAECBAgQINBfoLLXaD311FMpThFcbbXV0lZbbZW23HLL/PV+++2X5s2b19/BewIECBAgQIAAAQIECJQmUNmgdcghh6Srr746XXzxxemxxx7LHxdddFE+Ln7M2ECAAAEC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QIAAAQIECHSLgKDVLS2lnAQIECBAgAABAgQIdI2AoNU1TaWgBAgQIECAAAECBAh0i4Cg1S0tpZwECBAgQIAAAQIECHSNwISuKamCEiBAgAABApUROP/2Oa3VZcGCNL61JS1FgACBtgro0Wort40RIECAAAECBAgQINALAoJWL7SyOhIgQIAAAQIECBAg0FYBQaut3DZGgAABAgQIECBAgEAvCLhGqxdaWR07Q2Dmrq2XY+YFrS9rSQIECBAYVQHXm40qr5UT6FoBPVpd23QKToAAAQIECBAgQIBApwro0erUllEuAgQIECBAgEC3CdyxTErj57dQ6uktLGMRAp0toEers9tH6QgQIECAAAECBAgQ6EIBQauERps5c2YaN25cn8cqq6xSX3OtVksxz2qrrZYmTZqUttlmm3TrrbfWp3tBgAABAgQIECBAgEC1BAStktrzVa96VZozZ079ccstt9TXfOyxx6avfvWr6etf/3r67W9/myKEbbfddumJJ56oz+MFAQIECBAgQIAAAQLVERC0SmrLCRMm5AEqQlQ8VlxxxXzN0Zt1/PHHpyOOOCLttttuaerUqek73/lOmjdvXjrnnHNK2rrVECBAgAABAgQIECDQSQKCVkmtMXv27PzUwClTpqQ99tgj/e1vf8vXfOedd6b7778/TZs2rb6lxRdfPG299dbp2muvrY/zggABAgQIECBAgACB6gi462AJbbnJJpukM844I62zzjrpgQceSJ///OfT5ptvnl+HFSErhpVXXrnPluL93//+9z7jGt88/fTTKR7FMHfu3Pzls88+m+LRLUNR1uK5W8rdrJxFHYrnZvMMOm6xiYNOHnRiszZfsGDQRQac+H/LPfv8pAFnGXJC2XUZcoPNZyjaouW6jKQeUaROapeR1KXMeoTLSPcxdQnF0dm/mrX1v7c29L+d0i7F/tVqXUZSj05rl5HUpZlfq/+vhEvRLq3+39IpdRlpPcKi7LrEOkdxKP4vHcVN9Oyqx2WnttV6tvajVPGnnnoqvexlL0uHH3542nTTTdMWW2yR7rvvvrTqqqvWt7j//vune+65J1166aX1cY0v4uYZRx11VOOo/HWcbjh58uSFxhtBgAABAgQIECBAYLgCcTnLnnvumR5//PG09NJLD3dx8w8ioEdrEJxWJy255JJp/fXXT3E64fTp//5diOjZagxaDz744EK9XI3bmzFjRjrkkEPqo6JHa4011shPQeymD0F8S3LFFVfkN/+YOHEEPTp1ibF7MeK6HLNX64WfcfZCy/5o9gMLjVukEdm3deP/dlPabq33pomLtfJbJ9lWzttpkTbVdKYmdWk63yKMrLdJq3UZST2ifE3qMmbtMpK6lFmPcBnpPqYuoTg6+1d2I6aW/xZ32t+wVusyknp0WruMpC4+9/nHbKF/Rvr3K1ZY8t+whcpY8ojirKmSV2t1mYCgNQq7QZzyN2vWrLTlllumuGYrbo4RYWPDDTfMt/bMM8+kq6++On3pS18acOtxHVc8+g/xH2TL/0n2X1kb33druZsRtVyX50dwymezkDp+fLPiLfK4CFkTW/pRyWwTZddlkUvdfMaW6zKSekRROqldRlKXUahHztPqPqYu/97RR6FdWv77FSXqsHZpuS4jqUe+Yzf50nCkf4+zto76DHsYSV2abW+E9ch5KvK5b/n/lUAou12GvWMMb4GW9r3hbaJn5xa0Smj6ww47LO28885pzTXXTNFTFddoxbcDe++9d/7bWgcffHA6+uij09prr50/4nWc/hfdtAYCBAgQIECAAAECBKonIGiV0Kb33ntveuc735keeuih/LbucV3Wddddl17ykpfka49rtebPn58+9KEPpUcffTTFzTMuv/zytNRSS5WwdasgQIAAAQIECBAgQKDTBAStElrk3HPPHXQt48aNS3Fzi3gYCBAgQIAAAQIECBCovoDf0ap+G6shAQIECBAgQIAAAQJtFhC02gxucwQIECBAgAABAgQIVF9A0Kp+G6shAQIECBAgQIAAAQJtFhC02gxucwQIECBAgAABAgQIVF9A0Kp+G6shAQIECBAgQIAAAQJtFhC02gxucwQIECBAgAABAgQIVF9A0Kp+G6shAQIECBAgQIAAAQJtFhC02gxucwQIECBAgAABAgQIVF9A0Kp+G6shAQIECBAgQIAAAQJtFhC02gxucwQIECBAgAABAgQIVF9A0Kp+G6shAQIECBAgQIAAAQJtFhC02gxucwQIECBAgAABAgQIVF9A0Kp+G6shAQIECBAgQIAAAQJtFhC02gxucwQIECBAgAABAgQIVF9A0Kp+G6shAQIECBAgQIAAAQJtFhC02gxucwQIECBAgAABAgQIVF9A0Kp+G6shAQIECBAgQIAAAQJtFpjQ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HPruU5b6PAJSL/VXL9RJ/dWJckS91F+9NFOd1J9uvnLEqIP5qm9KiwACCCCAAAIIIIAAAikI8IPFKSCzCQQQQAABBBBAAAEEEMiXAIFWvuqb0iKAAAIIIIAAAggggEAKAgRaKSCzieYUeOmll/xvmk2aNKk5C0ipEEDAC+i3Cx955BE0EEAAAQQQmCcBAq154mLmuMChhx5qe+21V3xSw71WGXQRVfzvn//8Z0OVJSxHqZ8KOO6443z5NE+jpdGjR/sHxXfZZZdGy7o1a52oXM3wvW/0MsS/EI38PYmXY/z48X6QqBVXXNH/juSyyy5rO++8s/3tb3+Lz9ZQr7/88ksbOHCg/yFY/Z6mRhn+3e9+50cgLqcgWd/QC49jF110UUF2deNB581GSWE5lOeOHTvaMsssYzvuuKPdfvvtNmfOnEYpBvlsQAECrQasNLJcWwFdxGu4/fi/lVdeubYbSWFtPXr0sPvvv9+mT58ebe2HH36w++67z3ThUk2aNWtWNYtXvKxOgr/97W/tlVde8b85V/GK3IKzZ89O/YSaZJ1UY8GyzSVQy+9JljJ77723vffee3bnnXfaJ598Yo899pgfsXbixIlZZqvibf/rX//yv5upsug4rBt4N954oz3//PP+tzQbpVydO3e2iy++2L777ruKLephwfBcP3bsWHv66adt22239UHv7rvvbj/++GM9ZJE8NKEAgVYTVmoWRfrzn/9sW265pS222GK25JJLmg5cn376aZQVHdh0J2nkyJH+4LbQQgvZz3/+87q4U9mpUyfTndP4Pw3tGgSBXXLJJbbKKqvYggsu6PP74IMPRmUKX4waNcp/ppPRpptuah988EH4Uap/N9xwQx9QyThMeq2L/Q022CCcZOXW1Z/+9Cd/kaNy3XPPPdHyab34/vvvTXk49thj/f40YsSIaNPhXd4nn3yyVXvNr/3xiSeesLXWWsvfIf/888+jdaTxolZ1st1229nxxx9fkGX9Jp/23RdeeKFgeppvevbsaVdddVXBJtdff32L/2qIvve33nqr9evXz/S9X3311f0FdMFCGb4ppwzx7NVbXbT1PQm/A/H8l2qJOP/8823ppZe2RRdd1I444gg744wzTPWYZlIXbN1Q0QW9LoDV8rPJJpvYmWeeabvttpvPyuTJk+2oo47yee3SpYupLhSYhUn7nfJ90003+eOe9rd9993Xsure/Zvf/MbUivWXv/zFtt56a3987tOnjz333HP21Vdf2aBBg3zWZ8yYYaeddprPs77T+o7cdtttNtadN2WhtPjii2fWM2GHHXbw58cLL7zQ56XUfw899JCtvfba/pik79Tll18ezaY6/MUvfhG9D1+st956du6554ZvE/8bnutXWGEF07H5D3/4gz366KM+6ArPL+3tY8qkbgD07t3bdG7s1q2b/epXv0o872ygcQUItBq37uoq5zrZn3zyyfbGG2/4u3Xzzz+/v7AqbpLXieX3v/+9vfvuu7bGGmvYAQccULd3ks466yy74447bPjw4fbhhx/aSSedZAcffLD99a9/LbA/9dRT7bLLLvNl18XKnnvuaVm1AB122GE+z2EGdaf78MMPD9/6v+XW1emnn24nnHCCffTRR777TsFKUnjzwAMP2Jprrun/yV11oeA3ntqznzZtmuniQBf6qkPVT9qpFnWii98//vGPpguyMN17772+O1J4IRZOr8e/Q4YMsf3228/ef/9923XXXe2ggw6yRrmbX+xZb3VRzvekuAzx99qPhg0b5gOct956ywcDOualnRZZZBHTPwWC8f08zIe++wq4vvnmG3vqqadMedXF8vbbb1+wL6nVSDdoHn/8cX9TSecaBTxpJ+3fzzzzjKnrtm7UxZNu6uk7oLpTuX7961/73gjXXHONP96q1UsWukmmAEZpzJgxvtfF1VdfHV9VKq914/GCCy6wa6+91v7973/PtU3Vhb7f+++/v7/RqIBXvxUaBi8q62uvvVZw81XHY92U1GdZJgXruumrm5Ll7GO6uafASvviO++84693FHSREGhVwO1YJAQqEjjkkEOCvn37llzW9bXXFXHgDqT+888++8y/dxe80fzuQOunuQv5aFraL1QGdxIJFl544ejfPvvsE/zvf/8L3N2qwD37UJAl19c+cMGhn/biiy/6/LvuetE8rpUhcCfVwJ1Ao2lpvAjr4r///W/g7toF8nZ3Q30ZNE31pHlKpdbqyrVUlJo9tWmbb755EObBBa6Bu3MYPPvss3775di7wMzXj7vQSi3P8Q3Vsk5cF9BgiSWWKNiv3J37wF3QxDeZyuuwXNqYa3UIrrzyyoLtuouWwN2ljqbpOOBuWkTv9d1yrVyB67oTTUv7RSVlePjhh30266kulKG2vif6DnTt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IBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAAOijFQAAAAjklEQVQCCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5FmAQCvPtU/ZEUAAAQQQQAABBBBAIBEBAq1EWFkpAggggAACCCCAAAII5Fng/wBHuBxvTQVzrwAAAABJRU5ErkJggg==" width="858">





    ([<matplotlib.axis.XTick at 0x11eaed8d0>,
      <matplotlib.axis.XTick at 0x11eaed240>,
      <matplotlib.axis.XTick at 0x11eaed0f0>,
      <matplotlib.axis.XTick at 0x11f1fc710>,
      <matplotlib.axis.XTick at 0x11f1fcbe0>,
      <matplotlib.axis.XTick at 0x11f205160>,
      <matplotlib.axis.XTick at 0x11f205630>,
      <matplotlib.axis.XTick at 0x11f205b38>,
      <matplotlib.axis.XTick at 0x11f20c0f0>,
      <matplotlib.axis.XTick at 0x11f20c588>,
      <matplotlib.axis.XTick at 0x11f20ca90>,
      <matplotlib.axis.XTick at 0x11f20ce80>],
     <a list of 12 Text xticklabel objects>)




```python
plt.grid()
plt.title('Winner VS Nominate Movie - Monthly Avg of Box Office', fontsize=10)
plt.xlabel('Month', fontsize=10)
plt.ylabel('Box Office (Million)', fontsize=10)
plt.show()
```


```python
# Save Figure
plt.savefig("../Month/avg_WN_boxMonth.png")
```


```python

```
