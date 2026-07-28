### Pandas

- read_csv : read a CSV file
- head : return all first lines
- columns : return all column's real name
- to_numpy : convert into numpy ndarray

```sh
import pandas as pd

df = pd.read_csv("Normal_1.csv")

# It will print pandas.core.frame.DataFrame. A DataFrame is like an Excel sheet in memory.
print(type(df))

# It will print first lines to check if file loads successfully.
print(df.head())

print(df.columns)

# fuel become a Series pandas. A Series is a column.
fuel = df["Fuel Volume"]

# It will print pandas.core.series.Series
print(type(fuel))

# Then we need to convert the Series into NumPy ndarray. Now type(fuel) will return ndarray
fuel = fuel.to_numpy()


```
