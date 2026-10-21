# Introduction to NumPy with Python

## What is NumPy?

**NumPy (Numerical Python)** is a Python library for working with numerical data. Its main structure is the **ndarray**, an N-dimensional array. Arrays allow calculations to be applied to many values at once.

NumPy is commonly used to prepare data, calculate statistics and support scientific computing and machine learning.

## Getting Started

Install NumPy in the terminal:

```bash
pip install numpy
```

Import it in a notebook code cell:

```python
import numpy as np
```

`np` is the short name used to access NumPy. Run notebook cells from top to bottom using **Shift + Enter**. Use Markdown cells for headings and explanations.

The workbook begins with Python variables, `print()` and addition before introducing arrays.

## 1. Creating Arrays

### From a list

```python
list1 = [5, 10, 15, 20]
arr1 = np.array(list1)
arr1
```

`np.array()` converts the list into an array. `type(arr1)` confirms that it is a NumPy `ndarray`.

### Using arange

```python
arr2 = np.arange(5, 30, 5)
arr2
```

Result: `[5, 10, 15, 20, 25]`.

The arguments are **start, stop and step**. The stop value, 30, is excluded.

## 2. Array Dimensions and Shape

| Dimension | Structure | Example shape |
| --- | --- | --- |
| 1D | One sequence of values | `(4,)` |
| 2D | Rows and columns | `(3, 4)` |
| 3D | Layers of rows and columns | `(2, 5, 4)` |

### A 2D array

```python
list1 = [5, 10, 15, 20]
list2 = [40, 45, 50, 55]

arr3 = np.array([list1, list2])
arr3.shape
```

Result: `(2, 4)` — 2 rows and 4 columns.

### A 3D array

```python
a3 = np.arange(40).reshape(2, 5, 4)
a3.shape
```

Result: `(2, 5, 4)` — 2 layers, each with 5 rows and 4 columns. The array contains 40 values, from 0 to 39.

`.shape` is an attribute, so it does not need parentheses.

## 3. Lists, Arrays and Calculations

Multiplying a list repeats its values. Multiplying an array calculates a new value for each element.

```python
[5, 10] * 2                 # [5, 10, 5, 10]
np.array([5, 10]) * 2       # array([10, 20])
```

A **scalar** is a single number. Adding a scalar to an array adds it to every element.

```python
arr1 + 5
```

Arrays can also be multiplied element by element:

```python
arr11 = np.array([40, 45, 50, 55])
arr1 * arr11
```

Result: `[200, 450, 750, 1100]`.

Arrays with different shapes must follow NumPy's **broadcasting** rules: when comparing dimensions from the right, each pair must be equal or one must be 1. This allows compatible shapes to work together.

## 4. Accessing Values

Indexes start at **0**. For the `arr3` example above:

| Code | Meaning | Result |
| --- | --- | --- |
| `arr3[1, 2]` | Second row, third column | `50` |
| `arr3[1]` | Second row | `[40, 45, 50, 55]` |
| `arr3[:, 3]` | All rows, fourth column | `[20, 55]` |

The colon `:` means all entries along that axis.

## 5. Statistical Methods

| Method | Purpose |
| --- | --- |
| `.sum()` | Total of the values |
| `.mean()` | Average of the values |
| `.var()` | Variance: how spread out the values are |
| `.min()` | Lowest value |
| `.max()` | Highest value |
| `.argmin()` | Index of the lowest value |
| `.argmax()` | Index of the highest value |

NumPy's `.var()` uses population variance by default (`ddof=0`). If minimum or maximum values tie, `.argmin()` and `.argmax()` return the first matching position.

### Calculating by axis

For a 2D array:

| Code | Calculation |
| --- | --- |
| `arr3.sum(0)` | Down the rows: one total per column |
| `arr3.sum(1)` | Across the columns: one total per row |
| `arr3.sum()` | Total of the whole array |

The same axis rule applies to `.mean()` and the other statistical methods.

## 6. Iterating Through Arrays

A loop can access each value in a 1D array:

```python
for x in arr1:
    print(x)
```

For a 2D array, nested loops access each row and then each value:

```python
for row in arr3:
    for num in row:
        print(num)
```

`np.nditer()` visits individual elements in an array of any dimension:

```python
for num in np.nditer(arr3):
    print(num)
```

## 7. Saving and Loading Arrays

```python
#Save in NumPy's binary format
np.save("JNotebook Array", arr3)

#Load the saved array
np.load("JNotebook Array.npy")

#Save as comma-separated text
np.savetxt("JNotebook Array.txt", arr3, delimiter=",")
```

`np.save()` adds `.npy` if needed. `np.savetxt()` uses the filename supplied; it does not add a text extension automatically. The workbook's text example uses the name `JNotebook Array` without an extension.

Files are saved in the notebook's current working folder unless another path is provided.

## 8. Student Scores Analysis

```python
scores = np.array([78, 85, 92, 67, 88, 95, 74, 81, 90, 69])
```

| Calculation | Code | Answer |
| --- | --- | --- |
| Highest score | `scores.max()` | 95 |
| Lowest score | `scores.min()` | 67 |
| Average score | `scores.mean()` | 81.9 |
| Total score | `scores.sum()` | 819 |

```python
#Add 5 bonus marks to each student
bonus_scores = scores + 5
```

Result: `[83, 90, 97, 72, 93, 100, 79, 86, 95, 74]`. The original `scores` array is unchanged.

## 9. Weather Data

```python
temperatures = np.array([18, 21, 25, 17, 16, 23, 28,
                         30, 22, 19, 15, 24, 27, 20])
avg_temp = temperatures.mean()
```

**Boolean indexing** selects values that meet a condition:

```python
temperatures[temperatures > 25]
```

Result: `[28, 30, 27]`.

A condition returns True or False for each value. `.sum()` counts matching days because True counts as 1 and False as 0.

| Calculation | Code | Answer |
| --- | --- | --- |
| Days above 25°C | `(temperatures > 25).sum()` | 3 |
| Days below 20°C | `(temperatures < 20).sum()` | 5 |
| Average temperature | `temperatures.mean()` | About 21.79°C |
| Hottest temperature | `temperatures.max()` | 30°C |
| Coldest temperature | `temperatures.min()` | 15°C |
| Hottest day number | `temperatures.argmax() + 1` | Day 8 |
| Coldest day number | `temperatures.argmin() + 1` | Day 11 |
| Days above average | `(temperatures > avg_temp).sum()` | 7 |

The temperatures below 20°C are `[18, 17, 16, 19, 15]`. Above and below exclude values equal to the limit.

**Why add 1?** Indexes start at 0, while day numbers start at 1. `.max() + 1` would add 1 to the temperature, so it cannot identify the day.

## 10. Retail Sales

```python
sales = np.array([
    [120, 150, 180, 200],
    [90, 110, 140, 160],
    [200, 220, 250, 300]
])

store_totals = sales.sum(1)
week_totals = sales.sum(0)
```

Rows represent 3 stores; columns represent 4 weeks.

| Calculation | Code | Answer |
| --- | --- | --- |
| Total per store | `sales.sum(1)` | `[650, 500, 970]` |
| Total per week | `sales.sum(0)` | `[410, 480, 570, 660]` |
| Overall sales | `sales.sum()` | 2120 |
| Best store | `store_totals.argmax() + 1` | Store 3 |
| Best week across all stores | `week_totals.argmax() + 1` | Week 4 |
| Average weekly sales per store | `sales.mean(1)` | `[162.5, 125.0, 242.5]` |

## 11. Random Customer Purchases

```python
rng = np.random.default_rng()
purchases = rng.integers(1, 501, size=10)
purchases
```

- `default_rng()` creates a random number generator.
- `.integers()` returns random whole numbers.
- `1` is included; `501` is excluded, allowing values from £1 to £500.
- `size=10` creates an array of 10 purchases.

Results can change each time the cell runs. The array stores numbers; pounds are the unit used in this example.

## 12. Reshape and Transpose

```python
numbers = np.array([1, 2, 3, 4, 5, 6])
reshaped = numbers.reshape(2, 3)
transposed = reshaped.transpose()
```

| Method | Purpose | Result in this example |
| --- | --- | --- |
| `.reshape(2, 3)` | Arrange the values into a new shape | `[[1, 2, 3], [4, 5, 6]]` |
| `.transpose()` | Swap rows and columns in a 2D array | `[[1, 4], [2, 5], [3, 6]]` |

Reshape must keep the same number of elements: 6 values fit into 2 × 3 or 3 × 2. With the default order, it places values row by row.

```python
reshaped.reshape(3, 2)
```

Result: `[[1, 2], [3, 4], [5, 6]]`. This differs from transpose, even though both results have shape `(3, 2)`.

For higher-dimensional arrays, transpose rearranges axes; without arguments, it reverses their order. Transposing a 1D array leaves its shape unchanged.

## Official Documentation

- [NumPy beginner guide](https://numpy.org/doc/stable/user/absolute_beginners.html)
- [Broadcasting](https://numpy.org/doc/stable/user/basics.broadcasting.html)
- [Variance](https://numpy.org/doc/stable/reference/generated/numpy.var.html)
- [argmax](https://numpy.org/doc/stable/reference/generated/numpy.argmax.html) and [argmin](https://numpy.org/doc/stable/reference/generated/numpy.argmin.html)
- [Iterating over arrays](https://numpy.org/doc/stable/reference/arrays.nditer.html)
- [Saving and loading data](https://numpy.org/doc/stable/reference/routines.io.html)
- [Random generators](https://numpy.org/doc/stable/reference/random/generator.html) and [integers](https://numpy.org/doc/stable/reference/random/generated/numpy.random.Generator.integers.html)
- [Reshape](https://numpy.org/doc/stable/reference/generated/numpy.reshape.html) and [transpose](https://numpy.org/doc/stable/reference/generated/numpy.transpose.html)
