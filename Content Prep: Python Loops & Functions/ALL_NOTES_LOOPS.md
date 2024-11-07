# [Looping Over Collections](https://colab.research.google.com/gist/bpurdy-ds/d2355a4a06b8fc15a75ad0ea60199d75/index.ipynb)

## Introduction
Loops allow us to iterate over each element in a collection, like a list. Perhaps we could already do that by writing out a line of code for each element in the collection, but that wouldn't be very efficient, would it? No, not at all. With loops, we can write one line of code that operates on each element in a collection. Pretty cool, right? Let's get started!

## Objectives

You will be able to:

- Use a `for` loop to iterate over a collection

## What is a for loop and how do I write one?

A `for` loop in Python, is primarily used for going through elements of a list one by one. We'll use a simple collection with 4 elements `0,1,2,3` as an example. Without a loop, if we wanted to print each element of the list we'd have to write it out like we do below:


```python
zero_to_three = [0, 1, 2, 3]
```


```python
print(zero_to_three[0])
print(zero_to_three[1])
print(zero_to_three[2])
print(zero_to_three[3])
```

    0
    1
    2
    3


> Press shift + enter

In the example above, we are sequentially accessing each index in the list and printing its value (the element). That works well enough, but if our list were 100 elements long it would become extremely tedious. And what if the length of our list were ***unknown***. Spooky, right? 

In fact, it may very often be the case that we don't know the length of the collection we are working with. So, writing all this static code for each element becomes not only unmanageable but impossible.

Let's see how we would do the same operation above with a `for` loop!


```python
for number in zero_to_three:
    print(number)
```

    0
    1
    2
    3


Great! We were able to reproduce the exact same functionality as we had previously. However, in this example, we used only **2** lines of code. 

Now, the `for` loop may look a bit confusing at first, so, let's take a closer look at the syntax. A `for` loop essentially has two necessary components, which we'll refer to as arguments. The first argument is the variable name we are assigning to an element, or in this case, `number`. The second argument is the collection we are iterating over, or in this case, the list `zero_to_three`.

We can give any name to the variable. The important thing to understand here is **it is the reference** to each **element** in the collection. So, when we print `number`, we are printing an element of the collection `zero_to_three`. 

Every `for` loop needs to end the first line with a colon `:`. This indicates the start of the **block** of code. The block is simply the code that we want executed in each iteration of our loop. So, if all we want to do is print each element, then the line that prints the element is our block. Our block is indicated by indenting. So the first line after the colon `:` should be indented. When we want to end our block, we simply stop indenting. Any code following the `for` loop will only be executed after the `for` loop finishes.

> *Remember, the block of code in a `for` loop is executed the same amount of times as there are elements in the collection.*

Let's take a look at changing the variable names and adding more code to our example:


```python
iteration_count = 0
for whatever_we_want in zero_to_three:
    iteration_count += 1
    print("This is iteration:", iteration_count)
    print(whatever_we_want)
print("The for loop is finished now! I am not in the for loop block, which is why I only printed once!")
```

    This is iteration: 1
    0
    This is iteration: 2
    1
    This is iteration: 3
    2
    This is iteration: 4
    3
    The for loop is finished now! I am not in the for loop block, which is why I only printed once!


## Using list elements as indices

In the examples above, we used the elements in our list to perform an operation, which was printing them. We can also use a list of numbers to access elements from another list. Let's take a look at an example.


```python
countries = ['Croatia', 'USA', 'Argentina', 'France', 'Brazil', 'Japan', 'Vietnam']
```


```python
for index in [0,1,2,3,4,5,6]:
    print(index)
    print(countries[index])
```

    0
    Croatia
    1
    USA
    2
    Argentina
    3
    France
    4
    Brazil
    5
    Japan
    6
    Vietnam


So, in the example above, we are still using the elements in the list of numbers from 0 to 7 in our `for` loop, but we are instead using them to access each element of another list. This example is a bit contrived, but perhaps you have two lists that are ordered correctly and have information like the capital cities in one list and the corresponding countries in another. How would we print both of those out in the same line?


```python
countries = ['Croatia', 'USA', 'Argentina', 'France', 'Brazil', 'Japan', 'Vietnam']
cities = ['Zagreb', 'District of Columbia', 'Buenos Aires', 'Paris', 'Rio de Janeiro', 'Tokyo', 'Hanoi']
```


```python
for index in [0,1,2,3,4,5,6]:
    print(cities[index]+",", countries[index])
```

    Zagreb, Croatia
    District of Columbia, USA
    Buenos Aires, Argentina
    Paris, France
    Rio de Janeiro, Brazil
    Tokyo, Japan
    Hanoi, Vietnam


Of course, this does not work if our indices do not match up with the size of our list.


```python
for index in [0,1,2,3,4,5,6,7,8,9,10]:
    print(cities[index]+",", countries[index])
```

    Zagreb, Croatia
    District of Columbia, USA
    Buenos Aires, Argentina
    Paris, France
    Rio de Janeiro, Brazil
    Tokyo, Japan
    Hanoi, Vietnam



    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    Cell In[11], line 2
          1 for index in [0,1,2,3,4,5,6,7,8,9,10]:
    ----> 2     print(cities[index]+",", countries[index])


    IndexError: list index out of range


So, the preferred way of figuring out the number of iterations on a list when you are unsure of its length would be to use the `len` function to calculate the size of the list.


```python
len(countries)
```




    7



Then we can turn this length into a successive list of elements in the following way:   

First, create a range object:


```python
range(0, len(countries))
```




    range(0, 7)



And then convert this into a list:


```python
list(range(0, len(countries)))
```




    [0, 1, 2, 3, 4, 5, 6]



Note that the range object is marking the starting and ending point, and excluding the end.  So this works perfectly:


```python
for index in list(range(0, len(countries))):
    print(cities[index]+",", countries[index])
```

    Zagreb, Croatia
    District of Columbia, USA
    Buenos Aires, Argentina
    Paris, France
    Rio de Janeiro, Brazil
    Tokyo, Japan
    Hanoi, Vietnam


And as we add or subtract countries, we will still be iterating through our list elements.


```python
countries.append('Mexico')
cities.append('Mexico City')
for index in list(range(0, len(countries))):
    print(cities[index]+",", countries[index])
```

    Zagreb, Croatia
    District of Columbia, USA
    Buenos Aires, Argentina
    Paris, France
    Rio de Janeiro, Brazil
    Tokyo, Japan
    Hanoi, Vietnam
    Mexico City, Mexico


> Note: More conventionally, these contrived examples would employ the `enumerate()` method, but that is beyond the scope of the current lesson. At some point in the future, examine how this code snippet works:
```
for idx, item in enumerate(['A', 'B', 'C']):
    print(idx, item)
```

## Iterating through different datatypes

So far our loop variable has always been an element of a list that is a number.  However, our loop variable can represent any data type.  For example, let's have the loop variable represent each of the countries directly:


```python
different_elements = ['A String', ["a", 'list', "of", 5, ["elements"]], {'this': "is a dictionary"}]
for element in different_elements:
    print(element)
```

    A String
    ['a', 'list', 'of', 5, ['elements']]
    {'this': 'is a dictionary'}


Now that we know we can iterate through a list that contains multiple data types, let's explore iterating through a data type that's **not a list**. 

Another collection we commonly will iterate over is a **dictionary**. Dictionaries differ from lists, on a high level, in that elements are **key, value pairs** instead of one single element. So, when we go through each item in a dictionary, we are actually working with a two-part element (with a key & value). Similarly to how we name a variable for the element in a list for a `for` loop, we name a variable for both the **key** and **value** when we iterate over a dictionary. However, in Python, we can't iterate directly over the dictionary, we iterate over the **items** of a dictionary, which are the key-value pairs.  Let's take a look at an example.


```python
example_dictionary = {'first_name': "Terrance", 'last_name': "KOAR", 'favorite_language': "Python"}
print(example_dictionary.items())
type(example_dictionary.items())
```

    dict_items([('first_name', 'Terrance'), ('last_name', 'KOAR'), ('favorite_language', 'Python')])





    dict_items



Here we can see this **dict_items** object looks almost like a list, but each item has **two** parts, the **key** and **value**. So, in our first iteration, the first **key** will be **first_name**, and the first **value** will be **Terrance**.


```python
for key, value in example_dictionary.items():
    print("this is the key:", key)    
    print("this is the value:", value, "\n")
```

    this is the key: first_name
    this is the value: Terrance 
    
    this is the key: last_name
    this is the value: KOAR 
    
    this is the key: favorite_language
    this is the value: Python 
    


So, we can see that the **dict_items** object groups the key values together in a way that we can iterate over them and access them. We can even use them to inform our program to operate on keys and values in a certain way. Such as, the last name is inexplicably in all caps. Let's look at how we can rectify that and title case the last name when we print out the full name of the `example_dictionary` object.


```python
first_name = ""
last_name = ""
for key, value in example_dictionary.items():
    if key == "last_name":
        last_name = value.title()
    if key == "first_name":
        first_name = value
print(first_name, last_name)
```

    Terrance Koar


## Conventional Naming Patterns

Typically, when we are looping through a collection of things like `countries`, we will name the looping variable, `country`, since that is the singular version of the plural name that represents our list. This is convention and helps to not only remind us, but tell other people looking at our code what that variable is. Let's take a look at a couple examples.


```python
for country in countries:
    print(country)
```

    Croatia
    USA
    Argentina
    France
    Brazil
    Japan
    Vietnam
    Mexico



```python
ice_cream_flavors = ['Mint Chocolate Chip', 'Coffee', 'Cookie Dough', 'Fudge Mint Brownie', 'Vanilla Bean']
for ice_cream_flavor in ice_cream_flavors:
    print('I love ' + ice_cream_flavor + ' ice cream!!')
```

    I love Mint Chocolate Chip ice cream!!
    I love Coffee ice cream!!
    I love Cookie Dough ice cream!!
    I love Fudge Mint Brownie ice cream!!
    I love Vanilla Bean ice cream!!


## Summary

In this lesson, we learned how to use loops to iterate through a collection of elements. We started with iterating through a list of numbers, and performed the same operation on each number. Then we saw how we can loop through the numbers and have each number be used to access a successive element from a separate list, like `countries`.  We then saw that to ensure our list of numbers matched the indices of our other list, we had to use the expression, `for element in list(range(0, len(list)))`. Finally, we introduced a naming convention that is commonly used when naming the variable for our loops when iterating over a collection that is a list of common elements (i.e. `ice_cream_flavor` for a list of `ice_cream_flavors`).

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
