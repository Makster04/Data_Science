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
