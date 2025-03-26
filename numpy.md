# NumPy Cheat Sheet

## 1. Importing NumPy

```python
import numpy as np
```

## 2. Creating Arrays

### Basic Array Creation

```python
# 1D array
arr = np.array([1, 2, 3])

# 2D array
arr2d = np.array([[1, 2, 3], [4, 5, 6]])

# 3D array
arr3d = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
```

### Common Array Creation Functions

```python
# Array of zeros
np.zeros((3, 3))  # 3x3 array of zeros

# Array of ones
np.ones((2, 2))  # 2x2 array of ones

# Array filled with a value
np.full((2, 3), 7)  # 2x3 array filled with 7

# Identity matrix
np.eye(3)  # 3x3 identity matrix

# Range arrays
np.arange(0, 10, 2)  # [0 2 4 6 8]
np.linspace(0, 1, 5)  # [0. 0.25 0.5 0.75 1.]

# Random arrays
np.random.rand(3, 3)  # Random floats in [0, 1)
np.random.randn(3, 3)  # Random from normal distribution
np.random.randint(1, 10, (2, 3))  # Random integers
```

## 3. Array Properties

```python
arr.shape    # Dimensions of the array
arr.size     # Total number of elements
arr.ndim     # Number of dimensions
arr.dtype    # Data type of elements
arr.itemsize # Bytes per element
```

## 4. Reshaping and Flattening

```python
arr.reshape((2, 3))  # Reshape to 2x3
arr.ravel()          # Flatten array (1D)
arr.flatten()        # Another way to flatten
arr.T                # Transpose
```

## 5. Indexing and Slicing

### Basic Indexing

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

arr[0, 1]     # Element at row 0, column 1
arr[:, 1]     # All rows, column 1
arr[0, :]     # Row 0, all columns
arr[1, 1:3]   # Row 1, columns 1 to 2
arr[-1, -1]   # Last element
```

### Boolean Indexing

```python
arr[arr > 2]                    # Elements greater than 2
arr[(arr > 2) & (arr < 5)]      # Elements between 2 and 5
```

## 6. Mathematical Operations

### Basic Operations

```python
arr + 2          # Add 2 to each element
arr * 2          # Multiply each element by 2
np.add(arr, 2)   # Element-wise addition
np.multiply(arr, 2)  # Element-wise multiplication
```

### Statistical Operations

```python
np.sum(arr)      # Sum of all elements
np.mean(arr)     # Mean of elements
np.std(arr)      # Standard deviation
np.min(arr)      # Minimum value
np.max(arr)      # Maximum value
np.argmin(arr)   # Index of min value
np.argmax(arr)   # Index of max value
np.cumsum(arr)   # Cumulative sum
np.cumprod(arr)  # Cumulative product
```

## 7. Linear Algebra

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

np.dot(A, B)                    # Matrix multiplication
np.matmul(A, B)                 # Matrix multiplication (preferred)
np.linalg.inv(A)                # Inverse of a matrix
np.linalg.det(A)                # Determinant
np.linalg.eig(A)                # Eigenvalues and eigenvectors
np.linalg.solve(A, np.array([1, 2]))  # Solve Ax = b
```

## 8. Stacking and Splitting

```python
np.hstack((arr, arr))  # Horizontal stack
np.vstack((arr, arr))  # Vertical stack
np.split(arr, 2, axis=0)  # Split into 2 parts along rows
```

## 9. Copying and Views

```python
arr_copy = arr.copy()  # Creates a new copy
arr_view = arr.view()  # Creates a view (shares memory)
```

## 10. Saving and Loading

```python
# Binary format
np.save('array.npy', arr)  # Save array
loaded_arr = np.load('array.npy')  # Load array

# Text format
np.savetxt('array.txt', arr, delimiter=',')  # Save as CSV
np.loadtxt('array.txt', delimiter=',')  # Load from CSV
```
