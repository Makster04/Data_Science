# [Getting Started with NumPy - Lab](https://colab.research.google.com/gist/bpurdy-ds/81963e175eb8c707ae91298c495104d1/index.ipynb#scrollTo=oDxQ7C2VckdJ)

## Introduction

Now that we have introduced NumPy, let's put it to practice. In this lab, you are going to be creating arrays, performing operations on them, and returning new arrays all using the NumPy library. Let's get started!

# Objectives

You will be able to:

- Instantiate a numpy array with specified values
- Use broadcasting to perform a math operation on an entire numpy array


```python
Import NumPy under the standard alias
import numpy as np
```


## Generate some mock data

Create a NumPy array for each of the following:
    1. Using a range
    2. Using a Python list
    
Below, create a list in Python that has 5 elements (i.e. [0,1,2,3,4]) and assign it to the variable `py_list`.

Next, do the same, but instead of a list, create a range with 5 elements and assign it to the variable, `py_range`.

Finally, use the list and range to create NumPy arrays and assign the array from list to the variable `array_from_list`, and the array from the range to the variable `array_from_range`.

```python
# Your code here
py_list: [0, 1, 2, 3, 4]
py_range: range(0, 5)
array_from_list: np.array([0, 1, 2, 3, 4])
array_from_range: np.array([0, 1, 2, 3, 4])
```

Next, we have a list of heights and weights and we'd like to use them to create a collection of BMIs. However, they are both in inches and pounds (imperial system), respectively.

Let's use what we know to create NumPy arrays with the metric equivalent values (height in meters & weight in kg).

> **Remember:** *NumPy can make these calculations a lot easier and with less code than a list!*
________________________________________
> 1.0 inch = 0.0254 meters

> 2.2046 lbs = 1 kilogram
________________________________________
### Codes
#### Input:
```python
# Use the conversion rate for turning height in inches to meters
list_height_inches = [65, 68, 73, 75, 78]

array_height_inches = np.array(list_height_inches)
array_height_meters = (array_height_inches) * (0.0254)

array_height_meters
```
#### Output:
```
array([1.651 , 1.7272, 1.8542, 1.905 , 1.9812])
```
________________________________________
#### Input:
```python
# Use the conversion rate for turning weight in pounds to kilograms
list_weight_pounds = [150, 140, 220, 205, 265]

# Your code here
array_weight_pounds = np.array(list_weight_pounds)
array_weight_kg = (array_weight_pounds) / (2.2046)

array_weight_kg
```
#### Output:
```
array([ 68.03955366,  63.50358342,  99.79134537,  92.98739   ,
       120.20321147])
```
________________________________________
The metric formula for calculating BMI is as follows:

> BMI = weight (kg) ÷ height^2 (m^2)

So, to get BMI we divide weight by the squared value of height. For example, if I weighed 130kg and was 1.9 meters tall, the calculation would look like:

> BMI = 130 / (1.9*1.9)

Use the BMI calculation to create a NumPy array of BMIs
________________________________________
### Codes

#### Input:
```python
# Your code here
BMI_array = array_weight_kg / (array_height_meters ** 2)

BMI_array
```
#### Output:
```
array([24.9613063 , 21.28692715, 29.02550097, 25.62324316, 30.62382485])
```
________________________________________
## Create a vector of ones the same size as your BMI vector using `np.ones()`
________________________________________
### Code

#### Input:
```python
# Your code here
identity = np.ones(5)
identity
```
#### Output:
```
array([1., 1., 1., 1., 1.])
```
________________________________________
## Multiply the BMI_array by your vector of ones

The resulting product should have the same values as your original BMI numpy array.
________________________________________
### Code

#### Input:
```python
# Your code here
identity * BMI_array
```
#### Output:
```
array([24.9613063 , 21.28692715, 29.02550097, 25.62324316, 30.62382485])
```
________________________________________
## Level Up: Using NumPy to Parse a File
The Pandas library that we've been using is built on top of NumPy; all columns/series in a Pandas DataFrame are built using NumPy arrays. To get a better idea of a how a built-in method like `pd.read_csv()` works, we'll try and recreate that here!

#### Input:
```python
import numpy as np

# Open the file
with open('/content/bp (1).txt') as f:
    # Read the entire file into lines
    lines = f.readlines()

# The first line contains the column headers, so we can skip it
# Let's determine the number of rows and columns in the file
num_rows = len(lines) - 1  # Subtract 1 for the header
num_cols = len(lines[0].split())  # Assuming columns are space-separated, split the first line

# Step 1: Create a NumPy matrix of zeros with the correct size
matrix = np.zeros((num_rows, num_cols))

# Step 2: Iterate through the file and populate the matrix with data
for i, line in enumerate(lines[1:]):  # Skip the first line (header)
    # Step 3: Convert each line to a list of float values
    data = [float(x) for x in line.split()]
    # Step 4: Update the matrix row by row
    matrix[i] = data

# Step 5: Preview the results
print(matrix)
```
#### Output:
```
[[  1.   105.    47.    85.4    1.75   5.1   63.    33.  ]
 [  2.   115.    49.    94.2    2.1    3.8   70.    14.  ]
 [  3.   116.    49.    95.3    1.98   8.2   72.    10.  ]
 [  4.   117.    50.    94.7    2.01   5.8   73.    99.  ]
 [  5.   112.    51.    89.4    1.89   7.    72.    95.  ]
 [  6.   121.    48.    99.5    2.25   9.3   71.    10.  ]
 [  7.   121.    49.    99.8    2.25   2.5   69.    42.  ]
 [  8.   110.    47.    90.9    1.9    6.2   66.     8.  ]
 [  9.   110.    49.    89.2    1.83   7.1   69.    62.  ]
 [ 10.   114.    48.    92.7    2.07   5.6   64.    35.  ]
 [ 11.   114.    47.    94.4    2.07   5.3   74.    90.  ]
 [ 12.   115.    49.    94.1    1.98   5.6   71.    21.  ]
 [ 13.   114.    50.    91.6    2.05  10.2   68.    47.  ]
 [ 14.   106.    45.    87.1    1.92   5.6   67.    80.  ]
 [ 15.   125.    52.   101.3    2.19  10.    76.    98.  ]
 [ 16.   114.    46.    94.5    1.98   7.4   69.    95.  ]
 [ 17.   106.    46.    87.     1.87   3.6   62.    18.  ]
 [ 18.   113.    46.    94.5    1.9    4.3   70.    12.  ]
 [ 19.   110.    48.    90.5    1.88   9.    71.    99.  ]
 [ 20.   122.    56.    95.7    2.09   7.    75.    99.  ]]
```

## Summary
________________________________________
In this lab, we practiced creating NumPy arrays from both lists and ranges. We then practiced performing math operations like converting imperial measurements to metric measurements on each element of a NumPy array to create new arrays with new values. Finally, we used both of our new NumPy arrays to operate on each other and create new arrays containing the BMIs from our arrays containing heights and weights.
________________________________________


