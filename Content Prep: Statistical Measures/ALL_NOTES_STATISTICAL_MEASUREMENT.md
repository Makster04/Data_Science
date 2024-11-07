# [Introduction to Numpy](https://colab.research.google.com/gist/bpurdy-ds/50550af4e7007d580a6658c875b820b0/index.ipynb)

## Introduction

In this section, we'll take a more formal look at *NumPy*. Besides being ubiquitous in Data Science, NumPy also provides us with blistering fast and efficient, list-like, data types called N-Dimensional Arrays or **ndarrays** or more simply arrays. This list-like data type is effectively a lighter weight version of a Python **list**, as it uses less of your computer's memory, which makes it more efficient, especially when dealing with large datasets. Don't worry if that seems a little vague. We will take a closer look at NumPy and how its arrays work in this lesson.

An important note: *Pandas* was actually built on top of *NumPy*! So many of the functionalities that *NumPy* has, are also part of *Pandas*. It is still important to cover *NumPy* separately as *NumPy* arrays are very important building blocks in many Data Science applications!

## Objectives
You will be able to: 

- Describe why NumPy is used at times over standard Python 
- Instantiate a NumPy array with specified values 
- Use broadcasting to perform a math operation on an entire NumPy array 

## Getting Started With NumPy

Just like with any other library, we need to first install the library with a package manager like `pip`. We have already installed this library in the background, so, no need to worry about this step. Next, we need to import the dependency into our code. 

The conventional method to import NumPy is by aliasing it as `np`, like this:


```python
import numpy as np
```

That was easy! Now we can use any functions from the NumPy library by simply typing `np.function_name()`. For example, if we wanted to create a NumPy array containing the values 1, 2, 3, and 4, we would write `np.array([1,2,3,4])`. Let's try it out below:


```python
numpy_arr = np.array([1, 2, 3, 4])
print('Here is a NumPy array:', numpy_arr)
print('You know it is a NumPy array because its type is:', type(numpy_arr))
```

    Here is a NumPy array: [1 2 3 4]
    You know it is a NumPy array because its type is: <class 'numpy.ndarray'>


While we'll focus on one-dimensional arrays in this lesson, it is important to mention that NumPy is very famous for its multi-dimensional arrays, like:


```python
numpy_ndarr = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
numpy_ndarr
```




    array([[1, 2, 3, 4],
           [5, 6, 7, 8]])



The benefits of using NumPy here will become more obvious in our math-heavier, linear algebra / matrices sections!

## Performing array operations

So why would you want to use a NumPy array instead of a list? Because compared to a list, NumPy makes it very easy to perform array operations, like adding, multiplying, and otherwise operating on each element of the array. 

First, let's take a look at a simple example. We have a list of integers, and we want to add 3 to each element in the list. One might try the following:


```python
list_of_integers = [0, 1, 2, 3]
```


```python
# Add 3 to each element
list_of_integers + 3
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-5-9c3da9888927> in <module>
          1 # Add 3 to each element
    ----> 2 list_of_integers + 3
    

    TypeError: can only concatenate list (not "int") to list


You'll see that this doesn't work, because Python expects a list-like object. And even if you convert the integer 3 to a list-like element, you won't exactly get the desired result.


```python
# Add 3 to each element
list_of_integers + [3]
```




    [0, 1, 2, 3, 3]



Let's see what happens if we convert our list to a *NumPy* array!


```python
# Convert to NumPy Array
array_of_integers = np.array(list_of_integers)
# Add 3
array_of_integers + 3
```




    array([3, 4, 5, 6])



It worked this time! So what actually happens behind the scenes here, is referred to as *broadcasting*. The term broadcasting describes how NumPy treats objects with different shapes during arithmetic operations: So, what this means in this context is that the value "3" when performing the addition is actually being *reused* throughout the entire array. This might seem trivial, but lists don't support this behavior!

So, we see that NumPy can operate on each element just by giving an operation to a NumPy array. But NumPy can *also* use two arrays to operate on one another. This is useful in cases where you have two sets of data that are indirectly related, but commonly used to create statistics like population and area of a given city or state, which would give us population density (i.e. nyc_population_density = nyc_population / nyc_square_miles )
 
What if we had a friend who is trying to figure out the square footage of their apartment. They've measured out the lengths of each room and put those into a list for us, and then made another list for the widths of each room. Instead of trying to figure out this bizarre way our friend grouped their data, let's use NumPy to create a list with the area in square feet for each room.


```python
lengths_of_each_room = np.array([10, 12, 20, 5])
widths_of_each_room = np.array([13, 15, 16, 4])
areas_of_each_room = lengths_of_each_room * widths_of_each_room
print ('Here is an array with the square footages for each room:', areas_of_each_room)
```

    Here is an array with the square footages for each room: [130 180 320  20]


### A Temperature Conversion Example

Now, let's imagine we have a list of temperatures that represent the average high temperatures for each month of the year in NYC. Currently, this list has all the temperatures in Fahrenheit. However, since NYC has such a large international presence and population, it would be great to have these numbers in Celsius as well. Without NumPy, we would have to access each element individually, get its value, convert the value to Celsius, and add the new value to a new array. With NumPy, we can just multiply each element by the factor we need to convert Fahrenheit to Celsius.

The formula for converting Fahrenheit to Celsius is below: 
```
T(°C) = (T(°F) - 32) × 5/9
```
Let's see an example of how we would perform this conversion with a Python list and a NumPy array.


```python
# Average temps in NYC from January -> December (in fahrenheit)
nyc_avg_temps_f = [39, 42, 50, 62, 72, 80, 85, 84, 76, 65, 54, 44]

# ----- Without NumPy -----
nyc_avg_temps_c = list(range(0,12))
nyc_avg_temps_c[0] = (nyc_avg_temps_f[0] - 32) * (5/9)
nyc_avg_temps_c[1] = (nyc_avg_temps_f[1] - 32) * (5/9)
nyc_avg_temps_c[2] = (nyc_avg_temps_f[2] - 32) * (5/9)
nyc_avg_temps_c[3] = (nyc_avg_temps_f[3] - 32) * (5/9)
nyc_avg_temps_c[4] = (nyc_avg_temps_f[4] - 32) * (5/9)
nyc_avg_temps_c[5] = (nyc_avg_temps_f[5] - 32) * (5/9)
nyc_avg_temps_c[6] = (nyc_avg_temps_f[6] - 32) * (5/9)
nyc_avg_temps_c[7] = (nyc_avg_temps_f[7] - 32) * (5/9)
nyc_avg_temps_c[8] = (nyc_avg_temps_f[8] - 32) * (5/9)
nyc_avg_temps_c[9] = (nyc_avg_temps_f[9] - 32) * (5/9)
nyc_avg_temps_c[10] = (nyc_avg_temps_f[10] - 32) * (5/9)
nyc_avg_temps_c[11] = (nyc_avg_temps_f[11] - 32) * (5/9)
# -------------------------

# ------ With NumPy -------
np_nyc_avg_temps_f = np.array(nyc_avg_temps_f)
np_nyc_avg_temps_c = (np_nyc_avg_temps_f - 32) * (5/9)
# -------------------------

print('1. Without NumPy:', nyc_avg_temps_c)
print('2. With NumPy:', np_nyc_avg_temps_c)
```

    1. Without NumPy: [3.8888888888888893, 5.555555555555555, 10.0, 16.666666666666668, 22.22222222222222, 26.666666666666668, 29.444444444444446, 28.88888888888889, 24.444444444444446, 18.333333333333336, 12.222222222222223, 6.666666666666667]
    2. With NumPy: [ 3.88888889  5.55555556 10.         16.66666667 22.22222222 26.66666667
     29.44444444 28.88888889 24.44444444 18.33333333 12.22222222  6.66666667]


Woah! Okay, we can see that in the first example, without NumPy, it took us **thirteen (13)** lines of code to accomplish the conversion from Fahrenheit to Celsius. With a NumPy array, we condensed that operation to **two (2)** lines of code. 

Let's break this down. Essentially the problem was to operate on each number in the list of NYC average monthly temperatures. The operation was to convert the number in Fahrenheit to Celsius. To do this, without NumPy, we must access each value from the `nyc_avg_temps_f` list separately, use the value to convert it to Celsius, and assign the converted value to the `nyc_avg_temps_c` list. *With* NumPy, we just need to use the variable name for the list, as if it were a single element, within the operation. NumPy then quickly performs the operation on each element and returns a **new** array.

Don't worry too much about how this is implemented behind the scenes. The key takeaway is that when we have large datasets that we want to operate on, NumPy can usually greatly simplify our code as well as make it more performant, which we will learn about later!

## Performance Benefits of NumPy Arrays

Another benefit to NumPy arrays, as we mentioned earlier, is that they use less memory and therefore make it easier for us to perform operations on them. However, this performance benefit is only really noticed when dealing with very large datasets. So, for now, the performance benefits of NumPy are purely educational, and we do not need to worry about them just yet. 

Let's take a look at an example. We will perform a simple operation on two sets of data. One is a regular list and the other is a NumPy array. Don't worry about the code. We are only focusing on the time difference between how long it takes us to perform the same operation with and without NumPy.


```python
import time

# Using 1 million integers
huge_list_of_integers = list(range(0, 1000000))
huge_np_array_of_integers = np.array(huge_list_of_integers)

def add_one(list_of_ints):
    return [num + 1 for num in list_of_ints]


start_time = time.perf_counter() # Time when operation starts
add_one(huge_list_of_integers) # Adds 1 to each number in the list of integers above
end_time = time.perf_counter() # Time when operation finishes
total_time = (end_time - start_time) # Total time for operation


start_time_with_np = time.perf_counter() # Time when operation starts
huge_np_array_of_integers + 1 # Adds 1 to each number in the array of integers
end_time_with_np = time.perf_counter() # Time when operation finishes
total_time_with_np = (end_time_with_np - start_time_with_np) # Total time for operation

print('Time it takes to add 1 to each element in a list without NumPy:', total_time)
print('Time it takes to add 1 to each element in a list with NumPy:', total_time_with_np)

percent_faster = int((((total_time - total_time_with_np)/total_time)*100))
print('NumPy completes the operation', percent_faster, '% faster than a traditional list')
```

    Time it takes to add 1 to each element in a list without NumPy: 0.061647489000002054
    Time it takes to add 1 to each element in a list with NumPy: 0.002932601000001256
    NumPy completes the operation 95 % faster than a traditional list


## Simulations with NumPy

To conclude this lesson, it is important to mention that NumPy is a very useful library to perform random sampling. What this means is that, given that we know what a certain population looks like, we can use `numpy.random` to essentially "produce" random samples given the population information.

Don't worry if this doesn't make sense right now. We'll explore this NumPy functionality later on.

## Summary

In this lesson, we introduced using NumPy to create arrays in Python. NumPy is a library that is very commonly used in Python when performing scientific computing operations. We looked at how NumPy can greatly reduce the amount of code we write while keeping our code very clear and concise. Next, we briefly looked at an example of the performance benefits of NumPy compared to a traditional list in Python. Finally, we touched upon NumPy's random number generating capabilities.

# [Getting Started with NumPy](https://colab.research.google.com/gist/bpurdy-ds/50550af4e7007d580a6658c875b820b0/index.ipynb)

## Introduction

NumPy is one of the main libraries for performing scientific computing in Python. Using NumPy, you can create high-performance multi-dimensional arrays, and several tools to work with these arrays. 

A NumPy array can store a grid of values. All the values must be of the same type. NumPy arrays are n-dimensional, and the number of dimensions is denoted by the *rank* of the NumPy array. The shape of an array is a tuple of integers which holds the size of the array along each of the dimensions.

For more information on NumPy, refer to http://www.numpy.org/.


## Objectives

You will be able to:
  
- Use broadcasting to perform a math operation on an entire numpy array    
- Perform vector and matrix operations with numpy 
- Access the shape of a numpy array    
- Use indexing with numpy arrays    




## NumPy array creation and basic operations

First, remember that it is customary to import NumPy as `np`.


```python
import numpy as np
```

One easy way to create a numpy array is from a Python list. The two are similar in a number of manners but NumPy is optimized in a number of ways for performing mathematical operations, including having a number of built-in methods that will be extraordinarily useful.


```python
x = np.array([1, 2, 3])
print(type(x))
```

    <class 'numpy.ndarray'>


## Broadcasting Mathematical Operations

Notice right off the bat how basic mathematical operations will be applied elementwise in a NumPy array versus a literal interpretation with a Python list:


```python
# Multiplies each element by 3
x * 3 
```




    array([3, 6, 9])




```python
# Returns the list 3 times
[1, 2, 3] * 3 
```




    [1, 2, 3, 1, 2, 3, 1, 2, 3]




```python
# Adds two to each element
x + 2 
```




    array([3, 4, 5])




```python
# Returns an error; different data types
[1, 2, 3] + 2 
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-6-b2ec0299a1e2> in <module>
          1 # Returns an error; different data types
    ----> 2 [1, 2, 3] + 2
    

    TypeError: can only concatenate list (not "int") to list


## Even more math!

### Scalar Math

|   |   |
|---|---|
|`np.add(arr,1)` | Add 1 to each array element  |
|`np.subtract(arr,2)`  | Subtract 2 from each array element  |
|`np.multiply(arr,3)`  | Multiply each array element by 3 |
|`np.divide(arr,4)`    | Divide each array element by 4 (returns `np.nan` for division by zero) |
|`np.power(arr,5)`     | Raise each array element to the 5th power | 




### Vector Math

|   |   |
|---|---|
|`np.add(arr1,arr2)` | Elementwise add arr2 to arr1  |
|`np.subtract(arr1,arr2)`  | Elementwise subtract arr2 from arr1  |
|`np.multiply(arr1,arr2)`  | Elementwise multiply arr1 by arr2 |
|`np.divide(arr1,arr2)`    | Elementwise divide arr1 by arr2 |
|`np.power(arr1,arr2)`     | Elementwise raise arr1 raised to the power of arr2 | 
|`np.array_equal(arr1,arr2)`| Returns True if the arrays have the same elements and shape |
|`np.sqrt(arr)`            |  Square root of each element in the array                    |
|`np.sin(arr)`             |  Sine of each element in the array                           |
|`np.log(arr)`             |  Natural log of each element in the array                    |
|`np.abs(arr)`             |  Absolute value of each element in the array                 |
|`np.ceil(arr)`            |  Rounds up to the nearest int                                |
|`np.floor(arr)`           |  Rounds down to the nearest int                              |
|`np.round(arr)`           |  Rounds to the nearest int                                   |

### Here's a few more examples from the list above


```python
# Adding raw lists is just appending
[1, 2, 3] + [4, 5, 6] 
```




    [1, 2, 3, 4, 5, 6]




```python
# Adds elements
np.array([1, 2, 3]) + np.array([4, 5, 6]) 
```




    array([5, 7, 9])




```python
# Same as above with built-in method
x = np.array([1, 2, 3])
y = np.array([4, 5, 6])
np.add(x, y)
```




    array([5, 7, 9])



## Multidimensional Arrays
NumPy arrays are also very useful for storing multidimensional data such as matrices. Notice how NumPy tries to nicely align the elements.


```python
# An ordinary nested list
y = [[1, 2], [3, 4]]
print(type(y))
y
```

    <class 'list'>





    [[1, 2], [3, 4]]




```python
# Reformatted as a NumPy array
y = np.array([[1, 2], [3, 4]])
print(type(y))
y
```

    <class 'numpy.ndarray'>





    array([[1, 2],
           [3, 4]])



## The Shape Attribute
One of the most important attributes to understand with this is the shape of a NumPy array.


```python
y.shape
```




    (2, 2)




```python
y = np.array([[1, 2, 3],[4, 5, 6]])
print(y.shape)
y
```

    (2, 3)





    array([[1, 2, 3],
           [4, 5, 6]])




```python
y = np.array([[1, 2],[3, 4],[5, 6]])
print(y.shape)
y
```

    (3, 2)





    array([[1, 2],
           [3, 4],
           [5, 6]])



### We can also have higher dimensional data such as working with 3 dimensional data
<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/Image_195_3D array.png" width=500>


```python
y = np.array([[[1, 2],[3, 4],[5, 6]],
             [[1, 2],[3, 4],[5, 6]]
             ])
print(y.shape)
y
```

    (2, 3, 2)





    array([[[1, 2],
            [3, 4],
            [5, 6]],
    
           [[1, 2],
            [3, 4],
            [5, 6]]])



## Built-in Methods for Creating Arrays
NumPy also has several built-in methods for creating arrays that are useful in practice. These methods are particularly useful:
* `np.zeros(shape)` 
* `np.ones(shape)`
* `np.full(shape, fill)`


```python
# One dimensional; 5 elements
np.zeros(5)  
```




    array([0., 0., 0., 0., 0.])




```python
# Two dimensional; 2x2 matrix
np.zeros([2, 2]) 
```




    array([[0., 0.],
           [0., 0.]])




```python
# 2 dimensional;  3x5 matrix
np.zeros([3, 5]) 
```




    array([[0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.]])




```python
# 3 dimensional; 3 4x5 matrices
np.zeros([3, 4, 5]) 
```




    array([[[0., 0., 0., 0., 0.],
            [0., 0., 0., 0., 0.],
            [0., 0., 0., 0., 0.],
            [0., 0., 0., 0., 0.]],
    
           [[0., 0., 0., 0., 0.],
            [0., 0., 0., 0., 0.],
            [0., 0., 0., 0., 0.],
            [0., 0., 0., 0., 0.]],
    
           [[0., 0., 0., 0., 0.],
            [0., 0., 0., 0., 0.],
            [0., 0., 0., 0., 0.],
            [0., 0., 0., 0., 0.]]])



### Similarly the `np.ones()` method returns an array of ones


```python
np.ones(5)
```




    array([1., 1., 1., 1., 1.])




```python
np.ones([3, 4])
```




    array([[1., 1., 1., 1.],
           [1., 1., 1., 1.],
           [1., 1., 1., 1.]])



### The `np.full()` method allows you to create an array of arbitrary values


```python
# Create a 1d array with 5 elements, all of which are 3
np.full(5, 3) 
```




    array([3, 3, 3, 3, 3])




```python
# Create a 1d array with 5 elements, filling them with the values 0 to 4
np.full(5, range(5)) 
```




    array([0, 1, 2, 3, 4])




```python
# Sadly this trick won't work for multidimensional arrays
np.full([2, 5], range(10))
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-24-ea647ac42aad> in <module>
          1 # Sadly this trick won't work for multidimensional arrays
    ----> 2 np.full([2, 5], range(10))
    

    //anaconda3/lib/python3.7/site-packages/numpy/core/numeric.py in full(shape, fill_value, dtype, order)
        334         dtype = array(fill_value).dtype
        335     a = empty(shape, dtype, order)
    --> 336     multiarray.copyto(a, fill_value, casting='unsafe')
        337     return a
        338 


    ValueError: could not broadcast input array from shape (10) into shape (2,5)



```python
# NumPy also has useful built-in mathematical numbers
np.full([2, 5], np.pi) 
```




    array([[3.14159265, 3.14159265, 3.14159265, 3.14159265, 3.14159265],
           [3.14159265, 3.14159265, 3.14159265, 3.14159265, 3.14159265]])



## Numpy array subsetting

You can subset NumPy arrays very similarly to list slicing in python.


```python
x = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]])
print(x.shape)
x
```

    (4, 3)





    array([[ 1,  2,  3],
           [ 4,  5,  6],
           [ 7,  8,  9],
           [10, 11, 12]])




```python
# Retrieving the first row
x[0] 
```




    array([1, 2, 3])




```python
# Retrieving all rows after the first row
x[1:] 
```




    array([[ 4,  5,  6],
           [ 7,  8,  9],
           [10, 11, 12]])



### This becomes particularly useful in multidimensional arrays when we can slice on multiple dimensions


```python
# All rows, column 0
x[:,0] 
```




    array([ 1,  4,  7, 10])




```python
# Rows 2 through 4, columns 1 through 3
x[2:4,1:3] 
```




    array([[ 8,  9],
           [11, 12]])



### Notice that you can't slice in multiple dimensions naturally with built-in lists


```python
x = [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]
x
```




    [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]




```python
x[0]
```




    [1, 2, 3]




```python
x[:,0]
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-33-879a04ce8a40> in <module>
    ----> 1 x[:,0]
    

    TypeError: list indices must be integers or slices, not tuple



```python
# To slice along a second dimension with lists we must verbosely use a list comprehension
[i[0] for i in x]
```




    [1, 4, 7, 10]




```python
# Doing this in multiple dimensions with lists
[i[1:3] for i in x[2:4]]
```




    [[8, 9], [11, 12]]



### 3D Slicing


```python
# With an array
x = np.array([
              [[1,2,3], [4,5,6]],
              [[7,8,9], [10,11,12]]
             ])
x
```




    array([[[ 1,  2,  3],
            [ 4,  5,  6]],
    
           [[ 7,  8,  9],
            [10, 11, 12]]])




```python
x.shape
```




    (2, 2, 3)




```python
x[:,:,-1]
```




    array([[ 3,  6],
           [ 9, 12]])



## Summary

Great! You learned about a bunch of NumPy commands. Now, let's move over to the lab to put your new skills into practice!

# [Measures of Central Tendency](https://colab.research.google.com/gist/bpurdy-ds/ce22cb9200ecfcf54c20d3deea527a98/index.ipynb)

## Introduction

When we are working with a small set of data values, it is often possible to discuss these values individually. However, when we are dealing or working with large sets of data in real-world problems, we prefer to have some features that can summarize and represent the data in a concise format.

In this lesson, we will look at such measures first for a single data variable. e.g., the salary of workers in a particular factory. These measures will include measures of central tendency and measures of dispersion.


## Objectives

You will be able to:

* Compare the different measures of central tendency

## Background

The term *Central Tendency* or a *Measure of Central Tendency* is the **typical** or **central** value for a data distribution. It is also commonly known as just the *Center* of the distribution. If you weren't becoming a Data Scientist, you might just call it the "average", but it turns out that there are different types of "averages" that work better for answering different sorts of problems.

There are three main measures of central tendency: the mean, the median, and the mode. Each of these measures describes a different way of indicating the typical or central value in the data as we will see below. 


## Mean

The **Mean** or **Arithmetic Average** is the value obtained by dividing the sum of all the data by the total number of data points as shown in the formula below:

$$ 
\Large\bar X = \dfrac{\sum X}{N} $$

> Yes, we're using the dreaded "mathematical notation". It's OK. It's just a concise way to write things down. It's one of the reasons (along with long, confusing model names like "Recurrent Neural Networks") that Data Scientists make so much money. The math and long words scare people away from ideas that are actually pretty straightforward!

So if you're a math whiz, great. If not, take a little time to look at and unpack the formulas we show in this course. Over time it'll become second nature and that's going to be really important as a practicing Data Scientist.

Let's start with the $\bar{x}$ (x-bar) - the bar over the top just means "mean of the sample".   

The mean value, shown as $\bar{x}$ (x-bar) for a vector $X$ is achieved by adding together all values of $X$ (shown as $\sum{X}$),  and dividing $N$ (number of observations).
e.g. Let’s look at a very simple set of data representing the retirement age of 11 individuals
```
54, 54, 54, 55, 56, 57, 57, 58, 58, 60, 60
```

The mean value is calculated as: 
1.  Adding together all the values 
```
54+54+54+55+56+57+57+58+58+60+60 = 623 
```
2. Dividing by the numbers of observations
```
623/11 = 56.6
```

For most people, the "mean" is what they think of as the "average". If I got paid \\$20k and you got paid \\$40k last year our "average" salary was \\$30k.

### Sample Mean vs. Population Mean

Think back to the retirement age example above. The data set only included information about 11 individuals. There are certainly more than 11 people who retired out there but, for whatever reason, their data are not available. In mathematical terms, you would say the 11 individuals are a **sample** of the entire **population** of people who retired.  

As a Data Scientist, you will often run into situations where you do not have access to data on the entire population of people you might be interested in. Instead you will only have access to a smaller sample from the entire population. It will be your job to estimate features of the population based on the sample. As you might imagine, as the sample size increases (in other words: a larger fraction of the population is sampled), it approximates the population more accurately. 

The difference between sample and population does not impact the way you calculate mean - you still divide the sum of all values by the total number of values - but it is important to distinguish between a sample mean and population mean. This is why there are different mathematical symbols to represent them. The sample mean is represented by the $\bar{x}$ described above. The population mean is represented by the Greek letter, $\mu$ (mu, pronounced "mew"). The distinction between sample and population metrics will pop up every now and then throughout the course so keep this in the back of your head.   

## Median

The median is another measure of central tendency. It refers to the data situated at exactly the middle location of the distribution.

In a set with an odd number of data points, the median is the middle value. So the median of 2, 4, 12 is 4. In our retirement data above, as we have 11 values, we can pick the 6th value (57) to be our median.

If the number of data points is even then the median is the average (mean) of the two middle items. Let's look at this dataset for the average weight of 10 individuals:
```
55, 56, 56, 58, 60, 61, 63, 64, 70, 78
```

So here, for the even number of observations (i.e. 10), the median would be calculated as:
```
Median = (60 + 61)/2 = 60.5
```

Why might we want to use the median instead of the mean? Well, imagine there are 10 people sitting in a bar. All of them make \\$50k a year. A hedge fund manager comes in who makes \\$20m a year. The "average" (mean) salary of people in the bar is now just over \\$1.86m a year! It is true, but it might be misleading if you relied on that data to ask any of the first 10 people to loan you \\$500k!

So median is particularly useful for datasets where there are a number of significant outliers (like the hedge fund manager's salary) and you want to get a sense of a "representative" measure of centrality. If we looked at the median salary in the bar, it'd still be \\$50k even with the hedge fund manager. It'd be a little misleading for that one person but would give you a better sense of the kind of salary that most people in the bar made.

## Mode

The Mode refers to the data value that occurs most frequently in a given dataset. Hence, it uses the frequency (repetition) of a certain value to be a representative of the central tendency of data. 

For our retirement data above, we can see that the value 54 appears most frequently (i.e. 3 times). So the mode value for retirement age, based on our data, would be 54 years. Similarly, for the weight data, the value 56 appears more frequently than the rest and hence would be considered a mode for this data.  

If two (or more) values occur with the same frequency in a dataset, both (or all) of the items are considered the mode of the data and the data set is **multimodal**. (Multimodality and its impact on data analysis will be discussed later in the course.)

The mode is particularly useful for categorical data (data grouped into categories) and is often used for filling in missing data in a messy data set. However, it's important to look at a plot of the distribution of data before using the mode to represent centrality as sometimes the most popular category will not be centrally positioned.

## Histograms and Central Tendency

Histograms are a type of plot used to show the distribution of a single variable. The x-axis shows bins of values present in the dataset, and the y-axis shows a count of the number of cases falling into each bin.

They can be used as an additional aid to help decide between different measures of central tendency.

For the sample data above, let's draw a histogram for retirement ages.


```python
import matplotlib.pyplot as plt
x = [54, 54, 54, 55, 56, 57, 57, 58, 58, 60, 60]
bins = 5
plt.hist(x, bins=bins, edgecolor="black", color="#00C8AD")
plt.title("Retirement Ages");
```


    
![png](index_files/index_1_0.png)
    


Here we can see that the mean value, i.e. 56.6 does not fully reflect the typical behavior of this particular data if we wanted to use this as a representative figure for retirement age. The median i.e. 57 also fails to represent the general tendency found in this dataset. The mode, i.e. 54 shows the most commonly occurring value which could be used as a representative value. Such decisions, however, are subjective and may differ based on the analytical question asked. For this example, the average or median may still be used to reflect the overall range of values present in the dataset. 

> In a histogram, you can always visually locate the bin where most of the values occur (as peaks). That's the concept that a measure of central tendency attempts to represent as a number.

Try putting in the values for the weight dataset and see what you think of the histogram. Also, try changing the bin size and see if it helps you better understand the distribution of underlying data. 


```python
# Use this cell to explore the weight dataset from previous lessons,
# or a set of values of your choice
x = []
bins = 5

plt.hist(x, bins=bins, edgecolor="black", color="#00C8AD")
plt.title("Weights");
```

## Histogram Shape and Measures of Central Tendency

### Symmetrical Distributions

For symmetric distributions, the mode, median, and mean are all in the middle of the distribution. The following histogram shows a larger retirement age dataset with a distribution which is symmetrical. All central measures in this case are equal to 58 years.

<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/image_sym.png" width="450">

### Skewed Distributions

A non-symmetrical distribution is called a "skewed distribution". For skewed distribution, the mode and median remain unchanged, but the mean generally moves in the direction of the tails. For such distributions, the median is often a preferred measure of central tendency, as the mean does not clearly reflect the central tendency. Based on the direction of mean's movement, such distributions can be further categorized as positively or negatively skewed distributions as shown below:

<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/image_pos.png" width="450">

<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/image_neg.png" width="450">

While performing analytical tasks, skewed distributions need special treatment at times. We will look deeper into this later during the course. 

### Outliers and Measures of Central Tendency

Outliers are extreme or unusual data values that are notably different from the rest of the data. It is important to detect outliers within a distribution, because they can alter the results of the data analysis. The mean is more sensitive to the existence of outliers than the median or mode. 

Let's look again at our retirement dataset, but with one difference; the last observation of 60 years has been replaced with a retirement age of 81 years. 

```
54, 54, 54, 55, 56, 57, 57, 58, 58, 60, **81**
```

The new value is unusual as it is much higher than the other values, and hence considered an *outlier*. 

As all values are included in the calculation of the mean, the outlier will influence the mean value. 

```
54+54+54+55+56+57+57+58+58+60+81 = 644 divided by 11 = 58.5 years
```
So we see that in this distribution the mean has increased due to the outlier. However, it has not changed the middle of the distribution, and therefore the median value is still 57 years. 

Despite the existence of outliers in a distribution, the mean can still be an appropriate measure of central tendency, especially if the rest of the data is normally distributed. If the outlier is confirmed as a valid extreme value, it should be treated accordingly. 

## Summary

In this lesson, we looked at three measures that can be used to identify the central tendency of a given dataset, the mean, the mode, and the median. These measures will be used throughout our data analysis journey and, with practice, we will learn to see how we can choose one (or more) of these measures to represent different datasets with different characteristics.

# [Measures of Dispersion](https://colab.research.google.com/gist/bpurdy-ds/77fc0de471e8faaf99fd6788cc7db30f/index.ipynb)

## Introduction

Previously, you learned about three measures of central tendency: the mean, median, and mode. These metrics can give you a general understanding of where data values lie within the range of the whole dataset but they don't tell you the whole story. In fact, they can often be misleading!

To truly understand your data, you also need **Measures of Dispersion**, namely: absolute deviation, standard deviation, and variance. These measures tell you how tightly (or loosely) your data is clustered around its center. Generally, measures of dispersion report on how "noisy" your dataset is. 

In this lesson, you'll learn about the different measures of dispersion and explore how they are related to each other as well as other summary statistics.
 
## Objectives
You will be able to:

* Compare the different measures of dispersion
* Create a box plot and use it to interpret the spread of data


## Absolute Deviation

**Absolute Deviation** is the simplest way of calculating the dispersion of a data set. It is calculated by taking a value from the dataset and subtracting the mean of the dataset. This helps to identify the "distance" between a given value and the mean. In other words, how much a value *deviates* from the mean.  

> $\left|x_i - \bar{x}\right|$

Here $x_i$ denotes an element from $[x_1, x_2, .., x_n]$ , where $n$ is the total number of data points in the dataset. Recall, the symbol $\bar{x}$ (pronounced "x-bar") represents the sample mean. The vertical bars are used to denote absolute value so all absolute deviation values are positive. This is important because when measuring deviation, you just want to focus on how big the difference is, not its sign.

If that sounded a little confusing, consider this example: Say the mean test score for a group of 100 students is 58.75 out of 100. If a particular student scored 60 out of 100, the absolute deviation of that score from the mean is:

> $ \left|60 - 58.75\right| = 1.25 $ 

**Average Absolute Deviation** is calculated by taking the mean of all individual absolute deviations in a data set as shown in the formula below:

$$\large \dfrac{1}{n}\sum^n_{i=1}\left|(x_i-\bar x)\right| $$

The advantage here is that the average absolute deviation yields one number to describe dispersion. To illustrate this, consider this example: In a group of four people, two people earn 50K USD a year and two earn 60K USD a year. The mean of the data set is 55K USD. The absolute deviations are:

> $ \left|50 - 55\right| = 5 $   
> $ \left|50 - 55\right| = 5 $   
> $ \left|60 - 55\right| = 5 $     
> $ \left|60 - 55\right| = 5 $     

The average absolute deviation is:

> $ \large \frac{5+5+5+5}{4} = 5 $

## Variance

A more complex measure of dispersion is **Variance**. Remember, measures of dispersion emphasize the magnitude of differences from the mean, not their sign. Unlike the absolute deviation, which uses the absolute value of the deviation to take care of negative values, the variance achieves positive values by *squaring* each of the deviations. Similar to what you saw with the average absolute deviation, the next step in calculating variance is to add up the squared deviations (the **sum of squares**), then divide by the total number of values in your dataset. 

OK, that was a mouthful but you can break it down mathematically as follows:

$$ \large \sigma^2 = \dfrac{1}{n}\displaystyle\sum^n_{i=1}(x_i-\mu)^2 $$

> Recall the distinction between the sample mean ($\bar{x}$) and the population mean ($\mu$) - namely, that a sample mean is calculated using a subset of the population whereas the population mean is calculated using the entire population. You'll see here that the population mean is used. This is because unlike the mean, the variance formula changes slightly depending on whether you are working with data from a sample or data from the entire population. Don't worry if this is a little confusing now, the details will be discussed later. 

Say you want to calculate the variance of our salary data above. The first step is to calculate all of the differences from the mean:

> $ 50 - 55 = -5 $   
> $ 50 - 55 = -5 $   
> $ 60 - 55 = 5 $     
> $ 60 - 55 = 5 $  

*Note: no absolute values, the signs are kept*

Next, square the differences:

> $ (-5)^2 = 25 $   
> $ (-5)^2 = 25 $   
> $ 5^2 = 25 $     
> $ 5^2 = 25 $

Finally, add them up and divide by the total number of data points:

> $ \large \frac{25+25+25+25}{4} = 25 $

As a measure of dispersion, the variance is very useful. If the values in the data set are spread out about their mean, the variance will be a large number. On the other hand, if the values are clustered closely around their mean, the variance will be a much smaller number. 

There are, however, two potential problems with the variance. First, because the deviations of values from the mean are squared, this gives more weight to extreme values. Outliers, which differ substantially more from the mean than the rest of the data in a data set, will impact the variance. Secondly, the variance is not in the same *units* as the individual values in a data set. Variance is measured in the *units squared*. This means we cannot directly relate a variance value to the values in our data set. If this isn't clear, go back to the salary example above. The salaries are measured in USD but the variance is measured in *USD squared* which is not the same thing.

Fortunately, calculating the standard deviation rather than the variance fixes this problem. 

## Standard Deviation

The **Standard Deviation** is another measure of the spread of values within a dataset. 
It is simply the square root of the variance. In the above formula, $\sigma^2$ is the variance so $\sigma$ is the standard deviation. 

$$ \large \sigma = \sqrt{\dfrac{1}{n}\displaystyle\sum^n_{i=1}(x_i-\mu)^2} $$

So for the salary example above, you can calculate:

> $ \sigma = \sqrt{\sigma^2} = \sqrt{25} = 5 $

Now, the units are in USD again!

## Quantiles, Percentiles, and Quartiles

**Quantiles** are points in a distribution that relate to the *rank order* of values in that distribution. Rank ordering just means the data are sorted in ascending order. You can find any quantile by sorting the sample. The middle value of the sorted sample (middle quantile, 50th percentile) is known as the **median**. The **limits** are the **minimum** and **maximum** values. Any other locations between these points can be described in terms of **percentiles**.

Percentiles are descriptions of quantiles relative to 100. So the 80th percentile is 80% of the way up an ascending list of sorted values of data. For example, take a look at the image below: 80% of people in the data set are shorter than you so you are in the 80th percentile for height. 

<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/new_percent.png" width="600">


## InterQuartile Range - IQR
The **quartiles** of a dataset divide the data into **four** equal parts. Since there are four equal parts, there are 3 quartile positions that divide them. These are denoted by Q1, Q2, and Q3. The second quartile position, Q2, is the median of the dataset, which divides the dataset in half. Q1 divides the lower half and is known as the "lower quartile". Similarly, Q3 divides the upper half and is known as the "upper quartile". The image below illustrates how this looks:

<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/new_measuresofdispersion2.png" width="600">

The **InterQuartile Range (IQR)** is a measure of where the “middle fifty” is in a dataset which is given by $ Q3 - Q1 $. This is useful because it tells you where the bulk of the values lie. To relate these concepts back to percentiles, Q1 is the 25th percentile and Q3 is the 75th percentile. The IQR is calculated by subtracting the 25th percentile from the 75th percentile. 

In practice, there are actually several different methods for determining percentiles which are accepted and you may have encountered some of these methods before. For now, you can just focus on the method shown below which is what is used by default in the go-to statistical and mathematical Python packages that you will use throughout this course and your career like `numpy`.

### Calculating IQR for a Given Data Set

You will now get a feel for how IQR is calculated using the collection of numbers from the image above. First, put the numbers in a list.


```python
# List of numbers
x = [3, 5, 8, 12, 15, 18, 20, 22, 25, 30, 50, 80, 687]
```

**Step 1:** Sort the data in ascending order (these numbers are already sorted but don't skip this step when you do this on other data- it's important!).


```python
# Sort in ascending order
x = sorted(x)
```

**Step 2:** Calculate the distance between the last element and the first element.


```python
# Distance between last and first element
distance = len(x) - 1
```

**Step 3:** Multiply the distance by the desired percentiles, 25th and 75th, expressed as fractions. This will yield the indices of the elements that correspond to the 25th percentile and 75th percentile, respectively.


```python
# Multiply distance by percentiles

# Index of 25th percentile
index_p25 = 0.25*distance
index_p25
```




    3.0




```python
# Index of 75th percentile
index_p75 = 0.75*distance
index_p75
```




    9.0



**Step 4:** Using the indices calculated above, determine the 25th and 75th percentiles.


```python
# 25th Percentile
p25 = x[int(index_p25)]
p25
```




    12




```python
# 75th Percentile
p75 = x[int(index_p75)]
p75
```




    30



**Step 5:** Calculate the IQR by subtracting the 25th percentile from the 75th percentile.


```python
# IQR
iqr = p75 - p25
iqr
```




    18



In practice, you will probably never calculate the IQR by hand since `numpy` has a built-in method for calculating percentiles.  


```python
import numpy as np

np.percentile(x, 75) - np.percentile(x, 25)
```




    18.0



You might have noticed that the indices calculated above happened to be whole numbers. Whole numbers are great to work with here since they can be used as indices directly. The calculation becomes a little more complicated when the indices are fractional numbers. In this case, `numpy` will use a technique called "linear interpolation" to take the fractional components into account. This is beyond the scope of what you need to know but if you are curious about how it works you can check out the [documentation]("https://docs.scipy.org/doc/numpy/reference/generated/numpy.percentile.html"). 

## Visualizing Dispersion with Box Plots

As a Data Scientist, you will need to be able to present your analysis visually. Box plots are a commonly used visual representation of centrality and spread of data that is based on quartiles.

A general depiction of a box plot is shown below:

<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/new_boxplot.png" width="600">

An important feature of the box plot is the set of lines that radiate from the middle to the "minimum" and "maximum" values. These lines are commonly called **"whiskers."** You've probably noticed in the image above that the lines do not go to the true minimum and maximum values (confusing right?) but rather $ Q1 - 1.5*IQR $ and $ Q3 + 1.5*IQR $, respectively. Any values that fall outside this range are shown as individual data points. These values are considered outliers. 

> Note: You might have read about some alternative definitions for how to draw the whiskers. Though these alternative definitions may be acceptable in some contexts, the definition presented here is what Python uses so it's best to stick with that.

Matplotlib can be used to generate box plots given a collection of values. Consider the retirement age data again:


```python
import matplotlib.pyplot as plt
%matplotlib inline

plt.style.use('ggplot') # for viewing a grid on plot
x = [54, 54, 54, 55, 56, 57, 57, 58, 58, 60, 81]
plt.boxplot(x)
plt.title ("Retirement Age Box Plot")
plt.show()
```


    
![png](index_files/index_20_0.png)
    


In this box plot, you can see that it is very easy to visualize the central tendency of the data. The median is drawn as a blue line at 57. The IQR identifies the middle 50% of the data which is shown as the box. The whiskers (two horizontal lines) show the minimum (54) and maximum (60) values in our dataset that fall within $Q1-1.5*IQR$ and $Q3+1.5*IQR$, respectively. The point at 81 falls outside the range of the whiskers so it is shown as a data point and is considered an outlier.

The outlier data point squishes the visualization of the box. Sometimes, it is convenient to hide the outliers to get a better view of the box. You can pass the argument `showfliers=False` to hide the outliers:


```python
plt.boxplot(x, showfliers=False)
plt.title ("Retirement Age Box Plot - Without Outliers")
plt.show()
```


    
![png](index_files/index_22_0.png)
    


Use the ```showfliers``` option with caution. You don't want to ignore data! 


## Summary

In this lesson, you learned about some commonly used measures of dispersion. These measures identify the spread or deviation present in a dataset. You also looked at quantiles, percentiles, quartiles, and IQR as well as how to use those concepts to construct box plots for visualizing the distribution of data in a given dataset. You will revisit these topics continuously throughout the course and will see how these concepts are used toward effective data analysis. 


# [Covariance and Correlation](https://colab.research.google.com/gist/bpurdy-ds/cc1d87832f3cc32adcc0ec9b2a6a45d3/index.ipynb)

## Introduction

In this lesson, you'll learn how the **variance** of a variable is used to calculate **covariance** and **correlation** as key measures used in statistics to find causal relationships between variables. Based on these measures, you can find out if two variables are associated with each other, and to what extent. This lesson will help you develop a conceptual understanding, necessary calculations, and some precautions while using these measures.

## Objectives

You will be able to:

- Distinguish between correlation and causation
- Interpret correlation and its relationship to covariance  
- Calculate covariance and correlation  

## Variance

In an earlier lesson, you learned about __variance__ (represented by $\sigma^2$) as a measure of dispersion for continuous variables from its expected mean value. Let's quickly revisit this, as variance formula plays a key role while calculating covariance and correlation measures.

The formula for calculating variance as shown below:

$$\sigma^2 = \dfrac{1}{n}\displaystyle\sum_{i=1}^{n}(x_i-\mu)^2$$

- $x$ represents an individual data points
- $\mu $ is the mean of the data points
- $n$ is the total number of data points

**Example**: Let's consider the monthly ice cream sales for a small ice cream vendor in NYC (January-May):

| Month   |   Amount  |
|----------|-----|
|  January | 100 |
| February | 200 |
| March    | 300 |
| April    | 500 |
| May      | 900 |

You can calculate that, with a mean of 400 over these 5 months, the variance of the sales amounts is 80,000 (and the standard deviation is 282.84).

Now, let's take this further and see how this relates to **covariance**.

## Covariance

In some cases, you'll want to look at **two variables** to get an idea about how they **change together**. In statistics, when trying to figure out how two variables **vary together**, you can use the **covariance** between these variables.

Covariance calculation plays a major role in a number of advanced machine learning algorithms like dimensionality reduction, predictive analyses, etc.

### Calculating Covariance
If you have $X$ and $Y$, two variables having $n$ elements each. You can calculate covariance ($\sigma_{xy}$) between these two variables by using the formula:

$$\sigma_{XY} = \dfrac{1}{n}\displaystyle\sum_{i=1}^{n}(x_i -\mu_x)(y_i - \mu_y)$$

- $\sigma_{XY}$ = Covariance between $X$ and $Y$
- $x_i$ = ith element of variable $X$
- $y_i$ = ith element of variable $Y$
- $n$ = number of data points (__$n$ must be same for $X$ and $Y$__)
- $\mu_x$ = mean of the independent variable $X$
- $\mu_y$ = mean of the dependent variable $Y$


> You can see that the formula calculates the variance of $X$ and $Y$ by multiplying the variance of each of their corresponding elements. Hence the term **covariance**.


**Back to our ice cream sales example**:

Imagine there is another ice cream vendor, Vendor B. Let's calculate the covariance between our previous Vendor A and this new Vendor B.

Ice cream sales for a small ice cream vendor in NYC (January-May):

| Month   |   Vendor A  | Vendor B |
|----------|-----|-----|
|  January | 100 |220|
| February | 200 |400|
| March    | 300 |600|
| April    | 500 |900|
| May      | 900 |1300|

Recall that Vendor A sold on average 400, and Vendor B sells on average 684, considerably higher.

Using this along with the covariance formula, you can compute that the covariance between ice cream Vendor A and B sales is 106800. Now the question is, what does that mean?


### Interpreting Covariance Values

Covariance values range from positive infinity to negative infinity.

* A **positive covariance** indicates that two variables are **positively related**

* A **negative covariance** indicates that two variables are **inversely related**

* A **covariance equal or close to 0** indicates that there is **no linear relationship** between two variables


Looking back at our ice cream example, it is no surprise that you found a positive covariance there. While the sales amounts are different, it is clear that when sales went up for Vendor A, they also went up for Vendor B.

You'll immediately notice the main shortcoming of covariance: because it ranges between negative and positive infinity, it only tells us when two variables are inversely or positively related. It doesn't tell us anything about to what **extent** they are inversely or positively related. This makes interpretation difficult and comparing covariances to each other impossible.

Assume you have four different variables `a`, `b`, `p`, and `q`. Next, let's say you can have $ Cov(a, b)  = 3.6$ and $Cov(p, q) = 9$. These covariance values tell us that these pairs are positively associated, but it is difficult to tell whether the relationship between `a` and `b` is stronger than `p` and `q` without looking at the **means and distributions of these variables**.

This is where the concept of correlation comes in.

> Correlation is calculated by **standardizing covariance** by some measure of variability in the data. It produces a quantity that has intuitive interpretations and consistent scale.


Let's consider another ice cream Vendor C to reinforce this idea. The mean sales amount for this vendor is 1,120, and the covariance between Vendor A and C is 132,000, which is considerably higher than the covariance of 106,800 which we've seen before. Does this mean the positive relationship between A and C is stronger? We need the correlation here to answer this question!

| Month   |   Vendor A  | Vendor B | Vendor C |
|----------|-----|-----|-------|
|  January | 100 |220|900 |
| February | 200 |400|800 |
| March    | 300 |600|500 |
| April    | 500 |900|1400 |
| May      | 900 |1300|2000 |

## Correlation

Covariance uses a formulation that only depends on the units of $X$ and $Y$ variables. When doing data science, it is often not appropriate to use covariance as such because different experiments may contain underlying data measured in different units.

Because of this, it is important to normalize this degree of variation into a standard unit, with interpretable results, *independent of the units of data*. You can achieve this with a derived normalized measure, called **correlation**.

The term "correlation" refers to a relationship or association between variables. In almost any business, it is useful to express one quantity in terms of its relationship with others. For example:
- Sales might increase when the marketing department spends more on TV advertisements
- Customer's average purchase amount on an e-commerce website might depend on a number of factors related to that customer, e.g. location, age group, gender etc.
- Social media activity and website clicks might be associated with revenue that a digital publisher makes. etc.

Correlation is the first step to understanding these relationships and subsequently building better business and statistical models.


### Pearson's Correlation Coefficient ( $r$ )

__Pearson Correlation Coefficient__, $r$, also called the __linear correlation coefficient__, measures the strength and the direction of a __linear relationship__ between two variables. This coefficient quantifies the degree to which a relationship between two variables can be described by a line.

**Note:** There are a [number other correlation coefficients](https://math.tutorvista.com/statistics/correlation.html),  but for now, we will focus on __Pearson correlation__ as it is the go-to correlation measure for most needs. If someone says "correlation" without further clarification, you can assume that they mean Pearson correlation.




### Calculating Correlation Coefficient

Pearson Correlation ($r$) is calculated using following formula :

$$ r = \frac{\sum_{i=1}^{n}(x_i -\mu_x)(y_i - \mu_y)} {\sqrt{\sum_{i=1}^{n}(x_i - \mu_x)^2 \sum_{i=1}^{n}(y_i-\mu_y)^2}}$$

So just like in the case of covariance,  $X$ and $Y$ are two variables having $n$ elements each.


- $x_i$ = ith element of variable $X$
- $y_i$ = ith element of variable $Y$
- $n$ = number of data points (__$n$ must be same for $X$ and $Y$__)
- $\mu_x$ = mean of the independent variable $X$
- $\mu_y$ = mean of the dependent variable $Y$
- $r$ = Calculated Pearson Correlation

### Interpreting Correlation Values

> _The Pearson Correlation formula always gives values in a range between -1 and 1_

You'll often see patterns or relationships in scatter plots. Pearson correlation, which is a linear measure can be identified through a scatter plot by inspecting the "linearity of association" between two variables.

If two variables have a correlation of +0.9,  this means the change in one item results in an almost similar change to another item. A correlation value of -0.9 means that the change is one variable results in an opposite change in the other variable. A Pearson correlation near 0 would be no effect.


Here are some example of Pearson correlation calculations as scatter plots.

<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/correlation.png/correlation.png" width="500">


** Let's go back to our ice cream example**:

| Month   |   Vendor A  | Vendor B | Vendor C |
|----------|-----|-----|-------|
|  January | 100 |220|900 |
| February | 200 |400|800 |
| March    | 300 |600|500 |
| April    | 500 |900|1400 |
| May      | 900 |1300|2000 |

Recall that $Cov(A, C)$ was higher than $Cov(A, B)$. Using the formula for correlation coefficient, vendors A and B have a correlation coefficient of 0.9888 whereas vendors A and C have a **lower** correlation coefficient of 0.8858!

**Ice cream and the weather:**

Let's take a deep dive into an ice cream vendor's sales data. Now, we're going to look at the relationship between the average daily temperature and the daily profit on 12 days in April (the degrees are on the Celsius scale):


| Temp (°C) |   Ice Cream Sales (USD) |
|--------|------|
|14.2|	215|
|16.4|	325|
|11.9|	185|
|15.2|	332|
|18.5|	406|
|22.1|	522|
|19.4|	412|
|25.1|	614|
|23.4|	544|
|18.1|	421|
|22.6|	445|
|17.2|	408|

And here is the same data as a scatter plot:

<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/ice.png/ice.png" width="450">

Just by looking at the plot, you can easily see that hotter weather goes along with higher ice cream sales. The relationship is good but not perfect.
The correlation for this example is 0.9575 which indicates a very strong positive relationship.

## Correlation Is Not Causation

You may have come across the saying: **“correlation is not causation”** or **“correlation does not imply causation”**.

What do we mean by this?

Causation takes correlation a step further.

> Causation is when any change in the value of one variable leads to a change in the value of another variable, which means one variable _causes_ the change in another. This is also referred to as __cause and effect__.

Let's try to understand this with an example.

### Consider Hidden Factors

Suppose for the above ice cream sales example, we now have some extra data on the number of homicide cases in New York. Out of curiosity,  we analyze sales numbers vs. homicide rate as scatter plot and see that these two are also related to each other. Mind blown... Is ice cream turning people into murderers?

<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/ice_murder.png/ice_murder.png" width="450">

#### Example 1: Ice cream sales are correlated with the number of homicides in New York

For our example, it's actually the weather as a hidden factor that is causing both these events. It is actually causing the rise in ice cream sales and homicides. As in summer people usually go out, enjoy a nice sunny day and chill themselves with ice creams. So when it’s sunny, a wide range of people are outside and there is a wider selection of victims for predators. There is no causal relationship between the ice cream and rate of homicide, sunny weather is bringing both the factors together. We can say that ice cream sales and homicide rate have a __causal relationship__ with weather.

This is reflected in the image below:

<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/hidden_factor.png/hidden_factor.png" width="800">

**Just after finding the correlation, we shouldn't draw the conclusion too quickly. Instead, we should take time to find other underlying factors as correlation is just the first step. Find the hidden factors, verify if they are correct and then conclude.**


Here are some other (rather funny) examples of how correlation analysis may lead to inconceivable findings.


#### Example 2: Number of Nicholas Cage movie releases correlates with people drowning in pools


<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/cage.png/cage.png" width="900">

So, how about this chart?

The internet is full of other funny and weird correlations. You'll come across other ones if you do a quick Google search. This particular correlation between Nicolas Cage movies and drowning accidents was found on [this website](http://www.tylervigen.com/spurious-correlations). The key takeaway here is that covariance and correlation analysis should be used with care. The thing is that nowadays, you can find data on a wide variety of subjects. This means that if you search long enough, you'll find a high correlation somewhere between two completely unrelated subjects. This phenomenon is also referred to as "the law of large numbers".

#### Example 3: Our very own ice cream example

Our very own ice cream example in this lesson is a good example of why correlation does not automatically imply causation.

The sales increase for Vendor A did not _cause_ a sales increase for vendor B. The hidden factor here was (clearly) the weather.

What is important to note is here that, although correlation does not imply causation, *IF* there is a causal effect, there generally will be a high correlation as well. In other words:

> If one factor has an effect on another one (causation), there generally will be a high correlation as well.
   Yet, this doesn't mean that a high correlation means that there is causation.


## Key Takeaways
- Covariance is dimensionless, i.e. it is a unit-free measure of the relationship between variables    
- Correlation is a normalized form of covariance and ranges between [-1,1]    
- **Correlation is not causation**


**IMPORTANT NOTE:** The variance formula used in this lesson considers $X$ and $Y$ to be population variables.  For samples, we divide by $n-1$, instead of $n$ due to the principle called Bessel's correction. [Here is a mathematical proof for this](https://lazyprogrammer.me/covariance-matrix-divide-by-n-or-n-1/). We will visit this point again later in the course to explore it in greater detail.


## Summary
In this lesson, you reviewed how to compute the variance of variables as a measure of deviation from the mean. Next, you learned how this measure can be used to first calculate covariance, and the correlation to analyze how two variables change together. You learned the formulas for calculating these measures and how they can be applied to real-world situations.


