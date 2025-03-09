The `dropna()` method in pandas is used to remove missing values (`NaN`, `NaT`, etc.) from a DataFrame or Series. It is a convenient way to clean your data by either dropping rows or columns that contain missing values.

### Syntax for `dropna()` in a DataFrame:
```python
DataFrame.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)
```

### Parameters:
1. **`axis`**:
   - `0` or `'index'`: Drop rows that contain missing values (default).
   - `1` or `'columns'`: Drop columns that contain missing values.

2. **`how`**:
   - `'any'`: Drop the row/column if **any** of the values are missing (default).
   - `'all'`: Drop the row/column only if **all** of the values are missing.

3. **`thresh`**:
   - Specifies the minimum number of non-missing values required to keep the row/column.
   - For example, `thresh=2` means a row/column must have at least 2 non-missing values to be kept.

4. **`subset`**:
   - A list of columns (or rows, if `axis=1`) to consider when dropping missing values.
   - Only the specified subset is checked for missing values.

5. **`inplace`**:
   - If `True`, the DataFrame is modified in place, and `None` is returned.
   - If `False` (default), a new DataFrame with the missing values dropped is returned.

---

### Syntax for `dropna()` in a Series:
```python
Series.dropna(axis=0, inplace=False, how=None)
```
- The parameters are similar to the DataFrame version, but simpler since a Series is one-dimensional.

---

### Examples:

#### Example 1: Drop rows with any missing values
```python
import pandas as pd
import numpy as np

data = {
    'A': [1, 2, np.nan, 4],
    'B': [5, np.nan, np.nan, 8],
    'C': [10, 11, 12, 13]
}

df = pd.DataFrame(data)
cleaned_df = df.dropna()
print(cleaned_df)
```
Output:
```
     A    B   C
0  1.0  5.0  10
3  4.0  8.0  13
```

#### Example 2: Drop columns with any missing values
```python
cleaned_df = df.dropna(axis=1)
print(cleaned_df)
```
Output:
```
    C
0  10
1  11
2  12
3  13
```

#### Example 3: Drop rows where all values are missing
```python
cleaned_df = df.dropna(how='all')
print(cleaned_df)
```
Output:
```
     A    B   C
0  1.0  5.0  10
1  2.0  NaN  11
2  NaN  NaN  12
3  4.0  8.0  13
```

#### Example 4: Drop rows with at least 2 non-missing values
```python
cleaned_df = df.dropna(thresh=2)
print(cleaned_df)
```
Output:
```
     A    B   C
0  1.0  5.0  10
1  2.0  NaN  11
3  4.0  8.0  13
```

#### Example 5: Drop missing values only in specific columns
```python
cleaned_df = df.dropna(subset=['A', 'B'])
print(cleaned_df)
```
Output:
```
     A    B   C
0  1.0  5.0  10
3  4.0  8.0  13
```

#### Example 6: Modify the DataFrame in place
```python
df.dropna(inplace=True)
print(df)
```
Output:
```
     A    B   C
0  1.0  5.0  10
3  4.0  8.0  13
```

---

### Notes:
- Missing values are represented as `NaN` (Not a Number) or `NaT` (Not a Time) in pandas.
- Use `fillna()` if you want to fill missing values instead of dropping them.
- Be cautious when using `inplace=True`, as it modifies the original DataFrame.
