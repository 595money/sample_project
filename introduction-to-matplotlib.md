---
jupyter:
  jupytext:
    formats: ipynb,md,py:percent
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.2'
      jupytext_version: 1.4.2
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

```python
%matplotlib inline
import matplotlib.pylab as plt
import numpy as np
import pandas as pd
from jupyterthemes import jtplot
from IPython.core.display import display, HTML
display(HTML("<style>.container { width:70% !important; }</style>"))
jtplot.style()
```

# Introduction to Matplotlib

```python
plt.plot()
plt.show()
```

```python
plt.plot([1, 2, 3, 4])
```

```python
x = [1, 2, 3, 4]
y = [11, 22, 33, 44]
plt.plot(x, y)
```

```python
# 1st method
fig = plt.figure() # creates a figure
ax = fig.add_subplot() # adds some axes
plt.show()
```

```python
# 2nd method
fig = plt.figure() # creates a figure
ax = fig.add_axes([1, 1, 1, 1])
ax.plot(x, y) # add some data
plt.show()
```

```python
# 3rd method (recommended)
fig, ax = plt.subplots()
plt.plot(x, [50, 100, 200, 250]);
type(fig), type(ax)
```

## Matplotlib example workflow

```python
# 0. import matplotlib and get it ready for plotting in Jupyter
%matplotlib inline
import matplotlib.pyplot as plt

# 1. Prepare data
x = [1, 2, 3, 4]
y = [11, 22, 33, 44]

# 2. Setup plot (產生一張新畫布, 設定畫布長寬等)
fig, ax = plt.subplots(figsize=(10, 10)) # (width, height)

# 3. Plot data
ax.plot(x, y)

# 4. Customize plot
ax.set(title='Simple Plot',
      xlabel='x-axis',
      ylabel='y-axis')
# 5. Save & show (you save the whole figure)
fig.savefig('./myplot/sample-plot.png')
```

## Making figures ith NumPy arrays
We want:
* Line plot
* Scatter plot
* Bar plot
* Histogram
* Subplots

```python
import numpy as np

# Create some data
x = np.linspace(0, 10, 100)
x[:10]
```

```python
# Plot the data and create a line plot
fig, ax = plt.subplots()

# plot default line plot 
ax.plot(x, x**2);
```

```python
# Use same data to make a scatter
fig, ax = plt.subplots()
ax.scatter(x, np.exp(x));
```

```python
# Acother scatter plot
fig, ax = plt.subplots()
ax.scatter(x, np.sin(x));
```

```python
# Make a plot from dictionary
nut_butter_prices = {'Almond butter': 10,
                    'Peanut butter': 8,
                    'Cashew butter': 12}
fig, ax = plt.subplots()
ax.bar(nut_butter_prices.keys(), nut_butter_prices.values())
ax.set(title="Dan's Nut Butter Store",
      ylabel='Price ($)');
```

```python
fig, ax = plt.subplots()
ax.barh(list(nut_butter_prices.keys()), list(nut_butter_prices.values()))
```

```python
# Make some data for histograms and plot it
# 高斯分布、標準常態分布
x = np.random.randn(1000)
fig, ax = plt.subplots()
ax.hist(x);
```

## Two options for subplots

```python
# Subplot option 1
fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(nrows=2,
                                            ncols=2,
                                            figsize=(10, 5))
ax1.plot(x, x/2);
ax1.set(title="Dan's Nut Butter Store",
      ylabel='Price ($)')
ax2.scatter(np.random.random(10), np.random.random(10));
ax3.bar(nut_butter_prices.keys(), nut_butter_prices.values());
ax4.hist(np.random.randn(1000));
```

```python
# Subplot option 2
fig, ax = plt.subplots(nrows=2,
                      ncols=2,
                      figsize=(10, 5))
ax[0, 0].plot(x, x/2);
ax[0, 1].scatter(np.random.random(10), np.random.random(10));
ax[1, 0].bar(nut_butter_prices.keys(), nut_butter_prices.values());
ax[1, 1].hist(np.random.randn(1000));
```

## Plotting from pandas DataFrames

```python
# Make a dataframe
car_sales = pd.read_csv('./source/car_sales.csv')
car_sales['Price'] = car_sales['Price'].str.replace('[\$\,\.]', '') 
car_sales
```

```python
ts = pd.Series(np.random.randn(1000), index=pd.date_range('1/1/2020', periods=1000))
ts = ts.cumsum()
ts.plot();
```

```python
car_sales['Totla Sales'] = car_sales['Price'].cumsum()
car_sales
```

```python

```
