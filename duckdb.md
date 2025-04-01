# DuckDB Cheat Sheet

DuckDB is a lightweight, in-memory analytical database that works efficiently with Pandas, NumPy, and Parquet files.

## Table of Contents

- [Installation & Setup](#installation--setup)
- [Database Connections](#database-connections)
- [Table Operations](#table-operations)
- [Data Querying](#data-querying)
- [Pandas Integration](#pandas-integration)
- [File Operations](#file-operations)
- [Advanced SQL Features](#advanced-sql-features)
- [JSON Operations](#json-operations)
- [Python Integration](#python-integration)
- [Performance Tips](#performance-tips)

## Installation & Setup

```python
# Install DuckDB
pip install duckdb

# Import
import duckdb
```

## Database Connections

### In-Memory Database (Fast & Temporary)

```python
conn = duckdb.connect(":memory:")
```

### Persistent Database (Stored in a File)

```python
conn = duckdb.connect("my_database.db")
```

## Table Operations

### Create a Table

```python
conn.execute("""
    CREATE TABLE users (
        id INTEGER,
        name TEXT,
        age INTEGER
    );
""")
```

### Insert Data

```python
conn.execute("INSERT INTO users VALUES (1, 'Alice', 30), (2, 'Bob', 25)")
```

## Data Querying

### Basic Queries

```python
# Fetch all records
result = conn.execute("SELECT * FROM users").fetchall()
print(result)

# Query with condition
result = conn.execute("SELECT name FROM users WHERE age > 25").fetchdf()
print(result)
```

## Pandas Integration

### Working with DataFrames

```python
import pandas as pd

# Create a sample DataFrame
df = pd.DataFrame({
    'id': [1, 2, 3],
    'name': ['Alice', 'Bob', 'Charlie'],
    'age': [30, 25, 35]
})

# Register DataFrame as a DuckDB Table
conn.register('users_df', df)

# Query DataFrame using SQL
result = conn.execute("SELECT * FROM users_df WHERE age > 28").fetchdf()
print(result)
```

## File Operations

### CSV Operations

```python
# Read CSV File
df = duckdb.read_csv("data.csv")

# Write to CSV
conn.execute("COPY users TO 'users_output.csv' (FORMAT CSV, HEADER)")
```

### Parquet Operations

```python
# Read Parquet File
df = duckdb.read_parquet("data.parquet")

# Write to Parquet
conn.execute("COPY users TO 'users_output.parquet' (FORMAT PARQUET)")
```

## Advanced SQL Features

### Filtering & Sorting

```python
conn.execute("SELECT * FROM users WHERE age > 25 ORDER BY age DESC").fetchdf()
```

### Grouping & Aggregations

```python
conn.execute("SELECT age, COUNT(*) FROM users GROUP BY age").fetchdf()
```

### Joins

```python
conn.execute("""
    SELECT u.name, o.amount
    FROM users u
    JOIN orders o ON u.id = o.user_id
""").fetchdf()
```

### Window Functions

```python
conn.execute("""
    SELECT name, age,
           RANK() OVER (ORDER BY age DESC) AS rank
    FROM users
""").fetchdf()
```

## JSON Operations

```python
conn.execute("SELECT json_extract('{\"name\": \"Alice\", \"age\": 30}', '$.name')").fetchall()
```

## Python Integration

### Custom Functions

```python
def square(x):
    return x * x

conn.create_function('square', square)
print(conn.execute("SELECT square(4)").fetchall())
```

## Performance Tips

```python
# Use Multiple Threads
conn.execute("PRAGMA threads=4")

# Enable Query Profiling
conn.execute("PRAGMA enable_profiling")
```
