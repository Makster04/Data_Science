# [Customizing Visualizations with Matplotlib - Lab](https://colab.research.google.com/gist/bpurdy-ds/979c85ea513dc6a70a3005a03f1cc2a8/index.ipynb)

## Introduction

This lab requires you to draw some basic visualizations using the techniques from the previous lesson.

## Objectives

You will be able to:

* Create subplots using a Matplotlib figure
* Use different linestyles within a Matplotlib visualization
* Create labels and titles for visualizations
* Create a lineplot using linspace

Let's give you a head start by generating some data for you to plot:
________________________________________
```python
# Run this cell without changes
import numpy as np

# Generate a list of numbers from 0 to 99
x_values = np.arange(0,100)

# Multiply values of x_values with 2 to get y_values
y_values = x_values*2

# Calculate square of values in for variable z_values
z_values = x_values**2

# Print x_values, y_values and z_values
print (x_values, y_values, z_values)
```
```
[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23
 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47
 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71
 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95
 96 97 98 99] [  0   2   4   6   8  10  12  14  16  18  20  22  24  26  28  30  32  34
  36  38  40  42  44  46  48  50  52  54  56  58  60  62  64  66  68  70
  72  74  76  78  80  82  84  86  88  90  92  94  96  98 100 102 104 106
 108 110 112 114 116 118 120 122 124 126 128 130 132 134 136 138 140 142
 144 146 148 150 152 154 156 158 160 162 164 166 168 170 172 174 176 178
 180 182 184 186 188 190 192 194 196 198] [   0    1    4    9   16   25   36   49   64   81  100  121  144  169
  196  225  256  289  324  361  400  441  484  529  576  625  676  729
  784  841  900  961 1024 1089 1156 1225 1296 1369 1444 1521 1600 1681
 1764 1849 1936 2025 2116 2209 2304 2401 2500 2601 2704 2809 2916 3025
 3136 3249 3364 3481 3600 3721 3844 3969 4096 4225 4356 4489 4624 4761
 4900 5041 5184 5329 5476 5625 5776 5929 6084 6241 6400 6561 6724 6889
 7056 7225 7396 7569 7744 7921 8100 8281 8464 8649 8836 9025 9216 9409
 9604 9801]
```
________________________________________
Import ``matplotlib.pyplot`` as plt and set ``%matplotlib`` inline for generating inline images in Jupyter notebooks.
________________________________________

```python
# Import pyplot for plotting
import matplotlib.pyplot as plt
# Import numpy to generate some dummy data
import numpy as np
%matplotlib inline
```

________________________________________
Now that we have our data all set and Matplotlib in our Python environment, we can try some basic plotting techniques.

## Exercise 1

Perform the following steps in the cell below:

* Create a new figure object `fig` using `.figure()` function.
* Use `add_axes()` to add an axis `ax` to the canvas at absolute location [0,0,1,1].
* Plot (x,y) on that axes and set the labels and title.

The graph you create should look like this:

![line plot](https://curriculum-content.s3.amazonaws.com/data-science/images/line_plot.png)

________________________________________
### Code
```python
# Sample data for the plot
x = [0, 20, 40, 60, 80, 100]
y = [0, 40, 80, 120, 160, 200]

# Create a new figure object
fig = plt.figure()

# Add an axis at location [0, 0, 1, 1]
ax = fig.add_axes([0, 0, 1, 1])

# Plot (x, y) on the axis
ax.plot(x, y)

# Set labels and title
ax.set_xlabel('x-axis label')
ax.set_ylabel('y-axis labal')
ax.set_title('Plot Title')

# Show the plot
plt.show()
```
![image](https://github.com/user-attachments/assets/8563e70e-708e-4599-90ad-db619aca72bf)

________________________________________
This was easy, let's move on to drawing multiple plots within a figure space.

## Exercise 2

Perform following actions:

* Create a subplots figure with 3 rows and 4 columns and a `figsize` of 15 by 15
* Plot the lines $y=x$, $y=2x$, $y=3x$, $y=4x$,...$y=10x$, $y=11x$, $y=12x$ in the respective subplots. So, $y=x$ in the 0th row, 0th column, $y=2x$ in the 0th row, 1th column, etc.
* Use the variable `x` that we have already created for you as $x$, then calculate your own $y$. Call this $y$ `y_new` (within a for loop).

The graph you create should look like this:

![subplots showing 1x through 12x](https://curriculum-content.s3.amazonaws.com/data-science/images/subplots_1x_12x.png)
________________________________________
### Code
```python
fig, axes = plt.subplots(nrows=3, ncols=4, figsize=(15, 15)) 
fig.suptitle('Graphs of y = nx', fontsize=16)
fig.tight_layout(pad=3.0)
x = np.linspace(0, 100)

# Loop over n from 1 to 12
for n in range(1, 13):
    # Calculate the row and column indices for the subplot
    row = (n - 1) // 4  # Integer division to get the row index
    col = (n - 1) % 4   # Modulus to get the column index

    ax = axes[row][col]  # Get the appropriate axes

    # Calculate y for the current n
    y_new = n * x
    
    # Plot y vs. x
    ax.plot(x, y_new, label=f'y = {n}x')
    ax.set_title(f'{n}*x')
    
# Adjust layout to prevent overlap
plt.show()
```
![image](https://github.com/user-attachments/assets/dd7ebd42-65c7-402d-8af0-966022f940b9)

________________________________________
## Exercise 3

As you might have noticed, the y-axis of those graphs automatically adjusted based on the value of `y_new`. This creates the appearance of all of the lines having the same slope, even though they actually have quite different slopes.

Repeat the above exercise, but standardize the axes of all of your subplots so that you can more easily compare the slopes of the lines. Because the final graph goes up to 1200, use this as the maximum for all plots.

The graph you create should look like this:

![subplots showing 1x through 12x with the same y-axis](https://curriculum-content.s3.amazonaws.com/data-science/images/subplots_1x_12x_normalized.png)
________________________________________
### Code
```python
fig, axes = plt.subplots(nrows=3, ncols=4, figsize=(15, 15)) 
fig.suptitle('Graphs of y = nx', fontsize=16)
fig.tight_layout(pad=3.0)
x = np.linspace(0, 100)


# Loop over n from 1 to 12
for n in range(1, 13):
    # Calculate the row and column indices for the subplot
    row = (n - 1) // 4  # Integer division to get the row index
    col = (n - 1) % 4   # Modulus to get the column index
    
    ax = axes[row][col]  # Get the appropriate axes

    # Calculate y for the current n
    y_new = n * x
    
    # Plot y vs. x
    ax.plot(x, y_new, label=f'y = {n}x')
    ax.set_title(f'{n}*x')
    ax.set_ylim(0, 1200)
    

# Adjust layout to prevent overlap
plt.show()
```
![image](https://github.com/user-attachments/assets/e7d3b451-72b1-43a2-8846-a5e7eb0a44aa)

________________________________________
## Exercise 4

Perform the following steps in the cell below:

* Using `plt.subplots`, create a figure of size 8 by 6 with 2 columns, and "unpack" the 2 created axes into variables `ax1` and `ax2`.
* Plot (`x`,`y`) and (`x`,`z`) on `ax1` and `ax2` respectively.
* Set the line width of first axes to 3, line style as dotted and color it red.
* Set the line width of second axes to 5, line style as dash-dot (-.) and color it blue.
* Give the plots some labels and titles

Hints:
* If `y` is looking "off" but your graph code seems correct, it's possible you overwrote the original values in a previous exercise. Go back to the top of the notebook and re-run the first cell that created `x`, `y`, and `z`.
* The label `variable - z` is intentionally overlapping the graph on the left. We will address that issue later in the lab.

The graph you create should look like this:

![two subplots](https://curriculum-content.s3.amazonaws.com/data-science/images/subplots_left_right.png)
 
________________________________________
### Code
```python
# Create the plot
fig, (ax1, ax2) = plt.subplots(figsize=(15,15), ncols=2)

# Set different limits of x and y axes for subplots
ax1.set_xlim(0, 100), ax1.set_ylim(0, 200)
ax2.set_xlim(0, 100), ax2.set_ylim(0, 10000)

# Plotting Subplot One
ax1.plot(x_values, y_values, color='red', linestyle = 'dotted', linewidth=3)

# Plotting Subplot Two
ax2.plot(x_values, z_values, color='blue', linestyle = '-.', linewidth=5)

# Add Ax1 Label
ax1.set_xlabel('x-axis label')
ax1.set_ylabel('y-axis labal')

# Add Ax2 Label
ax2.set_xlabel('x-axis label')
ax2.set_ylabel('z-axis label')

# Add Titles
ax1.set_title('Left Plot')
ax2.set_title('Right Plot')
```

![image](https://github.com/user-attachments/assets/dd6cd4e7-5620-43b8-a06e-c9edec89e3d9)
___________________________________
## Exercise 5

The above figure looks fine but a bit out of proportion. Let's resize this to make the plots look more appealing by ensuring that subplots are square in shape. Also change the line style of first plot (left) and change the type of 2nd plot (right) to a scatter plot with a `^` marker style.

The plot you create should look like this:

![two square subplots](https://curriculum-content.s3.amazonaws.com/data-science/images/subplots_left_right_square.png)
 
________________________________________
### Code
```python
# Create the plot
fig, (ax1, ax2) = plt.subplots(figsize=(10,4), ncols=2)

fig.subplots_adjust(wspace=0.5)  # Increase the value to increase the space


# Set different limits of x and y axes for subplots
ax1.set_xlim(0, 100), ax1.set_ylim(0, 200)
ax2.set_xlim(0, 100), ax2.set_ylim(0, 10000)

# Plotting Subplot One
ax1.plot(x_values, y_values, color='red', linestyle = '-', linewidth=1)

# Plotting Subplot Two
ax2.plot(x_values, z_values, color='blue', linestyle = 'dashdot', linewidth=1)

# Add Ax1 Label
ax1.set_xlabel('x-axis label')
ax1.set_ylabel('y-axis labal')

# Add Ax2 Label
ax2.set_xlabel('x-axis label')
ax2.set_ylabel('z-axis label')

# Add Titles
ax1.set_title('Left Plot')
ax2.set_title('Right Plot')
```
![image](https://github.com/user-attachments/assets/5a982502-a1ed-4cbf-b886-8e0af5f0dc69)


________________________________________
**Note:** Instead of changing the plot size as you did in Exercise 5, one other technique you could have used to help with overlapping plot labels is a "tight layout" (see [Matplotlib guide](https://matplotlib.org/tutorials/intermediate/tight_layout_guide.html)).

By default, Matplotlib doesn't consider the space taken by axes labels when it determines how to draw the plots. Turning on the tight layout setting tells Matplotlib to include the axes labels in this calculation, in order to avoid clipping or overlapping.

Here is a version of the Exercise 4 solution using a tight layout:
________________________________________
```python
# Run this cell without changes

new_figure, (ax1, ax2) = plt.subplots(figsize=(8,6), ncols=2)
# Telling Matplotlib to include axes labels when creating the layout
new_figure.set_tight_layout(True)

ax1.plot(x_values, y_values, color='red', linewidth=3, linestyle = ':')
ax2.plot(x_values, z_values, color='blue', linewidth=5, linestyle = '-.')

ax1.set_xlabel('variable - x')
ax1.set_ylabel('variable - y')
ax1.set_title ('Left Plot')

ax2.set_xlabel('variable - x')
ax2.set_ylabel('variable - z')
ax2.set_title ('Right Plot');
```
________________________________________
Compared to Exercise 4, we are now avoiding the label `variable - z` overlapping with the plot on the left, without changing the overall figure size like we did in Exercise 5.

Note that the above example uses the object-oriented interface, by calling the `.set_tight_layout` method on the figure object.

A tight layout can also be set using the PyPlot interface (state machine interface) introduced in the previous lesson. You will frequently see this in examples online, adding this line of code as the last line before the figure is displayed:

```python
plt.tight_layout()
```
________________________________________
Congratulations! You've practiced the basics of plotting, labeling, and customizing plots with Matplotlib. You will use these skills throughout the rest of the course.
________________________________________
## Summary
This lab focused on ensuring that you understand the basic plotting techniques in Matplotlib using plotting objects and functions to draw single plots, as well as figures with multiple subplots. You also practiced customizing the plots with labels, titles and axes definitions.
________________________________________

# [Data Visualization - Lab](https://colab.research.google.com/gist/bpurdy-ds/ee543f3ad14d6101db31d80e0967c45b/index.ipynb#scrollTo=KcPv7irjk6fU)

## Introduction
This lab will give you some structured practice performing data visualization!

## Objectives

You will be able to:

* Use Matplotlib to create a bar graph
* Use Matplotlib to create a scatter plot
* Use Matplotlib to create a histogram

________________________________________

```python
# Run this cell without changes

import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
```
________________________________________

## Exercise 1

Make a vertical bar graph using `ax.bar()` for the following set of data:

> Jim's Video Library contains 40 crime, 30 science fiction, 10 drama, 50 comedy, 25 action and 5 documentary movies.

* Set x-axis (genres) and y-axis (number of movies)
* Plot and label the bar graph
* Provide a suitable title
* Label x and y-axis

Notes:

1. We are asking you to "hard-code" the numbers listed above into Python. There is no file or other data source to open.
2. `x` and `height` must be iterables of numbers, so `x` should just be 6 evenly-spaced numbers. To set the labels of "crime" etc. pass the `labels` into the `.bar()` function using the `tick_label` argument.

The graph you create should look like this:

![bar graph](https://curriculum-content.s3.amazonaws.com/data-science/images/bar_chart.png)


________________________________________
### Code
```python
# Replace None with appropriate code
height = [40, 30, 10, 50, 25, 5]
labels = ['Crime', 'Sci-Fi', 'Drama', 'Comedy', 'Action', 'Documentary']
x = range(len(labels))

# Create the plot
fig, ax = plt.subplots(figsize=(8, 6))

# Plot vertical bars of fixed width by passing x and height values to .bar() function
plt.bar(x, height, tick_label= labels)

# Give a title to the bar graph and label the axes
plt.title("Jim's Video Library")
plt.xlabel("Genres")
plt.ylabel("Number of Movies")
```
![image](https://github.com/user-attachments/assets/2ef59099-aa7c-4c4a-898c-84871c69d8bf)

________________________________________

## Exercise 2

The table shows the data collected by a Consumer Products Group on the relationship between the weight of a car and its average gas mileage.

      Car Type  Weight	miles per gallon
        A	    2750	   29
        B	    3125	   23
        C	    2100	   33
        D	    4082	   18
        E	    2690	   20
        F	    3640	   21
        G	    4380	   14
        H	    2241	   25
        I	    2895	   31
        J	    3659	   17
        
* Use a scatter plot to show the relationship between mpg and weight of a car using `.scatter()`
* Set appropriate labels for axes
* Give a title to the plot
* Create a legend

Looking the scatter plot, think about: how would you describe the relationship between these two attributes?

The graph you create should look like this:

![scatter plot](https://curriculum-content.s3.amazonaws.com/data-science/images/scatter_plot.png)
________________________________________
### Code
```python
# Replace None with appropriate code

weight = [2750, 3125, 2100, 4082, 2690, 3640, 4380, 2241, 2895, 3659]
mpg = [29, 23, 33, 28, 20, 21, 14, 25, 31, 17]

# Create the plot
plt.scatter(weight, mpg, label = "weight vs. mileage")

# Plot with scatter()
None

# Set x and y axes labels, legend, and title
plt.title('Consumer Car')
plt.xlabel("Car Weight")
plt.ylabel("Miles per Gallon")
plt.legend()
plt.show()
```
_![image](https://github.com/user-attachments/assets/170241e8-3ca7-4e3f-ae73-b40a6255dc86)
_______________________________________
## Exercise 3

Joe is the branch manager at a bank. Recently, Joe has been receiving customer feedback saying that the waiting times for clients to be served by customer service representatives are too long. Joe decides to observe and write down the time spent waiting by each customer. Here are his findings from observing and writing down the wait times (in seconds), spent by 20 customers:

43.1, 35.6, 37.5, 36.5, 45.3, 43.4, 40.3, 50.2, 47.3, 31.2, 42.2, 45.5, 30.3, 31.4, 35.6, 45.2, 54.1, 45.6, 36.5, 43.1

* Build a histogram of these values using the `hist()` function. Use `bins=5` to represent the 20 data points
* Plot, label and give a title as above.

The graph you create should look like this:

![histogram](https://curriculum-content.s3.amazonaws.com/data-science/images/histogram.png)

________________________________________
### Code
```python
# Replace None with appropriate code

x = [43.1, 35.6, 37.5, 36.5, 45.3, 43.4,
     40.3, 50.2, 47.3, 31.2, 42.2, 45.5,
     30.3, 31.4, 35.6, 45.2, 54.1, 45.6,
     36.5, 43.1]

# Create the plot
None

# Plot the histogram with hist() function
plt.hist(x, bins = 5)

# Label axes and set title
plt.title('Customer Waiting Time')
plt.xlabel('Waiting Times')
plt.ylabel('Number of Customer')
```
![image](https://github.com/user-attachments/assets/4e60599c-663b-4251-a26c-561e77294646)

________________________________________
## Summary
In this lab, you got some good practice working with creating plots in Python using Matplotlib.
________________________________________

# Seaborn - Lab

## Introduction

In this lab, we'll get some practice working with a second, more advanced visualization library, **_Seaborn_**!

## Objectives

You will be able to:

* Construct plots with Seaborn using its pre-built functionality

## Getting Started

In this lab, we'll explore several different kinds of visualizations we can create with Seaborn. Seaborn is built on top of Matplotlib, so you'll find that it will feel quite familiar. 

Let's get started by importing some things and creating a toy dataset to work with for our first visualization. 


In the cell below: 

* Import `numpy` and set the standard alias of `np`
* Import `seaborn` and set the standard alias of `sns`
* Set `%matplotlib inline` so that our visualizations appear in the notebook, and not as separate files


```python
import numpy as np

import seaborn as sns

%matplotlib inline
```

Great! Now, run the cell below to create a sample dataset. 

#### Input:
```python
data = np.random.normal(size=(20, 10)) + np.arange(10) / 2

data
```
#### Output:
```
array([[-0.4910446 ,  0.96625651,  2.11518517,  2.55725425,  2.48252072,
         1.17664717,  3.21901381,  3.31070445,  4.18299629,  5.11076087],
       [ 1.75471787,  1.1865344 ,  0.5377167 ,  0.97481617,  1.95728331,
         1.3909737 ,  1.24400246,  3.51766202,  3.68950567,  6.62717875],
       [-0.99923626, -0.03829269,  1.18381474,  2.62328713,  1.89684756,
         3.58854945,  4.01849336,  5.1546867 ,  3.38097028,  4.3244238 ],
       [ 0.82510861, -1.16295145,  1.39756072,  1.46963151,  3.80778164,
         0.32742599,  4.00812776,  3.59443515,  2.92732148,  4.11192962],
       [ 0.93498066,  1.07366076,  1.3354102 ,  2.06947528,  3.62879494,
         3.26722394,  2.81361111,  2.81680414,  3.84368504,  3.68998221],
       [ 1.14579874,  0.91074442,  1.24831117,  0.83291617,  3.01001093,
         0.58179268,  3.03145221,  3.29618236,  4.3944523 ,  4.55804545],
       [-1.1121505 ,  1.60287629,  0.97790683,  0.78531892,  1.77053384,
         3.41634838,  2.4202794 ,  3.11270531,  4.74620865,  4.76852145],
       [ 1.5221644 ,  0.45850084,  1.9042652 ,  1.66785307,  0.51492245,
         1.3012282 ,  3.91005236,  6.2011828 ,  5.65578277,  4.48045731],
       [-0.69725309, -0.15858059,  1.45358845,  1.51650968,  1.73125124,
         1.28948831,  1.85419218,  2.58696397,  4.26405976,  4.07858591],
       [-1.02120108,  1.0530996 ,  0.35763199,  1.63659903,  0.6035771 ,
         1.14288918,  3.13777114,  3.96383058,  4.20319226,  4.2397489 ],
       [ 0.95420282, -0.25461111,  1.00809651,  2.62467951,  3.74043526,
         3.96136698,  3.46647611,  3.36292456,  5.82872253,  5.39599122],
       [-0.20518756, -2.06280751,  2.29962529,  0.14034103,  3.41014428,
         3.34044613,  2.82513932,  4.46879264,  6.5241618 ,  5.83337244],
       [ 0.42088708,  0.73200053, -0.28809514,  0.96292286,  2.701553  ,
         2.83039424,  2.99625081,  3.45069896,  3.65434207,  3.93306079],
       [-1.23364512, -0.64093216,  2.11342494,  1.84455482,  0.10376203,
         1.58970966,  3.35068349,  5.13942921,  2.8014744 ,  4.57074946],
       [ 0.02724973,  0.11366319, -0.49424966,  2.86508863,  3.72018445,
         4.47741816,  3.86042011,  4.83158731,  4.3245444 ,  5.20307209],
       [ 1.1090115 ,  0.30189579,  1.96787099,  2.85015937,  3.27025476,
         5.37263603,  2.18056071,  3.89284126,  5.83103865,  4.85543614],
       [-2.28245729,  1.51608788,  1.54814851,  1.72160907,  2.4741283 ,
         2.89104251,  2.5880604 ,  2.89129689,  3.77233836,  4.33326694],
       [-1.03284875,  0.01618925,  2.64997774,  1.34129974,  2.02976186,
         3.42986109,  2.70346921,  3.36192528,  4.99681938,  2.1975835 ],
       [ 1.84035287, -0.33106804, -0.31436489, -0.74291608,  1.26497875,
         0.42919199,  3.073776  ,  3.19473304,  2.89734799,  4.70023313],
       [-0.61186834, -1.39206033,  0.13169423,  1.84127736,  2.07966352,
         2.89590552,  2.60304565,  2.29007072,  4.62463189,  4.56821275]])
```

### Basic Visualizations with Seaborn

We'll start off by creating a boxplot with the dataset we just created so that we can get a feel for the common workflow of Seaborn. 

In the cell below:

* Create a `boxplot` and pass in the parameter `data=data`. Store the object returned in the variable `boxplot`


```python
boxplot = sns.boxplot(data=data)
```
![image](https://github.com/user-attachments/assets/9eff80c4-e371-46eb-b5d8-a258b740c1c1)

That's a nice looking visualization, for only a single line of code! However, it's missing axis labels and a title. Let's fix that. 

In the cell below: 

* Copy and paste the code from the cell above to recreate our boxplot
* Call the `boxplot` object's `set()` method and pass in the following parameters:
    * `xlabel= 'X Label'`
    * `ylabel= 'Y Label'`
    * `title = 'Example Boxplot'`    

#### Input:
```python
boxplot.set(xlabel='X Label', ylabel='Y Label', title='Example Boxplot')
```
#### Output:
```
[Text(0.5, 4.444444444444445, 'X Label'),
 Text(4.444444444444445, 0.5, 'Y Label'),
 Text(0.5, 1.0, 'Example Boxplot')]
```

That wasn't too bad! Note that we can also use **_Method Chaining_** to set all the label and title information by combining the two lines in the cell above!

In the cell below:

* Recreate the labeled boxplot by calling `.set()` and passing in the appropriate parameter values immediately after calling `sns.boxplot(data=data)` to create the visualization. 

**_NOTE_**: For this visualization, you do not need to store the object in a variable. Just call the methods.

#### Input:
```python
sns.boxplot(data=data).set(xlabel='X Label', ylabel='Y Label', title='Example Boxplot')
```
#### Output:
```
[Text(0.5, 0, 'X Label'),
 Text(0, 0.5, 'Y Label'),
 Text(0.5, 1.0, 'Example Boxplot')]
```
![image](https://github.com/user-attachments/assets/537fbff5-86a0-4842-9965-5bc05f523388)


Great! As you can see, Seaborn is a pretty easy library to work with. It also has very detailed and easy-to-follow documentation, complete with a ton of examples and tutorials. If you're ever unsure of how to build something, don't be afraid to look at the [Seaborn Documentation](https://seaborn.pydata.org/), or Google!

### Changing Style and Context

One of the main reasons Data Scientists love Seaborn is because the visualizations it creates are just plain prettier than those made by matplotlib. Seaborn makes it very simple to style our visualizations--all we need to do is use the `set_style()` method!

In the cell below:

* Call Seaborn's `set_style()` method and pass in the string `'darkgrid'`. 
* Recreate the labeled boxplot that we made in the cell above. 

#### Input:
```python
sns.set_style("darkgrid")
sns.boxplot(data=data).set(xlabel='X Label', ylabel='Y Label', title='Example Boxplot')
```
#### Output:
```
[Text(0.5, 0, 'X Label'),
 Text(0, 0.5, 'Y Label'),
 Text(0.5, 1.0, 'Example Boxplot')]
```
![image](https://github.com/user-attachments/assets/28321a54-ad89-4c00-a9f7-d4d6160d6752)


That's much easier to read! There are several different styles that we can choose from. To see examples of the different styles we can use, check out the [documentation](https://seaborn.pydata.org/tutorial/aesthetics.html) for controlling figure aesthetics.

Before we move on, let's make one more change. While the plot looks much better now, the size of the text for ticks and axis labels so small that it would be hard for people to read it unless they're right in front of the monitor--that's a problem, if the visualizations are going to be used in something like a tech talk or presentation!

For this reason, we can also set the context, using the--you guessed it--`set_context()` method!

In the cell below:

* Call Seaborn's `set_context()` method and pass in the string `'poster'`.
* Recreate the labeled boxplot that we made in the cell above.

#### Input:
```python
sns.set_style("darkgrid")
sns.set_context("poster")
sns.boxplot(data=data).set(xlabel='X Label', ylabel='Y Label', title='Example Boxplot')
```
#### Output:
```
[Text(0.5, 0, 'X Label'),
 Text(0, 0.5, 'Y Label'),
 Text(0.5, 1.0, 'Example Boxplot')]
```
![image](https://github.com/user-attachments/assets/0fcfac6e-5f66-42e7-a810-bf4d8edfcd69)

Much better! That's much more readable. From smallest to largest, the different context settings we can use are `'paper'`, `'notebook'`, `'talk'`, and `'poster'`. 

### A  Quick Note on Contexts and Styles

When you call `set_context` or `set_style`, you're setting a global parameter that will apply to all future plots you create during this session. Any visualizations you have already created will not change--however, they will change if you rerun the cell that created them! 

Let's change our context back to `'notebook'` so that the next visualizations we create don't look too big. 

In the cell below, change the context back to `'notebook'`.

#### Input:
```python
sns.set_style("darkgrid")
sns.set_context("notebook")
sns.boxplot(data=data).set(xlabel='X Label', ylabel='Y Label', title='Example Boxplot')
```
#### Output:
```
[Text(0.5, 0, 'X Label'),
 Text(0, 0.5, 'Y Label'),
 Text(0.5, 1.0, 'Example Boxplot')]
```
![image](https://github.com/user-attachments/assets/90189718-3c25-4dd6-9bcf-514f6d7b0649)



## More Advanced Visualizations

One awesome feature of Seaborn is the ability to quickly and easily create advanced visualizations such as **_Regression Plots_**. To end this lab, we'll see a few examples, and explore how they are created. 

### Regression Lines with Confidence Intervals

There are also several different types of regression plots Seaborn makes available for this purpose. For this example, we're going to create an advanced regression plot that also visualizes the confidence interval for our regression line. We'll even have the visualization **_condition on_** a 3rd variable, to show how the regression lines differ for each group, depending on the value of the 3rd variable. 

For this visualization, we'll need a more advanced dataset than the example we created and used above. Luckily, Seaborn comes with some preloaded datasets. We can see the names of all the datasets by calling Seaborn's `get_dataset_names()` method. 

Do this now in the cell below.

#### Input:
```python
sns.get_dataset_names()
```
#### Output:
```
['anagrams',
 'anscombe',
 'attention',
 'brain_networks',
 'car_crashes',
 'diamonds',
 'dots',
 'dowjones',
 'exercise',
 'flights',
 'fmri',
 'geyser',
 'glue',
 'healthexp',
 'iris',
 'mpg',
 'penguins',
 'planets',
 'seaice',
 'taxis',
 'tips',
 'titanic']
```


Great! For the reamainder of this notebook, we'll use the `'tips'` dataset. We can get this dataset by calling Seaborn's `load_dataset()` method and passing in the string `'tips'`. Seaborn is even considerate enough to return the dataset as a pandas DataFrame!

In the cell below, get the tips dataset and store it in the variable `tips`. Then, display the head of the DataFrame so we can see what we're working with. 

#### Input
```python
tips = sns.load_dataset('tips')

print(tips.head())
```
#### Output:
```
   total_bill   tip     sex smoker  day    time  size
0       16.99  1.01  Female     No  Sun  Dinner     2
1       10.34  1.66    Male     No  Sun  Dinner     3
2       21.01  3.50    Male     No  Sun  Dinner     3
3       23.68  3.31    Male     No  Sun  Dinner     2
4       24.59  3.61  Female     No  Sun  Dinner     4
```
Now that we have our dataset, we can create our regression plot. There are several kinds of regression plots we can use. For this example, we'll use the `lmplot` function. 

In the cell below: 

* Call Seaborn's `lmplot` function and pass in the following arguments:
    * `x='total_bill'`
    * `y='tip'`
    * `hue='smoker'`
    * `data= tips`

#### Input:
```python
sns.lmplot(x='total_bill', y='tip', hue='smoker', data=tips)
```
#### Output:
```
<seaborn.axisgrid.FacetGrid at 0x7f6abf701090>
```
![image](https://github.com/user-attachments/assets/b96df0b6-42ad-4a4e-bb7c-a7a1f485d832)



Very cool! That visualization contains _a lot_ of information, and it does it in a way that is easy to interpret and understand. Best of all, it didn't take much work on our part--all we had to do was tell the function the name of the column to use for the x axis, the name of the column to use for the y axis, and the name of the variable to condition on, as denoted by the two different colors. 

If we want to get even more ambitious, we can create mutiple subplots by using the `row=` and `column=` parameters, as well! 

Run the cell below to see an example, and see if you can figure out how the code works. 


```python
sns.lmplot(x="total_bill", y="tip", hue="smoker",
           col="time", row="sex", data=tips)
```
![image](https://github.com/user-attachments/assets/6bfe0e52-191c-4e96-9506-d15abd82371f)

## Summary

In this lab, we explored the **_Seaborn_** library, and explored the sorts of data visualizations we can create with it!

# [Data Visualization - Cumulative Lab](https://colab.research.google.com/gist/Makster04/7c15c54f15ed24e7e7949bb61eb1545f/index.ipynb#scrollTo=Yh3yKkmonskj)

## Introduction
You've completed the data visualization section — excellent work. Now we're going to do some rudimentary analysis of Shakespeare's classic play: Macbeth! You will get practice working with lists and dictionaries, conditionals, visualizing data, and thinking analytically about data.

## Objectives

You will be able to:

* Apply string methods to make changes to a string
* Use a `for` loop to iterate over a collection
* Assign values in a dictionary
* Use data visualizations to present your findings

## Your Task: Analyze the Text of Shakespeare's Macbeth

![cover page of macbeth](https://curriculum-content.s3.amazonaws.com/data-science/images/macbeth.jpg)

<span>Photo by <a href="https://unsplash.com/@voodoojava?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Matt Riches</a> on <a href="https://unsplash.com/s/photos/shakespeare?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>

### Business Understanding

**Natural language processing** (also known as **NLP**) is a major subfield within data science. At its most advanced, NLP has helped us build interactive AI assistants like Siri and Alexa.

Even in a simpler business context where you just need to summarize the contents of a dataset, text data often requires much more substantial preprocessing work compared to data that is already in a numeric format.

One typical technique for understanding a text dataset is to find the **most common** or **least common** words. To do this, we need to build a ***Frequency Distribution*** table, just like when we were finding the mode of a dataset. We'll display the thousands of word frequencies as a **histogram**.

Then we can find the mode (the word that appears most often), as well as the "runner-up" words, in order to describe a large text dataset with a minimal set of words and numbers. We'll display this information as a **bar graph** with the words as labels on the x-axis and the counts as the y-axis.

### Data Understanding

For this lab we'll be using the **full text of Shakespeare's Macbeth**. We will retrieve it for you from the [Project Gutenberg](https://www.gutenberg.org/) website in the format of a single (giant) string, containing over one hundred thousand characters. We'll refer to this string variously as the "document", "corpus", or "text dataset", all terms used frequently within NLP.

We don't recommend that you try to print the entire string due to its length, but if you're curious about any particular segment, you can use string slicing just like any other string. E.g. `macbeth[1000:2000]` will select just the slice from the 1000th to the 2000th character.

When counting the words, make sure you remove any punctuation and convert all words to lowercase. We want all of the following strings to be counted as instances of `"is"`:

 - `"is"`
 - `"Is"`
 - `"is,"`
 - `"is!"`
 - etc.

### Requirements

#### 1. Word Count Summary

Extract each word from the document and print a count of all words.

#### 2. Unique Word Count

First, clean up the collection of words so all punctuation is removed and every word is lowercase. Then print a count of the unique words in that collection.

#### 3. Frequency Table

Using the cleaned collection of words, build a frequency table that has the words as keys and the counts of those words as values. From that frequency table, print the modal (most common) word as well as the least common word, along with their frequencies.

#### 4. Visualizations

**Histogram:** Using Matplotlib or Seaborn, create a histogram of all of the word frequencies in Macbeth.

**Bar graph:** Using Matplotlib or Seaborn, create a bar graph of the 25 most common words in Macbeth, from the 1st to 25th most common.


## Getting the Data
Here we start by importing a Python package called `requests`. You'll see this package described in more detail in future lessons, but for now all you need to know is that it allows us to fetch data over the internet!

We'll use it to pull the transcript of Macbeth from the Project Gutenberg website, specifically [this page](https://www.gutenberg.org/cache/epub/2264/pg2264.txt). We'll also preview a few details about what is now stored in the variable `macbeth`. As you can see, it's a string with 103,605 characters - the first 500 of which are printed below. 


```python
# Run this cell without changes
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import requests

sns.set_context("talk")
sns.set_style("whitegrid")
%matplotlib inline
```

```python
# Run this cell without changes
response = requests.get('https://www.gutenberg.org/cache/epub/2264/pg2264.txt')
full_text = response.text

# The beginning describes the source/copyright, it isn't the actual text
# of the play until the 4863rd character
macbeth = full_text[4863:]

# Print string summary
print("Data type:", type(macbeth))
print()
print("Number of characters:", len(macbeth))
print()
print("First 500 characters:")
print(macbeth[:500])
```

#### Output:
```
    Data type: <class 'str'>
    
    Number of characters: 122550
    
    First 500 characters:
    
    The Tragedie of Macbeth
    
    Actus Primus. Scoena Prima.
    
    Thunder and Lightning. Enter three Witches.
    
      1. When shall we three meet againe?
    In Thunder, Lightning, or in Raine?
      2. When the Hurley-burley's done,
    When the Battaile's lost, and wonne
    
       3. That will be ere the set of Sunne
    
       1. Where the place?
      2. Vpon the Heath
    
       3. There to meet with Macbeth
    
       1. I come, Gray-Malkin
    
       All. Padock calls anon: faire is foule, and foule is faire,
    Houer through the fogg
```

## Word Count Summary

Create a variable `word_count` that is an integer representing the total count of words in `macbeth`. In order to do this, first create a variable `words_raw` that is a list containing all words in the string.

Hint: look at the `.split()` string method ([documentation here](https://docs.python.org/3/library/stdtypes.html#str.split))


#### Input:

```python
# __SOLUTION__
words_raw = macbeth.split()
word_count = len(words_raw)

print("Macbeth contains {} words".format(word_count))
print("Here are some examples:", words_raw[11:21])
```
#### Output:
```
    Macbeth contains 20641 words
    Here are some examples: ['Enter', 'three', 'Witches.', '1.', 'When', 'shall', 'we', 'three', 'meet', 'againe?']
```

## Unique Word Count

Create a variable `unique_word_count` that is an integer representing the count of unique words in Macbeth.

In order to create an accurate count, first create a variable `words_cleaned` that contains each word stripped of punctuation and made lowercase. Then assign `unique_word_count` to the count of words in `words_cleaned`.

Hint: look at the `.strip()` string method ([documentation here](https://docs.python.org/3/library/stdtypes.html#str.strip)). Note that you need to strip each individual word, not just the whole `macbeth` string.

**Reminder:** strings are an *immutable* data type. That means that in order to modify their values, you have to reassign them with `=`. So, for example, if you wanted to make the variable `name` be title case, you need to do `name = name.title()`, not just `name.title()`.



#### Input:
```python
# __SOLUTION__
import string
punctuation = string.punctuation

words_cleaned = []

for word in words_raw:
    # Remove punctuation
    word = word.strip(punctuation)
    # Make lowercase
    word = word.lower()
    # Append to words_cleaned
    words_cleaned.append(word)

print("Cleaned word examples:", words_cleaned[11:21])
```
#### Output:
```
    Cleaned word examples: ['enter', 'three', 'witches', '1', 'when', 'shall', 'we', 'three', 'meet', 'againe']
```

#### Input:
```python
# Use set() to only include unique words
unique_word_count = len(set(words_cleaned))

print("Macbeth contains {} unique words".format(unique_word_count))
```

#### Output:
```
    Macbeth contains 4102 unique words
```

## Frequency Table

Now that we have a general sense of how *many* words there are, let's investigate how *frequently* each of those words appears in the dataset. Build a frequency table called `word_counts` where the keys are the words (strings) and the values are the number of times that string appears. Then set `most_frequent_word` to the word that occurs most frequently and `least_frequent_word` to the word that occurs least frequently.

To accomplish this, use the same algorithm used in the **Implementing Statistics with Functions** lab earlier, specifically the function to find the mode. This time we will provide you with some clues, but fewer than before. Remember that you can look at that lab (and its solution) or the solution to this lab if you are getting really stuck.

The general algorithm for building a frequency table is:

1. Initialize an empty dictionary (`word_counts`)
2. Loop over every element in the collection (`words_cleaned`) and add to the dictionary
    - If the element is not already in the dictionary keys, add a new key-value pair with the value 1
    - If the element is already in the dictionary keys, add 1 to the associated value



```python
# Your code here

print(type(word_counts)) # <class 'dict'>
print(len(word_counts))  # 4102
```

#### Input:
```python
# __SOLUTION__
word_counts = {}

for word in words_cleaned:
    if word not in word_counts:
        word_counts[word] = 1
    else:
        word_counts[word] += 1

print(type(word_counts))
print(len(word_counts))
```
#### Output:
```
    <class 'dict'>
    4102

```
Now it's time to find `most_frequent_word` and `least_frequent_word`. Again, this follows the logic of the mode function from the previous lab.

The general algorithm for finding the most frequent word is:

1. Find the *maximum* value in the dictionary (`word_counts`)
2. Loop over all items in the dictionary until you find the key associated with that *maximum* value

Then the algorithm for finding the least frequent is just the inverse:

1. Find the *minimum* value in the dictionary
2. Loop over all items in the dictionary until you find the key associated with that *minimum* value

Think about how you might accomplish this with a single loop, but don't worry if it takes you two loops (just look at the solution when you are done and compare).


```python
# Your code here

print("The most frequent word in Macbeth is '{}', which appears {} times".format(
    most_frequent_word, word_counts[most_frequent_word]
))
print("The least frequent word in Macbeth is '{}', which appears {} times".format(
    least_frequent_word, word_counts[least_frequent_word]
))
```

#### Input:
```python
# __SOLUTION__
max_frequency = max(word_counts.values())
min_frequency = min(word_counts.values())

most_frequent_word = None
least_frequent_word = None

for word, frequency in word_counts.items():
    if frequency == max_frequency:
        most_frequent_word = word
    elif frequency == min_frequency:
        least_frequent_word = word

print("The most frequent word in Macbeth is '{}', which appears {} times".format(
    most_frequent_word, word_counts[most_frequent_word]
))
print("The least frequent word in Macbeth is '{}', which appears {} times".format(
    least_frequent_word, word_counts[least_frequent_word]
))
```
#### Output:
```
    The most frequent word in Macbeth is 'the', which appears 823 times
    The least frequent word in Macbeth is 'hear', which appears 1 times
```

## Visualizations

### Histogram

At last, it's time for some visualizations! First, let's make a **histogram** to visualize the frequency distribution of all 3,577 words (i.e. the distribution of `word_counts.values()`). 

Details:

 - We recommend using Matplotlib for this, since it allows you to customize the figure size. A `figsize` of (15,5) will work well for this, since it has a "long tail". 100 bins is also a good number.
 - Make sure you include appropriate labels on the axes and the title
 - You can use any colors or styles that look good to you

#### Input:
```python

# Matplotlib version
fig, ax = plt.subplots(figsize=(15,5))
ax.hist(word_counts.values(), bins=100)
ax.set_xlabel("Word Frequency")
ax.set_ylabel("Number of Words with This Frequency")
ax.set_title("Word Frequency Distribution for Macbeth");
```
 ![image](https://github.com/user-attachments/assets/db899931-4052-4ed6-981f-f799dbdcd521)
   
```python
# __SOLUTION__

# Technically you can use Seaborn also but it requires making
# the figure and axes in Matplotlib first, otherwise you don't
# see any data drawn with the default width

fig, ax = plt.subplots(figsize=(15,5))
sns.histplot(
    word_counts.values(),
    bins=100,
    ax=ax, # telling it to plot using the axes already created  
    legend=False # seaborn has a legend by default but I don't think it's useful here
).set(
    xlabel="Word Frequency", 
    ylabel="Number of Words with This Frequency", 
    title="Word Frequency Distribution for Macbeth"
);
```
![image](https://github.com/user-attachments/assets/42ec0187-6a6d-476b-a9ab-19237304f79f)


Wow, that is a very skewed dataset! It looks like the overwhelming majority of words appear about 20 times or fewer, but we also have words (like 'the', the most common word discovered above) that appear hundreds of times. Those very frequent words are so rare that we can't even see their associated counts, the bars are so small.

### Bar Graph

Let's move on to making a bar graph of the most frequent words, to gain more insight into that end of the distribution's "tail". To do this, we need to sort the contents of `word_counts` by value, and then select only the top 25 key-value pairs.

For this task we are giving you even fewer hints than before. Check out the [Sorting HOW TO](https://docs.python.org/3/howto/sorting.html) Python documentation, especially the `student_tuples` example. Part of being a data scientist is figuring out how to do tasks that you may not have done before. Remember, in these situations, Google is your friend!


##### Input:

```python
# __SOLUTION__

counts_list = list(word_counts.items())

# Sort the list of tuples by the frequency (second element in each tuple)
# Make sure it goes from most to least frequent
counts_list_sorted = sorted(counts_list, key = lambda item: item[1], reverse=True)

# Slice the sorted list to just the first 25 tuples
top_25 = counts_list_sorted[:25]

# Make a list of dummy numbers to populate the axis
ticks = np.arange(25)

# Get just the words from top_25 and assign to labels
# Get just the frequencies from top_25 and assign to frequencies
labels = []
frequencies = []
for word, frequency in top_25:
    labels.append(word)
    frequencies.append(frequency)
    
# ^ Alternatively you could use list comprehension:
# labels = [item[0] for item in top_25]
# frequencies = [item[1] for item in top_25]

print("Tick values:", ticks)
print()
print("Labels:", labels)
print()
print("Frequencies:", frequencies)
```
#### Output:
```
    Tick values: [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23
     24]
    
    Labels: ['the', 'and', 'to', 'of', 'i', 'a', 'you', 'in', 'that', 'my', 'is', 'with', 'not', 'it', 'be', 'his', 'this', 'macb', 'your', 'for', 'our', 'but', 'haue', 'all', 'me']
    
    Frequencies: [823, 609, 464, 454, 331, 296, 273, 257, 242, 203, 201, 198, 192, 173, 154, 146, 146, 137, 135, 134, 127, 124, 122, 113, 113]
;
```
Now that we have our data, let's make a bar graph. Just to keep it interesting, let's make this a ***horizontal*** **bar graph**. Horizontal bar graphs are useful when you have a lot of text labels — it avoids having to turn the labels diagonally or even sideways in order for them to fit next to each other.

**Matplotlib:** In a horizontal bar graph with Matplotlib, `y` is where you pass in the dummy tick values, and `width` is where you pass in the frequencies (vs. `x` and `height` in a standard bar chart). Full documentation for `.barh()`, the horizontal bar chart method, [here](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.axes.Axes.barh.html#matplotlib.axes.Axes.barh).

**Seaborn:** With Seaborn, you still use the `.barplot()` function, just with the `orient` argument set to `"h"`. You'll want to pass in the dummy tick values as `y` and frequencies as `x`. Full documentation [here](https://seaborn.pydata.org/generated/seaborn.barplot.html).

Details:

 - You can use either Matplotlib or Seaborn
 - Make sure you include appropriate labels on the axes and the title
 - You can use any colors or styles that look good to you

#### Input:


#### Matplotlib Version:
```python
# __SOLUTION__

# Matplotlib version

# You don't have to reverse the order, I just think it looks better
# for the largest to be at the top rather than closest to the x-axis
# (the default behavior)

frequencies_reversed = frequencies[::-1]
labels_reversed = labels[::-1]

fig, ax = plt.subplots(figsize=(6, 12))
ax.barh(ticks, frequencies_reversed)

# You have to set both the ticks themselves and the labels
# The ticks make it so there are fully 25 ticks, not just 6

ax.set_yticks(ticks)
# The labels put the words next to the tick marks
ax.set_yticklabels(labels_reversed)

ax.set_ylabel("Word")
ax.set_xlabel("Number of Occurrences")
ax.set_title("Top 25 Words in Macbeth");
```
    
![image](https://github.com/user-attachments/assets/ba1b1fc2-9d09-4375-a6a7-bdea45b98a36)

#### Seaborn Version:
```python
# __SOLUTION__

# Seaborn version

# Seaborn automatically puts the largest at the top, so you
# don't need to create reversed versions

# Text overlaps if you use the default width, so start with
# Matplotlib fig and ax
fig, ax = plt.subplots(figsize=(6, 12))

sns.barplot(
    x=frequencies, 
    y=ticks, 
    orient="h",
    ax=ax, # telling it to plot using the axes already created  
    palette="flare" # set a sequential colormap
).set(
    yticklabels=labels,
    ylabel="Word",
    xlabel="Number of Occurrences", 
    title="Top 25 Words in Macbeth"
);
```
![image](https://github.com/user-attachments/assets/c9d15c57-e9bb-4a42-96af-891321b1a3f3)



## Level Up (Optional)
This cumulative lab should take you about an hour and a half to complete. If you're done much more quickly than that and are not behind in the course, feel free to deepen your knowledge by completing any or all of the following tasks until you run out of time (creating a relevant visualization for each):

* **When counting words, skip** ***stopwords***
  * Stopwords are commonly-occurring words that NLP analysts often disregard. Most of the top 25 words in our current version are stopwords ("the", "and", etc.). Try redoing both the histogram and the horizontal bar chart with stopwords removed
  * Mechanically, that means skipping adding a word to `word_counts` if it is a stop word. Try using this list of stopwords:
```
["i", "me", "my", "myself", "we", "our", "ours", "ourselves", "you", "your", "yours", "yourself", "yourselves", "he", "him", "his", "himself", "she", "her", "hers", "herself", "it", "its", "itself", "they", "them", "their", "theirs", "themselves", "what", "which", "who", "whom", "this", "that", "these", "those", "am", "is", "are", "was", "were", "be", "been", "being", "have", "has", "had", "having", "do", "does", "did", "doing", "a", "an", "the", "and", "but", "if", "or", "because", "as", "until", "while", "of", "at", "by", "for", "with", "about", "against", "between", "into", "through", "during", "before", "after", "above", "below", "to", "from", "up", "down", "in", "out", "on", "off", "over", "under", "again", "further", "then", "once", "here", "there", "when", "where", "why", "how", "all", "any", "both", "each", "few", "more", "most", "other", "some", "such", "no", "nor", "not", "only", "own", "same", "so", "than", "too", "very", "s", "t", "can", "will", "just", "don", "should", "now"]
```
* **Create a list of top characters by mentions of their names**
  * Mechanically, that means only adding a word to `word_counts` if it is the name of a character. Try using this list of single-word characters (leaving out characters like "Young Seyward", and "Lady Macduff" is referred to as "wife" in this version):
```
["duncan", "malcolm", "donalbaine", "macbeth", "banquo", "macduff", "lenox", "rosse", "menteth", "angus", "cathnes", "fleance", "seyward", "seyton", "boy", "lady", "messenger", "wife"]
```
* **Split the text by which character is talking**
  * A character speaking is indicated by an (often-abbreviated) version of their name followed by a `.` as the first thing on a line. So for example, when Macbeth speaks it starts with `"Macb."` (notice how `"macb"` appears in the top 25 words — that is Macbeth speaking). You'll need to revise how you handle punctuation, since you can't just strip all punctuation
* **Create subgraphs of the most common words by character**
* **Come up with some other fun analyses of the text!**

There is no solution version of these level-up options. If you're having too much trouble, it's fine to move on without completing any of them!


```python
# Your code here
```

## Summary
Congratulations! You've got some extra practice combining various data types into useful programming patterns and done an initial analysis of a classic text!
