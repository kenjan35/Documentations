### Numpy

- array : this function is used to create a numpy array.
- shape (attribute) : A tuple showing the length of each dimension of an ndarray.
- size (attribute) : The total number of elements in array

```sh
import numpy as np

data = np.array([180, 176.2, 176.3])

# It will print <class 'numpy.ndarray'>. ndarray means N-Dimensional Array.
print(type(data))

# It will print (3,). It means 3 values.
print(data.shape)

fuel = np.array([
    [180,179,178],
    [177,176,175]
])

# It will print (2,3). It means 2 lines and 3 columns.
print(fuel.shape)

windows = np.array([
    [180,179,178,177,176],
    [179,178,177,176,175],
    [178,177,176,175,174]
])

# It will print (3,5). It means 3 windows and 5 measurements per window.
print(windows.shape)
```

*Note : We can slice data like : tab[begin:end]. End is never include.*
