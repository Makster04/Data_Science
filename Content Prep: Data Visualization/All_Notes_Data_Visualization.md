# [Data Visualization](https://colab.research.google.com/gist/bpurdy-ds/1f3676813ca2fac433cac8882d4f585b/index.ipynb)

## Introduction

This lesson introduces data visualization using Python and the popular Matplotlib plotting library. You will explore the fundamental features of standard Matplotlib plots and how to use them for creating and customizing visualizations. 

## Objectives

You will be able to:

* Use Matplotlib to create a scatter plot
* Use Matplotlib to create a histogram
* Interpret a histogram to gain insight about a distribution of data

## Matplotlib Plotting Library

The Matplotlib plotting library provides a range of built in functions to start visualizing data with minimal effort. 

First, import `matplotlib`'s `pyplot` module (a module is a unit of prewritten code that you can use in your projects) into your working environment along with `numpy` (one of the most popular Python libraries for scientific computing) to create some sample data. You will see that importing the `pyplot` module from Matplotlib provides simple and agile creation of plots. 

```python
import matplotlib.pyplot as plt

```

In Jupyter notebooks, you can use the `%matplotlib` "magic command" with `inline` to show plots inside the notebook or `qt` for external plots. The `inline` option is recommended for most requirements (external plots are suitable for interactive visualizations).  


```python
# Import matplotlib
import matplotlib.pyplot as plt

# Set plot space as inline for inline plots and qt for external plots
%matplotlib inline
```

## Scatter Plots

A scatter plot is a two-dimensional data visualization that uses individual data points to represent the values obtained for two different variables - one plotted along the x-axis and the other plotted along the y-axis. 

Scatter plots are used when you want to show the relationship between two variables. Scatter plots are sometimes called correlation plots because they show how two variables are correlated. 

For this example, you will use Python's `numpy` library to create sample data. The industry standard is to alias `numpy` as `np`. Since `numpy` is a specialized library for scientific computing, it is primarily used for performing numerical operations. Don't worry about all of the details surrounding `numpy` right now, it will be introduced formally later. For now, use [numpy's `linspace()` function](https://docs.scipy.org/doc/numpy-1.14.5/reference/generated/numpy.linspace.html) to quickly generate some dummy data for visualizations.


```python
# Import numpy to generate some dummy data
import numpy as np

# Generate an array x of 30 equally spaced data points on a line space of 0 - 10.
x = np.linspace(0, 10, 30)
# Calcuate sin(x) and save in a new array y
y = np.sin(x)
```

Now that you have your data ready, create a scatter plot using the `plt.scatter()` function which takes in two lists and shows their relationship. You can optionally pass in extra parameters like `label` to provide information about what you are plotting, `plt.title()` for defining a title, and `plt.legend()` to add the label information to the plot in a legend. Finally, use the `plt.show()` function to display the plot.


```python
# Pass in x and y values with a label 
plt.scatter(x, y, label = "Function: sin(x)" )
plt.title('Scatter Plot in Matplotlib')
plt.legend()
plt.show()
```


    
![png](index_files/index_5_0.png)
    


In case you are wondering, the above plot shows a sine wave where the y-variable has a periodic dependence on the x-variable. You can customize the plot further to make it easier to read. First, provide some labels for both axes by using `plt.xlabel()` and `plt.ylabel()`. You can also change the size of the plot with `plt.figure(figsize=(a,b))`, where a and b specify the width and height of the plot in inches.


```python
# Set the figure size in inches
plt.figure(figsize=(10,6))

plt.scatter(x, y, label = "y = sin(x)" )

# Set x and y axes labels
plt.xlabel('X Values')
plt.ylabel('Y Values')

plt.title('Scatter Plot in Matplotlib')
plt.legend()
plt.show()
```


    
![png](index_files/index_7_0.png)
    


The nice thing is labels and other customizations that you see here are applicable to almost all kinds of plots in Matplotlib. 

### Bar Graphs

Bar graphs (also called "bar charts") are one of the most common plot types for showing comparisons across data. Bar graphs allow comparisons across categories by presenting categorical data as rectangular bars with heights or lengths proportional to the values that they represent. One axis of the graph shows the specific categories being compared and the other axis represents a value scale. The bars can be plotted vertically or horizontally. When the bars are plotted vertically, it is usually referred to as a "column graph." Some examples of bar graphs are shown below.

<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/image_bar.png" width="700">


Matplotlib features a number of handy plotting functions. Matplotlib's `.bar()` and `.barh()` functions can be used to draw constant width vertical and constant height horizontal bar graphs for a simple sequence of x, y values. 

Now that you understand the concepts, try to generate some plots. To do this, first generate some data using functions from the `np.random` module. This is a specialized module for generating random numbers. Don't worry if the code seems unfamiliar now, the details of using `numpy` for generating random numbers will be covered in detail later.


```python
# Set seed for reproducibility
np.random.seed(100)

# Generate the x-axis variable as 10 categories using numpy's arange function
x = np.arange(10)

# For y-axis, generate 10 random quantities
y = np.random.randn(10)
```

Now, plot a bar graph using the above data.


```python
plt.figure(figsize=(10,6))

# Use the bar() function to create a plot using the above values of x and y. Add a label.
plt.bar(x, y, label='Sample Data')

plt.xlabel('X Values - Categories')
plt.ylabel('Y Values - Quantities')

plt.title('Bar Plot in Matplotlib')
plt.legend()

# Output the final plot
plt.show()
```


    
![png](index_files/index_11_0.png)
    


That bar graph above is useful because you can easily inspect the quantities in each category (0-10) and make informed decisions about how data are distributed across these categories. 

##  Histograms 

A histogram is a plot that lets you discover the underlying frequency distribution of a data set. It allows you to visualize fundamental properties about the data like if it is skewed in any particular direction or if it has outliers. An example of a histogram of the ages of people is shown below:


<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/image_histogram.png" width="300">


Basically, histograms are used to represent data that has been split into some number of groups. The x-axis describes the groups and the y-axis describes the frequency of occurrence. If this is a little confusing, consider the histogram of ages above. The x-axis shows ages in groups of 10 years. The y-axis is a count of how many times a member from each group appears in the data. For example, there are 2 occurrences of ages between 20-30.

It is important to distinguish bar graphs from histograms. Bar graphs show category-specific values and consist of two variables. Histograms show counts of how frequently a given range of values occurs in a data set. Take a look at the examples below and think about how they are different: 

<br>
<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/image_bar_hist.png" width="700">
<br>

You can use the `plt.hist()` function in matplotlib to draw a histogram while passing in values from the required data variable. Say you want to plot a histogram of the retirement ages of 200 people. You can use ```plt.hist()``` to do this:


```python
# Set seed for reproducability
np.random.seed(100)

# Generate a data set of 200 retirement age values
x = 5*np.random.randn(200) + 65

#Plot the histogram with hist() function
plt.hist(x, bins = 10, edgecolor='black')

plt.xlabel('Retirement Age')
plt.ylabel('Frequency of Values')
plt.title('Histograms in Matplotlib')
plt.show()
```


    
![png](index_files/index_14_0.png)
    


Recall, the y-axis tells you how often a certain range of numbers appears in the data set. From the histogram, you can see that there are a lot of people who retire around 65. There are significantly fewer people who retire at 75 and even fewer people who retire at 50. 

### The `bins` Argument
Say you want to change the range of values that define the groups of a histogram. You can optionally pass the `bins` argument to set the number of groups. In the plot above, the data have been separated into 10 groups. Check out what happens when you change the number of bins to 5:


```python
plt.hist(x, bins=5, edgecolor='black')
plt.xlabel('Retirement Age')
plt.ylabel('Frequency of Values')
plt.title('Histograms in Matplotlib')
plt.show()
```


    
![png](index_files/index_16_0.png)
    


Note the scale of the y-axis and the width of the bars compared to the histogram using 10 bins. The granularity of the bins can be changed according to your specific analytical needs and the amount of data available. For example, if you had 50 data points, you would not want to use 500 bins.  

For the final example, say you got a much larger data set of 10000 retirement ages.


```python
# Set seed for reproducability
np.random.seed(100)

# Generate a data set of 10000 retirement age values
x = 5*np.random.randn(10000) + 65

#Plot the distogram with hist() function
plt.hist(x, bins=50, edgecolor="black")

plt.xlabel('Retirement Age')
plt.ylabel('Frequency of Values')
plt.title('Histograms in Matplotlib')
plt.show()
```


    
![png](index_files/index_18_0.png)
    


Notice that the shape of the distribution begins to look more bell-shaped as the size of the data set increases. This is characteristic of an important distribution known as the "Normal" distribution which you will learn more about later.


## Summary

In this lesson, you learned how to use Matplotlib's basic plotting techniques to visually describe your data as scatter plots, bar graphs, and histograms. You also identified use cases for each of these techniques and learned how to customize and add basic details to a plot. 

# [Customizing Visualizations with Matplotlib](https://colab.research.google.com/gist/bpurdy-ds/136421b81a52be82071eaa468de21518/index.ipynb)

## Introduction

We had a quick introduction to plotting with `matplotlib` in previous lessons. This lesson covers plotting with Python and `matplotlib` using a more structured approach. In this section, we'll look into the components of standard Matplotlib plots used for creating and customizing visualizations. The lesson will also provide you with lots of example code to get you started with data visualization and customizations. 

## Objectives

You will be able to:

* Create a line plot with Matplotlib
* Plot multiple graphs on the same axes
* Customize axes limits and ticks
* Customize line styles and colors
* Understand the distinction between Matplotlib figure and axes
* Create multiple subplots within a Matplotlib figure

Let's first import Matplotlib's `pyplot` module into our working environment along with `numpy` to create sample data.

In Jupyter notebooks, you can use `%matplotlib` magic with `inline` to show plots inside the notebook or `qt` for external/interactive plots. `inline` is recommended for most needs.


```python
# Import pyplot for plotting
import matplotlib.pyplot as plt
# Import numpy to generate some dummy data
import numpy as np
%matplotlib inline
```

We can use numpy's `linspace()` function to quickly generate some dummy data for visualizations.


```python
years = range(1975, 2000)
# Create a numpy array of 25 values from 0 - 1000
data = np.linspace(0, 1000, 25)
data
```




    array([   0.        ,   41.66666667,   83.33333333,  125.        ,
            166.66666667,  208.33333333,  250.        ,  291.66666667,
            333.33333333,  375.        ,  416.66666667,  458.33333333,
            500.        ,  541.66666667,  583.33333333,  625.        ,
            666.66666667,  708.33333333,  750.        ,  791.66666667,
            833.33333333,  875.        ,  916.66666667,  958.33333333,
           1000.        ])



As you can see, this code produced 25 equally spaced numbers from 0 to 1000.

## `matplotlib` Line Plot

Throughout this lesson we'll be using a new type of plot in our examples: a *line plot*.

### What Are Line Plots?

A line plot (or line graph) is a two-dimensional data visualization that is used to represent a trend. The x-axis should represent something that "increases" — either a time measure like seconds, hours, or years or an ordinal measure like finishing places in a competition (1st, 2nd, 3rd, etc.).

Line plots look kind of like scatter plots, except that each point is connected by a trend line.

### Line Plots in Matplotlib

The function to make a line plot in `matplotlib` is just `.plot()` ([documentation here](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.plot.html#matplotlib.axes.Axes.plot)). Let's plot our generated data and set a legend:


```python
# Create the plot
fig, ax = plt.subplots()

# Use plot() function to create a plot using above values
ax.plot(years, data)

# Add a legend to the plot
ax.legend(["Sample Data"]);
```


    
![png](index_files/index_7_0.png)
    


**Note:** Notice the semicolon at the end of the last line. If this is not included, the location in memory of the last object to be created in the graph can be displayed before the graph is displayed.

If you re-run the above cell without the semicolon, you may see something like `<matplotlib.legend.Legend at 0x120f17910>` displayed above the line graph. It doesn't interfere with the plot creation, but it can be distracting to someone reading your notebook.

In order to suppress this print statement, just include a semicolon at the end of the last line of a given visualization!

### Labelling the Plots

With a simple plot as shown above, `matplotlib` also allows users to provide context for the visual information by adding plot titles and labels for axes. The following functions can be used to achieve this:

 - **`ax.set_xlabel("text") / ax.set_ylabel("text")`**: define labels for x and y axes
 - **`ax.set_title("text")`**: define the plot title. 

These functions can be used with the `.legend()` function as we just saw above to add a legend to the plot. The legend function takes an optional keyword argument `loc` that can be used to specify where in the figure the legend is to be drawn. 

 - `ax.legend(["text"], loc=1)`: upper right corner
 - `ax.legend(["text"], loc=2)`: upper left corner
 - `ax.legend(["text"], loc=3)`: lower left corner
 - `ax.legend(["text"], loc=4)`: lower right corner

Let's add some more information to the above plot using these functions below:


```python
# Create the plot
fig, ax = plt.subplots()

# Use plot() function to create a plot using above values
ax.plot(years, data)

# Add labels for x and y axes
ax.set_xlabel('X Axis Label')
ax.set_ylabel('Y Axis Label')

# Add a title for the plot
ax.set_title('PLOT TITLE')

# Add a legend to the plot with legend() in lower right corner
ax.legend(["Sample Data"], loc=4);
```


    
![png](index_files/index_10_0.png)
    


## Multiple Plots on the Same Axes

To plot multiple sets of data on the same axes, simply call multiple plotting methods on the same `ax` object.


```python
# Create more fake data
other_data = data - (data % 150) + 50

# Create the plot
fig, ax = plt.subplots()

# Plot both sets of data
ax.plot(years, data)
ax.plot(years, other_data)

# Add labels for x and y axes
ax.set_xlabel('X Axis Label')
ax.set_ylabel('Y Axis Label')

# Add a title for the plot
ax.set_title('PLOT TITLE')

# Add a legend to the plot with legend() in lower right corner
# Note there are 2 strings in the legend now
ax.legend(["Sample Data", "Other Data"], loc=4);
```


    
![png](index_files/index_12_0.png)
    


It is also possible to plot more than one kind of graph on the same axes. For example, this shows both a line graph and a scatter plot:


```python
# Create fake data
x1 = [1, 4, 6, 8]
y1 = [10, 15, 27, 32]
x2 = [0.5, 2.2, 4.2, 6.5]
y2 = [21, 19, 9, 26]

# Create the plot
fig, ax = plt.subplots()

# Generate a line plot
ax.plot(x1, y1)

# Draw a scatter plot on same axes
ax.scatter(x2, y2)

# Add a legend
ax.legend(["Dataset 1", "Dataset 2"]);
```


    
![png](index_files/index_14_0.png)
    


Be careful when combining plots this way. Consider: *Do they really have the same x and y axis? Why do they need to be represented by two different kinds of plots?*

## Customizing Axes

For these examples, we'll start with this line plot showing an exponential curve:


```python
# Generate data
x = np.arange(101)
y = x**2

# Create the plot
fig, ax = plt.subplots()

# Draw a line graph
ax.plot(x,y)

# Set title to explain what we're doing
ax.set_title("Line Plot with Default Axes");
```


    
![png](index_files/index_17_0.png)
    


### Axis Limits

Sometimes it is helpful (or just aesthetically pleasing) to "zoom in" or "zoom out" of a plot. To do this, set the *limits* of the axes using `set_xlim(min,max)` and/or `set_ylim(min,max)`.

Here is the above graph "zoomed out" some, so there is more whitespace around the edges:


```python
# Create plot, draw graph, set title
fig, ax = plt.subplots()
ax.plot(x,y)
ax.set_title("Zoomed Out")

# Set the limits of x and y to "zoom out"
ax.set_xlim(min(x)-15, max(x)+15)
ax.set_ylim(min(y)-1500, max(y)+1500);
```


    
![png](index_files/index_19_0.png)
    


And here it is "zoomed in" so we are only looking at x values between 80 and 100:


```python
# Create plot, draw graph, set title
fig, ax = plt.subplots()
ax.plot(x,y)
ax.set_title("Zoomed In")

# Set the limits of x and y to "zoom in"
ax.set_xlim(80, 100)
ax.set_ylim(6000, 10000);
```


    
![png](index_files/index_21_0.png)
    


## Axis Ticks

You've seen that you can change the limits of the x and y axes, but you can also change the scales and numbering of the ticks on the axes themselves. You do this via the `.set_xticks()` and `.set_yticks()` methods.

Let's change the default axes so there are 11 ticks on the x-axis 5 ticks on the y-axis. (This would be a relevant technique if more granularity is useful for the x-axis data than the y-axis data.)


```python
# Create plot, draw graph, set title
fig, ax = plt.subplots()
ax.plot(x,y)
ax.set_title("More Ticks on x-axis, Fewer Ticks on y-axis")

# Customize the x and y axis ticks so x-axis has 11 and y-axis has 5
xticks = np.linspace(start=min(x), stop=max(x), num=11)
yticks = np.linspace(start=min(y), stop=max(y), num=5)
ax.set_xticks(xticks)
ax.set_yticks(yticks);
```


    
![png](index_files/index_23_0.png)
    


Axis ticks that go beyond the minimum and maximum of the data can make for poor graphs:


```python
# Create plot, draw graph, set title
fig, ax = plt.subplots()
ax.plot(x,y)
ax.set_title('Displaying Terrible Use of xticks and yticks')

# Customize the x and y axis ticks so the max tick is higher than the max data
xticks = np.linspace(start=min(x), stop=max(x)*2, num=11)
yticks = np.linspace(start=min(y), stop=max(y)*10, num=11)
ax.set_xticks(xticks)
ax.set_yticks(yticks);
```


    
![png](index_files/index_25_0.png)
    


But smaller tick ranges then the data itself will not crop the graph (use `set_xlim` and/or `set_ylim` to crop):


```python
# Create plot, draw graph, set title
fig, ax = plt.subplots()
ax.plot(x,y)
ax.set_title('More Things to Avoid')

# Customize the x and y axis ticks so the max tick is smaller than the max data
xticks = np.linspace(start=min(x), stop=max(x)/2, num=11)
yticks = np.linspace(start=min(y), stop=max(y)/2, num=11)
ax.set_xticks(xticks)
ax.set_yticks(yticks);
```


    
![png](index_files/index_27_0.png)
    


### Customizing Line Styles

The `.plot` function takes additional parameters like `color`, `linewidth`, `linestyle` and `marker` etc. for customization of plots and to "prettify" them. A complete list of arguments can be viewed in the [official documentation](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.plot.html).

For example, with the line graph + scatter plot example from above, here we have customized:

1. X and Y axis limits (to add some whitespace)
2. Color, width, and line style for the line graph
3. Color and marker style for the scatter plot

(Note that the legend automatically reflects the style of the plots.)


```python
# Create the plot
fig, ax = plt.subplots()

# Set the limits of x and y axes
ax.set_xlim(0, 9), ax.set_ylim(5,35)

# Generate a line plot with custom styling
ax.plot(x1, y1, color='lightblue', linewidth=3, linestyle = '-.')

# Draw a scatter plot on same axes with custom styling
ax.scatter(x2, y2, color='red', marker='x')

# Add a legend
ax.legend(["Dataset 1", "Dataset 2"]);
```


    
![png](index_files/index_29_0.png)
    


The following plot summarizes different types of line styles you can draw in Matplotlib:


```python
# Set up data and plot
x = np.arange(0, 10)
fig, ax = plt.subplots(figsize=(12,6))

ax.plot(x, x, color="red", linewidth=0.25)
ax.plot(x, x+2, color="red", linewidth=0.50)
ax.plot(x, x+4, color="red", linewidth=1.00)
ax.plot(x, x+6, color="red", linewidth=2.00)

# possible linestyle options ‘-‘, ‘–’, ‘-.’, ‘:’, ‘steps’
ax.plot(x, x+10, color="green", lw=3, linestyle='-')
ax.plot(x, x+12, color="green", lw=3, ls='-.')
ax.plot(x, x+14, color="green", lw=3, ls=':')

# custom dash
line, = ax.plot(x, x+18, color="black", lw=1.50)
line.set_dashes([5, 10, 15, 10]) # format: line length, space length, ...

# possible marker symbols: marker = '+', 'o', '*', 's', ',', '.', '1', '2', '3', '4', ...
ax.plot(x, x+22, color="blue", lw=3, ls='-', marker='+')
ax.plot(x, x+24, color="blue", lw=3, ls='--', marker='o')
ax.plot(x, x+26, color="blue", lw=3, ls='-', marker='s')
ax.plot(x, x+28, color="blue", lw=3, ls='--', marker='1')

# marker size and color
ax.plot(x, x+32, color="purple", lw=1, ls='-', marker='o', markersize=2)
ax.plot(x, x+34, color="purple", lw=1, ls='-', marker='o', markersize=4)
ax.plot(x, x+36, color="purple", lw=1, ls='-', marker='o', markersize=8, markerfacecolor="red")
ax.plot(x, x+38, color="purple", lw=1, ls='-', marker='s', markersize=8, markerfacecolor="yellow", markeredgewidth=3, markeredgecolor="green");
```


    
![png](index_files/index_31_0.png)
    


## More `matplotlib` Objects

The structure of a plot in `matplotlib` can be generalized as shown below.  
![](https://curriculum-content.s3.amazonaws.com/data-science/images/gplot.png)

### Figure and Axes Objects
Looking at the above image, a **figure** is a top level component that refers to the overall image space. **Axes** are added to the figure to define the area where data is plotted with the `plot()` function seen above. A figure can have a number of components like **title(s)** which may be used to further explain and customize the plot.  Axes have **ticks** and **labels** providing a perspective to the plot.

In this example, we set the color of the figure to be gray and the color of the axes to be blue, to help visually distinguish them:


```python
fig, ax = plt.subplots()

fig.set_facecolor("gray")
fig.suptitle("This is the title of the figure")

ax.set_facecolor("blue")
ax.set_title("This is the title of the axes");
```


    
![png](index_files/index_33_0.png)
    


### Sub-Plots

In all of the examples so far, we have used this syntax to create a single figure with a single axes:

```python
fig, ax = plt.subplots()
```

#### Rows and Columns

We can also create multiple axes (i.e. multiple subplots) within a single figure by specifying the `nrows` and/or `ncols` arguments.

For example, here we are creating 3 side-by-side axes within a figure:


```python
fig, axes = plt.subplots(figsize=(11, 3), ncols=3)
```


    
![png](index_files/index_35_0.png)
    


Here we have 3 axes stacked on top of one another:


```python
fig, axes = plt.subplots(figsize=(3, 11), nrows=3)
```


    
![png](index_files/index_37_0.png)
    


#### Customizing Individual Axes

If you try to apply methods like `set_facecolor` to this `axes` variable, you will get an error message:


```python
axes.set_facecolor("orange")
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-18-28b51014d60b> in <module>
    ----> 1 axes.set_facecolor("orange")
    

    AttributeError: 'numpy.ndarray' object has no attribute 'set_facecolor'


This is because `axes` is a collection of axes objects, not just one.

We can access an individual axes object like this:


```python
fig, axes = plt.subplots(figsize=(11, 3), ncols=3)
axes[1].set_facecolor("orange")
```


    
![png](index_files/index_41_0.png)
    


**Note:** `axes` is a collection of objects stored in a list-like data structure (a NumPy `ndarray`), and like other lists in Python it is "zero indexed": the "first" element in the list is selected with a 0, the "second" element selected with a 1, and so on.

Thus, in order to change the "middle" graph in the line of graphs, we change the "second" object stored in `axes`, by using `axes[1]`.

If we wanted to change the "first" graph, we would change the "first" object stored in axes, by using `axes[0]`.

Alternatively if we don't want to use this `axes[index]` notation every time we want to access a value from within a list, we can "unpack" each axes object into its own uniquely-named variable like this:


```python
fig, (first_ax, second_ax, third_ax) = plt.subplots(figsize=(11, 3), ncols=3)
third_ax.set_facecolor("yellow")
```


    
![png](index_files/index_43_0.png)
    


Whether you use an `axes` variable or unpack the values is up to you — depending on the context of your code, either one might be the cleaner or clearer option.

### Alternative Techniques for Creating Figure and Axes

#### `.add_subplots` Technique

It is also possible to create a figure with `.figure` and add subplots to a figure after the figure has already been created using the `.add_subplots` method. This allows you to create subplots that take up more than one space in the grid.

(Don't worry if this syntax is confusing or you're not able to customize it; we are mainly demonstrating a different syntax that you might see in example code.)


```python
fig = plt.figure(figsize=(10,4))

# Each add_subplot starts with 1, 3 specifying 1 row and 3 cols
# Then the 3rd specifies which "cells" to fill, which are 1-indexed

# This axes fills the left 2/3rds, spanning cell 1 and 2
wide_axes = fig.add_subplot(1, 3, (1, 2))
# This axes fills the right 1/3rd, just filling cell 3
narrow_axes = fig.add_subplot(1, 3, 3)

# 1/3rd includes the axes labels, so the actual plotting area is
# not exactly 1/3rd
```


    
![png](index_files/index_45_0.png)
    


#### "PyPlot" Syntax

So far, all of these examples have used the "object-oriented" syntax, which is the preferred interface for Matplotlib. (The object-oriented syntax uses `fig, ax = plt.subplots()` or `fig = plt.figure()`.)

When you are looking at examples online, you might also encounter the "PyPlot" syntax.

This syntax does not create variables representing the figure and axes directly. Instead, it calls functions on `plt` (the alias we used to import PyPlot) directly with a "state machine" approach. This is a less-flexible technique but it is nevertheless popular in some circles, especially for programmers who are more familiar with MATLAB than Python. You may see examples of the PyPlot syntax in our lessons when we are creating quick graphs, where precise control of the graph is less important and we are just trying to produce an example with the fewest possible lines of code.

Recall the first plot in this lesson. The object-oriented syntax looked like this:

```python
# Create the plot
fig, ax = plt.subplots()

# Use plot() function to create a plot using above values
ax.plot(years, data)

# Add a legend to the plot
ax.legend(["Sample Data"]);
```

The PyPlot syntax to produce the same plot looks like this:


```python
# You don't need to create the plot before adding the line

# Use plot() function to create a plot using above values
plt.plot(years, data)

# Add a legend to the plot
plt.legend(["Sample Data"]);

# You will often see this line in examples, but it isn't 
# needed with %matplotlib inline
# plt.show()
```


    
![png](index_files/index_47_0.png)
    


Note that we saved 1 line of code by using this syntax in this example. However, say we want to reproduce this example:

```python
fig, axes = plt.subplots(figsize=(11, 3), ncols=3)
axes[1].set_facecolor("orange")
```

Now instead of just being able to use the `axes` variable, we have to call `plt.gcf().axes` in order to get the current figure and access its axes:


```python
plt.subplots(figsize=(11, 3), ncols=3)
plt.gcf().axes[1].set_facecolor("orange")
```


    
![png](index_files/index_49_0.png)
    


In general, you want to use the object-oriented syntax when possible, but it's useful to be able to recognize what's happening when you see examples that use the PyPlot syntax.

### Plotting with Subplots

Let's re-draw the above combined line plot and scatter plot in two different subplots.


```python
# Create the plot
fig, (ax1, ax2) = plt.subplots(figsize=(11,4), ncols=2)

# Set different limits of x and y axes for subplots
ax1.set_xlim(0, 9), ax1.set_ylim(7, 35)
ax2.set_xlim(-1, 8), ax2.set_ylim(5, 30)

# On one subplot, plot a line graph
ax1.plot(x1, y1, color='lightblue', linewidth=3, linestyle = '-.')

# On the other subplot, plot a scatter plot
ax2.scatter(x2, y2, color='red', marker='x')

# Add a title to the figure
fig.suptitle("Plots Across Two Subplots", fontsize=24, x=0.44)

# Add a legend to the figure
# (in general, these are quite nitpicky to style and position)
fig.legend(labels=["Dataset 1", "Dataset 2"], loc=(.68, .88));
```


    
![png](index_files/index_52_0.png)
    


Note that it is possible to recreate this using PyPlot syntax, it just makes many of the lines longer:


```python
# Create the plot
plt.subplots(figsize=(11,4), ncols=2)

# Set the limits of x and y axes for both subplots
# If we wanted the same x and y limits for both, we could use:
# plt.xlim(0, 9)
# plt.ylim(5, 35)
plt.gcf().axes[0].set_xlim(0, 9), plt.gcf().axes[0].set_ylim(7, 35)
plt.gcf().axes[1].set_xlim(-1, 8), plt.gcf().axes[1].set_ylim(5, 30)

# On one subplot, plot a line graph
plt.gcf().axes[0].plot(x1, y1, color='lightblue', linewidth=3, linestyle = '-.')

# On the other subplot, plot a scatter plot
plt.gcf().axes[1].scatter(x2, y2, color='red', marker='x')

# Add a title to the figure
plt.gcf().suptitle("Plots Across Two Subplots", fontsize=24, x=0.44)

# Add a legend to the figure
plt.gcf().legend(labels=["Dataset 1", "Dataset 2"], loc=(.68, .88));
```


    
![png](index_files/index_54_0.png)
    


## More Subplots

You can also define a two-dimensional grid of subplots like this:

```python
fig, axes = plt.subplots(ncols=2, nrows=3) # 2 columns, 3 rows
```

From there, you can then plot on the individual subplots by accessing the subplot through the `axes` which is now 2-dimensional:

```python
top_left = axes[0][0]
top_right = axes[0][1]
row2_col1 = axes[1][0]
row2_col2 = axes[1][1]
row3_col1 = axes[2][0]
row3_col2 = axes[2][1]
```

It is possible to loop over these indices more succinctly using floor division and modular arithmetic in a for loop:


```python
# Set up fake data and figure
x = np.linspace(-10, 10, 101)
fig, axes = plt.subplots(nrows=3, ncols=2, figsize=(10,10))
fig.suptitle('Graphs of Various Polynomials')
fig.tight_layout()

for n in range(6):
    # Find the relevant subplot
    row = n//2 # n divided by 2 without the remainder
    col = n%2  # just the remainder of n divided by 2
    ax = axes[row][col]
    
    # Plot x to the power of n
    y = x**n
    ax.plot(x,y)
    ax.set_title('x^{}'.format(n), y=0.85)
```


    
![png](index_files/index_56_0.png)
    


## Other Plotting Functions in `matplotlib`

In this lesson, we used `ax.scatter()` for generating a scatter plot and `ax.plot()` for generating a line plot. The following is a list of other similar functions which can be readily used for visualizing data:

    .plot()           Line plot
    .scatter()        Scatter plot
    .bar()	        Vertical bar graph
    .barh()	       Horizontal bar graph
    .axhline()	    Horizontal line across axes
    .vline()	      Vertical line across axes
    .stackplot()	  Stack plot
    
You'll learn more about these functions in upcoming labs and lessons, and you can find more information in the [Matplotlib axes documentation](https://matplotlib.org/api/axes_api.html#plotting).

## Summary

This lesson provided you with some more experience with plotting in `matplotlib`. We introduced line plots, an additional type of plot used for two-dimensional data. Then the lesson demonstrated how to customize the axes and line style. Next, the lesson dove into the details of figures, axes, and techniques for drawing multiple plots within the same figure. The lesson then ended by providing a quick reference list of further plotting functions. 

# Data Visualization - Best Practices and Common Mistakes

## Introduction

In this lesson, we'll learn some best practices for creating high-quality data visualizations, as well as some common mistakes to avoid!

## Objectives

You will be able to:

* Choose a type of visualization that is appropriate for a given set of data
* Describe how some types of visualizations can be misleading to viewers

## Creating High-Quality Data Visualizations

Creating your own data visualizations can be trickier than it looks. Not because they're hard to code, but because there are so many different stylistic choices you have to make! Most of Data Science is based in math, where there is a probably correct answer. Unfortunately, there is no "right answer" when it comes to building the best data visualization for a given task or project. However, there are some good rules we can follow, and some common mistakes we can avoid. The goal of this lesson is to get you thinking about both of them by looking at some real-world examples. 

## Don't: Use a Pie Chart

From the Wikipedia page on Pie Charts:

> "Pie charts are very widely used in the business world and the mass media. However, they have been criticized, and many experts recommend avoiding them, pointing out that research has shown it is difficult to compare different sections of a given pie chart, or to compare data across different pie charts. Pie charts can be replaced in most cases by other plots such as the bar chart, box plot or dot plots."

This is the _second paragraph_ on the page. What does this tell us? Pie charts are such a bad choice for data visualizations that it's own Wikipedia page starts with a warning against using them!

So why are Pie Charts a bad choice? The simple answer is because humans don't think in radians, and we aren't good at judging the area of a circle. For instance, take a look at the following infographic:

<img src='https://curriculum-content.s3.amazonaws.com/data-science/images/bad_data_viz.png'>

Infographic from [Vox](https://www.vox.com/2014/8/20/6040435/als-ice-bucket-challenge-and-why-we-give-to-charity-donate)

It takes a little while to get a feel for the information this misguided data visualization is trying to get across. It's hard to compare the different items, which is a problem, because the entire goal of this visualization is to show comparisons between the different diseases! 

## Do: Choose the Right Tool for the Job

Consider the following Pie Charts:


<img src='https://curriculum-content.s3.amazonaws.com/data-science/images/piechart.png'>


The pie charts all look pretty much the same. It's hard for us to tell the differences between them, especially when it comes to ranking the different colored sections by size in the each chart. However, when we examine the bar charts below the image, the differences in each become immediately apparent--you couldn't miss them if you tried. 

When deciding what visualization to use, consider what information you're trying to communicate, and then pick the plot that communicates that information in the most obvious manner. 


## Don't: Get Your Percentages Wrong

This one seems like an easy mistake to avoid, but it still happens all the time. Double check your math, and always double check your calculations! Nothing destroys a Data Scientist's credibility in front of a crowd like simple arithmetic errors or visualizations that don't match your numbers. 

Consider the following infographic, and try to figure out what is wrong with it:

<img src='https://curriculum-content.s3.amazonaws.com/data-science/images/new_percentages.png' height="75%" width="75%">


There are two things wrong with this infographic. The first is that the percentages add up to 243%, which makes no sense. We can intuit that respondents were allowed to choose more than one category, but that's too ambiguous on its own, and doesn't tell us anything!

The second issue with this visualization is that the area taken up by each colored section doesn't fit with their corresponding percentages. In a good data visualization, if 78%  of the respondents chose the category represented by purple, then 78% of the person should be purple!  Mismatches like this undermine the message of your visualization because they are confusing and ambiguous. Avoid them!


## Don't: Make Your Visualizations Too Busy or Unique

One of the easier mistakes to make is to make visualizations that simply have so much going on that they are almost impossible to interpret. Consider the line graph below. Take a minute and try to make sense of it.

<img src='https://curriculum-content.s3.amazonaws.com/data-science/images/new_bad-time-series.png' width="600">

Almost impossible, right? Mistakes like this can be avoided by breaking information up into a series of smaller graphs, or by picking a more appropriate type of visualization, when possible. 

Another big mistake is to try and create new, unique visualizations that people haven't seen before. While it may seem like a good idea to get creative, fight the urge. You don't see weird, unique stuff often for a reason--because they don't work well. Stick to formats people are used to. Switching up things to try and be unique can make your visualization confusing, or in the case below, purposefully misleading!


<img src='https://curriculum-content.s3.amazonaws.com/data-science/images/new_gun-deaths-in-FL.png' width="400">

In this visualization, the author broke the common convention of having a line go up as a number goes up. Instead, the line goes down as the number of gun deaths in Florida increases. However, most people that view this visualization leave with the exact opposite impression, because they are paying more attention to the direction of the line than they are to the numbers on the y-axis. That's because we focus on **_Preattentive Attributes_** first!

## Do: Use Preattentive Attributes

**_Preattentive Attributes_** are things that our eyes are drawn to. We can't help but notice them, because our brains are wired to. There will be times when you need a visualization to communicate a specific piece of information, that you want to make as obvious as possible. The best way to do this is to pick the right preattentive attribute to highlight this!

Take a look at some of the examples in the chart below: 


<img src='https://curriculum-content.s3.amazonaws.com/data-science/images/new_preattentive-attributes.png' width="700">

Note that preattentive attributes are not one size fits all. Most of them work well for certain types of data, but not others. Consider the following chart, and refer back to the preattentive attributes listed above and consider how they would look trying to highlight each different type of information. 

## Don't: Use 3D Visualizations

The final mistake we'll cover today is the use of 3D Visualizations. While they may seem like a cool idea, in practice, they are almost always trouble. The reason for this is because they easily cause **_Occlusion_**, which is just a fancy way of saying that the things in front block the things in back so that you can't see them! For example:

<img src='https://curriculum-content.s3.amazonaws.com/data-science/images/new_occlusion.png' width="500">

Note that there may be some times where a 3D visualization may actually be your best choice, but those are almost always going to be related to visualizing a point cloud in a 3D space. If you absolutely have to use a 3D visualization (or any other sort of visualization where occlusion could be a problem), consider changing the opacity of the visualization to make items more see-through. 


## Summary

In this lesson, we saw many examples of bad data visualizations, and learned about how to make great data visualizations by avoiding these mistakes and following the best practices!

# Seaborn

## Introduction

In this lesson, we'll be introduced to a second, more powerful data visualization library, **_Seaborn_**!

## Objectives

You will be able to:

* Construct plots with Seaborn using its pre-built functionality

## What is Seaborn?

[Seaborn](https://seaborn.pydata.org/) is a Data Visualization library that makes it really, really easy to create professional-quality statistical visualizations with only one or two lines of code. Seaborn also makes it really easy to modify the _aesthetics_ of a plot, so that we can make sure all of our visualizations are eye-catching and easy to interpret, which isn't always the case with Matplotlib. 

## Seaborn and Matplotlib

If seaborn is so awesome, you may be wondering why we bothered teaching you Matplotlib at all! The answer is that Seaborn is not a competing library--it's actually built on top of Matplotlib! Whereas Matplotlib provides the basic functionality for creating plots and filling them with different kinds of shapes and colors, Seaborn takes this functionality a step farther by providing a bunch of ready-made mathematical visualizations that are commonly used in Data Science. Best of all, Seaborn is written to be simple to use and easy to understand, so most visualizations only take 1 or 2 lines of code! 

The plot on the left is a standard plot from Matplotlib. The plot on the right is from Seaborn. What a difference!

| <img src='https://curriculum-content.s3.amazonaws.com/data-science/images/ugly_plot.png'> | <img src='https://curriculum-content.s3.amazonaws.com/data-science/images/pretty_plot.png'> |
|---------------------------|-----------------------------|

### When to Use Each

When you're just performing some basic EDA and exploring a dataset, there are times when matplotlib may be most useful to you. If that's the case, don't be afraid to stick to matplotlib. However, Seaborn shines in two particular areas--providing ready-made plots for statistical analysis, and making beautiful plots for presenting to others.  Perhaps, during your EDA, you want to see the regression line between two features. If that's the case, Seaborn should be your choice, because it only takes a single line of code, whereas Matplotlib would be more complicated. 

When it comes to presentations, it is highly recommended to use Seaborn. Whether in a PowerPoint Presentation or just a Jupyter Notebook you'll be making publicly available, Seaborn visualizations are easier on the eyes, and worth the time.  As a rule of thumb, if you plan on showing the plot to other people, consider using Seaborn. 

##  Basic Plots with Seaborn

Like any python library, the first thing we have to do to use Seaborn is to import it. The standard alias for Seaborn is `sns`. Once we've imported Seaborn, most visualizations are as simple as calling the function for the plot we want, and passing in the data and necessary parameters. 

The main parameter you'll need to specify is `data`. This would be where you pass in your DataFrame. Some plots, such as a boxplot, don't need more than that--Seaborn can usually figure the rest out on its own (depending on the shape and complexity of your data). For bivariate plots that show the relationship between two different columns, you'll need to specify which column should be used for the x-axis and which should be used for the y-axis. 

Let's look at some examples from the Seaborn documentation.

### Simple Univariate Boxplot

```python
import seaborn as sns

tips = sns.load_dataset('tips') # Seaborn comes prepackaged with several different datasets that are great for visualizing!

boxplot = sns.boxplot(data=tips["total_bill"])
```

<img src='https://curriculum-content.s3.amazonaws.com/data-science/images/boxplot-1.png'>

### Boxplot Grouped by Categorical Variable

```python
sns.boxplot(x="day", y="total_bill", data=tips)
```

<img src='https://curriculum-content.s3.amazonaws.com/data-science/images/boxplot-2.png'>

### More Complex Boxplot with Nest Grouping of Categorical Variables

```python
sns.boxplot(x="day", y="total_bill", hue="smoker", data=tips, palette="Set3")
```

<img src='https://curriculum-content.s3.amazonaws.com/data-science/images/boxplot-3.png'>

## Regression Plots

One of the coolest features of Seaborn is the ability to create complex plots like **_Regression Plots_**, which automatically perform regression and fit a line to your data. We'll learn to create these ourselves in the next lab--as you'll see, it's quite simple!

<img src='https://curriculum-content.s3.amazonaws.com/data-science/images/regression.png'>

## Summary

In this lesson, we learned all about Seaborn!

