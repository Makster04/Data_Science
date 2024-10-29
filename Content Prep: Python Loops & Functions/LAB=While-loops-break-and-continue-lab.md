# [While Loops, Break and Continue - Lab](https://colab.research.google.com/gist/bpurdy-ds/3395343dca5ff676700ffc257c904aa2/index.ipynb)

## Introduction
In this lab, we will practice using `while` loops, and `break` and `continue` statements in our code. We will use our control flow statements to iterate through collections and filter out or selectively operate on each element. We'll use `while` loops to perform operations until a given condition is no longer true. 

## Objectives
You will be able to:

* Use a `while` loop
* Use `break` and `continue` to add control flow to a `while` loop

## Instructions

### While Loops

Imagine a person named Agnes is finally ready to achieve her dream of becoming a competitive eater! Because the competition is so fierce, she knows she'll need to do lots of training to become number one.

Her first regiment of training consists of eating pizza. Below is a `for` loop version of her training process. Using your knowledge of `while` loops, translate the pizza eating code below from a `for` loop to a `while` loop.


```python
slices_of_pie = 6
slices_eaten = 0

for slice in range(slices_of_pie):
    print('Another slice eaten!')
    slices_eaten += 1
    print('Now eaten {} slices!'.format(slices_eaten))
```

    Another slice eaten!
    Now eaten 1 slices!
    Another slice eaten!
    Now eaten 2 slices!
    Another slice eaten!
    Now eaten 3 slices!
    Another slice eaten!
    Now eaten 4 slices!
    Another slice eaten!
    Now eaten 5 slices!
    Another slice eaten!
    Now eaten 6 slices!


#### Input:
```python
slices_of_pie = 6
slices_eaten = 0

# add your while loop here that achieves the same results as the for loop above
for slice in range(slices_of_pie):
  print('The slice was eaten')
  slices_eaten += 2  # Increase the count of slices eaten by 2 (instead of 1)
  print('Now eaten {} slices!'.format(slices_eaten))
```
#### Output:
```
The slice was eaten
Now eaten 2 slices!
The slice was eaten
Now eaten 4 slices!
The slice was eaten
Now eaten 6 slices!
The slice was eaten
Now eaten 8 slices!
The slice was eaten
Now eaten 10 slices!
The slice was eaten
Now eaten 12 slices!

```


After a long night of training with pizza, Agnes sleeps like a rock. When she wakes up in the morning, she realizes that her journey is not over. It has only just begun! In the next cell, continue her training; this time she'll be eating pancakes. None of the pancakes are prepared yet, and she wants to determine how much time she'll have left over after making all the pancakes. Here are the important details:

* Agnes has 1468 seconds allotted for breakfast today
* Agnes will be making herself 5 pancakes
* Each pancake takes 27 seconds to cook on each side
* It takes an average of 5 seconds to either flip a pancake, add it or remove it from the pan
* There is only room for one pancake at a time on the frying pan
* Remember there are two sides to every pancake!  

After Agnes cooks the 5 pancakes, how much time will she have left over to eat them? Use a while loop to find out below.

#### Input:
```python
# Initialize variables
time_for_breakfast = 1468  # total time in seconds
number_of_cooked_pancakes = 0  # pancakes cooked

# Constants for cooking process
time_per_side = 27  # seconds per side of the pancake
time_for_action = 5  # seconds to flip, add, or remove pancake
total_pancakes = 5  # number of pancakes to make

# While loop similar to the hydration example
while number_of_cooked_pancakes < 5 and time_for_breakfast > 0:
    # Add pancake to the skillet (5 seconds)
    time_for_breakfast -= time_for_action
    # Cook first side (27 seconds)
    time_for_breakfast -= time_per_side
    # Flip pancake (5 seconds)
    time_for_breakfast -= time_for_action
    # Cook second side (27 seconds)
    time_for_breakfast -= time_per_side
    # Remove pancake from skillet (5 seconds)
    time_for_breakfast -= time_for_action
    # Increment number of cooked pancakes
    number_of_cooked_pancakes += 1

# Print the remaining time after all pancakes are cooked
print(time_for_breakfast)

```
#### Output:
```
1123
```

## For Loops

Fast forward 5 years, and Agnes has become an international competitive eating superstar. Using her starpower, she decides to open up a restaurant chain. As part of a promotional deal, at a grand opening, she tells her fans that if they are part of the first 30 people to the restaurant, there is a 50% chance that they'll receive free food. Agnes executes this by giving each of the first 30 people a number ranging from 0-29. All people who have an even number will receive free food, and all those with odd numbers will sadly remain hungry :(. Use a loop to create two lists below of:

* `hungry_patrons`
* `fed_patrons`

All people will start out in the list of `hungry_patrons`, and only the lucky ones will move to `fed_patrons`.

> **Hint:** You may find the [remove method](https://www.programiz.com/python-programming/methods/list/remove) to be useful for the next problem

#### Input:
```python
# each list should contain 15 elements
# Loop through the list of hungry patrons
line_of_hungry_patrons = list(range(0,30))
fed_patrons = []
# use a for or while loop to feed the hungry patrons who have an even number
for patron in line_of_hungry_patrons[:]:  
# add the patrons with an even number to the fed_patrons list
  if patron % 2 == 0:  
    fed_patrons.append(patron)  # Add even numbered patrons to fed_patrons list
    line_of_hungry_patrons.remove(patron)  # Remove the even numbered patrons from the hungry list

# Output the results
print("Hungry Patrons:", line_of_hungry_patrons)
print("Fed Patrons:", fed_patrons)

```
#### Output:
```
Hungry Patrons: [1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29]
Fed Patrons: [0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28]

```


### `break` And `continue` Statements

Agnes decides that she wants to start creating targeted advertisements for people. Here is a list of customer objects with information about their name, age, job, pet, and pet name. You'll use loops to find people that meet certain requirements for Agnes' targeted marketing. Write `for` loops with conditional statements in conjunction with `break` and `continue` to get the desired output.


```python
people = [
    {'name': "Daniel", 'age': 29, 'job': "Engineer", 'pet': "Cat", 'pet_name': "Gato"}, 
    {'name': "Katie", 'age': 30, 'job': "Teacher", 'pet': "Dog", 'pet_name': "Frank"},
    {'name': "Owen", 'age': 26, 'job': "Sales person", 'pet': "Cat", 'pet_name': "Cosmo"},
    {'name': "Josh", 'age': 22, 'job': "Student", 'pet': "Cat", 'pet_name': "Chat"},
    {'name': "Estelle", 'age': 35, 'job': "French Diplomat", 'pet': "Dog", 'pet_name': "Gabby"},
    {'name': "Gustav", 'age': 24, 'job': "Brewer", 'pet': "Dog", 'pet_name': "Helen"}
]
```

Use a `for` loop to find the first person in the list of people that has a dog as their pet. The iteration count shouldn't exceed 2. In your loop add a print statement that says

```python
 "{person} has a dog! Had to check {number} of records to find a dog owner."

```
The code has been started for you below: 

#### Input:
```python
ffirst_dog_person = []
iteration_count = 0

for person in people:
    iteration_count += 1
    if iteration_count > 2:
        break  # Stop if more than 2 iterations
    if person['pet'] == 'dog':  # Assuming each person has a 'pet' field
        first_dog_person = person
        print(f"{person['name']} has a dog! Had to check {iteration_count} records to find a dog owner.")
        break  # Stop once a dog owner is found
```

Now, use a `for` loop to create a list of all the cat owners who are under the age of 28.

#### Input:
```python
cat_owners = [] 

for person in people:
  if person['pet'] == 'Cat' and person['age'] < 28:
    cat_owners.append(person)
    print(cat_owners)
```
#### Output:
```
[{'name': 'Owen', 'age': 26, 'job': 'Sales person', 'pet': 'Cat', 'pet_name': 'Cosmo'}]
[{'name': 'Owen', 'age': 26, 'job': 'Sales person', 'pet': 'Cat', 'pet_name': 'Cosmo'}, {'name': 'Josh', 'age': 22, 'job': 'Student', 'pet': 'Cat', 'pet_name': 'Chat'}]
```
Use a `for` loop to find the first person who is above 29 years old. Use a print statement to state their name and how old they are.

#### Input:
```python
thirty_something_yr_old = None
# for loop goes here
for person in people:
    if person['age'] > 29:
        print(f"{person['name']} is {person['age']} years old.")
        continue
```
#### Output:
```
Katie is 30 years old.
Estelle is 35 years old.
```

Use a `for` loop to create a list of people's names and another list of pet names for all the **dog owners**.

#### Input:
```python
dog_owner_names = None
dog_names = None
# for loop goes here
for person in people:
  if person['pet'] == 'Dog':
    print(f"{person['name']} has a dog named {person['pet_name']}.")
    continue
```
#### Output:
```python
Katie has a dog named Frank.
Estelle has a dog named Gabby.
Gustav has a dog named Helen.
```

## Level Up 
Use a `for` loop to create a list of odd numbers from the list of numbers from 0 to 100. Each time there is an odd number, add 10 to it and append it to `list_of_odd_numbers_plus_ten`. Stop adding numbers to the list when there are 35 numbers in it. Once you have reached 35 numbers, return the sum of the new list of numbers.

#### Input:
```python
list_of_numbers = list(range(0, 100))
list_of_odd_numbers_plus_ten = []
# use a for loop to create a list of odd numbers from the list of numbers from 0 to 100
# each time there is an odd number, add 10 to it and append it to the list_of_odd_numbers_plus_ten
# stop adding numbers to the list when there are 35 numbers
# use break and continue statements in your code
for number in list_of_numbers:
  if number % 2 != 0:
    number += 10
    list_of_odd_numbers_plus_ten.append(number)
   
    print(number)
  elif len(list_of_odd_numbers_plus_ten) > 34:
    break
    print(number)
    continue
```
#### Output:
```
11
13
15
17
19
21
23
25
27
29
31
33
35
37
39
41
43
45
47
49
51
53
55
57
59
61
63
65
67
69
71
73
75
77
79
```

## Summary

In this lab, we practiced using `while` loops, which continue executing their block of code until the given condition is no longer true. This is useful for instances where we do not have a collection or do not need a collection to solve our problem, especially when we would only like to stop the process according to a certain condition. We then practiced using control flow statements, `break` and `continue`, to selectively operate on elements, append them to new lists, or assign them to new variables.