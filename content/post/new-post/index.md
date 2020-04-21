---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "New Post"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-20T14:42:20+02:00
lastmod: 2020-04-20T14:42:20+02:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

<!-- Hello. This is a test.

 <iframe
       src="./learning.html"
       width="90%"
       height="1000px"
       style="border:none;">
 </iframe> -->

 ```python
import numpy as np
import pandas as pd

import toolbox.datatools as dt
```


```python
dfu, dfa, dft = dt.download_s3_data()
df = dt.combine_data(dft, dfa, dfu)
df.head()
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-2-aa0463d375b3> in <module>
          1 dfu, dfa, dft = dt.download_s3_data()
    ----> 2 df = combine_data(dft, dfa, dfu)
          3 df.head()


    NameError: name 'combine_data' is not defined


# Creating datetime indices


```python
from dateutil.parser import parse

parse('3 Apr 2020').month
parse('3.4.2020').month
parse('3.4.2020', dayfirst=True).month
```




    4






    3






    4




```python
dates = pd.date_range(start='1/1/2000', freq='A-DEC', periods = 100)
values = np.random.randn(100)
ts = pd.Series(values, index=dates)
ts.head(10)
```




    2000-12-31    0.843433
    2001-12-31   -0.391251
    2002-12-31    0.149087
    2003-12-31    0.086131
    2004-12-31   -2.308920
    2005-12-31   -0.569420
    2006-12-31    0.033575
    2007-12-31    0.449340
    2008-12-31    0.846790
    2009-12-31    0.633025
    Freq: A-DEC, dtype: float64




```python
idx = pd.period_range('2018-1', '2019-12', freq='Q-DEC')
s = pd.Series(np.random.randn(len(idx)), index=idx)
s.asfreq('d', how='start').asfreq('Q')
```




    2018Q1   -0.205351
    2018Q2   -0.673207
    2018Q3   -0.872625
    2018Q4    2.045383
    2019Q1   -0.696708
    2019Q2   -0.798782
    2019Q3   -1.904917
    2019Q4   -0.436799
    Freq: Q-DEC, dtype: float64




```python
idx = pd.date_range('2000', periods=100)
s = pd.Series(np.random.randn(len(idx)), index=idx)
s.resample('M', kind='period').mean()
```




    2000-01    0.014726
    2000-02    0.056242
    2000-03   -0.016878
    2000-04   -0.690987
    Freq: M, dtype: float64




```python
idx = pd.date_range('2000', freq='H', periods=100)
s = pd.Series(np.random.randn(len(idx)), index=idx)
s.resample('d').ohlc()
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
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-01</th>
      <td>-1.945039</td>
      <td>2.231004</td>
      <td>-2.751270</td>
      <td>0.272018</td>
    </tr>
    <tr>
      <th>2000-01-02</th>
      <td>0.335163</td>
      <td>2.173964</td>
      <td>-0.895301</td>
      <td>0.995886</td>
    </tr>
    <tr>
      <th>2000-01-03</th>
      <td>0.771501</td>
      <td>1.399791</td>
      <td>-2.465960</td>
      <td>-0.030100</td>
    </tr>
    <tr>
      <th>2000-01-04</th>
      <td>1.765987</td>
      <td>1.765987</td>
      <td>-1.698415</td>
      <td>-0.056522</td>
    </tr>
    <tr>
      <th>2000-01-05</th>
      <td>0.215849</td>
      <td>1.192958</td>
      <td>0.215849</td>
      <td>0.786069</td>
    </tr>
  </tbody>
</table>
</div>




```python
s.resample('min').asfreq().ffill()
```




    2000-01-01 00:00:00   -1.945039
    2000-01-01 00:01:00   -1.945039
    2000-01-01 00:02:00   -1.945039
    2000-01-01 00:03:00   -1.945039
    2000-01-01 00:04:00   -1.945039
                             ...
    2000-01-05 02:56:00    1.192958
    2000-01-05 02:57:00    1.192958
    2000-01-05 02:58:00    1.192958
    2000-01-05 02:59:00    1.192958
    2000-01-05 03:00:00    0.786069
    Freq: T, Length: 5941, dtype: float64




```python
data = df.reset_index(level=0).head(100).sort_index()[['amount']]
data
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
      <th>amount</th>
    </tr>
    <tr>
      <th>transaction_date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-08-29</th>
      <td>12.00</td>
    </tr>
    <tr>
      <th>2012-08-30</th>
      <td>13.50</td>
    </tr>
    <tr>
      <th>2012-08-30</th>
      <td>7.44</td>
    </tr>
    <tr>
      <th>2012-08-30</th>
      <td>7.44</td>
    </tr>
    <tr>
      <th>2012-08-30</th>
      <td>13.50</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>2012-12-27</th>
      <td>135.00</td>
    </tr>
    <tr>
      <th>2012-12-27</th>
      <td>3.60</td>
    </tr>
    <tr>
      <th>2012-12-27</th>
      <td>8.50</td>
    </tr>
    <tr>
      <th>2012-12-27</th>
      <td>135.00</td>
    </tr>
    <tr>
      <th>2012-12-27</th>
      <td>8.50</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 1 columns</p>
</div>



# IPython / notebook shortcuts


```python
clean_nb = !ls *2*
clean_nb
```




    ['2.0-fgu-clean-and-split-data.ipynb']




```python
%%timeit
a = range(1000)
```

    174 ns ± 4.23 ns per loop (mean ± std. dev. of 7 runs, 10000000 loops each)



```python
%%writefile pythoncode.py

import numpy
def append_if_not_exists(arr, x):
    if x not in arr:
        arr.append(x)

def some_useless_slow_function():
    arr = list()
    for i in range(10000):
        x = numpy.random.randint(0, 10000)
        append_if_not_exists(arr, x)
```

    Writing pythoncode.py



```python
%pycat pythoncode.py
```


    [0;34m[0m
    [0;34m[0m[0;32mimport[0m [0mnumpy[0m[0;34m[0m
    [0;34m[0m[0;32mdef[0m [0mappend_if_not_exists[0m[0;34m([0m[0marr[0m[0;34m,[0m [0mx[0m[0;34m)[0m[0;34m:[0m[0;34m[0m
    [0;34m[0m    [0;32mif[0m [0mx[0m [0;32mnot[0m [0;32min[0m [0marr[0m[0;34m:[0m[0;34m[0m
    [0;34m[0m        [0marr[0m[0;34m.[0m[0mappend[0m[0;34m([0m[0mx[0m[0;34m)[0m[0;34m[0m
    [0;34m[0m[0;34m[0m
    [0;34m[0m[0;32mdef[0m [0msome_useless_slow_function[0m[0;34m([0m[0;34m)[0m[0;34m:[0m[0;34m[0m
    [0;34m[0m    [0marr[0m [0;34m=[0m [0mlist[0m[0;34m([0m[0;34m)[0m[0;34m[0m
    [0;34m[0m    [0;32mfor[0m [0mi[0m [0;32min[0m [0mrange[0m[0;34m([0m[0;36m10000[0m[0;34m)[0m[0;34m:[0m[0;34m[0m
    [0;34m[0m        [0mx[0m [0;34m=[0m [0mnumpy[0m[0;34m.[0m[0mrandom[0m[0;34m.[0m[0mrandint[0m[0;34m([0m[0;36m0[0m[0;34m,[0m [0;36m10000[0m[0;34m)[0m[0;34m[0m
    [0;34m[0m        [0mappend_if_not_exists[0m[0;34m([0m[0marr[0m[0;34m,[0m [0mx[0m[0;34m)[0m[0;34m[0m[0;34m[0m[0m




```python
# %magic -brief
```

I can transfer variables with any content from one notebook to the next (useful if you run a number of notebooks in sequence, for instance, and the ouput of one serves as the input of another).


```python
var_to_pass_on = dfu.head()
%store var_to_pass_on
```

    Stored 'var_to_pass_on' (DataFrame)



```python
# I can pass on variables from one notebook (3.0-fgu) to another
%store -r var_to_pass_on
var_to_pass_on
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
      <th>user_id</th>
      <th>year_of_birth</th>
      <th>user_registration_date</th>
      <th>salary_range</th>
      <th>postcode</th>
      <th>gender</th>
      <th>soa_lower</th>
      <th>soa_middle</th>
      <th>user_uid</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3706</td>
      <td>1967-01-01</td>
      <td>2012-09-30</td>
      <td>NaN</td>
      <td>XXXX 0</td>
      <td>M</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3706-0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1078</td>
      <td>1964-01-01</td>
      <td>2011-11-29</td>
      <td>20K to 30K</td>
      <td>M25  9</td>
      <td>M</td>
      <td>E01005038</td>
      <td>E02001043</td>
      <td>1078-0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>232</td>
      <td>1965-01-01</td>
      <td>2010-09-09</td>
      <td>30K to 40K</td>
      <td>CM4  0</td>
      <td>M</td>
      <td>E01021551</td>
      <td>E02004495</td>
      <td>232-0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6133</td>
      <td>1968-01-01</td>
      <td>2012-10-21</td>
      <td>10K to 20K</td>
      <td>SK12 1</td>
      <td>M</td>
      <td>E01018665</td>
      <td>E02003854</td>
      <td>6133-0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7993</td>
      <td>1961-01-01</td>
      <td>2012-10-29</td>
      <td>20K to 30K</td>
      <td>LS17 8</td>
      <td>M</td>
      <td>E01011556</td>
      <td>E02002344</td>
      <td>7993-0</td>
    </tr>
  </tbody>
</table>
</div>




```python
!conda list | grep pandas

```

    pandas                    1.0.1            py37h6c726b0_0
    pandas-flavor             0.2.0                      py_0    conda-forge


### Using R and Python together


```python
# %conda install -c conda-forge rpy2
# %conda install tzlocal
# %conda install simplegeneric
```


```python
import rpy2

```


```python
# from rpy2.robjects import pandas2ri
# pandas2ri.activate()

```


```python
%reload_ext rpy2.ipython
```


```python
%R require(ggplot2)
```

    R[write to console]: Loading required package: ggplot2






    array([0], dtype=int32)




```python
import pandas as pd
df = pd.DataFrame({
        'Letter': ['a', 'a', 'a', 'b', 'b', 'b', 'c', 'c', 'c'],
        'X': [4, 3, 5, 2, 1, 7, 7, 5, 9],
        'Y': [0, 4, 3, 6, 7, 10, 11, 9, 13],
        'Z': [1, 2, 3, 1, 2, 3, 1, 2, 3]
    })
```


```r
%%R -i df
ggplot(data = df) + geom_point(aes(x = X, y= Y, color = Letter, size = Z))
```

    R[write to console]: Error in ggplot(data = df) : could not find function "ggplot"
    Calls: <Anonymous> -> <Anonymous> -> withVisible

    R[write to console]: In addition:
    R[write to console]: Warning messages:

    R[write to console]: 1:
    R[write to console]: In library(package, lib.loc = lib.loc, character.only = TRUE, logical.return = TRUE,  :
    R[write to console]:

    R[write to console]:  there is no package called ‘ggplot’

    R[write to console]: 2:
    R[write to console]: In library(package, lib.loc = lib.loc, character.only = TRUE, logical.return = TRUE,  :
    R[write to console]:

    R[write to console]:  there is no package called ‘ggplot2’




    Error in ggplot(data = df) : could not find function "ggplot"
    Calls: <Anonymous> -> <Anonymous> -> withVisible


### Printing virtually anything


```python
happy_squirrels = !ls /Users/fgu/Library/Mobile\ Documents/com~apple~CloudDocs/fab/photos/squirrels/
```


```python
from IPython.display import display, Image
for s in happy_squirrels:
    display(Image('/Users/fgu/Library/Mobile Documents/com~apple~CloudDocs/fab/photos/squirrels/' + s, width=100))

```


![jpeg](learning_files/learning_30_0.jpg)



![jpeg](learning_files/learning_30_1.jpg)



![png](learning_files/learning_30_2.png)


### Write code to and load code from file


```python
%%writefile test.py

print('Hello')
```

    Overwriting test.py



```python
%pycat test.py
```


    [0;34m[0m
    [0;34m[0m[0mprint[0m[0;34m([0m[0;34m'Hello'[0m[0;34m)[0m[0;34m[0m[0;34m[0m[0m



# Data from wide to long and back


```python
data = pd.read_csv('https://raw.githubusercontent.com/wesm/pydata-book/2nd-edition/examples/macrodata.csv')
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
      <th>year</th>
      <th>quarter</th>
      <th>realgdp</th>
      <th>realcons</th>
      <th>realinv</th>
      <th>realgovt</th>
      <th>realdpi</th>
      <th>cpi</th>
      <th>m1</th>
      <th>tbilrate</th>
      <th>unemp</th>
      <th>pop</th>
      <th>infl</th>
      <th>realint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1959.0</td>
      <td>1.0</td>
      <td>2710.349</td>
      <td>1707.4</td>
      <td>286.898</td>
      <td>470.045</td>
      <td>1886.9</td>
      <td>28.98</td>
      <td>139.7</td>
      <td>2.82</td>
      <td>5.8</td>
      <td>177.146</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1959.0</td>
      <td>2.0</td>
      <td>2778.801</td>
      <td>1733.7</td>
      <td>310.859</td>
      <td>481.301</td>
      <td>1919.7</td>
      <td>29.15</td>
      <td>141.7</td>
      <td>3.08</td>
      <td>5.1</td>
      <td>177.830</td>
      <td>2.34</td>
      <td>0.74</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1959.0</td>
      <td>3.0</td>
      <td>2775.488</td>
      <td>1751.8</td>
      <td>289.226</td>
      <td>491.260</td>
      <td>1916.4</td>
      <td>29.35</td>
      <td>140.5</td>
      <td>3.82</td>
      <td>5.3</td>
      <td>178.657</td>
      <td>2.74</td>
      <td>1.09</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1959.0</td>
      <td>4.0</td>
      <td>2785.204</td>
      <td>1753.7</td>
      <td>299.356</td>
      <td>484.052</td>
      <td>1931.3</td>
      <td>29.37</td>
      <td>140.0</td>
      <td>4.33</td>
      <td>5.6</td>
      <td>179.386</td>
      <td>0.27</td>
      <td>4.06</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1960.0</td>
      <td>1.0</td>
      <td>2847.699</td>
      <td>1770.5</td>
      <td>331.722</td>
      <td>462.199</td>
      <td>1955.5</td>
      <td>29.54</td>
      <td>139.6</td>
      <td>3.50</td>
      <td>5.2</td>
      <td>180.007</td>
      <td>2.31</td>
      <td>1.19</td>
    </tr>
  </tbody>
</table>
</div>




```python
periods = pd.PeriodIndex(year=data.year, quarter=data.quarter, name = 'date')
columns = pd.Index(['realgdp', 'cpi', 'unemp', 'infl'], name='item')
df = data.reindex(columns=columns)
df.index = periods.to_timestamp('D', 'End')
dfl = df.stack().reset_index().rename(columns={0:'value'})
dfl
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
      <th>date</th>
      <th>item</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1959-03-31 23:59:59.999999999</td>
      <td>realgdp</td>
      <td>2710.349</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1959-03-31 23:59:59.999999999</td>
      <td>cpi</td>
      <td>28.980</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1959-03-31 23:59:59.999999999</td>
      <td>unemp</td>
      <td>5.800</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1959-03-31 23:59:59.999999999</td>
      <td>infl</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1959-06-30 23:59:59.999999999</td>
      <td>realgdp</td>
      <td>2778.801</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>807</th>
      <td>2009-06-30 23:59:59.999999999</td>
      <td>infl</td>
      <td>3.370</td>
    </tr>
    <tr>
      <th>808</th>
      <td>2009-09-30 23:59:59.999999999</td>
      <td>realgdp</td>
      <td>12990.341</td>
    </tr>
    <tr>
      <th>809</th>
      <td>2009-09-30 23:59:59.999999999</td>
      <td>cpi</td>
      <td>216.385</td>
    </tr>
    <tr>
      <th>810</th>
      <td>2009-09-30 23:59:59.999999999</td>
      <td>unemp</td>
      <td>9.600</td>
    </tr>
    <tr>
      <th>811</th>
      <td>2009-09-30 23:59:59.999999999</td>
      <td>infl</td>
      <td>3.560</td>
    </tr>
  </tbody>
</table>
<p>812 rows × 3 columns</p>
</div>




```python
# Use unstack to get wide data

dfl.set_index(['date', 'item']).unstack()
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
      <th colspan="4" halign="left">value</th>
    </tr>
    <tr>
      <th>item</th>
      <th>cpi</th>
      <th>infl</th>
      <th>realgdp</th>
      <th>unemp</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1959-03-31 23:59:59.999999999</th>
      <td>28.980</td>
      <td>0.00</td>
      <td>2710.349</td>
      <td>5.8</td>
    </tr>
    <tr>
      <th>1959-06-30 23:59:59.999999999</th>
      <td>29.150</td>
      <td>2.34</td>
      <td>2778.801</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>1959-09-30 23:59:59.999999999</th>
      <td>29.350</td>
      <td>2.74</td>
      <td>2775.488</td>
      <td>5.3</td>
    </tr>
    <tr>
      <th>1959-12-31 23:59:59.999999999</th>
      <td>29.370</td>
      <td>0.27</td>
      <td>2785.204</td>
      <td>5.6</td>
    </tr>
    <tr>
      <th>1960-03-31 23:59:59.999999999</th>
      <td>29.540</td>
      <td>2.31</td>
      <td>2847.699</td>
      <td>5.2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2008-09-30 23:59:59.999999999</th>
      <td>216.889</td>
      <td>-3.16</td>
      <td>13324.600</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2008-12-31 23:59:59.999999999</th>
      <td>212.174</td>
      <td>-8.79</td>
      <td>13141.920</td>
      <td>6.9</td>
    </tr>
    <tr>
      <th>2009-03-31 23:59:59.999999999</th>
      <td>212.671</td>
      <td>0.94</td>
      <td>12925.410</td>
      <td>8.1</td>
    </tr>
    <tr>
      <th>2009-06-30 23:59:59.999999999</th>
      <td>214.469</td>
      <td>3.37</td>
      <td>12901.504</td>
      <td>9.2</td>
    </tr>
    <tr>
      <th>2009-09-30 23:59:59.999999999</th>
      <td>216.385</td>
      <td>3.56</td>
      <td>12990.341</td>
      <td>9.6</td>
    </tr>
  </tbody>
</table>
<p>203 rows × 4 columns</p>
</div>




```python
# Use pivot to get wide data

dfl.pivot('date', 'item', 'value')
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
      <th>item</th>
      <th>cpi</th>
      <th>infl</th>
      <th>realgdp</th>
      <th>unemp</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1959-03-31 23:59:59.999999999</th>
      <td>28.980</td>
      <td>0.00</td>
      <td>2710.349</td>
      <td>5.8</td>
    </tr>
    <tr>
      <th>1959-06-30 23:59:59.999999999</th>
      <td>29.150</td>
      <td>2.34</td>
      <td>2778.801</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>1959-09-30 23:59:59.999999999</th>
      <td>29.350</td>
      <td>2.74</td>
      <td>2775.488</td>
      <td>5.3</td>
    </tr>
    <tr>
      <th>1959-12-31 23:59:59.999999999</th>
      <td>29.370</td>
      <td>0.27</td>
      <td>2785.204</td>
      <td>5.6</td>
    </tr>
    <tr>
      <th>1960-03-31 23:59:59.999999999</th>
      <td>29.540</td>
      <td>2.31</td>
      <td>2847.699</td>
      <td>5.2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2008-09-30 23:59:59.999999999</th>
      <td>216.889</td>
      <td>-3.16</td>
      <td>13324.600</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2008-12-31 23:59:59.999999999</th>
      <td>212.174</td>
      <td>-8.79</td>
      <td>13141.920</td>
      <td>6.9</td>
    </tr>
    <tr>
      <th>2009-03-31 23:59:59.999999999</th>
      <td>212.671</td>
      <td>0.94</td>
      <td>12925.410</td>
      <td>8.1</td>
    </tr>
    <tr>
      <th>2009-06-30 23:59:59.999999999</th>
      <td>214.469</td>
      <td>3.37</td>
      <td>12901.504</td>
      <td>9.2</td>
    </tr>
    <tr>
      <th>2009-09-30 23:59:59.999999999</th>
      <td>216.385</td>
      <td>3.56</td>
      <td>12990.341</td>
      <td>9.6</td>
    </tr>
  </tbody>
</table>
<p>203 rows × 4 columns</p>
</div>



## HDF5

Following [this](https://www.youtube.com/watch?v=wZEFoVUu8h0) video.


```python
import h5py
import numpy as np
```

Create a HDF5 file object, which works kind of like a Python dictionary.


```python
f = h5py.File('demo.hdf5')
```


```python
data = np.arange(10)
data
```




    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])




```python
f['array'] = data
```


```python
dset = f['array']
```


```python
dset
```




    <HDF5 dataset "array": shape (10,), type "<i8">




```python
dset[:]
```




    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])




```python
dset[[1, 2, 5]]
```




    array([1, 2, 5])




```python
dset.attrs
```




    <Attributes of HDF5 object at 4425393432>



Atributes again have dictionarry structure, so can add attribute like so:


```python
dset.attrs['sampling frequency'] = 'Every other week between 1 Jan 2001 and 7 Feb 2010'
dset.attrs['PI'] = 'Fabian'
```


```python
list(dset.attrs.items())
for i in dset.attrs.items():
    print(i)
```

    ('sampling frequency', 'Every other week between 1 Jan 2001 and 7 Feb 2010')
    ('PI', 'Fabian')



```python
f.close()
```


```python
f = h5py.File('demo.hdf5')
```


```python
list(f.keys())
```




    ['array']




```python
dset = f['array']
```

hdf5 files are organised in a hierarchy - that's what "h" stands for.


```python
dset.name
```




    '/array'




```python
root = f['/']
```


```python
list(root.keys())
```




    ['array']




```python
f['dataset'] = data
```


```python
f['full/dataset'] = data
```


```python
grp = f['full']
```


```python
'dataset' in grp
```




    True




```python
list(grp.keys())
```




    ['dataset']




```python
dset2 = f.create_dataset('/full/bigger', (10000, 1000, 1000, 1000), dtype='f', compression='gzip')
```


```python
list(f['full'].keys())
```




    ['bigger', 'dataset']



# Misc.


```python
# Slicing with hierarchical index

idx = pd.IndexSlice
df.loc[idx[:, "2014"], :]
```


```python
# Calculate z score manually

from scipy import stats

s = np.arange(5)

std = np.std(s)
mean = np.mean(s)

manual_z = (s - mean) / std
scipy_z = stats.zscore(s)

manual_z == scipy_z
```




    array([ True,  True,  True,  True,  True])




```python
np.arange(32).reshape((4, 8))
```




    array([[ 0,  1,  2,  3,  4,  5,  6,  7],
           [ 8,  9, 10, 11, 12, 13, 14, 15],
           [16, 17, 18, 19, 20, 21, 22, 23],
           [24, 25, 26, 27, 28, 29, 30, 31]])




```python
import random

print("one") if random.randint(0, 1) else print("zero")
```

    zero



```python
# Simulating a single random walk

ndraws = 1000
draws = np.random.randint(0, 2, ndraws)
steps = np.where(draws > 0, 1, -1)
walk = steps.cumsum()

# Find how long it took to make 10 steps in either direction

idx = (np.abs(walk) >= 10).argmax()
print("It took {} steps to get to {}".format(idx, walk[idx]))
```

    It took 57 steps to get to -10



```python
# Simulating many random walks together

nwalks = 5000
ndraws = 1000
draws = np.random.randint(0, 2, size=(nwalks, ndraws))
steps = np.where(draws > 0, 1, -1)
walk = steps.cumsum(axis=1)

# Find number of walks that cross 30 and the average crossing time

hit30 = (np.abs(walk) >= 30).any(1)
crossing_times = (np.abs(walk[hit30]) >= 30).argmax(1)

print(
    "{} walks cross 30, taking {} steps on average.".format(
        hit30.sum(), crossing_times.mean()
    )
)
```

    3385 walks cross 30, taking 498.33353028064994 steps on average.


# Grouping


```python
df = pd.DataFrame({'key1': ['a', 'b', 'c', 'd', 'e'],
                   'key2': ['one', 'two', 'one', 'two', 'one'],
                   'data1': np.random.randn(5),
                   'data2': np.random.randn(5)})
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
      <th>key1</th>
      <th>key2</th>
      <th>data1</th>
      <th>data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>one</td>
      <td>-0.722346</td>
      <td>1.350070</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>two</td>
      <td>-0.864278</td>
      <td>0.652911</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>one</td>
      <td>0.875035</td>
      <td>0.838726</td>
    </tr>
    <tr>
      <th>3</th>
      <td>d</td>
      <td>two</td>
      <td>1.420677</td>
      <td>-0.464896</td>
    </tr>
    <tr>
      <th>4</th>
      <td>e</td>
      <td>one</td>
      <td>-0.789309</td>
      <td>0.148121</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Loop over groups

for group, data in df.groupby('key1'):
    print(group)
    print(data)
```

    a
      key1 key2     data1    data2
    0    a  one -0.722346  1.35007
    b
      key1 key2     data1     data2
    1    b  two -0.864278  0.652911
    c
      key1 key2     data1     data2
    2    c  one  0.875035  0.838726
    d
      key1 key2     data1     data2
    3    d  two  1.420677 -0.464896
    e
      key1 key2     data1     data2
    4    e  one -0.789309  0.148121



```python
# Save groups in dict

pieces = dict(list(df.groupby('key1')))
pieces['a']
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
      <th>key1</th>
      <th>key2</th>
      <th>data1</th>
      <th>data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>one</td>
      <td>-0.722346</td>
      <td>1.35007</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped = df.groupby(df.dtypes, axis=1)
for dtype, data in grouped:
    print(dtype)
    print(data)
```

    float64
          data1     data2
    0 -0.722346  1.350070
    1 -0.864278  0.652911
    2  0.875035  0.838726
    3  1.420677 -0.464896
    4 -0.789309  0.148121
    object
      key1 key2
    0    a  one
    1    b  two
    2    c  one
    3    d  two
    4    e  one


# Solution to my common indexing problem (index with shorter boolean series)

Problem: I want to index my df based on a boolean series that is shorter than the length of the df. E.g. I have a subset of users that fulfill a condition and want to keep these only.


```python
# Data

data = o2.sample(frac=0.05)
```


```python
# The boolean array of users who spent more than £100

high_spender = data.groupby("user_id").amount.sum() > 350
```


```python

```


```python
# Use transform to get boolean series of same length as original df so I can use indexing
```


```python
# Use df.drop()

todrop = high_spender[~high_spender].index.values
data.drop(todrop, level=0).sort_index()
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
      <th></th>
      <th>transaction_id</th>
      <th>transaction_description</th>
      <th>amount</th>
      <th>auto_tag</th>
      <th>merchant_name</th>
      <th>account_type</th>
    </tr>
    <tr>
      <th>user_id</th>
      <th>transaction_date</th>
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
      <th rowspan="9" valign="top">20912</th>
      <th>2013-12-18</th>
      <td>12152457</td>
      <td>card purchase o2 uk ref xxx xxxxxx0000 bcc</td>
      <td>11.990000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2014-04-17</th>
      <td>17466459</td>
      <td>direct debit o2 gedxxxxx154 ddr</td>
      <td>44.160000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2015-01-19</th>
      <td>54324542</td>
      <td>direct debit o2 gedxxxx9154 ddr</td>
      <td>38.380001</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2015-03-24</th>
      <td>80422755</td>
      <td>direct debit o2 gedxxxx9097 ddr</td>
      <td>34.799999</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2015-09-23</th>
      <td>96952964</td>
      <td>counter credit &lt;mdbremoved&gt; o2 bgc</td>
      <td>54.500000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2016-04-25</th>
      <td>134730196</td>
      <td>direct debit o2 gedxxxx9097 ddr</td>
      <td>40.990002</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2016-05-17</th>
      <td>138708140</td>
      <td>direct debit o2 gedxxxx1717 ddr</td>
      <td>30.000000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2016-08-17</th>
      <td>154735556</td>
      <td>direct debit o2 gedxxxx9154 ddr</td>
      <td>34.270000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2016-10-07</th>
      <td>163699913</td>
      <td>counter credit &lt;mdbremoved&gt; o2/ &lt;mdbremoved&gt; bgc</td>
      <td>68.059998</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">160992</th>
      <th>2014-09-29</th>
      <td>38730708</td>
      <td>o2 uk cd 9531</td>
      <td>25.000000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2015-01-19</th>
      <td>54406685</td>
      <td>o2 uk cd 9531</td>
      <td>175.000000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2015-01-19</th>
      <td>54406686</td>
      <td>o2 uk cd 9531</td>
      <td>202.539993</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
  </tbody>
</table>
</div>




```python
high_spender
```




    user_id
    8         False
    659       False
    1078      False
    1146      False
    2324      False
              ...
    420102    False
    421678    False
    423912    False
    424865    False
    425830    False
    Name: amount, Length: 210, dtype: bool




```python
# Use isin()

hs = high_spender[high_spender].index.values
mask = data.index.isin(hs, level=0)
data[mask].sort_index()
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
      <th></th>
      <th>transaction_id</th>
      <th>transaction_description</th>
      <th>amount</th>
      <th>auto_tag</th>
      <th>merchant_name</th>
      <th>account_type</th>
    </tr>
    <tr>
      <th>user_id</th>
      <th>transaction_date</th>
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
      <th rowspan="9" valign="top">20912</th>
      <th>2013-12-18</th>
      <td>12152457</td>
      <td>card purchase o2 uk ref xxx xxxxxx0000 bcc</td>
      <td>11.990000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2014-04-17</th>
      <td>17466459</td>
      <td>direct debit o2 gedxxxxx154 ddr</td>
      <td>44.160000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2015-01-19</th>
      <td>54324542</td>
      <td>direct debit o2 gedxxxx9154 ddr</td>
      <td>38.380001</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2015-03-24</th>
      <td>80422755</td>
      <td>direct debit o2 gedxxxx9097 ddr</td>
      <td>34.799999</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2015-09-23</th>
      <td>96952964</td>
      <td>counter credit &lt;mdbremoved&gt; o2 bgc</td>
      <td>54.500000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2016-04-25</th>
      <td>134730196</td>
      <td>direct debit o2 gedxxxx9097 ddr</td>
      <td>40.990002</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2016-05-17</th>
      <td>138708140</td>
      <td>direct debit o2 gedxxxx1717 ddr</td>
      <td>30.000000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2016-08-17</th>
      <td>154735556</td>
      <td>direct debit o2 gedxxxx9154 ddr</td>
      <td>34.270000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2016-10-07</th>
      <td>163699913</td>
      <td>counter credit &lt;mdbremoved&gt; o2/ &lt;mdbremoved&gt; bgc</td>
      <td>68.059998</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">160992</th>
      <th>2014-09-29</th>
      <td>38730708</td>
      <td>o2 uk cd 9531</td>
      <td>25.000000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2015-01-19</th>
      <td>54406685</td>
      <td>o2 uk cd 9531</td>
      <td>175.000000</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
    <tr>
      <th>2015-01-19</th>
      <td>54406686</td>
      <td>o2 uk cd 9531</td>
      <td>202.539993</td>
      <td>mobile</td>
      <td>o2</td>
      <td>current</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python

```
