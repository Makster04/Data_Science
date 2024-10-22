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

# [Implementing Statistics with Functions - Lab](https://colab.research.google.com/gist/bpurdy-ds/a93b079e97db488b5d1f17172e1a37c5/index.ipynb)

## Introduction 
In this lab you'll dive deep into calculating the measures of central tendency and dispersion introduced in previous lessons. You will code the formulas for these functions in Python which will require you to use the programming skills that you have gained in the other lessons of this section. Let's get started!

## Objectives

You will be able to:

* Calculate the measures of dispersion for a dataset
* Compare the different measures of dispersion
* Calculate the measures of central tendency for a dataset
* Compare the different measures of central tendency

## Dataset

For this lab, we'll use the [NHIS dataset](http://people.ucsc.edu/~cdobkin/NHIS%202007%20data.csv), which contains weights, heights, and some other attributes for a number of surveyed individuals. The context of this survey is outside the scope this lab, so we'll just go ahead and load the heights column as a list for us to run some simple statistical experiments. We'll use the `pandas` library to import the data into our Python environment. This process will be covered in detail in a later section. For now, we'll do this part for you to give you a head start.  

Run the cell below to import the data. 


```python
import pandas as pd
df = pd.read_csv('nhis.csv')
height = list(df['height'])
```

We are only interested in the height column, so we saved it as a list in the variable `height` in the cell above. 

In the cells below:

* Display the number of items in `height`
* Slice and display the first 10 items from `height`

### Code

#### Input:
```python
# Replace None with appropriate code
num_records = height[:10]

num_records # [74, 70, 61, 68, 66, 98, 99, 70, 65, 64]
```
#### Output:
```
[74, 70, 61, 68, 66, 98, 99, 70, 65, 64]
```

So, around 4800 records of height. That's great. Next, we'll try plotting some basic **_histograms_** for these records. 

## Plotting Histograms

We'll begin by importing the `pyplot` module from the library `matplotlib` and setting an alias of `plt` for it (so that we only have to type `plt.` instead of `matplotlib.pyplot.` each time we want to use it).  Note that `plt` is considered the **_standard alias_** for Matplotlib.

Run the cell below to import Matplotlib and use it to create a histogram of our `height` data with 8 different bins. 


```python
# Run this cell without changes
import matplotlib.pyplot as plt
%matplotlib inline  
# ^^This is a 'magic command' built into jupyter notebooks. We use it so that the visualization displays 
# in the notebook directly, instead of in a separate window.  
```

Next, we'll use Matplotlib to create a histogram by passing in our data, as well as the parameter `bins=8`, into the `hist` function.


```python
# Run this cell without changes
# A histogram should display below
plt.hist(height, bins=8);
```
![image](https://github.com/user-attachments/assets/d2ea9a0a-14a1-4b71-868b-9198416e1c79)

Do you spot anything unusual above? Some outliers, maybe?

## Measures of Central Tendency

### Calculating the Mean

We're just beginning to dig into the data stored in `height`. We'll begin by writing a function to calculate the mean of the data.  Recall the formula for calculating mean:

$$ \Large \bar{x} = \frac{1}{n} \sum_{i=1}^{n}x_i $$

Using the Python skills you have learned so far, create a function `get_mean()` to perform the following tasks: 
* Input a list of numbers (like the height list we have above)
* Calculate the sum of numbers and length of the list 
* Calculate mean from above, round off to 2 decimals and return it.

#### Input:
```python
def get_mean(data):
    # Replace None with appropriate code
    total_sum = sum(data)
    length = len(data)
    mean = total_sum/length
    
    return round(mean,2)

test1 = [5, 4, 1, 3, 2]
test2 = [4, 2, 3, 1]

print(get_mean(test1)) # 3.0
print(get_mean(test2)) # 2.5
```
#### Output:
```
3.0
2.5
```
________________________________________

Now, we'll test the function by passing in the height list.

#### Input:
```python
# Run this cell without changes
mean = get_mean(height)

print("Sample Mean:", mean) # Sample Mean: 69.58
```
#### Output:
```
Sample Mean: 69.58
```
So, we have our mean length, 69.58, and this confirms our observations from the histogram. But we also have some outliers in our data above and we know outliers affect the mean calculation by pulling the mean value in their direction. So, let's remove these outliers and create a new list to see if our mean shifts or stays. We'll use a threshold of 80 inches, i.e. filter out any values greater than 80. 
 
Perform following tasks:

* Create a function `filter_height_outliers` that takes a list as an argument
* Perform a `for` loop to iteratively check and append values to a new list if the value is less than 80, for every element in the original list
* Return the new list 

#### Input:
```python
def filter_height_outliers(data):

    filtered_data = []
    for height in data:
      if height < 80:
        filtered_data.append(height)

    return filtered_data

test = [60, 70, 80, 90]
filter_height_outliers(test) # [60, 70]
```
#### Output:
```
[60, 70]
```

Great, now we can use `filter_height_outliers()` to filter our `height` list and plot a new histogram to see if things change considerably.  

#### Input:
```python
# Filter the height list using the above function
# Replace None with appropriate code
filtered_height = filter_height_outliers(height)

len(filtered_height) # 4347
```
#### Output:
```
4347
```

Now that we have filtered the outliers out of our data and reduced the size of the dataset from 4785 to 4347, let's recreate our histogram with 8 bins using our filtered data. 

**_NOTE_**: You do not need to reimport `matplotlib.pyplot as plt` -- once it's been imported, it's stored in memory and can be accessed whenever we like in other cells. 

#### Input:
```python
# Replace None with appropriate code
# A histogram should display below
plt.hist(height, bins=8);
```
![image](https://github.com/user-attachments/assets/b258334f-a36d-4a1b-9087-9ae1800e90dc)


Since we've filtered our data to remove outliers, we should also recalculate the mean.  Do this now in the cell below, using our `get_mean()` function. 

#### Input:
```python
# Replace None with appropriate code
new_mean = get_mean(filtered_height)

new_mean # 66.85
```
#### Output:
```
66.85
```

Does the mean height of our filtered data match up with what we see in our histogram of our filtered data?

Note that in some analytical situations we may not be able to exclude the outliers in such a naive manner. So, let's go ahead and calculate other measures of central tendency as well. We'll start by calculating the median value for our original (unfiltered) height data. 

### Calculating the Median 

The median is the value directly in the middle of the dataset. In statistical terms, this is the **_Median Quartile_**. If the dataset was sorted from lowest value to highest value, the median is the value that would be larger than the first 50% of the data, and smaller than the second 50%.

If the dataset has an odd number of values, then the median is the middle number.
If the dataset has an even number of values, then we take the mean of the middle two numbers.

In the cell below, write a function that takes in a list of numbers and returns the median value for that dataset. Make sure you first check for even / odd number of data points and perform the computation accordingly. The best approach to calculate the median is as follows:

1. Sort the data 
2. Check if the data has even or odd number of data points 
3. Calculate the median of the sorted data now that you know if the count is even or odd. 

Hints:

 - You can use the modulo operator `%` in Python to check if a value is even or odd -- odd numbers `% 2` (e.g. `5 % 2`) will equal `1`, while even numbers `% 2` (e.g. `4 % 2`) will equal `0`!
 - You can use integer division `//` to calculate the index -- for even numbers this just means that the result is an integer (e.g. `4 // 2` is `2` rather than `2.0`), while for odd numbers this means that the remainder is cut off (e.g. `7 // 2` is `3`, not `3.5`)


```python
def get_median(data):
    # Sort the data from smallest to largest
    data_sorted = sorted(data)
    
    # Calculate the length of the sorted data
    index = len(data_sorted)
    
    # Check if the number of data points is odd or even
    if index % 2 == 1:
        # If the number of elements is odd, return the middle element (index n//2)
        median = data_sorted[index // 2]
    else:
        # If the number of elements is even, find the two middle elements
        middle1 = data_sorted[index // 2 - 1]  # The element before the middle
        middle2 = data_sorted[index // 2]      # The element at the middle
        # Calculate the average of the two middle elements
        median = (middle1 + middle2) / 2

    # Return the calculated median value
    return median

# Test the function with two datasets: one odd-sized and one even-sized
test1 = [5, 4, 1, 3, 2]  # Odd number of elements
test2 = [4, 2, 3, 1]     # Even number of elements

# Print the median of the datasets
print(get_median(test1))  # 3
print(get_median(test2))  # 2.5

```
#### Output:
```
3
2.5
```

Great, now we can pass in our original `height` list to this function to check the median. 

#### Input:
```python
# Replace None with appropriate code
median = get_median(height)

median # 67
```
#### Output:
```
67
```

So, we have 67, which is much closer to the filtered list mean (66.85) than the mean we calculated with actual list (69.58). So, median in this case seems to be a much better indicator of the central tendency found in the dataset. This makes sense because we've already learned that medians are less sensitive to outliers than mean values are! 

Next, we'll calculate the mode. This could give us better insight into the typical values in the dataset based on how frequent a value is.  

### Calculating the Mode

The mode is the value that shows up the most in a dataset. A dataset can have 0 or more modes. If no value shows up more than once, the dataset is considered to have no mode value. If two numbers show up the same number of times, that dataset is considered bimodal. Datasets where multiple values all show up the same number of times are considered multimodal.

In the cell below, write a function that takes in a list of numbers and returns another list containing the mode value(s). In the case of only one mode, the list would have a single element. 

**_Hint_**: Building a **_frequency distribution_** table using dictionaries is probably the easiest way to approach this problem. Use each unique element from the height list as a key, and the frequency of this element as the value and build a dictionary. You can then simply identify the keys (heights) with maximum values. 

#### Input:
```python
# Throughout this cell, replace None with appropriate code

def get_mode(data):

    # Create and populate frequency distribution
    frequency_dict = {}

    for height in data:
        # If an element is not in the dict, add it to the dict with value 1
        if height not in frequency_dict:
          frequency_dict[height] = 1
        # If an element is already in the dict, +1 the value in place
        elif height in frequency_dict:
          frequency_dict[height] += 1
       

    # Find the frequency of the mode(s) by finding the largest
    # value in frequency_dict
    highest_freq = max(frequency_dict.values())

    # Create a list for mode values
    modes = []

    # From the dictionary, add element(s) to the modes list with max frequency
    for height, frequency in frequency_dict.items():
        if frequency == highest_freq:
          modes.append(height)

    # Return the mode list
    return modes

test1 = [1, 2, 3, 5, 5, 4]
test2 = [1, 1, 1, 2, 3, 4, 5, 5, 5]

print(get_mode(test1)) # [5]
print(get_mode(test2)) # [1, 5]

```
#### Output:
```
[5]
[1, 5]
````

That's done. Now you can use the above function to calculate the mode of the original `height` list to compare it with our mean and median values. 

#### Input:
```python
# Replace None with appropriate code
mode = get_mode(height)

mode # [64]
```
#### Output:
```
64
```

So, the mode value is much lower than our mean and median calculated earlier. What do you make of this? The answer to that could be subjective and depends on the problem. i.e. if your problem is to identify sizes for garments that would sell the most, you cannot disregard mode. However, if you want to get an idea about the general or typical height of individuals, you can probably still do that with the median and the average. 

To get an even clearer picture, we know we need to see how much the values deviate from the central values we have identified. We have seen variance and standard deviation before as measures of such dispersion. Let's have a go at these to strengthen our understanding of this data. 

## Measures of Dispersion

### Calculating the Variance

The formula for variance is: 

$$ \Large s^2 = \frac{1}{n - 1} \sum_{i=1}^{n}(x_i - \bar{x})^2 $$

Note that this formula is for the **sample** variance. The formula is slightly different than the formula for calculating population variance. Read more about the difference [here](https://www.macroption.com/population-sample-variance-standard-deviation/). In the cell below, write a function that takes a list of numbers as input and returns the variance (rounded to two decimal places) of the sample as output.

#### Input:
```python
# Replace None with appropriate code

def get_variance(sample):

    # First, calculate the sample mean using get_mean()
    sample_mean = get_mean(sample)

    sum_of_squares = 0
    
    for value in sample:
      # Now, calculate the sum of squares by subtracting the sample mean
      # from each height, squaring the result, and adding it to the total
      sum_of_squares += (value - sample_mean) ** 2

    # Divide the sum of squares by the number of items in the sample -1 to calculate variance
    variance = sum_of_squares / (len(sample) - 1)

    return round(variance, 2)

test1 = [1, 2, 3, 5, 5, 4]
test2 = [1, 1, 1, 2, 3, 4, 5, 5, 5]
print(get_variance(test1)) # 2.67
print(get_mean(test1)) # 3.33
print(get_variance(test2)) # 3.25
```
#### Output:
```
2.67
3.33
3.25

```
Now we can test the variance of our list `height` with our new `get_variance()` function. 

#### Input:

```python
# Replace None with appropriate code
variance = get_variance(height)

variance # 87.74
```
#### Output:
```
87.74
```

So this value, as we learned earlier, tells us a bit about the deviation but not in the units of underlying data. This is because it squares the values of deviations. Standard deviation, however, can deal with this issue as it takes the square roots of differences. So that would probably be a bit more revealing. 

## Calculating the Standard Deviation

In the cell below, write a function that takes a list of numbers as input and returns the standard deviation of that sample as output.

Recall that the formula for Standard Deviation is:

$$ \Large s = \sqrt{\frac{1}{n-1} \sum_{i=1}^{n}(x_i - \bar{x})^2} $$

To find the square root of a value in Python, you have two options (**either** approach will work):

One option is the `sqrt()` function from `math` library:

```python
from math import sqrt
sqrt(100) # 10.0
```

Alternatively, another approach would be to raise that number to the power of `0.5`:

```python
100**0.5 # 10.0
```

#### Input:
```python
#from math import sqrt

def get_stddev(sample):
    # Step 1: Calculate the mean
    mean = sum(sample) / len(sample)
    
    # Step 2: Calculate the squared differences and their sum
    squared_diffs = [(x - mean) ** 2 for x in sample]
    
    # Step 3: Calculate the variance (sum of squared differences divided by n-1)
    variance = sum(squared_diffs) / (len(sample) - 1)
    
    # Step 4: Calculate the standard deviation (square root of variance)
    stddev = sqrt(variance)
    
    return round(stddev, 2)

# Test the function
test = [120, 112, 131, 211, 312, 90]
print(get_stddev(test))  # This will print the standard deviation rounded to 2 decimal places
```
#### Output:
```
84.03
```
So now we can finally calculate the standard deviation for our `height` list and inspect the results. 

#### Input:
```python
# Replace None with appropriate code
standard_deviation = get_stddev(height)
standard_deviation # 9.37
```

#### Output:
```
9.37
```

So 9.37 inches is the amount of deviation present in our dataset. As we are still including outlier values, this might be slightly affected but these results are now much more reliable. 

Finally, we will build a boxplot for height data and see if it agrees with our understanding for this data that we have developed up to this point. Use the `matplotlib`'s `boxplot()` function with height data and comment on the output.

#### Input:
```python
# Replace None with appropriate code
# A boxplot should display below
plt.boxplot(filtered_height);
```
![image](https://github.com/user-attachments/assets/0f910feb-6eb9-4020-bf81-097b4958d173)


## Simplifying the Process with NumPy

We hope writing these functions was a useful experience in terms of deepening your understanding of these statistical measures as well as sharpening your Python skills. However in reality there is almost never a need to write these kinds of functions "by hand", since libraries like NumPy and SciPy can typically handle them for us in a single line.

Below is a demonstration of the same calculations performed above, written using Python libraries side-by-side with the results of the functions you've just written:


```python
# Run this cell without changes

import numpy as np
from scipy import stats

print("Mean:")
print(mean, "(our version)")
print(round(np.mean(height), 2), "(NumPy version)")
print()
print("Median:")
print(median, "(our version)")
print(np.median(height), "(NumPy version)")
print()
print("Mode:")
print(mode, "(our version)")
print(stats.mode(height, keepdims=True).mode, "(SciPy version)")
print()
print("Variance:")
print(variance, "(our version)")
print(round(np.var(height, ddof=1), 2), "(NumPy version)")
print()
print("Standard Deviation:")
print(standard_deviation, "(our version)")
print(round(np.std(height, ddof=1), 2), "(NumPy version)")
```

## Summary 

In this lab, we performed a basic, yet detailed, statistical analysis around measuring the tendencies of center and spread for a given dataset. We looked at building a number of functions to calculate different measures and also used some statistical visualizations to strengthen our intuitions around the dataset. We shall see how we can simplify this process as we study `numpy` and `pandas` libraries to ease out the programming load while calculating basic statistics. 

# [Covariance and Correlation - Lab](https://colab.research.google.com/gist/bpurdy-ds/af05b57ad3aabf52ef742deafbe0d4b2/index.ipynb)

## Introduction

In this lab, you will calculate covariance and correlation for some data in Python lists by using the formulas shown in the previous lesson. 

## Objectives

You will be able to:

- Calculate covariance and correlation  
- Declare and use a function with arguments   


## The Data

The two variables include 20 heights (in inches) and weights (in pounds). This will help us focus more on seeing covariance and correlation in action!

At this point, you should be able to calculate the average height and average weight. You can also explain the medians, variances, and standard deviations for this dataset.

But all of those measurements are only concerned with a **single variable**. Now that we have both heights and weights, we want to perform statistical analysis for **multiple variables**. In this lab, you'll answer the following questions:

1. Is there a linear relationship between weight an height? 
2. Does weight increase as height increases?
3. How strong is the linear relationship between weight and height?

There are always exceptions, but when you look at the population in general, taller people will tend to weigh more than shorter people. While you should *always* be cautious when generalizing, generalization of information can be very useful as it shows you a bigger picture that you can build your intuitions upon. This is also what a lot of core statistical principles are built upon.

First, run the below cells to load the heights and weights into memory.


```python
# Run this cell without changes
height = [68, 71, 61, 69, 71, 58, 72, 73, 58, 74, 
          61, 59, 69, 68, 64, 69, 72, 66, 65, 69]
weight = [165, 201, 140, 170, 192, 125, 195, 205, 
          115, 210, 135, 125, 172, 175, 145, 170, 
          200, 155, 150, 171]
```

## Calculating the Covariance 

In the previous lesson, we used this formula to represent population covariance:

$$\sigma_{XY} = \dfrac{1}{n}\displaystyle\sum_{i=1}^{n}(x_i -\mu_x)(y_i - \mu_y)$$

In this lab, we will be using the sample version of the formula, because of the assumption that this particular data is a _sample of a bigger population_. The bigger population here could be the entire world population. Here is this version of the formula:

$$cov (X,Y) = \frac{1}{n-1}\displaystyle\sum_{i=1}^{n}(x_i -\bar x)(y_i - \bar y)$$

This is mostly the same formula, with two differences:

1. Instead of $\mu_x$ and $\mu_y$ (the means for _populations_ $X$ and $Y$), we have $\bar x$ and $\bar y$, which are the means for _samples_ $X$ and $Y$. In both cases, the mean is the sum of the values divided by the count of the values.
2. We divide by $(n-1)$ here, instead of dividing by $n$. As with the differences in calculating variance and standard deviation for a *population* and a *sample*:
    - When calculating for a *population*, we would divide by $n$
    - When calculating for a *sample* (as we are now), we divide by $n-1$

These parts of the formula are the same:

- $x_i$ = ith element of variable $X$
- $y_i$ = ith element of variable $Y$
- $n$ = number of data points ($n$ must be same for $X$ and $Y$)

### Mean Normalization 

Looking at the formula of covariance, you'll notice that it is composed of $(x_i -\bar x)$ and $(y_i -\bar y)$. These are also known as the **mean normalized** variables $X$ and $Y$. The idea is that you take each element in $X$ and $Y$ and respectively subtract the mean of $X$ and $Y$. The result is that your altered ("normalized") $X$ and $Y$ now have mean 0.

So how do you do this? You can write a function that takes in a list, calculates the mean of this list, and returns a new list containing each element minus the calculated mean value. This will be used to calculate $(x_i -\bar x)$ and $(y_i -\bar y)$.

#### Input:
```python
# Replace None with appropriate code

def mean_normalize(var):
    # Initialize a list for storing normalized values
    normalized_values = []

    # Calculate the mean of var
    mean_value = sum(var) / len(var)

    # For each element in var, subtract the mean and add the result to the new list
    for value in var:
        normalized_values.append(value - mean_value)

    return normalized_values

# Test the function

mean_normalize([1, 2, 3, 4, 5]), mean_normalize([11, 22, 33, 44, 55])
# ([-2.0, -1.0, 0.0, 1.0, 2.0], [-22.0, -11.0, 0.0, 11.0, 22.0])
```
#### Output:
```
# ([-2.0, -1.0, 0.0, 1.0, 2.0], [-22.0, -11.0, 0.0, 11.0, 22.0])
```

Great! You'll see that our function maintains the _variance_ of list elements and moves the mean to zero. As a quick test, you can visualize what exactly happens to the data with mean normalization.

Use the `mean_normalize()` function to create a new variable `height_normalized` to be used in the plotting code below.

#### Input:
```python
# Mean normalize the height (replace None with appropriate code)
height_normalized = mean_normalize(height)
height_normalized
```
#### Output:
```
[1.1500000000000057,
 4.150000000000006,
 -5.849999999999994,
 2.1500000000000057,
 4.150000000000006,
 -8.849999999999994,
 5.150000000000006,
 6.150000000000006,
 -8.849999999999994,
 7.150000000000006,
 -5.849999999999994,
 -7.849999999999994,
 2.1500000000000057,
 1.1500000000000057,
 -2.8499999999999943,
 2.1500000000000057,
 5.150000000000006,
 -0.8499999999999943,
 -1.8499999999999943,
 2.1500000000000057]
________________________________________

```

Now, run the cell below to visualize the data before and after mean normalization. 


```python
# Run this cell without changes
import matplotlib.pyplot as plt
%matplotlib inline

fig, ax = plt.subplots()

ax.hist(height_normalized, label="normalized data", bins=6)
ax.hist(height, label="original data", bins=6)

ax.set_title("Distribution of Height Data Before and After Normalization")
ax.set_xlabel("Height")
ax.set_ylabel("Count")

ax.legend(loc="center");
```
![image](https://github.com/user-attachments/assets/13bc4a7f-e39e-4ae4-b176-e22ae339675a)


There you go! The _shape_ of the data isn't changed, but the mean is just shifted! You can also try this for the `weight` variable if you wish.

### The Dot Product
Now that you know how to normalize the variables `height` and `weight` (i.e. $(x_i -\mu_x)$ and $(y_i - \mu_y)$ in math notation) it's time to take the _dot product_ of these two normalized variables in order to find $\sum_{i=1}^{n}(x_i -\mu_x)(y_i - \mu_y)$.

> A dot product is a linear algebraic operation that takes two equal-length sequences of numbers and returns a single number which can be used as a measure of similarity between these sequences (also known as vectors).

[Here is a great article explaining this in detail](https://betterexplained.com/articles/vector-calculus-understanding-the-dot-product/).

For two vectors `a` and `b`, a dot product is calculated by multiplying each element of one vector to its counterpart in the second, and then adding them up together. Imagine you want to take the dot product of two variables `a` and `b`:

```
 a[0] * b[0] + a[1] * b[1] + a[2] * b[2] ...

```

Let's write a function that takes two iterables and returns their dot product. 

#### Input:
```python
# Replace None with appropriate code

def dot_product(x, y):
    # Initialize a variable to store the sum of the products
    dot_product_result = 0

    # Iterate over both lists and multiply corresponding elements
    for i in range(len(x)):
        dot_product_result += x[i] * y[i]

    return dot_product_result

# Test the function with sample data
a = [1, 2, 3]
b = [4, 5, 6]


dot_product(a,b)
#  32, calculated as (1*4 + 2*5 + 3*6)
```
#### Output:
```
32
```

If you apply `mean_normalize` then `dot_product`, you have $\sum_{i=1}^{n}(x_i -\mu_x)(y_i - \mu_y)$ (the numerator of the covariance formula).

Now that have the numerator of the formula sorted out, let's finally write a function `covariance()` that takes the `height` and `weight` lists and returns the covariance value using the functions you created earlier.

To accomplish this, apply `mean_normalize` and `dot_product`, and divide the whole thing by $n-1$ in order to get the covariance:

$$\frac{1}{n-1}\displaystyle\sum_{i=1}^{n}(x_i -\bar x)(y_i - \bar y)$$

#### Input:
```python
# Replace None with appropriate code

def covariance(x, y):
    # Mean normalize both lists
    x_norm = mean_normalize(height)
    y_norm = mean_normalize(weight)

    # Calculate the numerator
    numerator = dot_product(x_norm, y_norm)


    # Divide the numerator by n - 1 and return
    return numerator / (len(x)-1)


covariance(height, weight)
# 144.75789473684208
```
#### Output:
```
144.75789473684208
```


So, we have a covariance of about 144.8. Recall the questions posed at the beginning:

1. Is there a linear relationship between weight an height? 
2. Does weight increase as height increases?
3. How strong is the linear relationship between weight and height?

Before looking at the answer below, try to identify: **Which (if any) questions can we answer with this covariance value?**

.

.

.

*Answer: we can answer questions 1 and 2.* 

 - Because the covariance is not (close to) zero, we can say that there ***is*** a linear relationship between weight and height.
 - Because the covariance is positive rather than negative, we can say that in general, yes, weight increases as height increases.

So far, we cannot give a clear answer to question 3, because the scale of the covariance is based on the units of measurement in this data (inches and pounds, in this case). 

While the covariance can be used to figure out *in which direction* two variables have a linear relationship — does one increase while the other decreases, or vice versa — any conclusion we might draw about the *strength* of the linear relationship from the covariance would be an artifact of these particular units.

If we want to make a generalized claim about the strength of the relationship in order to compare it to measurements using different units (e.g. height and resting heart rate), we need a measure that compares like units with like units. **Correlation** (specifically Pearson correlation) converts the units of each variable to "units of standard deviation" and standardizes the scale of the resulting calculation from -1 to 1, allowing us to make claims about the strength of the relationship that are not tied to the original measurement units.

In order to answer question 3, let's calculate the correlation.

## Calculating the Correlation

In the previous lesson, we used this formula to represent population correlation:

$$ r = \frac{\sum_{i=1}^{n}(x_i -\mu_x)(y_i - \mu_y)} {\sqrt{\sum_{i=1}^{n}(x_i - \mu_x)^2 \sum_{i=1}^{n}(y_i-\mu_y)^2}}$$

Now we'll use this version to calculate the sample correlation:

$$ r = \frac{\sum_{i=1}^{n}(x_i -\bar x)(y_i - \bar y)} {\sqrt{\sum_{i=1}^{n}(x_i - \bar x)^2 \sum_{i=1}^{n}(y_i-\bar y)^2}}$$

Again, we are using $\bar y$ and $\bar x$ to represent sample means rather than $\mu_x$ and $\mu_y$ to represent population means.

The numerator of correlation is the covariance: 

$$\frac{1}{n-1}\displaystyle\sum_{i=1}^{n}(x_i -\mu_x)(y_i - \mu_y)$$

And the denominator of correlation is the standard deviation of $X$ times the standard deviation of $Y$:

$$\sqrt{\frac{1}{n-1} \sum_{i=1}^{n}(x_i - \bar{x})^2} * \sqrt{\frac{1}{n-1} \sum_{i=1}^{n}(y_i - \bar{y})^2}$$

(The complete formula looks a bit different because the $\frac{1}{n-1}$ is canceled out, and the square root is applied to both x and y at once.)

Let's use this helper function to calculate the standard deviation:

#### Input:
```python
# Run this cell without changes
from math import sqrt

def stddev(var):
    mean = sum(var)/len(var)

    sum_of_squares = 0
    for i in var:
        sum_of_squares += (i - mean)**2

    n = len(var)
    variance = sum_of_squares / (n - 1)
    return sqrt(variance)

stddev(height)
# 5.112162998801562

```
#### Output:
```
5.112162998801562
```


Now, use the functions `covariance()` and `stddev()` to define a function, `correlation()` that calculates the correlation between two lists. 

#### Input:
```python
# Calculate correlation between two variables using formula above
# Replace None with appropriate code

def correlation(x, y):
    # Find the numerator (covariance)
    numerator = covariance(x, y)

    # Find standard deviations of both lists
    s_x = stddev(x) 
    s_y = stddev(y) 

    # Return numerator divided by multiplied standard deviations
    return numerator / (s_x * s_y)


correlation(height, weight)
# 0.9773995748246297
```
#### Output:
```
0.9773995748246297
```

A correlation of 0.98, that's very close to 1! That means we can answer question 3: there is a **very strong** linear relationship between height and weight — at least for this particular sample.

That's one of the key takeaways, that sample size plays a major rule in determining the nature of a variable and its relationship with other variables. The set of 20 records used we seem to correlate highly, but if you look at 20 other people, you'll see that this result will be different. The correlation here will depend on the *sample*, and you'll see that this will differ more clearly when working with smaller samples.

(_Note:_ A correlation of a variable with itself is always equal to 1.)

A scatter plot of this sample of height and weight aligns well with this finding of a strong correlation:

#### Input:
```python
# Run this cell without changes

fig, ax = plt.subplots()

ax.scatter(height, weight, label="actual data")

x_bounds = [min(height), max(height)]
y_bounds = [min(weight), max(weight)]

ax.plot(x_bounds, y_bounds, "--", label="perfect correlation")

ax.set_title("Height vs. Weight for a Sample of Individuals")
ax.set_xlabel("Height (inches)")
ax.set_ylabel("Weight (pounds)")

ax.legend();
```
![image](https://github.com/user-attachments/assets/0a71906f-54b7-4af4-b8e9-86f74326c6ef)


## Simplifying the Process with NumPy

The goal of this exercise was for you to develop a deeper understanding of these statistics and to practice writing Python functions.

In a professional data science setting, you would not write these functions by hand, you would use a library to compute these statistics quickly and easily. Here, we'll use NumPy.


```python
# Run this cell without changes
import numpy as np
```

### Covariance with NumPy


```python
# Run this cell without changes
# NumPy calculates cov(height, height), cov(height, weight), cov(weight, height), and cov(weight, weight)
# We only need height vs. weight so we extract just that value
covariance_matrix = np.cov(height, weight)
covariance_matrix[0][1]
```
```
144.75789473684205
```

### Correlation with NumPy


```python
# Run this cell without changes
# Same as covariance, NumPy returns a matrix but we only need one value
correlation_matrix = np.corrcoef(height, weight)
correlation_matrix[0][1]
```
```
0.9773995748246294
```

That was a lot simpler than calculating it by hand!

## Summary 

In this lab, you practiced writing functions to calculate the covariance and correlation between variables. Along the way, you performed mean normalization and computed dot products. Finally, you learned how to calculate these measures using NumPy methods.

