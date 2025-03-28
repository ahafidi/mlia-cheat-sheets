# Matplotlib Cheat Sheet

Matplotlib is a powerful plotting library in Python. This cheat sheet covers common commands and usage patterns.

## 1. Basic Setup

### Importing Matplotlib

```python
import matplotlib.pyplot as plt
```

## 2. Basic Plot Types

### Line Plot

```python
x = [1, 2, 3, 4]
y = [10, 20, 25, 30]
plt.plot(x, y, marker='o', linestyle='-', color='b', label="Line")
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.title("Line Plot Example")
plt.legend()
plt.grid(True)
plt.show()
```

### Scatter Plot

```python
plt.scatter(x, y, color='r', marker='s', label="Points")
plt.legend()
plt.show()
```

### Bar Chart

```python
plt.bar(x, y, color='g', label="Bars")
plt.legend()
plt.show()
```

### Histogram

```python
data = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
plt.hist(data, bins=4, color='c', edgecolor='black')
plt.show()
```

### Pie Chart

```python
labels = ['A', 'B', 'C', 'D']
sizes = [10, 20, 30, 40]
plt.pie(sizes, labels=labels, autopct='%1.1f%%',
        colors=['red', 'blue', 'green', 'yellow'])
plt.show()
```

## 3. Plot Customization

### Line Styles and Markers

```python
plt.plot(x, y, linestyle='--', marker='d', color='m')
```

#### Available Options:

- Line styles: `-`, `--`, `-.`, `:`
- Markers: `o`, `s`, `^`, `d`, `x`

### Titles and Labels

```python
plt.title("My Title", fontsize=14, fontweight='bold')
plt.xlabel("X Label", fontsize=12)
plt.ylabel("Y Label", fontsize=12)
```

### Legend

```python
plt.legend(loc='upper left')
```

- Available locations: `upper right`, `upper left`, `lower right`, `lower left`

### Grid and Axis Control

```python
# Grid customization
plt.grid(True, linestyle='--', linewidth=0.5)

# Axis labels
plt.xticks(rotation=45)  # Rotate x-axis labels
plt.yticks(fontsize=10)  # Change y-axis font size

# Axis limits
plt.xlim(0, 5)
plt.ylim(5, 35)
```

## 4. Subplots

```python
fig, axs = plt.subplots(2, 2, figsize=(8, 6))  # 2x2 grid of plots

# Plot in each subplot
axs[0, 0].plot(x, y, 'r')                # Top-left
axs[0, 1].bar(x, y, color='g')           # Top-right
axs[1, 0].scatter(x, y, color='b')       # Bottom-left
axs[1, 1].hist(data, bins=4, color='c')  # Bottom-right

plt.tight_layout()  # Adjusts spacing
plt.show()
```

## 5. Saving Figures

```python
plt.savefig("plot.png", dpi=300)  # Save as PNG with 300 DPI
plt.savefig("plot.pdf")           # Save as PDF
```

## 6. 3D Plots

```python
from mpl_toolkits.mplot3d import Axes3D
import numpy as np

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')

# Create data for 3D plot
x = np.linspace(-5, 5, 100)
y = np.linspace(-5, 5, 100)
X, Y = np.meshgrid(x, y)
Z = np.sin(np.sqrt(X**2 + Y**2))

ax.plot_surface(X, Y, Z, cmap='viridis')
plt.show()
```

## 7. Seaborn Integration

```python
import seaborn as sns

sns.set(style="darkgrid")  # Apply seaborn style
plt.plot(x, y)
plt.show()
```
