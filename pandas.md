# Pandas Cheat Sheet

## Basic Operations

### Importing Pandas

```python
import pandas as pd
```

### Creating DataFrames

#### From Dictionary

```python
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['NY', 'LA', 'SF']
}
df = pd.DataFrame(data)
```

#### From Files

```python
# CSV
df = pd.read_csv('file.csv')

# Excel
df = pd.read_excel('file.xlsx')
```

### Data Exploration

```python
df.head()        # First 5 rows
df.tail()        # Last 5 rows
df.sample(5)     # Random 5 rows
df.info()        # Summary of DataFrame
df.describe()    # Statistical summary
df.shape         # Rows and columns count
df.columns       # List of column names
df.dtypes        # Data types of columns
```

## Data Manipulation

### Selecting Data

```python
# Column selection
df['Age']                # Single column
df[['Name', 'Age']]     # Multiple columns

# Row selection
df.iloc[0]              # By index
df.loc[0]              # By label
df.iloc[1:4]           # Index range
df.loc[df['Age'] > 30] # By condition
df.at[0, 'Name']       # Single value
```

### Filtering Data

```python
# Simple filtering
df[df['Age'] > 30]

# Multiple conditions
df[(df['Age'] > 25) & (df['City'] == 'NY')]

# String matching
df[df['Name'].str.contains('Ali')]
```

### Sorting Data

```python
# Single column
df.sort_values('Age')                    # Ascending
df.sort_values('Age', ascending=False)    # Descending

# Multiple columns
df.sort_values(['City', 'Age'], ascending=[True, False])
```

### Column Operations

#### Adding & Modifying

```python
# Add new column
df['Salary'] = [50000, 60000, 70000]

# Modify existing column
df['Age'] = df['Age'] + 1

# Derived column
df['NewCol'] = df['Age'] * 2

# Apply function
df['Category'] = df['Age'].apply(lambda x: 'Young' if x < 30 else 'Old')
```

#### Dropping

```python
df.drop(columns=['Salary'])    # Drop column
df.drop([0, 1])               # Drop rows by index
df.dropna()                   # Drop rows with NaN values
df.drop_duplicates()          # Remove duplicate rows
```

### Missing Data Handling

```python
df.fillna(0)             # Fill NaN with 0
df.fillna(df.mean())     # Fill NaN with column mean
df.dropna()              # Remove rows with NaN
df.isna().sum()          # Count NaNs in each column
```

## Advanced Operations

### Aggregation & Grouping

```python
# Basic grouping
df.groupby('City')['Age'].mean()

# Multiple aggregations
df.groupby('City').agg({
    'Age': 'mean',
    'Salary': 'sum'
})

# Statistical operations
df['Age'].mean()         # Mean
df['Age'].median()       # Median
df['Age'].mode()         # Mode
df['Age'].value_counts() # Frequency count
```

### Merging & Joining

```python
df1.merge(df2, on='ID', how='inner') # Inner join
df1.merge(df2, on='ID', how='left')  # Left join
df1.merge(df2, on='ID', how='right') # Right join
df1.merge(df2, on='ID', how='outer') # Outer join
```

### Pivot Tables

```python
df.pivot_table(
    values='Age',
    index='City',
    columns='Gender',
    aggfunc='mean'
)
```

### Date Operations

```python
# Convert to datetime
df['Date'] = pd.to_datetime(df['Date'])

# Extract components
df['Year'] = df['Date'].dt.year
df['Month'] = df['Date'].dt.month
df['Day'] = df['Date'].dt.day
```

### Exporting Data

```python
df.to_csv('output.csv', index=False)     # CSV
df.to_excel('output.xlsx', index=False)   # Excel
df.to_json('output.json')                 # JSON
```

### Function Application

```python
# Apply to single column
df['Age'] = df['Age'].apply(lambda x: x + 5)

# Apply to entire DataFrame
df.applymap(lambda x: x.upper() if type(x) == str else x)
```
