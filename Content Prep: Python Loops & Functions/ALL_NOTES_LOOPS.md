# [Looping Over Collections - Lab](https://colab.research.google.com/gist/bpurdy-ds/25844c0e0f99c9771e558a65f29b7d40/index.ipynb#scrollTo=T2AsRDyeV4Z7)

## Introduction
In this lab, we will be practicing what we know about `for` loops. We will use them to reduce the amount of code we write by hand to iterate through collections. We will use data from the excel file, `cities.xlsx`, that has data on different cities, their populations, and their areas. Finally, we will use this information to plot and compare each city. Let's get started!

## Objectives

You will be able to:

* Use a `for` loop to iterate over a collection

## Identifying When To Use a For Loop

In the last lesson, we worked with some of our travel data.  Additional data has been compiled in the `cities.xlsx` excel spreadsheet. Let's retrieve this data from excel using the Pandas library. Don't worry if Pandas feels unfamiliar, it will be covered in detail later. For now, just follow the provided code and get a feel for what is happening. First, read the information from the excel file as a list of dictionaries, with each dictionary representing a location. Then, assign this list to the variable `cities`.


```python
import pandas as pd
file_name = '/content/sample_data/cities.xlsx'
travel_df = pd.read_excel(file_name)
cities = travel_df.to_dict('records')
```

Next, retrieve the first three city names, stored as the `'City'` attribute of each dictionary, and `'Population'` of each of the cities.  Then plot the names as our `x_values` and the populations as our `y_values` using the `matplotlib` library. Again, don't worry about understanding all of the details behind what `matplotlib` is doing. It will be covered in more detail soon.


```python
import matplotlib.pyplot as plt

%matplotlib inline

x_values = [cities[0]['City'], cities[1]['City'], cities[2]['City']]
y_values = [cities[0]['Population'], cities[1]['Population'], cities[2]['Population']]
 
plt.bar(x_values, y_values)
plt.ylabel('Population')
plt.title('City Populations')
 
plt.show()
```
![image](https://github.com/user-attachments/assets/de2dece9-b94d-4a56-af91-6df03d052f1b)

Of course, as you may have spotted, there is a good amount of repetition in displaying this data.  Just take a look at how we retrieved the data for our `x_values` and `y_values`. And you'll notice that, unless we know the exact number of cities and populations in our excel file, this method of retrieving data might miss some data or try to access values that don't exist. 

We can take a close look at this below:


```python
x_values = [cities[0]['City'], cities[1]['City'], cities[2]['City']]
y_values = [cities[0]['Population'], cities[1]['Population'], cities[2]['Population']]
```

As we can see, if we have any more than 3 lines of data, our `x_values` and `y_values` will be incomplete, and if we had only 2 lines of data, our code would break.

So in this lesson, we will use `for` loop to display information about our travel locations with less repetition and more accuracy.

## Instructions

Before we get into creating graphs from our cities data, let's get a bit more comfortable with the data we are working with. Let's see if we can iterate through just one element (i.e. a city **dictionary** object) to get the **area**. 

#### Input:
```python
buenos_aires = cities[0]
buenos_aires
```
#### Output:
```
{'City': 'Buenos Aires',
 'Country': 'Argentina',
 'Population': 2891000,
 'Area': 4758}
```
#### Input:
```python
# here we want to find just the area of buenos_aires
buenos_aires_area = buenos_aires['Area']

buenos_aires_area
```
#### Output:
```
4758
```
Now that we have a bit more familiarity with our dictionaries, we can move to gathering all the information we need to create our traces. 

Our `cities` list contains information about the top 12 cities.  For our upcoming iteration tasks, it will be useful to have a list of the numbers 0 through 11.  Use what we know about `len` and `range`to generate a list of numbers 0 through 11.  Assign this to a variable called `city_indices`.

#### Input:
```python
city_indices = list(range(len(cities)))
city_indices # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
```
#### Output:
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
```

Now, using the `cities` list, we want to create a list of the names for each city. Loop through each city and append it's name (`'City'`) to the `city_names` list. 

#### Input:
```python
city_names = []

for city in cities:
    city_names.append(city['City'])

city_names  
```
#### Output:
```
['Buenos Aires',
 'Toronto',
 'Pyeongchang',
 'Marakesh',
 'Albuquerque',
 'Los Cabos',
 'Greenville',
 'Archipelago Sea',
 'Walla Walla Valley',
 'Salina Island',
 'Solta',
 'Iguazu Falls']
```

Your task is to assign the variable `names_and_ranks` to a list, with each element equal to the city name and its corresponding rank.  For example, the first element would be, `"1. Buenos Aires"` and the second would be `"2. Toronto"`. Luckily for us, the list of cities that we read from our excel file is already in order by most populous to least. So, all we need to do is add numbers 1 through 12 to the beginning of each city name.

Use a `for` loop and the lists `city_indices` and `city_names` to accomplish this.  We'll need to perform some nifty string interpolation to format our strings properly.  Check out [f-string interpolation](https://www.programiz.com/python-programming/string-interpolation#f) to see how we can pass values into a string.  Remember that list indices start at zero, but we want our `names_and_ranks` list to start at one!

#### Input:
```python
# write a for loop that adds the properly formatted string to the names_and_ranks list
names_and_ranks = []

# Use a for loop to go through city_indices and city_names
for i in city_indices:
    # Remember to add 1 to i because we want the ranks to start at 1
    rank = i + 1
    # Create the string using f-string interpolation
    names_and_ranks.append(f"{rank}. {city_names[i]}")

# Output the results
names_and_ranks
```
#### Output:
```
['1. Buenos Aires',
 '2. Toronto',
 '3. Pyeongchang',
 '4. Marakesh',
 '5. Albuquerque',
 '6. Los Cabos',
 '7. Greenville',
 '8. Archipelago Sea',
 '9. Walla Walla Valley',
 '10. Salina Island',
 '11. Solta',
 '12. Iguazu Falls']
```

#### Input:
```python
# run this cell to check that your output matches the format
print(names_and_ranks[0]) # '1. Buenos Aires'
print(names_and_ranks[1]) # '2. Toronto'
print(names_and_ranks[-1]) # '12. Iguazu Falls'
```

#### Output:
```
1. Buenos Aires
2. Toronto
12. Iguazu Falls
```

Ok, now use another `for` loop to iterate through our list of `cities` and create a new list called `city_populations` that has the population for each city (`Population`).

#### Input:
```python
# use a for loop to iterate through the list of cities with their corresponding population
city_populations = []

for population in cities:
    city_populations.append(population['Population'])

city_populations
```
#### Output:
```
[2891000,
 2800000,
 2581000,
 928850,
 559277,
 287651,
 84554,
 60000,
 32237,
 4000,
 1700,
 0]
```

#### Input:
```python
print(city_populations[0]) # 2891000
print(city_populations[1]) # 2800000
print(city_populations[-1]) # 0
```
#### Output:
```
2891000
2800000
0
```

Great! Now we can begin to plot this data. Again, we'll used `matplotlib` to create a bar graph with our cities and their respective population data. To do this, we use the `.bar()` function and pass in our x-axis and y-axis values, add a label and title, and finally we call the `.show()` function to view our new bar graph. 

> **Note:** In the example below, we are adding a custom rotation for our x-axis labels so that they do not overlap.


```python
plt.bar(names_and_ranks, city_populations)
plt.xticks(rotation='vertical')
plt.ylabel('Population')
plt.title('City Populations')
plt.show()
```
![image](https://github.com/user-attachments/assets/740375c8-200f-4047-bda6-75b2b9489fb9)

Now we want declare a variable called `city_areas` that points to a list of all of the areas of the cities.  Let's use a `for` loop to iterate through our `cities` and have `city_areas` equal to each area of the city.  

#### Input:
```python
# write a for loop that adds the 'Area' of each city to the list city_areas
city_areas = []

for Area in cities:
  city_areas.append(Area['Area'])

city_areas
```
#### Output:
```
[4758, 2731, 3194, 200, 491, 3750, 68, 8300, 33, 27, 59, 672]
```


Now that we have the city areas and populations, let's plot them to see how the size of each city compares to its population. 


```python
plt.bar(names_and_ranks, city_populations)

plt.ylabel('Population')
plt.xlabel('Cities')
plt.title('City Populations')
plt.xticks(rotation='vertical')
 
plt.show()
```
![image](https://github.com/user-attachments/assets/acd54dd4-bd70-484e-8e39-5092a271aade)


```python
plt.bar(names_and_ranks, city_areas)
plt.ylabel('Area')
plt.xlabel('Cities')
plt.title('City Areas')
plt.xticks(rotation='vertical')
 
plt.show()
```
![image](https://github.com/user-attachments/assets/65a5565b-a0a0-4968-a7ce-bcd5a2b744db)

## Summary

In this section we saw how we can use `for` loops to go through elements of a list and perform the same operation on each.  By using `for` loops we were able to reduce the amount of code that we wrote and write more expressive code.

# [While Loops, Break and Continue](https://colab.research.google.com/gist/bpurdy-ds/a53587ed0ae3f75333b4db564ee02ae2/index.ipynb)

## Introduction

Earlier in the course, we learned how to iterate over collections. But is there a way to have a loop **without** a collection to iterate over? Well, another way to create a loop is with **while** loops. We can use a while loop to perform the same action over and over until a condition is no longer `True`. We don't even need an *iterable* or collection to iterate over. We can just define a condition and perform the given code block until the condition is no longer `True`. Pretty cool, right?   

Or what if we would like to have a loop that stops at a certain point? Let's say we only want to collect half of the elements of a list, or stop a list once we find the first matching element? To perform operations like these we'll need `break` and `continue` statements. These statements **control the flow** of our loops and will help us make our loops even more effective.

## Objectives
You will be able to:

* Use a `while` loop
* Use `break` and `continue` to add control flow to a `while` loop


## What is a `while` loop and how does it work?

A `while` loop is just that; a loop! Similar to a `for` loop, except there is no need for a collection to iterate over. Instead, a `while` loop uses a condition to know when to stop executing. When the condition is true, the block inside the while loop is executed. When that condition is false, we exit the while loop and move on to the next piece of our code.

Let's look at an example:


```python
stop_number = 4
while stop_number > 0:
    print(stop_number)
    stop_number -=1
print("The stop_number reached", stop_number, "so the while loop's condition became False and stopped execution")
```

    4
    3
    2
    1
    The stop_number reached 0 so the while loop's condition became False and stopped execution


Note the lack of a `list` or other collection, and that our second print statement only printed after our `stop_number` become 0.

Also, notice that the structure of a `while` loop is such that it could execute for an *unknown* amount of times. For example, if we didn't know the `stop_number` because it changed from time to time, our while loop could execute 100 times or 3. 

For example, if we used a random number using the random library from `numpy`:


```python
import numpy as np
random_num = np.random.randint(1,20)
while random_num > 0:
    random_num -= 1
    print(random_num)
```

    8
    7
    6
    5
    4
    3
    2
    1
    0


However, we know that eventually that number will be less than 0 and the loop will eventually stop. This is of critical importance. A while loop must always have a condition that will stop the loop, otherwise we will have an **infinite** loop. Infinite loops can crash your browser or program if you don't have a way to end it. So, it is very important to make sure your loops have a fairly defined **end** case.

*If you do ever accidentally create an infinite loop, don't worry. Your current Notebook might freeze, and then kill the page to stop the execution. You can then re-open the browser again normally.*

## When To Use While Loops

While loops are fairly straight forward. We use them in instances where we have a **condition** that serves as the point at which we want a process to stop. For example, if we think about our appetite, we should eat until we aren't hungry, right? Some days that might be two slices of pizza, some days that might be 5 slices of pizza (and that is assuming all pizza slices are of equal size, which is a *generous* assumption).

![liz_lemon_eating_pizza](https://curriculum-content.s3.amazonaws.com/data-science/images/liz_lemon_eating_pizza.gif)

In keeping with our food theme, let's see how we can make sure we're drinking enough water during the day using a while loop:


```python
hydration = 0
water = 1 # in gallons
while hydration < 100 and water > 0:
    print('----[sips water]-----')
    water -= .1
    print('ah, that was refreshing')
    hydration += 10
    print('hydration is now at', hydration, '%\n')
```

    ----[sips water]-----
    ah, that was refreshing
    hydration is now at 10 %
    
    ----[sips water]-----
    ah, that was refreshing
    hydration is now at 20 %
    
    ----[sips water]-----
    ah, that was refreshing
    hydration is now at 30 %
    
    ----[sips water]-----
    ah, that was refreshing
    hydration is now at 40 %
    
    ----[sips water]-----
    ah, that was refreshing
    hydration is now at 50 %
    
    ----[sips water]-----
    ah, that was refreshing
    hydration is now at 60 %
    
    ----[sips water]-----
    ah, that was refreshing
    hydration is now at 70 %
    
    ----[sips water]-----
    ah, that was refreshing
    hydration is now at 80 %
    
    ----[sips water]-----
    ah, that was refreshing
    hydration is now at 90 %
    
    ----[sips water]-----
    ah, that was refreshing
    hydration is now at 100 %
    


## On To `break` And `continue` Statements

In the case of `break` and `continue` statements, it is almost best to not overthink. `break` and `continue` essentially do what they sound like. They are used in tandem with conditional statements (`if`, `elif`), inside loops, and they *break* out of a loop if a condition is met or *continue* a loop if a different condition is met. Before we dive too deeply into how these statements function, let's look at an example.


```python
numbers = list(range(0, 30))
new_list = []
for num in numbers:
    if len(new_list) > 4:
        print(f'We have enough even numbers in new_list ({len(new_list)}). break will stop the for loop now')
        break
    elif num % 2 == 0:
        new_list.append(num)
    elif num % 2 != 0:
        continue
        print('i never get executed')
    print(num, 'is even.')
    print('this does not print for odd numbers\nbecause the continue statement skips\nthe code that follows in the for loop\nand goes straight back to the next element in the for loop')
    
```

    0 is even.
    this does not print for odd numbers
    because the continue statement skips
    the code that follows in the for loop
    and goes straight back to the next element in the for loop
    2 is even.
    this does not print for odd numbers
    because the continue statement skips
    the code that follows in the for loop
    and goes straight back to the next element in the for loop
    4 is even.
    this does not print for odd numbers
    because the continue statement skips
    the code that follows in the for loop
    and goes straight back to the next element in the for loop
    6 is even.
    this does not print for odd numbers
    because the continue statement skips
    the code that follows in the for loop
    and goes straight back to the next element in the for loop
    8 is even.
    this does not print for odd numbers
    because the continue statement skips
    the code that follows in the for loop
    and goes straight back to the next element in the for loop
    We have enough even numbers in new_list (5). break will stop the for loop now


So, let's unpack what's happening here. 

First, we have a `for` loop that is iterating over our list, `numbers`, which has 30 numbers in it. Then we see that we have an `if` statement that only executes its code when our `new_list` has more than 4 numbers in it. Once this condition is met, we **break** out of our loop. We then have an `elif` statement that adds any even number to the `new_list`, and a final `elif` statement that tests to see if the number is odd, and if it is odd, then it **continue**s to the next element in our for loop's iteration process. 

So, first let's dig into the `continue` statement. `continue` is telling our loop to **skip** any code that comes after it and go straight to the next element in our loop. So, if we are dealing with number `1` in our list of numbers, we will hit our `continue` statement and immediately go to the next element in our for loop (i.e. `2`). Any code that comes after the `continue` will **not** be executed, **but** our for loop does **not** end execution. This contrasts with the `break` statement. Our break statement is only executed when we have met our condition that the `new_list` has reached the number of elements we want it to have. Once the `break` statement is executed, it will end the execution of the `for` loop altogether. All code after the `break` statement will be ignored, similar to our `continue`, but there will be no next step to the iteration. It stops the loop and that's the end.

So, essentially, we can use `continue` to *skip* operation on elements and code below `continue`. We can then use `break` when we have a condition that tells us we want to stop the process altogether.

We can look at two examples to really reinforce this difference in execution.


```python
for i in list(range(0, 5)):
    if True:
        print(i)
    print("Since we don't have a continue statement,\nI'll always get executed")
```

    0
    Since we don't have a continue statement,
    I'll always get executed
    1
    Since we don't have a continue statement,
    I'll always get executed
    2
    Since we don't have a continue statement,
    I'll always get executed
    3
    Since we don't have a continue statement,
    I'll always get executed
    4
    Since we don't have a continue statement,
    I'll always get executed



```python
for i in list(range(0, 5)):
    if True:
        print(i)
        continue
    print("I'll never get executed")
```

    0
    1
    2
    3
    4



```python
for i in list(range(0, 5)):
    if True:
        print(i)
        break
    print("I'll never get executed either")
```

    0


These examples are a bit contrived but they very clearly show how `continue` and `break` work inside loops and conditional statements as well as the difference between their execution.

## Identify Opportunities to Use Break and Continue

Let's say you have a collection of elements and that you want to filter out certain elements and create a new list with the elements you want. But you also want to perform a complex operation on each of the elements you **do** want. Well, you don't want to perform that operation on the elements that you don't want and you don't want to have to write multiple `for` loops on the collection. So, a `continue` statement would allow you to optimize your performance and avoid needing to perform those operations. And a `break` statement can be used when you want to put a limit on the number of iterations you perform, the number of elements you append to a new list, or even just stop your iteration when you have found the first element you want. Let's take a look:


```python
names = ['aNNE', 'JaNe', 'willIAM', 'WanDA', 'WeSt', 'HELEN', 'tHoMaS', 'HENrY', 'John', 'Marshall', 'May']
formatted_names = []
check_count = 0

for name in names:
    if name.startswith('w') or name.startswith('W'):
        check_count += 1
        continue
    elif len(formatted_names) >= 4:
        check_count += 1
        break
    else:
        formatted_names.append(name.title())

print('before', names)
print('after', formatted_names)
print(check_count)
```

    before ['aNNE', 'JaNe', 'willIAM', 'WanDA', 'WeSt', 'HELEN', 'tHoMaS', 'HENrY', 'John', 'Marshall', 'May']
    after ['Anne', 'Jane', 'Helen', 'Thomas']
    4


Okay, so, as we can tell from our code. We wanted to create a list of 4 names that are properly formatted and that **don't** start with the letter `w`. To optimize our code, we first check to see if the name starts with `w`. If it does, we skip all other operations that we need to do and go to the next name. Next we check to see if we have hit our quota of 4 names. If we have, then stop the iteration altogether. Lastly, if neither condition is met, format the given name and append it to our new list of formatted names.
This way, we are optimizing our code by making sure that we eliminate performing any operations that aren't absolutely necessary at each step. You may have noticed the variable, `check_count`. If you are feeling unconvinced that the `break` and `continue` are not cutting down on the number of times our code is executing, run the cell below and compare the `check_count`s, which increment after **each** check of a conditional statement.


```python
names = ['aNNE', 'JaNe', 'willIAM', 'WanDA', 'WeSt', 'HELEN', 'tHoMaS', 'HENrY', 'John', 'Marshall', 'May']
formatted_names = []
check_count = 0

for name in names:
    if len(formatted_names) < 4:
        check_count += 1
        if not (name.startswith('w') or name.startswith('W')):
            check_count += 1
            formatted_names.append(name.title())
            

print('before', names)
print('after', formatted_names)        
print(check_count)
```

    before ['aNNE', 'JaNe', 'willIAM', 'WanDA', 'WeSt', 'HELEN', 'tHoMaS', 'HENrY', 'John', 'Marshall', 'May']
    after ['Anne', 'Jane', 'Helen', 'Thomas']
    11


See that?! We have cut down on the different checks we perform by more than half (50%)! And on top of that, to get the same result we have to have a **nested** `if` statement, which is, technically put, ***gross***. All joking aside, nested `if` statements should be avoided if they can be since they make our code less readable and therefore harder to maintain on top of being half as efficient as our previous code.

It's important to note that these excess checks could represent much more expensive operations in our code. So, it is important to use `break` and `continue` when it makes sense.

## Summary

Awesome! `while` loops are great, right? We can use them to perform operations based on the truthiness of a condition instead of needing to iterate over the elements in a collection. They provide a more dynamic way to perform operations, but we need to be careful when writing while loops because we need to have a condition that ends the loop. Otherwise we will have an **infinite** loop which will give us and our computer a real headache. In this lesson, we also introduced some *control flow* statements, `break` and `continue`, which allow us to make our conditional statements and the rest of our code more efficient and more readable. We call these statements control flow statements because they allow us to *control* the *flow* of our code's execution. 

# [Using Nested Loops](https://colab.research.google.com/gist/bpurdy-ds/b70b3c4b90c8b51fe400ad391a946d16/index.ipynb)

## Introduction
In this lesson, we will be looking at how to perform nested iteration (or looping). What does this mean exactly? Well, we know that a nested data structure is having one form of data nested inside another. For example, a nested list would be a list that contains another list, or a dictionary that has a key that points to a list.

```python
# nested lists
list_of_lists = [[1,2,3], [4,5,6], [3,5,2]]
dict_nested_list = { 'name': "example", 'colors': ["blue", "green", "yellow", "red"] }
```

So, with that example, we can infer that a nested loop would be a loop inside another loop. Sounds exciting, right? Let's take a look at some nested loops.

## Objectives

You will be able to:

* Use a nested loop when it is appropriate

## Writing A Nested Loop

Working with a nested data structure is a little confusing at first, but after doing it a few times it becomes much less intimidating. The same is true for writing nested loops. They will be somewhat commonplace in our programming future and are important to be comfortable with. 

Basically what happens with a nested loop is the inner loop runs in its entirety **every** iteration of the outer loop. Let's take a look at an example before diving deeper.


```python
outer_numbers = [1,2,3]
inner_words = ["ONE", "TWO", "THREE"]
for number in outer_numbers:
    print(f"this is iteration **{number}** of the OUTER loop")
    for word in inner_words:
        print(f"     this is iteration {word} of the INNER loop")
    print("\n")
```

    this is iteration **1** of the OUTER loop
         this is iteration ONE of the INNER loop
         this is iteration TWO of the INNER loop
         this is iteration THREE of the INNER loop
    
    
    this is iteration **2** of the OUTER loop
         this is iteration ONE of the INNER loop
         this is iteration TWO of the INNER loop
         this is iteration THREE of the INNER loop
    
    
    this is iteration **3** of the OUTER loop
         this is iteration ONE of the INNER loop
         this is iteration TWO of the INNER loop
         this is iteration THREE of the INNER loop
    
    


## How Nested Loops Work

Alright, so, what we see happening here is that the **inner** loop runs through each of its iterations for each iteration of the **outer** loop. If we break this down even further, we can think of the block inside of a loop as a single operation. The current iteration only moves on to the next iteration once it has completed the entire operation. 

So, the operation of the outer loop is to print a string and execute a for loop on the `inner_words` collection. The outer block will do this three times. **BUT** the nested loop has to finish before the next iteration of the outer loop. The nested loop's job is to print its string three times, so that happens for each iteration of the outer loop.

We can nest any and all kinds of loops.


```python
outer = 0
inner = 0
while outer < 3:
    outer += 1
    print("outer iteration:", outer)
    while inner < 3:
        inner += 1
        print("    inner iteration:", inner)
    inner = 0
    print("\n")
```

    outer iteration: 1
        inner iteration: 1
        inner iteration: 2
        inner iteration: 3
    
    
    outer iteration: 2
        inner iteration: 1
        inner iteration: 2
        inner iteration: 3
    
    
    outer iteration: 3
        inner iteration: 1
        inner iteration: 2
        inner iteration: 3
    
    


## Using Nested Loops

Seeing how to use nested loops is great and all, but when do we really use them? Well, as we touched on earlier, nested data structures don't simply provide a convenient way to conceptualize nested loops, they provide a clear use case for them too.

Let's say we have a `list` of `dictionaries` that represent people. People can have attributes that also point to other collections, let's say their pets. So, if we wanted a way to list out the names of all people's pets, this would be a great opportunity to employ a nested loop. Let's take a look at an example.


```python
programmers = [{'name': "rachel", 'favorite_languages': ['Ruby', 'JavaScript', 'SQL', "Java"]},
               {'name': "daniel", 'favorite_languages': ['JavaScript', 'Elixir', 'Python']},
               {'name': "greg", 'favorite_languages': ['C#', 'CoffeeScript', 'R']},
               {'name': "meryl", 'favorite_languages': ['C++', 'PHP', 'Swift']}
              ]
```

So, if we wanted to take the above list of `programmers` and dynamically list out everyone's `favorite_languages` we would need to use two separate loops. 


```python
for programmer in programmers:
    for language in programmer['favorite_languages']:
        print(language)
```

    Ruby
    JavaScript
    SQL
    Java
    JavaScript
    Elixir
    Python
    C#
    CoffeeScript
    R
    C++
    PHP
    Swift


It's possible to get this done without a nested loop, but it would require much more code and would not be nearly as efficient or semantic as the above solution. So, in cases where we're dealing with nested data structures, nesting loops becomes very useful.

## Summary

In this lesson, we introduced nested loops. Nested loops are exactly what they sound like. A loop inside of another. Nested iteration is helpful when dealing with nested collections in cases where we would like to dynamically access and use nested data contained in these collections. Nested loops can quickly become hard to read and maintain, so, it is important to use them wisely and sparingly.

# [Creating Functions](https://colab.research.google.com/gist/bpurdy-ds/a2bcac57c4214877c588087d8688b8d3/index.ipynb)

## Introduction
Now that we learned about loops, it would be nice to have the ability to *reuse* our code to help us solve different problems. Functions allow us to do just that. They also give us the ability to name a sequence of operations (or block of code), thus making our code expressive. Let's see how this works, and why something like this is useful.

## Objectives

You will be able to:

* Declare and use a basic function

## Our problem so far 

Imagine that we have a group of employees who have just joined our company.  


```python
new_employees = ['jim', 'tracy', 'lisa']
```

> Press shift + enter to run this code.

We want to send each of them a nice welcome message.  We could use a `for` loop to create a list of `welcome_messages`.


```python
welcome_messages = []
for new_employee in new_employees:
    welcome_messages.append("Hi " + new_employee.title() + ", I'm so glad to be working with you!" )

welcome_messages
```




    ["Hi Jim, I'm so glad to be working with you!",
     "Hi Tracy, I'm so glad to be working with you!",
     "Hi Lisa, I'm so glad to be working with you!"]



Then a couple of weeks later, a few more employees join, and we want to send messages to them as well.


```python
new_employees = ['steven', 'jan', 'meryl']
```

Well to accomplish welcoming the new employees, we would likely copy our code from above.


```python
welcome_messages = []
for new_employee in new_employees:
    welcome_messages.append("Hi " + new_employee.title() + ", I'm so glad to be working with you!" )
    
welcome_messages
```




    ["Hi Steven, I'm so glad to be working with you!",
     "Hi Jan, I'm so glad to be working with you!",
     "Hi Meryl, I'm so glad to be working with you!"]



If each time we wanted to reuse code we would have to copy and paste the code and maintain a lot more code than is necessary.  Also, each time we recopied it is another opportunity to make a mistake.  So what if there was a way to write that code just one time, yet be able to execute that code wherever and whenever we want?  Functions allow us to do just that.

Here is that same code wrapped in a function: 


```python
def greet_employees():
    welcome_messages = []  # Initializes an empty list `welcome_messages` to store greeting messages.
    for new_employee in new_employees:  # Iterates over each item in the `new_employees` list.
        welcome_messages.append("Hi " + new_employee.title() + ", I'm so glad to be working with you!")  # Formats a greeting for each employee, capitalizes their name, and appends it to `welcome_messages`.

    return welcome_messages  # Returns the list `welcome_messages` containing all the formatted greetings.
    
```

```python

greet_employees() # Calls the `greet_employees` function.

```




    ["Hi Steven, I'm so glad to be working with you!",
     "Hi Jan, I'm so glad to be working with you!",
     "Hi Meryl, I'm so glad to be working with you!"]



> Make sure to press shift + enter for the two cells above.

There are two steps to using a function: defining a function and executing a function.  Defining a function happens first, and afterward when we call `greet_employees()` we execute the function.   


```python
new_employees = ['Jan', 'Joe', 'Avi']
greet_employees()
```




    ["Hi Jan, I'm so glad to be working with you!",
     "Hi Joe, I'm so glad to be working with you!",
     "Hi Avi, I'm so glad to be working with you!"]



Ok, let's break down how to define, or declare, a function.  Executing a function is fairly simple, just type the function's name followed by parentheses.


```python
greet_employees()
```




    ["Hi Jan, I'm so glad to be working with you!",
     "Hi Joe, I'm so glad to be working with you!",
     "Hi Avi, I'm so glad to be working with you!"]



## Declaring and using functions

There are two components to declaring a function: the function signature and the function body.


```python
def name_of_function(): # signature
    words = 'function body' # body
    print(words) # body
```

### Function Signature

The function signature is the first line of the function.  It follows the pattern of `def`, `function name`, `parentheses`, `colon`.

`def name_of_function():`

The `def` is there to tell Python that you are about to declare a function.  The name of the function indicates how to reference and execute the function later.  The colon is to end the function signature and indicate that the body of the function is next.  The parentheses are important as well, and we'll explain their use in a later lesson.

### Function Body

The body of the function is what the function does.  This is the code that runs each time we execute the function.  We indicate that we are writing the function body by going to the next line and indenting after the colon.  To complete the function body we stop indenting.  


```python
def name_of_function(): 
    words = 'function body' # function body
    print(words) # function body    
# no longer part of the function body
```

Let's execute the `name_of_function()` function.


```python
name_of_function()
```

    function body


> Press shift + enter

Did it work?  Kinda.  The lines of our function were run.  But our function did not return anything.  Functions are designed so that everything inside of them stays inside.  So for example, even though we declared the `words` variable, `words` is not available from outside of the function.


```python
words
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-12-730c51b3e7e0> in <module>
    ----> 1 words
    

    NameError: name 'words' is not defined


To get something out of the function, we must use the `return` keyword, followed by what we would like to return.  Let's declare another function called `other_function()` that has a body which is exactly the same, but has a return statement.


```python
def other_function(): # signature
    words = 'returned from inside the function body' # body
    return words
```


```python
other_function()
```




    'returned from inside the function body'



Much better.  So with the return statement we returned the string `'returned from inside the function body'`.

> We will learn more on what is available from inside and outside of the function, so, don't worry if it feels a little confusing right now.

## See it again

Now let's identify the function signature and function body of our original function, `greet_empoyees()`.


```python
def greet_employees(): # function signature
    welcome_messages = [] # begin function body
    for new_employee in new_employees:
        welcome_messages.append("Hi " + new_employee.title() + ", I'm so glad to be working with you!" )

    return welcome_messages # return statement

# no longer in function body
```

As you can see, `greet_employees()` has the same components of a function we identified earlier: the function signature, the function body, and the return statement. Each time we call, `greet_employees()`, all of the lines in the body of the function are run.  However, only the return value is accessible from outside of the function.


```python
greet_employees()
```




    ["Hi Jan, I'm so glad to be working with you!",
     "Hi Joe, I'm so glad to be working with you!",
     "Hi Avi, I'm so glad to be working with you!"]



## Summary

In this lesson we saw how using a function allows us to reuse code without rewriting it.  We saw that to declare a function we first write the function signature, which consists of the `def` keyword, the function name, parentheses, and a colon.  We indicate the body of the function by indenting our code and then writing the code that our function will execute.  To execute the function, we write the function's name followed by parentheses.  Executing the function will run the lines in the body of the function.

# [Functions with Arguments](https://colab.research.google.com/gist/bpurdy-ds/528c84f15a4e7a4158a69366dd5)

## Introduction
Function arguments are a powerful tool in programming.  As we'll see, arguments make our functions more flexible and reusable by explicitly allowing different inputs to be used in a function and changing the output of the function based on these inputs.

When used correctly, function arguments bring clarity to what inputs a function needs to operate, as well as how a function uses these inputs.  

## Objectives

You will be able to:

* Declare and use a function with arguments

### Predictability with arguments

In the previous lesson, we saw that functions were a powerful tool.  They allow us to repeat operations and apply these operations to different data.  For example, take a look at a function called `meet_traveller()`.


```python
def meet_traveller(): 
    welcome_message = "Hi " + traveller.title() + ", I'm so glad we'll be going on the trip together!"
    return welcome_message # return statement
```

The `meet_traveller()` function is designed to generate nice greetings to each new employee.  Do we need anything else to run the function?  How do we know which new employee the function will greet?  Let's run the function and see what happens.


```python
meet_traveller()
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-2-f6a9d4fa9473> in <module>()
    ----> 1 meet_traveller()
    

    <ipython-input-1-0f8a0b87e7e6> in meet_traveller()
          1 def meet_traveller():
    ----> 2     welcome_message = "Hi " + traveller.title() + ", I'm so glad we'll be going on the trip together!"
          3     return welcome_message # return statement


    NameError: name 'traveller' is not defined


The function requires the variable `traveller`, but it's hard to tell that before running the function.  When code requires something to work, we call that something a **dependency**. Below, our function `meet()` depends on a global variable named `traveller` being provided, otherwise it will not work and we'll get the `NameError` we see above. 
Ideally, our function's dependencies would be more explicit than in our `meet_traveller()` function.  Let's adapt this function to make its dependencies more explicit.


```python
def meet(traveller): 
    welcome_message = "Hi " + traveller.title() + ", I'm so glad we'll be going on the trip together!"
    return welcome_message
```

Ok, in the code above we changed the first line of the function, the function signature, to the following:

```def meet(traveller): ```

This tells us, and Python, to not even run the code unless the proper data is provided to our function.  Let's see what this means by calling the function **without** its argument.


```python
meet()
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-4-c60a3be83cb4> in <module>()
    ----> 1 meet()
    

    TypeError: meet() missing 1 required positional argument: 'traveller'


Do you see that error message at the bottom there?  It's pretty explicit about saying that this function requires a positional argument named `traveller`.  

So, by using an argument, the function signature tells us how to run this function.  We refer to the function by its name and then pass through a string representing the `traveller`.


```python
meet('sally')
```




    "Hi Sally, I'm so glad we'll be going on the trip together!"



> **Note:** Before we move on, it is important to note the difference between an **argument** and a **parameter**. We will see these terms **a lot** going forward and having a clear understanding of them is imperative. An **argument** is the data that we pass to a function before execution (i.e. `'sally'` in the example above). However, a **parameter** is the variable we define in the *function signature* (i.e. `traveller` in the example above). So, these two are very similar, but the difference comes down to whether we are talking about the variable we are using in the function *signature* or the actual data we are using when we *execute* the function later. 

### Flexibility

Let's take another look at the `meet()` function. Notice, that the argument operates like a variable in that we can easily alter the data that `traveller` points to. When we pass through the string, `'Sally'`, the function replaces `traveller` with the string `'Sally'`.  


```python
def meet(traveller): 
                              # "sally"
    welcome_message = "Hi " + traveller.title() + ", I'm so glad we'll be going on the trip together!"
    return welcome_message
```

And we can easily change what `traveller` points to just by passing through a different string.


```python
meet('fred')
```




    "Hi Fred, I'm so glad we'll be going on the trip together!"



But notice that the `traveller` argument is only accessible just inside of the function.


```python
traveller
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-8-12a71905bbfe> in <module>()
    ----> 1 traveller
    

    NameError: name 'traveller' is not defined


So by using arguments, we can easily see what a function requires to work, change the output by passing through different data to the function, and ensure that we only have to worry about what our argument is while inside that function. 

Now, we can use functions with arguments to do a lot more than just make some strings more dynamic. Let's say we have a math operation that we need to perform over and over. Let's say, the mean of a list of numbers. We could define a function named `find_the_mean()` that takes in a list and returns a number representing the mean from the list.


```python
def find_the_mean(list_nums): 
    length = len(list_nums)  # Calculates the length of `list_nums` and stores it in the variable `length`.
    total = sum(list_nums)  # Calculates the sum of all elements in `list_nums` and stores it in the variable `total`.
    return total / length  # Returns the mean by dividing `total` by `length`.

```

```python
find_the_mean([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])  # Calls the `find_the_mean` function with a list of numbers from 1 to 10.```




    5.5



Now let's imagine we are looking at a list of populations in a given state or region. Perhaps we would even like to get these numbers in order to compare the mean populations of different areas.


```python
area_one_pops = [10453, 12383, 8034, 800835, 76434, 32394]
find_the_mean(area_one_pops)
```




    156755.5




```python
area_two_pops = [43845, 54930, 59354, 96403, 73492, 729320]
find_the_mean(area_two_pops)
```




    176224.0



Great, so, we can *definitely* find the mean from lists of population. What if we would like to return the list that has the largest mean population? We could write a function that takes **2** arguments that are lists and returns the list that has the greatest mean.


```python
def find_biggest_pop(list_pops_one, list_pops_two):
    mean_one = find_the_mean(list_pops_one)
    mean_two = find_the_mean(list_pops_two)
    if (mean_one > mean_two):
        return print("The first list,", list_pops_one ," has the larger mean population")
    else:
        return print("The second list,", list_pops_two ,"has the larger mean population")
```


```python
find_biggest_pop(area_one_pops, area_two_pops)
```

    The second list, [10453, 12383, 8034, 800835, 76434, 32394] has the larger mean population


Awesome! Going forward, we will be able to use functions and arguments to write code that is much more reusable and concise to model mathematical and statistical equations.

## Summary

In this lesson, we saw some of the benefits of using arguments: they make our functions more flexible and predictable.  Our functions are more flexible as the functions vary based on the argument provided to the function.  Arguments make our functions predictable by making functions more explicit about their dependencies. They also allow us to change the value of an argument which only affects the function's internal values and more directly shows us how the output of our function will vary based on different inputs.  

# [User Input and Output in Python](https://colab.research.google.com/gist/bpurdy-ds/50550af4e7007d580a6658c875b820b0/index.ipynb)

## Introduction

Sometimes, you'll want Python to ask users for a certain input. This is where user inputs can help!

## Objectives 

You will be able to:

* Incorporate input/output functionality in code to allow for user interaction 

## User input in Python

To get user input in Python, you can use the `input()` function. You can store the result in a variable, and use it to your heart's content. Remember that the result you get from the user will be a string, even if they enter a number.

For example, run the following cell:


```python
name = input("Give me your name: ")
print("Your name is " + name)
```

    Give me your name: Billy
    Your name is Billy


When you use the `input()` function, the program waits for the user to type something and press ENTER. Only after the user presses ENTER does the program continue.

## Manipulating strings (a few ways)

What you get from the `input()` function is always a string. What can you do with it?

First, make the string into a number. Let’s say you are 100% positive that the user entered a number. You can turn the string into an integer with the function `int()`. (Later we will see what to do when the user does NOT enter a number and you try to do this. For now, don’t worry about that problem) 

Here is what this looks like:


```python
age = input("Enter your age: ")
age = int(age)
print ("You are", age , "years old" )
```

    Enter your age: 43
    You are 43 years old


Unlike using `+` for string concatenation as seen earlier, we simply use a `,` for joining strings with numbers. You can also convert an `int` to `str` and use concatenation normally: 


```python
print ("You are " + str(age) + " years old")
```

    You are 43 years old


## Example
Let's create a program that asks the user to enter their name, age, and the current year. Print out a message addressed to them that tells them the year that they will turn 100 years old.


```python
name = input("What is your name: ")
age = int(input("How old are you: "))
current_year = int(input("What is the current year: "))
year = str((current_year - age)+100)
print(name + " will be 100 years old in the year " + year)
```

    What is your name: Billy
    How old are you: 43
    what is the current year: 2019
    Billy will be 100 years old in the year 2076


## Summary

This lesson introduced you to character input/output and string manipulation. We also saw how we can take user input, do some basic processing and provide feedback to the user based on the input. 
