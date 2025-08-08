# Data Operations

## Introduction

This section covers the fundamental data operations used in Python data analysis.



### Why CSV Files?

CSV (Comma-Separated Values) files are one of the most common formats for data storage and analysis. 
They store tabular data in plain text, where each line is a row and columns are separated by commas. 
CSV files are simple, lightweight, and widely supported, making them ideal for data exchange and processing.




### Main Python Packages

The primary Python packages used here are:  
- **pandas**: For powerful data manipulation and analysis  
- **NumPy**: For numerical computations and array operations  
- **os**: For interacting with the operating system



### Modules vs Packages

- A **module** is a single Python file (`.py`) containing code such as functions, classes, and variables.  
- A **package** is a folder containing multiple modules and an `__init__.py` file to mark it as a package.

For example:  
- `os` is a module.  
- `pandas` and `NumPy` are packages that contain multiple modules.

You can import them using `import module_name` or `import package_name` to access their functions and classes.



### Functions and Classes

- A **function** is a reusable block of code designed to perform a specific task.  
- A **class** is a blueprint for creating objects that bundle data (attributes) and functions (methods) together.

Example:  
- A function can add two numbers.  

- A class can represent a car with attributes (color, model) and actions (drive, stop).

  


### Common Python Data Types

Python provides several built-in data types useful for data analysis:

- **List**: Ordered, mutable collection that allows duplicates, e.g., `[1, 2, 2, 3]`  

- **Tuple**: Ordered, immutable collection that can contain duplicates, e.g., `(1, 2, 2, 3)`  
- **Dictionary**: Key-value pairs with unique keys, e.g., `{'a': 1, 'b': 2}`  
- **Set**: Unordered collection of unique items (no duplicates), e.g., `{1, 2, 3}`

  


### Key Data Structures for Analysis

- **NumPy Array (`np.array`)**: 
  A fast, multi-dimensional array for numerical computations, foundational in scientific computing.
- **Pandas DataFrame (`pd.DataFrame`)**: 
  A 2D, size-mutable, heterogeneous tabular data structure with labeled rows and columns, built on top of NumPy arrays, widely used for data manipulation and analysis.


---



## Set Working Directory

The working directory is the default folder where Python reads and saves files.

```python
import os

# Get current working directory
os.getcwd()

# Change working directory
os.chdir("/path/to/your/folder")  
```

---



## Read and Save CSV Data

```python
import pandas as pd
# Read a CSV file in to a DataFrame
df = pd.read_csv("data.csv")

# If the CSV contains Chinese characters and shows garbled text, specify the encoding:
df = pd.read_csv("data.csv", encoding="gbk")

# Export a DataFrame to a CSV file
df.to_csv("output.csv", index=False)
# Set index=False to avoid saving the DataFrame’s index as a separate column.
```

---



## Data Exploration and Inspection

`head()` and `tail()`  display the first or last few rows of the DataFrame.

```python
df.head()  # Show first 5 rows

df.head(10)  # Show first 10 rows

df.tail(3) # Show last 3 rows
```



`shape` returns the number of rows and columns as a tuple.

```python
df.shape  # (rows, columns)
```



`columns` lists all column names.

```python
df.columns
```



`dtypes` shows the data type of each column.

```python
df.dtypes
```



`info()` provides a summary of the DataFrame including data types, non-null counts, and memory usage.

```python
df.info()
```



`describe()` generates descriptive statistics like mean, std, min, max for numeric columns.

```python
df.describe()
```

---



## Selecting Rows and Columns

**Name-based selection: `loc`**: select rows and columns by their names. 

```python
# Select value at row label 2 and column 'column_name'
df.loc[2, 'column_name']

# Select all rows and specific columns
df.loc[:, ['col1', 'col2']]
```



**Position-based selection: `iloc`**: select rows and columns by their integer positions **(starting from 0)**. 

```python
# Select value at first row and second column
df.iloc[0, 1]
# Select all rows and first three columns
df.iloc[:, 0:3]
```



**Conditional filtering (Boolean indexing)**: select rows based on a condition. 

```python
# Rows where 'col' values are greater than 10
df[df['col'] > 10]
```



**Multiple conditions**: use `&` (and), `|` (or) with parentheses to combine conditions. 

```python
# Rows where col1 > 10 AND col2 < 5
df[(df['col1'] > 10) & (df['col2'] < 5)]

# Rows where col1 is 'A' OR col2 is 'B'
df[(df['col1'] == 'A') | (df['col2'] == 'B')]
```

---



## Row and Column Operations

**Add new columns:** columns can be added by direct assignment, calculation, or by using `assign()`.

```python
# Directly assign a constant value
df['new_col'] = 0

# Create a new column based on calculation of existing columns
df['sum_col'] = df['col1'] + df['col2']

# Using assign() method (returns a new DataFrame)
df = df.assign(new_col2 = df['col1'] * 2)
```



**Delete columns:** use `drop()` with `axis=1` to remove columns. (Note: `axis=0` is used to delete rows.)

```python
# Drop a single column
df = df.drop('col_to_drop', axis=1)

# Drop multiple columns
df = df.drop(['col1', 'col2'], axis=1)
```



**Rename columns:** use `rename()` method with a dictionary.

```python
# Rename a single column
df = df.rename(columns={'old_name': 'new_name'})

# Rename multiple columns
df = df.rename(columns={'old1': 'new1', 'old2': 'new2'})
```



**Delete rows:** use `drop()` with row labels or boolean filtering.

```python
# Drop row by label/index
df = df.drop(0)

# Drop rows based on condition
df = df[df['col1'] > 0]
```

---



## Merging and Concatenation

**pd.concat():** concatenate DataFrames either by rows or columns.

```python
import pandas as pd

# Concatenate two DataFrames by rows (default: axis=0)
df_concat = pd.concat([df1, df2])

# Concatenate by columns
df_concat_col = pd.concat([df1, df2], axis=1)
```



**pd.merge():** perform database-style joins including inner, outer, left, and right joins.

- `on`: specify the column name(s) to join on (must exist in both DataFrames).
- `how`: type of join:
  - `inner` (default): returns only rows with keys common to both DataFrames (intersection).
  - `outer`: returns all rows from both DataFrames, filling missing values with NaN (union).
  - `left`: returns all rows from the left DataFrame, matching rows from the right (left join).
  - `right`: returns all rows from the right DataFrame, matching rows from the left (right join).
- `left_on` and `right_on`: specify different columns to join on in the left and right DataFrames respectively.

```python
# Inner join on a common column 'key'
df_merge_inner = pd.merge(df1, df2, on='key', how='inner')

# Left join with different key columns
df_merge_left = pd.merge(df1, df2, left_on='key1', right_on='key2', how='left')
```



**join() method:** join columns of another DataFrame, by default based on the index. 

```python
# Join df2 to df1 using index by default how='left'
df_joined = df1.join(df2)

# Equivalent to
df_joined = df1.join(df2, how='left')

# Keep only the rows with indexes present in both DataFrames (inner join)
df_inner = df1.join(df2, how='inner')
```

---



## Data Type Conversion

**astype():** convert a column to a different data type, such as numeric, string, or categorical.

```python
# Convert column to string
df['col'] = df['col'].astype(str)

# Convert column to numeric
df['col'] = df['col'].astype(float)

# Convert column to categorical
df['col'] = df['col'].astype('category')
```



**pd.to_datetime():** convert a column to datetime format for date/time processing.

```python
# Convert a column to datetime
df['date_col'] = pd.to_datetime(df['date_col'])
```

---



## Sorting and Removing Duplicates

**sort_values():** sort a DataFrame by the values of one or more columns.

```python
# Sort by a single column ascending
df_sorted = df.sort_values('col1')

# Sort by multiple columns, descending on second column
df_sorted = df.sort_values(['col1', 'col2'], ascending=[True, False])
```



**sort_index():** sort a DataFrame by its index.

```python
# Sort by index ascending
df_sorted_idx = df.sort_index()

# Sort by index descending
df_sorted_idx = df.sort_index(ascending=False)
```



**drop_duplicates():** remove duplicate rows based on all or some columns.

```python
# Drop duplicate rows based on all columns
df_unique = df.drop_duplicates()

# Drop duplicates based on specific columns only
df_unique = df.drop_duplicates(subset=['col1', 'col2'])
```

---



## Set Operations

Sets are unordered collections of unique elements and are very useful for data analysis tasks such as finding differences, intersections, and unions between datasets.



### Common Set Operations

- **Difference (`-`)**: elements in set A but not in set B.
- **Intersection (`&`)**: elements common to both sets.
- **Union (`|`)**: all elements from both sets, without duplicates.
- **Symmetric difference (`^`)**: elements in either set A or set B but not in both.



### Examples with lists and sets

```python
listA = [1, 2, 3, 4, 5]
listB = [3, 4, 6]

setA = set(listA)
setB = set(listB)

# Difference: elements in listA but not in listB
diff = setA - setB
print("Difference:", diff)  # Output: {1, 2, 5}

# Intersection: elements common to both lists
inter = setA & setB
print("Intersection:", inter)  # Output: {3, 4}

# Union: all elements from both lists
union = setA | setB
print("Union:", union)  # Output: {1, 2, 3, 4, 5, 6}

# Symmetric difference: elements in either listA or listB but not both
sym_diff = setA ^ setB
print("Symmetric Difference:", sym_diff)  # Output: {1, 2, 5, 6}
```



### Use cases in data analysis

- Finding missing values or unique items between datasets.
- Comparing categories or labels from different sources.
- Quickly removing duplicates by converting lists to sets.
- Performing membership tests efficiently (`in` operator with sets).

---



## **Index Operations**

**Set index:** use `set_index()` to set one or more columns as the DataFrame index.

```python
# Set 'col1' as index
df = df.set_index('col1')

# Set multiple columns as multi-level index
df = df.set_index(['col1', 'col2'])
```

**Multi-level index (hierarchical index):** allows indexing by multiple keys, useful for complex data analysis.



**Reset index:** use `reset_index()` to reset the index back to default integer index. 

```python
# Reset index to default integer index
df = df.reset_index()
```



After selecting a subset, the index is inherited from the original DataFrame and may be non-continuous. To obtain a sequential, continuous index in the subset, it is common to apply the reset_index() method.

When using `reset_index()`, the existing index is by default added as a new column in the DataFrame.  Setting `drop=True` will discard the old index instead of inserting it as a column.

```python
# Reset index and drop the old index column
df = df.reset_index(drop=True)
```




> **Tip:** `.copy()` method  
>  
> Creates a deep copy of an object, which means modifying the copy won’t affect the original.  
>  
> In pandas, use `.copy()` to avoid unintended changes to the original DataFrame when creating a new variable.  
>  
> ```python
> df_copy = df.copy()
> df_copy['col'] = 0  # This change will NOT affect df
> ```
>  
> Without `.copy()`, assigning like `df_copy = df` only creates a reference, so changes affect both variables.


---



## Grouping and Aggregation

**groupby():** group data by one or more columns to perform aggregate calculations.

```python
# Group by a single column and calculate mean
grouped = df.groupby('col1').mean()

# Group by multiple columns and calculate sum
grouped = df.groupby(['col1', 'col2']).sum()
```



**Common aggregation functions:**  

- `mean()` — calculate the average  
- `sum()` — calculate the total sum  
- `count()` — count non-null values  
- `agg()` — apply multiple aggregation functions at once

```python
# Apply multiple aggregations on grouped data
grouped = df.groupby('col1').agg({
    'col2': 'mean',
    'col3': 'sum',
    'col4': 'count'
})
```

---



## **Handling Missing Data**

**Detect missing values:** use `isna()` or `notna()` to identify missing (NaN) data.

```python
# Check for missing values (True where data is missing)
df.isna()

# Check for non-missing values
df.notna()
```



**Fill missing values:** use `fillna()` to replace missing data with a specific value or method.

```python
# Fill missing values with a constant
df['col'] = df['col'].fillna(0)

# Fill missing values with forward fill method
df['col'] = df['col'].fillna(method='ffill')

# Fill missing values with the mean of the column
mean_value = df['col'].mean()
df['col'] = df['col'].fillna(mean_value)
```



**Drop missing values:** use `dropna()` to remove rows or columns containing missing data.

```python
# Drop rows with any missing values
df_clean = df.dropna()

# Drop columns with missing values
df_clean_cols = df.dropna(axis=1)
```





   