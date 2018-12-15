

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
winner_value = winner_box_sum['Box Office']
nominate_value = nominate_box_sum['Box Office']
total_value = winner_value + nominate_value
ind = np.arange(N) 
width = 0.3 
w_ = plt.bar(ind, winner_value, width, label='Winner', color='lightblue')
n_ = plt.bar(ind + width, nominate_value, width, label='Nominate', color='gold')
total_ = plt.bar(ind + width*2, total_value, width, label='Nominate', color='coral')
plt.xticks(ind + width / 2, ('Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'July', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'))
plt.legend((w_[0], n_[0], total_[0]), ('Winner', 'Nominate', 'Total'))
```


    <IPython.core.display.Javascript object>



<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA3UAAALgCAYAAAAz0l5kAAAAAXNSR0IArs4c6QAAQABJREFUeAHs3QecFEX6//GHHFSSShIDBhAJJjwxoXfmrJhBBUVMnBwih4feKSYwYM5yHmA40TtBPXMGFcUEfxFRUUFAUQwgSBSYf3/rrubXszs77O7s7nT3fur1WjtVd1e9a1jn2aqurpEKkpEQQAABBBBAAAEEEEAAAQRiKVAzlqWm0AgggAACCCCAAAIIIIAAAk6AoI4PAgIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQQAABBBBAAAEEEECAoI7PAAIIIIAAAggggAACCCAQYwGCuhg3HkVHAAEEEEAAAQQQQAABBAjq+AwggAACCCCAAAIIIIAAAjEWIKiLceNRdAQQqHyBGjVq2BNPPFH5N+IOxQSwzyTp06ePHXPMMZk72coQGDZsmLVo0cLCn52i+3DMIGMDAQQSIkBQl5CGpBoIIFCywD333GMbbbSRrVmzJp3p119/tTp16tg+++yT3qeVN954w30h/Pzzz93+BQsW2KGHHpqRJwobq1evtk022cSuvvrqrMUZMWKEO658a9euNW1vv/321qBBA2vWrJl169bNRo8enfVc7Xz99dedQ6dOndz54YxNmjSxMWPGhHdVynpl2O+33342cODAvMvrfZo2bWorV67MuN67777r7BRYVGS69dZbq8S9aJnn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TjvNBXmnnnqqffjhh7btttu67VQqFT4tY10BmoZ+Pv300+5n4sSJGUNDly1bZoMGDbIpU6a4oLFmzZp27LHH2rp169x13n33Xbd8+eWXbcGCBTZ+/Hi3PWrUKLv00kvtmmuusZkzZ7r6qg5jx47NuD8bCCCAAAIIIIAAAgiURqB2aTKRB4GqFFBgpF6yyy+/3O6///6MW9900022//77u0BOB9q1a2effPKJ3XDDDaZn8nw67LDD7JxzznGbl112md19992222672QknnOD2XXzxxbbHHnvY999/73oG/XnhpYIzBYsbbbSR263A8JVXXnHBmHYcd9xxbr/ytWjRwv7+97+7a6k8nTp1sk033dQd33jjjTPucdVVV7nexR49erjj6tHTOffee6/17t3b7eM/CCCAAAIIIIAAAgiUVoCeutJKka9KBfRcnXquFOyEk3q21AMXTtqeNWuWrV27Nr27S5cu6XUFXEoacumT37dw4UK/q9hSwzh9QKeDrVq1snB+9eT17NnT9fptscUWts0227hrzJ07t9i1/A4NAZ03b5717dvXDQPV8FD9aLhoeOimz88SAQQQQAABBBBAAIH1CdBTtz4hjhdEoHv37nbwwQfbJZdcktEDp+GSmiEznLINoaxTp046i8+fbZ8fKpnOHFoJ59duXSecX8/Qbb755q6HrVGjRtawYUNTMLl69erQVTJX/fkagrn77rtnHNTQUxICCCCAAAIIIIAAAmUVIKgrqxj5q0xArzbQMEwNsfRphx12sDfffNNvuuXkyZNdnqoMin766Sf3PJyGTKqncMmSJfbRRx9llKtu3bpuO9yDqB7CzTbbzL766ivr1atXRn42EEAAAQQQQAABBBAojwBBXXnUOKdKBDRcUoGPJk3x6aKLLnLPxum5NL1b7u2337Y77rijymePbNq0qelZufvuu889T/fpp5+6IZS+nFrqFQl6VYJmyWzTpo2b6VKzaGpylwEDBph69w499FBbtWqVm4lTr3HQxCskBBBAAAEEEEAAAQTKIsAzdWXRIm+VCyh4Cw+v3GWXXeyxxx6zcePGuclINAnKlVdemTFEsyoKqZkuVQbNxqkhlxomqucAw6l27dp22223ueGZrVu3dq9T0PGzzjrLTaqiSVgUuO67775uQhb/CoTwNVhHAAEEEEAAAQQQQGB9AvTUrU8oSce3L3n6/ihUU0FO0aR3zK1cuTJjt2ad9DNPZhz438acOXOK7Q4HhjqoSVDC+zRzpn58Um+afsJp4MCBph+f9E49TeSi5+Q0/FI9b+FrKp8COP0UTZpgRT8kBBBAAAEEEEAAAQTyFaCnLl9BzkcAAQQQQAABBBBAAAEECihAUFdAfG6NAAIIIIAAAggggAACCOQrQFBXRPCbb76xU0891U2CoSnqNfuinpvyScPrNCxPz0hpEoz99tvPZsyY4Q+7pSa80IuqNSmGfrS+ePHijDzTp093z1LpGpoNUc+FFR26l3ECGwgggAACCCCAAAIIIIBAFgGCuhCKgjFNT6/3kz333HPueakbb7zRmjRpks51/fXX20033eRmXHzvvfesZcuWduCBB9rSpUvTefSs1LRp09ysh5r5UOsK7HzS81c6R4GhrqHZHUeOHOmu6/OwRAABBBBAAAEEEEAAAQRKI1C7NJmqSx7NXqiXSY8ePTpdZU2o4ZN60m655Ra79NJLrUePHm732LFj3ZT2//znP+2cc85x7y5TIPfOO++kXy6tF03vscce9tlnn1n79u3t4YcfdpN/aGKQevXquVkcP//8cxfUaUp7/7Jsf1+WCCCAAAIIIIAAAggggEBJAgR1IZmnnnrKDj74YDvhhBNs4sSJbljk+eefb/369XO5Zs+ebd99950ddNBB6bMUlGlKer0AW0Gd3pumIZe77757Ok+3bt3cPuVRUKc8Okfn+qT7Dh061OYEMzdmm9pe7zLTj0/q7VP67bff3I/f7/cpANWsjPqJWvLDTH0Zo1a+spanKuqjdtR91N6V/ZJ13UPJL8vqEcX8vi5+GcUylqVMvh5+WZZzo5rX18Uvo1rO0pbL18MvS3teVPP5evhlVMtZlnL5uvhlWc6NYl5fD7+MYhnLUiZfD78sy7lRzevr4pflKmfNOuU6zZ30v/+/l/8C5T8zrzqX/7bV6kyCulBzf/XVV3b33Xe7F0DrvWPvvvuue0m0gq/TTz/dBXTK3qJFi9BZ/93++uuv3T4FfXrpdNGkfTqmpGW4B1D7/DV1LFtQN2LECLviiiuUNSO9+OKLpmf/wknvR9Ow0F9//dVWr14dPhSp9fCQ1UgVrJyFqcz6qB1XrFhhkyZNsjVr1pSzhGU77aWXXirbCTHInbQ6Ja0++gglrU7UJ/q/GGijaLdR0ton799zO/Yqf4M9+2z5z83zzOXLl+d5BU5fnwBBXUhIvSFdu3a14cOHu70777yzmwRFgZ6COp+KDo9UD0p4X3jdn7O+PL63J9u5uoZ68TQ00yf11GmoqHoN9X60cNJ73ebNm2cbbrih1a9fP3woEuuqqwKgjTbaKMMtEoUrRyGqoj5qU02q071790pvU/01Tf8T1XOfer40CSlpdUpaffQZS1qdqE/0f3PQRtFuo6S1T4X9nhuRR1A39OGCNbofYVawAlSDGxPUhRq5VatWtsMOO4T2mHXo0MEef/xxt0+9X0rqTVNenxYuXJjuaVOe77//3h9KL3/44YeMPL7XzmfQNZR8j53f75fqLQwP1/T79aW76BfvtWvXumCpZs2app+oJT8kVAFsFMtXVq+qqI+c5JWtvcta3tLmr8p7lbZM+eZLWp2SVh+1b9LqRH3y/Vdb+efTRpVvnM8dktY+ssirTuv++4hEuUwL+Ida1ZlUuQLR+8ZfufXNeXXNfKnJTMJJE5hsueWWbpeGRSpoCw8F0LA4PX+35557ujyaEOWXX35xQzf9daZMmeL2hfNoGF14aKSGUWo2zKLDMv01WFauwF/+8hfTs48kBBBAAAEEEEAAAQTiJkBPXajFLrzwQhecafjliSee6AKz++67z/SjpJ6SgQMHuuGZ2223nelHefVMm15joKSevUMOOcRNrnLvvfe6fWeffbYdccQRbpIU7VBePR/Xp08f07N7s2bNcte57LLLKnc44rBjXXmq7D/DJpT6ViUNO/UX6N27t40ZM8Zvlrg8+eST3bFx48aVmIcDCCCAAAIIIIAAAggkSYCgLtSau+22m02YMME9v6aXgatnTq8w6NXr/8YvDxkyxE1YoVkx9V47zXKpXjY9H+aTXlkwYMCA9CyZRx11lHuvnT+u2THV29e/f3/3DF/Tpk3d83LhZ+Z83uqyXLBgQbqqjz76qCnADfea6nkyEgIIIIAAAggggAACCBQXIKgrYqIeNf2UlNSjNGzYMPdTUp5mzZrZQw89VNJht79z585uJsOcmarRQf+8oqqsoFfO4X2eYurUqa63VENaFUjr9RN6QbyCPg2hVECo5Jd6fYSGVaoX9umnn7b58+e7Ya7q+VMvqWYKJSGAAAIIIIAAAgggEGcBvtHGufWqWdk1c5Le57f//vvbBx98YN9++62dddZZ7l1899xzj/31r3+1Tz/91KloW2njjTd2yyZNmtgDDzzgJriZNm2aO0/71KNKQgABBBBAAAEEEEAgzgIEdXFuvWpW9rFjx7oajx492k3r37FjR7v55pvd8496j5+GsfpXOBTt5bv88svTWpqMZvr06fbYY48R1KVVWEEAAQQQQAABBBCIqwBBXVxbrhqWe+bMmbbrrrumAzcRaMZSvcJBk8387ne/K1HlkUcesdtvv92+/PJLW7ZsmXuBd7aXxJd4AQ4ggAACCCCAAAIIIBBRAV5pENGGoVjFBYq+wF051vfSduXRKyf08vhjjjnGnn32WdNzeYMHD854pYTykRBAAAEEEEAAAQQQiKMAPXVxbLVqWma9GF4vgl+5cmW6t27y5MlushO9XkKpbt26bnbSMNGbb75p7dq1M81c6tOcOXP8KksEEEAAAQQQQAABBGItQE9drJuvehVeM1YqnXnmmTZjxgz3WgjNatm3b1/TpCdKel5OE6FoOOaPP/7ohlluu+229sUXX7iAUMMvNVvmM8884/LzHwQQQAABBBBAAAEE4i5AUBf3FqxG5W/UqJE9//zz9s0337hn60455RQ7/PDD3WQpnuG8886zLbbYwnbeeWfbdNNN7f3333cTqWi/XgKv/Rp+OXToUH8KSwQQQAABBBBAAAEEYi3A8MtYN18ZCz9sQhlPKEz2Pn36mH6ypV122cU9I5ftmPa1atXKXnnllWKH9RJ5/YRTeDjmtddeGz7EOgIIIIAAAggggAACsRGgpy42TUVBEUAAAQQQQAABBBBAAIHiAgR1xU3YgwACCCCAAAIIIIAAAgjERoCgLjZNRUERQAABBBBAAAEEEEAAgeICBHXFTdiDAAIIIIAAAggggAACCMRGgKAuNk1V9oL6F3OX/UzOiJoAbRm1FqE8CCCAAAIIIIBAdAQI6qLTFhVWklq1arlrrV69usKuyYUKK7B8+XJXgDp16hS2INwdAQQQQAABBBBAIHICvNIgck2Sf4Fq165tDRs2tB9++MEUBNSsGa3Yfd26daaAc+XKlZErW3n0K7M+6qFTQLdw4UL3gnUfsJennJyDAAIIIIAAAgggkEwBgroEtmuNGjXc+9pmz55tX3/9deRqqEBlxYoV1qBBA1NZ456qoj5NmjSxli1bxp2K8iOAAAIIIIAAAghUggBBXSWgRuGSdevWte222871iEWhPOEy/PbbbzZp0iTr3r2760kMH4vjemXXR72t9NDF8ZNBmRFAAAEEEEAAgaoRIKirGueC3EXDLuvXr1+Qe+e6qQKUNWvWuLIl4RmxpNUnV9txDAEEEEAAAQQQQCB6AtF62Cp6PpQIAQQQQAABBBBAAAEEEIi0AEFdpJuHwiGAAAIIIIAAAggggAACuQUI6nL7cBQBBBBAAAEEEEAAAQQQiLQAQV2km4fCIYAAAggggAACCCCAAAK5BQjqcvtwFAEEEEAAAQQQQAABBBCItABBXaSbh8IhgAACCCCAAAIIIIAAArkFCOpy+3AUAQQQQAABBBBAAAEEEIi0AEFdpJuHwiGAAAIIIIAAAggggAACuQUI6nL7cBQBBBBAAAEEEEAAAQQQiLQAQV2km4fCIYAAAggggAACCCCAAAK5BQjqcvtwFAEEEEAAAQQQQAABBBCItABBXaSbh8IhgAACCCCAAAIIIIAAArkFCOpy+3AUAQQQQAABBBBAAAEEEIi0AEFdpJuHwiGAAAIIIIAAAggggAACuQUI6nL7cBQBBBBAAAEEEEAAAQQQiLQAQV2km4fCIYAAAggggAACCCCAAAK5BQjqcvtwFAEEEEAAAQQQQAABBBCItABBXaSbh8IhgAACCCCAAAIIIIAAArkFCOpy+3AUAQQQQAABBBBAAAEEEIi0AEFdpJuHwiGAAAIIIIAAAggggAACuQUI6nL7cBQBBBBAAAEEEEAAAQQQiLQAQV2km4fCIYAAAggggAACCCCAAAK5BQjqcvtwFAEEEEAAAQQQQAABBBCItABBXaSbh8IhgAACCCCAAAIIIIAAArkFCOpy+3AUAQQQQAABBBBAAAEEEIi0AEFdpJuHwiGAAAIIIIAAAggggAACuQUI6nL7cBQBBBBAAAEEEEAAAQQQiLQAQV2km4fCIYAAAggggAACCCCAAAK5BQjqcvtwFAEEEEAAAQQQQAABBBCItABBXaSbh8IhgAACCCCAAAIIIIAAArkFCOpy+3AUAQQQQAABBBBAAAEEEIi0AEFdpJuHwiGAAAIIIIAAAggggAACuQUI6nL7cBQBBBBAAAEEEEAAAQQQiLQAQV2km4fCIYAAAggggAACCCCAAAK5BQjqcvtwFAEEEEAAAQQQQAABBBCItABBXaSbh8IhgAACCCCAAAIIIIAAArkFCOpy+3AUAQQQQAABBBBAAAEEEIi0AEFdpJuHwiGAAAIIIIAAAggggAACuQUI6nL7cBQBBBBAAAEEEEAAAQQQiLQAQV2km4fCIYAAAggggAACCCCAAAK5BQjqcvtwFAEEEEAAAQQQQAABBBCItABBXaSbh8IhgAACCCCAAAIIIIAAArkFCOpy+3AUAQQQQAABBBBAAAEEEIi0AEFdpJuHwiGAAAIIIIAAAggggAACuQUI6nL7cBQBBBBAAAEEEEAAAQQQiLQAQV2km4fCIYAAAggggAACCCCAAAK5BQjqcvtwFAEEEEAAAQQQQAABBBCItABBXaSbh8IhgAACCCCAAAIIIIAAArkFCOpy+3AUAQQQQAABBBBAAAEEEIi0AEFdpJuHwiGAAAIIIIAAAggggAACuQUI6nL7cBQBBBBAAAEEEEAAAQQQiLQAQV2km4fCIYAAAggggAACCCCAAAK5BQjqcvtwFAEEEEAAAQQQQAABBBCItABBXaSbh8IhgAACCCCAAAIIIIAAArkFCOpy+3AUAQQQQAABBBBAAAEEEIi0AEFdpJuHwiGAAAIIIIAAAggggAACuQUI6nL7cBQBBBBAAAEEEEAAAQQQiLQAQV2oeYYNG2Y1atTI+GnZsmU6RyqVMuVp3bq1NWjQwPbbbz+bMWNG+rhWFi1aZKeddpo1btzY/Wh98eLFGXmmT59u++67r7vGZpttZldeeaXp2iQEEEAAAQQQQAABBBBAoKwCBHVFxDp27GgLFixI/ygA8+n666+3m266ye644w577733TAHfgQceaEuXLvVZrGfPnjZt2jR7/vnn3Y/WFdj5tGTJEneOAkNd4/bbb7eRI0e66/o8LBFAAAEEEEAAAQQQQACB0grULm3G6pKvdu3aLlgrWl/1pN1yyy126aWXWo8ePdzhsWPHWosWLeyf//ynnXPOOTZz5kwXyL3zzju2++67uzyjRo2yPfbYwz777DNr3769Pfzww7Zy5UobM2aM1atXzzp16mSff/65C+oGDRrkegmL3pttBBBAAAEEEEAAAQQQQKAkAYK6IjKzZs1ywysVcCkwGz58uG299dY2e/Zs++677+yggw5Kn6E8GkY5efJkF9S9/fbbbsilD+iUsVu3bm6f8iioUx6do3N9Ovjgg23o0KE2Z84ca9u2rd+dsVy1apXpxyf1+Cn99ttv7sfvj8NSZVbyyziUOVcZfT38MlfeOBzz9fDLOJR5fWX0dfHL9eWP+nFfD7+MenlLUz5fF78szTlRzuPr4ZdRLmtpyubr4ZelOSfqeXxd/DLq5V1f+Xw9/HJ9+aN+3NfDL6Ne3tKUz9fFL0tzTrE8NesU21XqHf/7/lXq/BWYMa86V2A5knwpgrpQ6yoYe+CBB6xdu3b2/fff29VXX2177rmne25OAZ2SeubCSdtff/2126U8zZs3Dx9269rnz9dyq622ysjjr6ljJQV1I0aMsCuuuCLjPG28+OKL1rBhw2L747DjpZdeikMxS11G6lNqqoJlpI0KRl/qG9NGpaYqSMaktY8Qk1Yn6lOQfxplumlebbRjrzLdKyPzs89mbFblxvLly6vydtXyXgR1oWY/9NBD01udO3d2wya32WYb0zBL9bgpaSKVcNKwzPC+8LrPt748fpKUbOf6a6gnT8MzfVJP3eabb+56Dhs1auR3x2Kpv9boF5qeR6xTJ4+/OEWkttQnIg2Roxi0UQ6ciByijSLSECUUI2nto2omrU7Up4QPb4R2V0gbjcgjqBv6cME0/AizghWgGtyYoC5HI2+wwQam4E5DMo855hiXU71prVq1Sp+1cOHCdO+dJk5RD1/R9MMPP2Tk8b12Pp+uoeR77Pz+8FLDNcNDNv0xBUVxDYziXHbvH15Sn7BGNNdpo2i2S7hUtFFYI3rrSWsfCSetTtQnev9uipYorzZa999HWIpes1TbBfxDuupMqlwBZr/M4atn2DT5iYI4DYtU0BbuMl+9erVNnDjRDdHUZTQhyi+//GLvvvtu+qpTpkxx+zSM0+eZNGmS6VyfNIRSs2EWHZbpj7NEAAEEEEAAAQQQQAABBEoSIKgLyQwePNgFaZoURcHY8ccfb+ou7t27txtiOXDgQDdxyoQJE+zjjz+2Pn36uOfZ9BoDpQ4dOtghhxxi/fr1M82AqR+tH3HEEW6SFOVRXvW46VxdQ9fSZCzMfCkdEgIIIIAAAggggAACCJRVgOGXIbH58+fbKaecYj/++KNtuumm7jk6BWZbbrmlyzVkyBBbsWKFnX/++e4l45pYRb1sG220UfoqemXBgAED0rNkHnXUUe69dj6DXkqu3r7+/ftb165drWnTpi6gCz8v5/OyRAABBBBAAAEEEEAAAQTWJ0BQFxIaN25caKv4qiYyGTZsmPspfvS/e5o1a2YPPfRQSYfdfj2npyGYJAQQQACBChIYdmx+Fxo2Ib/zORsBBBBAAIECCjD8soD43BoBBBBAAAEEEEAAAQQQyFeAoC5fQc5HAAEEEEAAAQQQQAABBAooQFBXQHxujQACCCCAAAIIIIAAAgjkK0BQl68g5yOAAAIIIIAAAggggAACBRQgqCsgPrdGAAEEEEAAAQQQQAABBPIVIKjLV5DzEUAAAQQQQAABBBBAAIECChDUFRCfWyOAAAIIIIAAAggggAAC+QoQ1OUryPkIIIAAAggggAACCCCAQAEFCOoKiM+tEUAAAQQQQAABBBBAAIF8BQjq8hXkfAQQQAABBBBAAAEEEECggAIEdQXE59YIIIAAAggggAACCCCAQL4CBHX5CnI+AggggAACCCCAAAIIIFBAAYK6AuJzawQQQAABBBBAAAEEEEAgXwGCunwFOR8BBBBAAAEEEEAAAQQQKKAAQV0B8bk1AggggAACCCCAAAIIIJCvAEFdvoKcjwACCCCAAAIIIIAAAggUUICgroD43BoBBBBAAAEEEEAAAQQQyFeAoC5fQc5HAAEEEEAAAQQQQAABBAooQFBXQHxujQACCCCAAAIIIIAAAgjkK0BQl68g5yOAAAIIIIAAAggggAACBRQgqCsgPrdGAAEEEEAAAQQQQAABBPIVIKjLV5DzEUAAAQQQQAABBBBAAIECChDUFRCfWyOAAAIIIIAAAggggAAC+QoQ1OUryPkIIIAAAggggAACCCCAQAEFCOoKiM+tEUAAAQQQQAABBBBAAIF8BQjq8hXkfAQQQAABBBBAAAEEEECggAIEdQXE59YIIIAAAggggAACCCCAQL4CBHX5CnI+AggggAACCCCAAAIIIFBAAYK6AuJzawQQQAABBBBAAAEEEEAgXwGCunwFOR8BBBBAAAEEEEAAAQQQKKAAQV0B8bk1AggggAACCCCAAAIIIJCvAEFdvoKcjwACCCCAAAIIIIAAAggUUICgroD43BoBBBBAAAEEEEAAAQQQyFeAoC5fQc5HAAEEEEAAAQQQQAABBAooQFBXQHxujQACCCCAAAIIIIAAAgjkK0BQl68g5yOAAAIIIIAAAggggAACBRQgqCsgPrdGAAEEEEAAAQQQQAABBPIVIKjLV5DzEUAAAQQQQAABBBBAAIECChDUFRCfWyOAAAIIIIAAAggggAAC+QoQ1OUryPkIIIAAAggggAACCCCAQAEFCOoKiM+tEUAAAQQQQAABBBBAAIF8BQjq8hXkfAQQQAABBBBAAAEEEECggAIEdQXE59YIIIAAAggggAACCCCAQL4CBHX5CnI+AggggAACCCCAAAIIIFBAAYK6AuJzawQQQAABBBBAAAEEEEAgXwGCunwFOR8BBBBAAAEEEEAAAQQQKKAAQV0B8bk1AggggAACCCCAAAIIIJCvAEFdvoKcjwACCCCAAAIIIIAAAggUUICgroD43BoBBBBAAAEEEEAAAQQQyFeAoC5fQc5HAAEEEEAAAQQQQAABBAooQFBXQHxujQACCCCAAAIIIIAAAgjkK0BQl68g5yOAAAIIIIAAAggggAACBRQgqCsgPrdGAAEEEEAAAQQQQAABBPIVIKjLV5DzEUAAAQQQQAABBBBAAIECChDUFRCfWyOAAAIIIIAAAggggAAC+QoQ1OUryPkIIIAAAggggAACCCCAQAEFCOoKiM+tEUAAAQQQQAABBBBAAIF8BQjq8hXkfAQQQAABBBBAAAEEEECggAIEdQXE59YIIIAAAggggAACCCCAQL4CBHX5CnI+AggggAACCCCAAAIIIFBAAYK6AuJzawQQQAABBBBAAAEEEEAgXwGCunwFOR8BBBBAAAEEEEAAAQQQKKAAQV0B8bk1AggggAACCCCAAAIIIJCvAEFdvoKcjwACCCCAAAIIIIAAAggUUICgroD43BoBBBBAAAEEEEAAAQQQyFeAoC5fQc5HAAEEEEAAAQQQQAABBAooQFBXQHxujQACCCCAAAIIIIAAAgjkK0BQl68g5yOAAAIIIIAAAggggAACBRQgqCsgPrdGAAEEEEAAAQQQQAABBPIVIKjLV5DzEUAAAQQQQAABBBBAAIECChDUFRCfWyOAAAIIIIAAAggggAAC+QoQ1OUryPkIIIAAAggggAACCCCAQAEFCOoKiM+tEUAAAQQQQAABBBBAAIF8BQjq8hXkfAQQQAABBBBAAAEEEECggAKJCOpWrVplb7zxhj344IN277332vjx42327Nl5s44YMcJq1KhhAwcOTF9L97rgggtsk002sQ022MCOOuoomz9/fvq4VubOnWtHHnmkO658AwYMsNWrV2fkmThxou26665Wv35923rrre2ee+7JOM4GAggggAACCCCAAAIIIFAagdqlyRTVPJMnT7bb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582bZxtttFGx/exAAAEEEEAAAQQQQAABBJIikIig7qSTTrK+ffvao48+agrk5s+fb+PGjXPDL0855ZSktBX1QAABBBBAAAEEEEAAAQSKCSRi+OXIkSPdjJenn366e5ZOtaxTp46dd955du211xarNDsQQAABBBBAAAEEEEAAgaQIJCKoq1u3rt166602YsQI+/LLLy2VStm2225rDRs2TEo7UQ8EEEAAAQQQQAABBBBAIKtAIoI6XzMFcZ07d/abLBFAAAEEEEAAAQQQQACBxAvENqjr0aOHjRkzxjRJitZzpfHjx+c6zDEEEEAAAQQQQAABBBBAILYCsQ3qGjdu7J6jk7zWSQgggAACCCCAAAIIIIBAdRSIbVA3evTodHuF19M7WUEAAQQQQAABBBBAAAEEqoFAIl5pUA3aiSoigAACCCCAAAIIIIAAAlkFYttTt/POO6eHX2atWWjnhx9+GNpiFQEEEEAAAQQQQAABBBBIjkBsg7pjjjkmOa1ATRBAAAEEEEAAAQQQQACBcgrENqi7/PLLy1llTkMAAQQQQAABBBBAAAEEkiPAM3XJaUtqggACCCCAAAIIIIAAAtVQILY9dU2bNi31M3U///xzNWxaqowAAggggAACCCCAAALVQSC2Qd0tt9xSHdqHOiKAAAIIIIAAAggggAACOQViG9T17t07Z8U4iAACCCCAAAIIIIAAAghUB4HYBnVLliyxRo0auTbSeq7k8+XKwzEEEEAAAQQQQAABBBBAII4CsQ3q9EzdggULrHnz5takSZOsz9elUim3f+3atXFsG8qMAAIIIIAAAggggAACCKxXILZB3auvvmrNmjVzFXzttdfWW1EyIIAAAggggAACCCCAAAJJFIhtULfvvvum2yO8nt7JCgIIIIAAAggggAACCCBQDQRiG9SpbebOnVuqJtpiiy1KlY9MCCCAAAIIIIAAAggggEDcBGId1LVt2zbtrefnlGrUqJGxT9s8U5cmYQUBBBBAAAEEEEAAAQQSJhDroE4BW5s2baxPnz525JFHWu3asa5Owj5aVAcBBBBAAAEEEEAAAQSqQiDWUdD8+fNt7NixNmbMGLvnnnvs1FNPtb59+1qHDh2qwo57IIAAAggggAACCCCAAAIFF6hZ8BLkUYCWLVvaxRdfbDNnzrR///vftmjRItt9992tW7duNmrUKFu3bl0eV+dUBBBAAAEEEEAAAQQQQCD6ArEO6sK8e++9t91///02a9Ysa9iwoZ177rm2ePHicBbWEUAAAQQQQAABBBBAAIHECSQmqJs8ebKdddZZ1q5dO/v111/tzjvvdC8lT1yLUSEEEEAAAQQQQAABBBBAICQQ62fqFixYYA888ICNHj3aDb3s1auXKbjr2LFjqIqsIoAAAggggAACCCCAAALJFYh1ULflllta69atrXfv3nbUUUdZnTp13OsLPvroo4wW69KlS8Y2GwgggAACCCCAAAIIIIBAUgRiHdStWbPGvYD8qquusquvvtq1iX9fnW8g3lPnJVgigAACCCCAAAIIIIBAEgViHdTNnj07iW1CnRBAAAEEEEAAAQQQQACBUgvEOqjT8EsSAggggAACCCCAAAIIIFCdBWI7++XcuXPL1G7ffPNNmfKTGQEEEEAAAQQQQAABBBCIg0Bsg7rddtvN+vXrZ++++26Jzr/88ot7CXmnTp1s/PjxJebjAAIIIIAAAggggAACCCAQV4HYDr+cOXOmDR8+3A455BA362XXrl3dTJj169d3rzf45JNPbMaMGab9N9xwgx166KFxbSPKjQACCCCAAAIIIIAAAgiUKBDbnrpmzZrZyJEj7dtvv7W7777bvXT8xx9/tFmzZrnK6p11H3zwgb311lsEdCU2PwcQQAABBBBAAAEEEEAg7gKx7anz8OqZ69Gjh/vx+1gigAACCCCAAAIIIIAAAtVFIPZBXXVpKOqJAAIIVAuBzxub1VpRjqoeU45zOAUBBBBAAIFkCMR2+GUy+KkFAggggAACCCCAAAIIIJCfAEFdfn6cjQACCCCAAAIIIIAAAggUVICgrqD83BwBBBBAAAEEEEAAAQQQyE+AoC4/P85GAAEEEEAAAQQQQAABBAoqkJig7sEHH7S99trLvavu66+/dqi33HKLPfnkkwUF5uYIIIAAAggggAACCCCAQGUKJCKo03vqBg0aZIcddpgtXrzY1q5d68yaNGliCuxICCCAAAIIIIAAAggggEBSBRIR1N1+++02atQou/TSS61WrVrpturatatNnz49vc0KAggggAACCCCAAAIIIJA0gUQEdbNnz7add965WNvUq1fPli1bVmw/OxBAAAEEEEAAAQQQQACBpAgkIqhr27atTZs2rVibPPfcc7bDDjsU288OBBBAAAEEEEAAAQQQQCApArWTUJE///nP1r9/f1u5cqWlUil799137ZFHHrERI0bY3//+9yRUkToggAACCCCAAAIIIIAAAlkFEhHUnXHGGbZmzRobMmSILV++3Hr27GmbbbaZ3XrrrXbyySdnrTg7EUAAAQQQQAABBBBAAIEkCCQiqFND9OvXz/38+OOPtm7dOmvevHkS2oc6IIAAAggggAACCCCAAAI5BRIR1GmiFPXUbbfddrbJJpukKzxr1iyrU6eObbXVVul9rCCAAAIIIIAAAgggUDCBzxub1VpRztsfU87zOC3pAomYKKVPnz42efLkYm01ZcoU0zESAggggAACCCCAAAIIIJBUgUQEdVOnTrW99tqrWBt169Yt66yYxTKyAwEEEEAAAQQQQAABBBCIqUAigroaNWrY0qVLizXBL7/8YmvXri22nx0IIIAAAggggAACCCCAQFIEEhHU7bPPPu71BeEATut6pcHee++dlLaiHggggAACCCCAAAIIIIBAMYFETJRy/fXXW/fu3a19+/amAE/pjTfesCVLltirr75arNLsQAABBBBAAAEEEEAAAQSSIpCInroddtjBPvroIzvxxBNt4cKFbijm6aefbp9++ql16tQpKW1FPRBAAAEEEEAAAQQQQACBYgKJ6KlTrVq3bm3Dhw8vVkF2IIAAAggggAACCCCAAAJJFohtUKeeOfXC1axZ0/XS5WqkLl265DrMMQQQQAABBBBAAAEEEEAgtgKxDep22mkn++6776x58+amdc2AmUqlijWE9ocnUCmWgR0IIIAAAggggAACCCCAQIwFYhvUzZ492zbddFNHr3USAggggAACCCCAAAIIIFAdBWIb1B177LH2yiuvWNOmTW3s2LE2ePBga9iwYXVsQ+qMAAIIIIAAAggggAAC1VggtrNfzpw505YtW+aa7oorrrBff/21GjcjVUcAAQQQQAABBBBAAIHqKhDbnjo9R3fGGWe4l4vrWbqRI0fahhtumLUdL7vssqz72YkAAggggAACCCCAAAIIxF0gtkHdmDFj7PLLL7enn37aTZLy3HPPWe3axaujiVII6uL+MaX8CCCAAAIIIIAAAgggUJJA8SiopJwR29++fXsbN26cK5Vea6Dn6zQTJgkBBBBAAAEEEEAAAQQQqE4CsX2mbpdddrFFixa5tlKPXUlDL6tTY1JXBBBAAAEEEEAAAQQQqH4Cse2p8xOlaPbLK6+80s477zxmv6x+n19qjAACCCCAAAIIZBcYdmz2/aXdO2xCaXOSD4GCC8S2p85PlKKZL/1EKQrusv2UVvnuu++2Ll26WKNGjdzPHnvsYXpWz6dVq1bZBRdcYJtssoltsMEGdtRRR9n8+fP9YbecO3euHXnkke648g0YMMBWr16dkWfixIm26667Wv369W3rrbe2e+65J+M4GwgggAACCCCAAAIIIIBAaQVi21NXGROltGnTxq699lrbdtttnZ/ef3f00Ufb1KlTrWPHjjZw4ED7z3/+457l23jjje2iiy6yI444wj744AOrVauWrV271g4//HD3UvQ333zTfvrpJ+vdu7cLOm+//XZ3Tb0o/bDDDrN+/frZQw89ZG+99Zadf/757pzjjjuutO1GPgQQQAABBBBAAAEEEEDACcQ2qKuMiVLUwxZO11xzjan37p133jEFfPfff789+OCDdsABB7hsCso233xze/nll+3ggw+2F1980T755BObN2+etW7d2uW58cYbrU+fPqZrqQdQvXJbbLGF3XLLLe54hw4d7P3333evZCCoC+uzjgACCCCAAAIIREtg/GcLyl+g4I//tcp/NmcikFMgtsMvw7Vat25dhc98qV43za6pF5xrGKZ643777Tc76KCD0rdW4NapUyebPHmy2/f222+7bR/QaaeCPQ3b1PlKyhO+hvYpjwI7XZ+EAAIIIIAAAggggAACCJRFILY9deFK/utf/7JHHnnEPv/8c/fOuu2228569uxpxx9/fDhbqdanT5/ugriVK1e6GTUnTJhgO+ywg02bNs3q1q1rmpglnFq0aGHfffed26WltsNJ+XVerjw6Z82aNfbjjz9aq1atwqen1xUY6senJUuWuFUFgnELBn15/dLXKa5LXw+/jGs9fLl9PfzS74/z0tfFL+NcF5Xd18Mv416fjDqta1C+6tSsU77z/FkV/Ec13zZ+6W8T16Wvh1/GtR7hcvu6+GX4WBzXfT38Mo51CJfZ18Mvw8dKvV4ZvxeCP/qXO/3v3N/K+3tON86nThX8e64sDnm1Y1luVI3zxjqoUw/dKaecYgrq2rVrZ9tvv717fm3GjBl20kkn2QknnOCCPb2AvLRJwzoVwC1evNgef/xx90ycJjYpKWmSlvD1w+v+nPXl0XGlbOf6a4wYMcI0KUzRpCGfDRs2LLo7FtsvvfRSLMpZ2kJSn9JKFS4fbVQ4+9Le+aWv/lHarJn5dszcLPPWs8+W+ZTSnMBnrjRKhc1DGxXWf313z6t9duy1vsvnPp7l90JFDJ8s9+85lTaf33VZ6pMboOKOLl++vOIuxpWyCsQ6qNNzaXqe7amnnnITloRrqH1nnHGG3XrrrW6Ck/CxXOvqVfMTpXTt2tXee+89dw0FiZrFUu/GC/fWLVy40Pbcc093yZYtW9qUKVMyLq/8+uuE78FTHt9r5zPqGrVr1zZNvlJSGjp0qA0aNCh9WD11ep5PQzn1rF6ckjz0S/rAAw+0OnXy/Ot6BCpOfSLQCOspAm20HqAIHE630dZnWp2aK8peosePKPs54TOGPhzeyns9XR9+z+VtWVkXoI0qS7Zirlsh7TMiz6Auy++F/8z6vvwV1DN1X02zA8v7e053zud3XZb6lL8yZTvTjzAr21nkLotArIM6zYB5ww03FAvoBKDXDVx//fVuQhLNWlnepF40DXvUKwgUgCgYOfHEE93lFixYYB9//LG7j3bo2TtNiKL9fhiletLq1avnzvd5NINmOCmPAshcAY6uoZ+iSefkOq9o/ihtx7ns2RypTzaVaO2jjaLVHtlKo4CuTq1yBHXr8nwmuZL+wMRnLlsrR2sfbRSt9ihamrzapzJ+LwSzneebyv17TjfOp06V9HuuNB5qR1LlCsR6opRZs2alZ6LMxqRZKr/44otsh7Luu+SSS+yNN96wOXPmmJ6tu/TSS+3111+3Xr16WePGja1v377uNQavvPKKe83Bqaeeap07d06XQb1mev7utNNOc8eVb/Dgwe71Bb437dxzz7Wvv/7a9brpBer/+Mc/3KyaykdCAAEEEEAAAQQQQAABBMoqEOueugYNGrhn3/SKgGxJXb3KU9r0/fffu4BMPW0K4vQi8ueff94NE9Q1br75ZjdMUj11K1assP3339/GBL2FekedkpbPPPOMe+/cXnvt5e6tCVtGjhzpjus/bdu2tWeDMc0XXnih3Xnnne7VB7fddpvxOoM0ESsIIIAAAggggAACCCBQBoFYB3Ua7qj3yOknW1LQpDylTXoPXa5Uv35900vE/YvEs+VVgPn0009nO5Tet++++9qHH36Y3mYFAQQQQAABBBBAAAEEECivQKyDOg2P3G+//eynn35ywxz97Jca1qiXfj/55JP22muvldeG8xBAAAEEEEAAAQQQQACByAvEOqjTrJOPPvqonX322e71A2FtzVCpd9dpGCQJAQQQQAABBBBAAAEEEEiqQKyDOjXKscceawcffLC98MILpolTlPTOOk1aEtf3t7lK8B8EEEAAAQQQQAABBBBAoBQCsQ/qVEcFbwruSAgggAACCCCAAAIIIIBAdROI9SsNqltjUV8EEEAAAQQQQAABBBBAoKgAQV1REbYRQAABBBBAAAEEEEAAgRgJENTFqLEoKgIIIIAAAggggAACCCBQVICgrqgI2wgggAACCCCAAAIIIIBAjAQSEdSV9NLwNWvW2NChQ2PUHBQVAQQQQAABBBBAAAEEECibQCKCuosuusiOO+44+/nnn9O1//TTT+13v/udPfbYY+l9rCCAAAIIIIAAAggggAACSRNIRFA3depU+/77761z58720ksv2Z133mm77LKLderUyaZNm5a0NqM+CCCAAAIIIIAAAggggEBaIBHvqWvbtq1NmjTJLrzwQjvkkEOsVq1a9sADD9jJJ5+crigrCCCAAAIIIIAAAggggEASBRLRU6eGefrpp+2RRx6xPffc05o0aWKjRo2yb7/9NoltRp0QQAABBBBAAAEEEEAAgbRAIoK6c845x0488UQbMmSI67H76KOPrF69em44Js/UpduaFQQQQAABBBBAAAEEEEigQCKGX7711ls2ZcoU23HHHV0TtWzZ0p599ln3bN2ZZ57pAr4Eth1VQgABBBBAAAEEEEAAAQQsEUHdBx984HrmirZn//797YADDii6m20EEEAAAQQQQAABBBBAIDECiQjqNNRS6YcffrDPPvvMatSoYe3atbNNN93U2rdvn5jGoiIIIIAAAggggAACCCCAQFGBRDxTt2zZMtMwy9atW1v37t1tn332cet9+/a15cuXF60z2wgggAACCCCAAAIIIIBAYgQSEdQNGjTIJk6caE899ZQtXrzY/Tz55JNun15MTkIAAQQQQAABBBBAAAEEkiqQiOGXjz/+uP373/+2/fbbL91Ohx12mDVo0MBNknL33Xen97OCAAIIIIAAAggggAACCCRJIBE9dRpi2aJFi2Lt0rx5c4ZfFlNhBwIIIIAAAggggAACCCRJIBFB3R577GGXX365rVy5Mt02K1assCuuuMJ0jIQAAggggAACCCCAAAIIJFUg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CBDoqICeuo5yWhkBAgQIECBAgAABAgR6KyCo6623rREgQIAAAQIECBAgQKCjAoK6jnJaGQECBAgQIECAAAECBHorIKjrrbetESBAgAABAgQIECBAoKMCgrqOcloZAQIECBAgQIAAAQIEeisgqOutt60RIECAAAECBAgQIECgowKCuo5yWhkBAgQIECBAgAABAgR6KyCo6623rREgQIAAAQIECBAgQKCjAoK6jnJaGQECBAgQIECAAAECBHorIKjrrbetESBAgAABAgQIECBAoKMC0zq6NisjQIAAAQIECBAg8LzAlYsWt2excmWa2t6SliIwKQX01E3KZldpAgQIECBAgAABAgSGRUBQNywtqR4ECBAgQIAAAQIECExKAUHdpGx2lSZAgAABAgQIECBAYFgEXFM3LC2pHgQIECBQPYF7Z6U0dVmb5dqvzeUsRoAAAQKTTUBQN9laXH0JECDQJYG2b4gQ5XFThC61itUSIECAwGQQMPxyMrSyOhIgQIAAAQIECBAgMLQCgrqhbVoVI0CAAAECBAgQIEBgMggI6iZDK6sjAQIECBAgQIAAAQJDK+CauqFtWhUjQGDoBdyEY+ibWAUJTHoBx7lJvwsAaE5AT11zTnIRIECAAAECBAgQIECgkgKCuko2i0IRIECAAAECBAgQIECgOQFBXXNOchEgQIAAAQIECBAgQKCSAoK6SjaLQhEgQIAAAQIECBAgQKA5AUFdc05yESBAgAABAgQIECBAoJICgrpKNotCESBAgAABAgQIECBAoDkBQV1zTnIRIECAAAECBAgQIECgkgKCuko2i0IRIECAAAECBAgQIECgOQFBXXNOchEgQIAAAQIECBAgQKCSAoK6SjaLQhEgQIAAAQIECBAgQKA5gWnNZZOLAAECLQjM37+FzA2yzr+qwUyzCBAgQIAAAQIEGgnoqWukYh4BAgQIECBAgAABAgQGREBQNyANpZgECBAgQIAAAQIECBBoJCCoa6RiHgECBAgQIECAAAECBAZEwDV1A9JQikmAAAECBAZawLW2A918Ck+AQLUF9NRVu32UjgABAgQIECBAgAABAmMKCOrG5PEiAQIECBAgQIAAAQIEqi0gqKt2+ygdAQIECBAgQIAAAQIExhQQ1I3J40UCBAgQIECAAAECBAhUW0BQV+32UToCBAgQIECAAAECBAiMKSCoG5PHiwQIECBAgAABAgQIEKi2gKCu2u2jdAQIECBAgAABAgQIEBhTQFA3Jo8XCRAgQIAAAQIECBAgUG0BQV2120fpCBAgQIAAAQIECBAgMKaAoG5MHi8SIECAAAECBAgQIECg2gKCumq3j9IRIECAAAECBAgQIEBgTAFB3Zg8XiRAgAABAgQIECBAgEC1BQR11W4fpSNAgAABAgQIECBAgMCYAoK6MXm8SIAAAQIECBAgQIAAgWoLTKt28ZSOAAECBAgQINBFgXtnpTR1WRsb2K+NZSxCgACB7gjoqeuOq7USIECAAAECBAgQIECgJwKCup4w2wgBAgQIECBAgAABAgS6I2D4ZXdcrZUAAQJjCly5aPGYr4/54sqVaeqYGbxIgAABAgQITCYBPXWTqbXVlQABAgQIECBAgACBoRMQ1A1dk6oQAQIECBAgQIAAAQKTSUBQN5laW10JECBAgAABAgQIEBg6AUFdqUm//e1vp7e//e1p0003TVOmTElf+cpXSq+mVKvV0vz58/PX11prrbTbbrulH/3oRyPyPPbYY2nevHlp1qxZ+V9MP/744yPy/OAHP0i77rprinVsttlm6eMf/3i+7hGZPCFAgAABAgQIECBAgEATAoK6EtLTTz+ddthhh/TZz362NPeFyVNPPTWdeeaZ+eu33XZb2njjjdMee+yRnnrqqXqm97znPemuu+5K3/jGN/K/mI7ArkhPPvlkvkwEjrGOs88+O51++un5eos8HgkQIECAAAECBAgQINCsgLtflqT22WefFH+NUvTSnXXWWemkk05K73rXu/IsF110Udpoo43SZZddlt7//vene+65Jw/kvvvd76bXv/71eZ7zzjsv7bTTTmnRokXpla98Zbr00kvTM888ky688MI0Y8aMtN1226V77703D+qOO+64vIew0fbNI0CAAAECBIZboCN3xW37x9TD1g+qD/cepnbDLCCoa7J177vvvvTII4+kPffcs75EBGUxjHLhwoV5UHfzzTfnQy6LgC4yvuENb8jnRZ4I6iJPLBPLFmmvvfZKJ554Yrr//vvTVlttVcwe8fjss8+m+CtS9PhFWrFiRf5XzB+ExyhzpOJxEMo8VhmLehSPY+UdhNeKehSPbZV5jeltLVZf6Pl9pP58ghNFXVY8t1Z7a+pGfbKfJWg7Pb9s2/WJDQ9bnbpRn7Yb6IXjW9/a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HHrooWm//fYbihpHXeIL2ei///7v/x7I+hX1afSzGUcffXRez8gziGnhwoX5Xez23nvvQSx+Gua2iQaJ+g3TcWFY6lK8WQb9/VPUo3hcsmRJev/735+22GKLNGPGjLTxxhunvfbaK918881FloF8fOihh9IRRxyRNt100xS/d/vbv/3b6U//9E/Tr3/966bqU4WTjcWx7lOf+tSIMseJj/isHcRU1CnKP3369LTRRhulPfbYI11wwQXpueeeG8QqKfOACgjqBrThFLs3AhEkLF68eMTfVltt1ZuNd2Ers2fPTl/+8pfzn9AoVv/MM8+kf/qnf8q/ABXz2nlcsWJFO4t1ZJn48Pzwhz+cvvOd7+S/9ziRla5cubIvH8TdbJuJeFh2+AU6+f6pgtYBBxyQvv/976eLLroo3Xvvvenqq6/Of0Ln0UcfrULx2irDz372s/x3baM+cbyOk4tf+MIX0g033JD/1u0g1W3NNddMf/d3f5cee+yxtiyquFDxXeH+++9P//Zv/5Z23333PODed9990//+7/9WscjKNIQCgrohbNSqVOkb3/hGeuMb35he+tLDjz/4AAAV5klEQVSX5r/JFwe3n/70p/XixcEvzmxdeeWV+QFw7bXXzn+nr0pnU4uzvHGmt/iL35ip1Wrp1FNPTS972cvSWmutlZf7X/7lX+p1KyZuuumm/LX4EHv961+ffvCDHxQv9eXxNa95TR68hXmRYjoCile/+tXFrNRs2/3zP/9z/mUp6nfJJZfUl+/lxNNPP52iHB/84AdT7GMXXnhhffPFmemvfe1rq22HyB/76Fe/+tW0zTbb5Gf2H3jggfo6ejXRqbb5/d///XTMMceMKHacyY99+d///d9HzO/Hky233DKdddZZIza94447pvJPpsZx4R/+4R/S/vvvn+K48IpXvCL/Yj5ioQo8aaYu5WJWsW3Gev8U741yHRr1qPzt3/5t2nDDDdM666yT3ve+96UTTjghRZv2I8WQ9zi5E0FDfLGO3qzXve516cQTT0xve9vb8iI98cQT6aijjsrLPHPmzBTtEkFgkWJfjPJ/8YtfzI+NsQ/+0R/9UerncPoPfehDee/cddddl3bdddf8OL7PPvukb37zm+nnP/95Oumkk/LiP/vss+n444/Pyx3v+XjvnH/++Sk+b8Mj0rrrrtvXkRlvectb8s/TT37yk3l5Gv274oor0rbbbpsft+J9dsYZZ9SzRVu+4Q1vqD8vJl71qlelv/mbvyme9vSx+K6w2WabpTiW/+Vf/mX613/91zzAKz6TxtvvosBxAmLu3LkpPlM32GCD9K53vaun9bCxwRYQ1A12+1W69PFl4bjjjku33XZbfjZxjTXWyL+kjR6OEB9Gf/7nf57uuuuutPXWW6eDDjqo8me2/uqv/ip96UtfSuecc0760Y9+lP7sz/4sHXLIIelb3/rWiDb52Mc+lv+4fBjEl553vOMdqZ89WlG4ww47LC97UdA4S3/44YcXT/PHZtvuL/7iL9Kxxx6b7rnnnnx404iV9OjJ5Zdfnl75ylfmf9EG0S4RdJfTeO2wdOnSFF8wIpCI9oy26kfqRNvEl+rLLrssxZe7Il166aX5kK3iS10xv8qPCxYsSAceeGC6++6701vf+tZ08MEHp0HqjWhkW8W2aeb906guxbzYt04++eQ8iLrjjjvyYCOOi/1KL3nJS1L8RfBZfg8U5YljQwR3jzzySPr617+eoszxJfwP/uAPRuxf0RMWJ4uuueaa/CRXfD5FYNWPFPv9tddem2KYfJxELKc42RjvjWjHqNuf/Mmf5KMxPvOZz+TH5ejNC484cReBUqRFixblo0/+/u//vryqnk3HidFTTjklnX322el//ud/VtlutEm89//4j/84PxEaQfZf//VfpyI4ivrecsstI04Sx3E7TprGa1VJcbJghx12yE9cN7PfxcnHCOJi//ze976Xf2+KAE8i0LRAtqNJBDom8N73vrf2zne+s+H6susc4pt2LTvw5q/fd999+fPsi3Q9f3ZgzudlQUJ9Xr8moi7Zh0/txS9+cf3vD//wD2u/+c1vatlZtFp2HcqIomXXOtSygDSf9x//8R95PbKhjvU8WW9JLftArmUfvvV5vZwo2uaXv/xlLTurWAv/7OxtXpeYF+0WeRql1bVd1uPSKHtP5+288861ohxZwFzLzm7Wrr/++rwMzbRDFgTmbZV9aetpucsb62TbZMNpa+utt96I/SzrdahlX4zKm+zpdFG/2GjWc1L79Kc/PWL72RefWnaGvT4vjhPZiZP683jPZb13tWxYU31evybaqctVV12VF7eKbTPW+yfeG7NmzRpBHXWJ9ilSNgKhlgU7xdP8cZdddqlFm/YrZaMmallvVH5si/plPTu1rCcuL042XLGW9c7Voi3K6Xd+53dqWc9cPiv2xTj2Z9ew1bPEvpedmKxlw/Hr83o18d3vfjc3L/aj0ds988wz89ezQCd/LI5/o/MVx8Ns2OPol3r2vPz+yXrbatkJxXzb5f3qPe95Ty27Jm1EmbITc7VsJEV9XtYrV/v4xz9efx5t/Hu/93v1572cKNdp9Hbf/e531+bMmVNrZr/baaedallQOnoVnhNoWkBPXdPhr4ytCsRQy+zgnA9RjCEuxbVoDz744IhVxZCJIm2yySb5ZFzoXoUUPRtxhrb4i7OfP/7xj1NchxYXQhdnhePxH//xH0ecOYzyZwfpejWyL9p5b1L0avUzxZCOOBMY15tEr1ZMx7xyarbt+n0WMc4433rrrfkZ3Sj/tGnTUvYhml+gXq7PeO0QNx0o74flZXs53Ym2iWFA0WMZPbCRYt+NoWVxMf8gpXJ7ZCdW8qF9VTkutOtYtbZp9v0zVn1jHTG8sZxGPy+/1ovpuKbu4YcfzoeyxQ1SYhh29MZFT0/0AmUnCfJLAsrH7+wk14jjd9xkZfPNN68XN44hMcok6lu1lH3jy4sUdYhesBieOQgphsjG51B8ppZTfEZmJwbKs/LnP/nJT1Jc8xwpeuSilzhS1D+uM6xSL11esOfLFsPJm9nv4lgdPcYSgXYFprW7oOUIjCfw9re/PR/ycd555+VDv+IDcbvttkvLly8fsWjcLapIcfCLNHqIZvF6rx/jy+TLX/7yEZstgtIYKhHj58spvrSNl4o6jpevm6/HcMviuqvPfe5zq2yq2bYLn36muFYkLkIvt0N8wMc+Nd5F+OV2iCFN5ef9rFMn2iaG+cU1QTG0KYK7+KKQ9ZD1s1r1bccw7OJLaDGz0ZDk8nEh8kX7VOW4UJS72boU+eOxSm0z3vun2fqNfu+Mbt9y/Xs1HdckxYm3+Pt//+//5e5ZD1w+hDFOHkagNzrFtbWrS0Udi8fV5evG/PgMiu1G8NPozqv/9V//lV8nF9f+DVJ685vfnA/bj+vPyiedYv8Z7Tx6n4oTxnHt5p133pnf+CvuDBrDNauWIkCNE9px7Bpvvxs9tLZqdVGe6gsI6qrfRgNZwrgxQxzM4kLzN73pTXkd4uL1YUjFzTQiuBvvjGg2bKZ+V8kIMuLOZb/7u7/bd4a4U1cRXMeZ7HIalLaLYC56R+MC+j333LNchRRn6uMsbpxEiFTVdhhR6OefdKJttt9++/xi+zihEtfXxbUrVUm/9Vu/lV/PU5TnySefTNHDMIipnbpUpW2aef9kQxLTU089leIa2+IETvQmlFNczxq95fPmzavPvv322+vTVZmI43ZcZxc9dnE9XfTqb5ndgGN1KY7v0dsXPx8QKW7gFUFuXPfd67T++uvnwennP//5/Prt8pf/qEsc6+Jauti3IniIa7vjZiSjU4xIiFT0do1+vR/P46cN4gRU2TXaavT3hfjZjcgTPZGRohc1gsKo+7Jly/L6xk8JVCnFjaniOr+45j7KO95+F6MT4m6mcW21RKAdAUFdO2qWGVcg7q4VH0TnnntufnYqPiDjrNowpLjDW9zYJQ7U8QEad/iML6bxoRPDebLx9fVqZmP+c4f4sIkbwsTwukZnWusL9GgiPhiLYaDFh2Sx6UFpu7hbZQTK8btN2XU/RfHzx+zax/yOb9m1W/nzqrbDiEI//6RTbRM9QtEbG2fv4y6SVUlx84AYBhe9wbGvxQ0QRu+DVSnreOVoty5VaJtm3j/xBTP2n+hJiZ8MieAt2q6cYv6RRx6Zn0TIrl/Lb9gRN7eJOwP3I8VJqbhTZfR4x5fkOF5HkBl3K86uG86//MdQyjgOx/C/CEojeIubpsS8Ykh59PTFsfz000/Pj+9xQ6i4eUfcmKQf6bOf/WwK3zgJF3cbjd6fuDlI3AQqRirEzWpiiH+UOeoelwrETTriTr4xbDnKHr310QMWbR83H4rgMD6z+pkiEI1hk+UTTx/96EdTdn1c+sQnPpEPp4+AOuofQW05xXLZtcL5CcriWF9+vZfTcVOeCNoiYP7FL36R31wnbr4Vd2SOgDtOCIy330VPcoyqiJMp0esYJ17i5xHibqYSgaYEsi5tiUDHBLKztbWslyRfX1ysHRcIx005sg/XWjbcpZbtlLXiYu+4UUc8z+7yVN9+XMAd8+KC7n6nsS5+zoK5WnbnsFr2haCWDROrZWfsa9mHbS07Q5oXu7ggPbtzWi27LXMtO0OaX8SdneXuW7XGqk8UqnyjlHbartcVyz4sa9kXk4abza5fyPejrBcvfxyrHRrdDKLhSrs4s5NtUxQz62GpZV/Ia9kd84pZfXssHxey23rXsi+Y+c0qsjvy1bIgIb+pxugbpRTHiaLQccOOaKt+p07UpQpt08z7J95H0Q7Z8L/8piOxTHaiLn9PldshbliRnbCqZQFCfuOLLACqxU0w+pHiBijZCcRa1iOX3+Ql3gNxnI4b72R3uc2LlJ2Eq2XBaC3rhcuP37EfZgFCLTv5mL8e+2Lc6CULIvI8cWOs7K6EtewulP2oUn2bcWOrbJhiLQss6+WOevzqV7+q58l6rWrZCcdaNtQv/9yJtsuGYNdfj7aK5bPgrhbHnV6nRse6qFd8T4jP/iLFzW7ixijx+Zpd31g77bTTipfqj/F9IZaLNo73VL9S1CnKHn9ZD3D+fSDrKc3dsyCvXqzx9rvImN2htBY3torvDPGeiv1OItCswJTImO2IEoGOCMTQsRj/H2fVJAL9FojrZuJmN9GjN9b1Mv0uZze2H9eYxPCy+DmNGHLWzzRMx4VO1KVKbdON/SKuY4serYsvvrgbq+/6OqP3J4Zqjh5q2vUN2wABAgQmIGD45QTwLPqCQHxpjuGH8SX6Ax/4wAsvmCJAoKcCcdOR7Lbr+XDn+IHefgZ0w3Rc6ERdqtQ2ndop4zce47fQYlhgDKONuxDGD2Jnvf2d2oT1ECBAgEATAoK6JpBkGV8gxvBHj0CMhY/rFiQCBPojcNNNN+W9k3FTgWwIU38K8fxWh+m40Im6VKltOrVjxDVacT1aXOcV1xXFNWrxI9eNbtTRqW1aDwECBAisKmD45aom5hAgQIAAAQIECBAgQGBgBPz4+MA0lYISIECAAAECBAgQIEBgVQFB3aom5hAgQIAAAQIECBAgQGBgBAR1A9NUCkqAAAECBAgQIECAAIFVBQR1q5qYQ4AAAQIECBAgQIAAgYERENQNTFMpKAECBAhUVSDuAhm/bSYRIECAAIF+CAjq+qFumwQIECDQEYFDDz00RUDV6Pcxjz766Py1yNOpFD9MveOOO3ZqddZDgAABAgQ6IiCo6wijlRAgQIBAvwRmz56dvvzlL6dly5bVi/DMM8/kP4S9xRZb1OeZIECAAAECwyogqBvWllUvAgQITBKB17zmNSmCtyuvvLJe45iOYO/Vr351fV78OPaxxx6bNtxww7TmmmumN77xjem2226rv37jjTfmPXs33HBDmjt3blp77bXTzjvvnBYtWpTnufDCC9OCBQvS97///Txf9BDGvCL96le/Svvvv3++3Cte8Yp09dVXFy95JECAAAECXRUQ1HWV18oJECBAoBcChx12WPrSl75U39QFF1yQDj/88PrzmDj++OPTFVdckS666KJ05513ppe//OVpr732So8++uiIfCeddFI644wz0u23356mTZtWX8+73/3u9NGPfjRtu+22afHixflfzCtSBHwHHnhguvvuu9Nb3/rWdPDBB6+y7iKvRwIECBAg0EkBQV0nNa2LAAECBPoiMG/evPSd73wn3X///emBBx5IN910UzrkkEPqZXn66afTOeeck0477bS0zz77pG222Sadd955aa211krnn39+PV9MnHzyyWnXXXfN85xwwglp4cKFKYZzRt6XvOQleaC38cYbp/iLeUWKa/cOOuigPFg85ZRTUmzz1ltvLV72SIAAAQIEuiYwrWtrtmICBAgQINAjgQ022CC97W1vy3vharVaPh3zivTTn/40rVixIu2yyy7FrDR9+vT0ute9Lt1zzz31eTHxqle9qv58k002yaeXLFmSD/Gsv9Bgorzci1/84rTOOuukWE4iQIAAAQLdFhDUdVvY+gkQIECgJwIx3PKYY47Jt/W5z31uxDYj0IsU18GVU8wfPS+CvSIVrz333HPFrNU+lpeLTLFsM8utdoVeIECAAAECTQoYftkklGwECBAgUG2BvffeOy1fvjz/i2vlyimun3vRi16UD9Es5kfPXVw3N2fOnGLWuI+xjpUrV46bTwYCBAgQINBLAT11vdS2LQIECBDomsDUqVPrQyljupxiOOQHP/jB9LGPfSytt956+VDKU089NS1dujQdccQR5axjTm+55ZbpvvvuS3fddVfafPPN8yGWM2bMGHMZLxIgQIAAgW4LCOq6LWz9BAgQINAzgZkzZ652W5/61Kfy4ZBxU5Wnnnoq/9mCa6+9Nq277rqrXWb0CwcccED+0wm77757evzxx/M7bnbyx81Hb89zAgQIECDQjMCU7HqC/7vQoJnc8hAgQIAAAQIECBAgQIBApQRcU1ep5lAYAgQIECBAgAABAgQItCYgqGvNS24CBAgQIECAAAECBAhUSkBQV6nmUBgCBAgQIECAAAECBAi0JiCoa81LbgIECBAgQIAAAQIECFRKQFBXqeZQGAIECBAgQIAAAQIECLQmIKhrzUtuAgQIECBAgAABAgQIVEpAUFep5lAYAgQIECBAgAABAgQItCYgqGvNS24CBAgQIECAAAECBAhUSkBQV6nmUBgCBAgQIECAAAECBAi0JiCoa81LbgIECBAgQIAAAQIECFRKQFBXqeZQGAIECBAgQIAAAQIECLQmIKhrzUtuAgQIECBAgAABAgQIVEpAUFep5lAYAgQIECBAgAABAgQItCYgqGvNS24CBAgQIECAAAECBAhUSkBQV6nmUBgCBAgQIECAAAECBAi0JiCoa81LbgIECBAgQIAAAQIECFRKQFBXqeZQGAIECBAgQIAAAQIECLQmIKhrzUtuAgQIECBAgAABAgQIVEpAUFep5lAYAgQIECBAgAABAgQItCYgqGvNS24CBAgQIECAAAECBAhUSkBQV6nmUBgCBAgQIECAAAECBAi0JiCoa81LbgIECBAgQIAAAQIECFRKQFBXqeZQGAIECBAgQIAAAQIECLQmIKhrzUtuAgQIECBAgAABAgQIVEpAUFep5lAYAgQIECBAgAABAgQItCYgqGvNS24CBAgQIECAAAECBAhUSkBQV6nmUBgCBAgQIECAAAECBAi0JiCoa81LbgIECBAgQIAAAQIECFRKQFBXqeZQGAIECBAgQIAAAQIECLQmIKhrzUtuAgQIECBAgAABAgQIVEpAUFep5lAYAgQIECBAgAABAgQItCYgqGvNS24CBAgQIECAAAECBAhUSkBQV6nmUBgCBAgQIECAAAECBAi0JiCoa81LbgIECBAgQIAAAQIECFRKQFBXqeZQGAIECBAgQIAAAQIECLQmIKhrzUtuAgQIECBAgAABAgQIVEpAUFep5lAYAgQIECBAgAABAgQItCYgqGvNS24CBAgQIECAAAECBAhUSkBQV6nmUBgCBAgQIECAAAECBAi0JiCoa81LbgIECBAgQIAAAQIECFRK4P8DBghngFVVdrQAAAAASUVORK5CYII=" width="885">





    <matplotlib.legend.Legend at 0x118247e48>




```python
plt.grid()
plt.title('Winner VS Nominate Movie -  Box Office', fontsize=10)
plt.xlabel('Month', fontsize=10)
plt.ylabel('Box Office (Million)', fontsize=10)
plt.show()
```


```python
# Save Figure
plt.savefig("../Month/WN_boxMonth.png")
```


```python

```
