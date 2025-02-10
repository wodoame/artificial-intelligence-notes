The `MinMaxScaler` class from `sklearn.preprocessing` is a preprocessing tool used to **scale and normalize features** in a dataset. It transforms the data such that all features are scaled to a specific range, typically between 0 and 1. This is useful for algorithms that are sensitive to the scale of input features, such as gradient descent-based models, neural networks, and distance-based algorithms (e.g., k-Nearest Neighbors).

---

### How `MinMaxScaler` Works:
1. **Transformation Formula**:
   - For each feature, `MinMaxScaler` applies the following transformation:
     \[
     X_{\text{scaled}} = \frac{X - X_{\text{min}}}{X_{\text{max}} - X_{\text{min}}}
     \]
     where:
     - \(X\) is the original feature value.
     - \(X_{\text{min}}\) is the minimum value of the feature.
     - \(X_{\text{max}}\) is the maximum value of the feature.

2. **Output Range**:
   - By default, the scaled values are in the range `[0, 1]`.
   - You can specify a different range using the `feature_range` parameter.

3. **Handling New Data**:
   - The `MinMaxScaler` learns the minimum and maximum values from the training data (using the `fit` method) and applies the same transformation to new data (using the `transform` method).

---

### Key Parameters:
- **`feature_range`**:
  - A tuple `(min, max)` specifying the desired range of the transformed data.
  - Default is `(0, 1)`.

- **`copy`**:
  - If `True` (default), a copy of the input data is created. If `False`, the transformation is applied in place.

---

### Example Usage:

```python
from sklearn.preprocessing import MinMaxScaler
import numpy as np

# Sample data
data = np.array([[1, 2], [2, 3], [3, 6], [4, 10]])

# Initialize MinMaxScaler
scaler = MinMaxScaler(feature_range=(0, 1))

# Fit and transform the data
scaled_data = scaler.fit_transform(data)

print("Original data:\n", data)
print("Scaled data:\n", scaled_data)
```

Output:
```
Original data:
 [[ 1  2]
  [ 2  3]
  [ 3  6]
  [ 4 10]]

Scaled data:
 [[0.         0.        ]
  [0.33333333 0.125     ]
  [0.66666667 0.5       ]
  [1.         1.        ]]
```

---

### Explanation:
- For the first column:
  - Minimum value = 1, Maximum value = 4.
  - The first value `1` is transformed to \((1 - 1) / (4 - 1) = 0\).
  - The last value `4` is transformed to \((4 - 1) / (4 - 1) = 1\).

- For the second column:
  - Minimum value = 2, Maximum value = 10.
  - The first value `2` is transformed to \((2 - 2) / (10 - 2) = 0\).
  - The last value `10` is transformed to \((10 - 2) / (10 - 2) = 1\).

---

### Key Features:
1. **Preserves Data Distribution**:
   - `MinMaxScaler` does not change the shape of the data distribution; it only scales the values.

2. **Sensitive to Outliers**:
   - Since `MinMaxScaler` uses the minimum and maximum values, outliers can significantly affect the scaling. For example, a single extreme outlier can compress the rest of the data into a small range.

3. **Inverse Transformation**:
   - You can use the `inverse_transform` method to revert the scaled data back to its original scale.

---

### When to Use `MinMaxScaler`:
- When you need to scale features to a specific range (e.g., for neural networks or algorithms that require input data to be within a bounded range).
- When the data does not contain significant outliers.

---

### Comparison with Other Scalers:
- **`StandardScaler`**:
  - Scales data to have a mean of 0 and a standard deviation of 1.
  - Less sensitive to outliers compared to `MinMaxScaler`.
- **`RobustScaler`**:
  - Uses the median and interquartile range (IQR) for scaling, making it robust to outliers.

In summary, `MinMaxScaler` is a simple and effective tool for scaling data to a specific range, but it should be used with caution when outliers are present in the dataset.
