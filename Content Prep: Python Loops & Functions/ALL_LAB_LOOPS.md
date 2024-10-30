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

# Using Nested Loops - Lab

## Introduction
In this lab, you'll practice using nested loops to iterate over nested data structures and create new collections. To do this, you'll be using data from a soccer match to practice our nested loops.

## Objectives

You will be able to:

* Use a nested loop when it is appropriate

## Instructions

Use nested loops and the below object, `soccer_match`, to complete the following prompts and get the desired return values.


```python
# Run this cell without changes
soccer_match = [
  { "home_team": True,
    "away_team": False,
    "country": "France",
    "num_passes": 484,
    "passes_completed": 423,
    "fouls_committed": 16,
    "colors": ["blue", "white", "red"],
    "players": [
      {
        "name": "Hugo LLORIS",
        "captain": True,
        "shirt_number": 1,
        "position": "Goalie"
      },
      {
        "name": "Benjamin PAVARD",
        "captain": False,
        "shirt_number": 2,
        "position": "Defender"
      },
      {
        "name": "Raphael VARANE",
        "captain": False,
        "shirt_number": 4,
        "position": "Defender"
      },
      {
        "name": "Samuel UMTITI",
        "captain": False,
        "shirt_number": 5,
        "position": "Defender"
      },
      {
        "name": "Paul POGBA",
        "captain": False,
        "shirt_number": 6,
        "position": "Midfield"
      },
      {
        "name": "Antoine GRIEZMANN",
        "captain": False,
        "shirt_number": 7,
        "position": "Forward"
      },
      {
        "name": "Kylian MBAPPE",
        "captain": False,
        "shirt_number": 10,
        "position": "Forward"
      },
      {
        "name": "Ousmane DEMBELE",
        "captain": False,
        "shirt_number": 11,
        "position": "Forward"
      },
      {
        "name": "Corentin TOLISSO",
        "captain": False,
        "shirt_number": 12,
        "position": "Midfield"
      },
      {
        "name": "Ngolo KANTE",
        "captain": False,
        "shirt_number": 13,
        "position": "Midfield"
      },
      {
        "name": "Lucas HERNANDEZ",
        "captain": False,
        "shirt_number": 21,
        "position": "Defender"
      }
    ],
  },
  { "home_team": False,
    "away_team": True,
    "country": "Australia",
    "num_passes": 390,
    "passes_completed": 332,
    "fouls_committed": 19,
    "colors": ["green", "gold"],
    "players": [
      {
        "name": "Mathew RYAN",
        "captain": False,
        "shirt_number": 1,
        "position": "Goalie"
      },
      {
        "name": "Mark MILLIGAN",
        "captain": False,
        "shirt_number": 5,
        "position": "Defender"
      },
      {
        "name": "Mathew LECKIE",
        "captain": False,
        "shirt_number": 7,
        "position": "Forward"
      },
      {
        "name": "Robbie KRUSE",
        "captain": False,
        "shirt_number": 10,
        "position": "Forward"
      },
      {
        "name": "Andrew NABBOUT",
        "captain": False,
        "shirt_number": 11,
        "position": "Forward"
      },
      {
        "name": "Aaron MOOY",
        "captain": False,
        "shirt_number": 13,
        "position": "Midfield"
      },
      {
        "name": "Mile JEDINAK",
        "captain": True,
        "shirt_number": 15,
        "position": "Midfield"
      },
      {
        "name": "Aziz BEHICH",
        "captain": False,
        "shirt_number": 16,
        "position": "Defender"
      },
      {
        "name": "Joshua RISDON",
        "captain": False,
        "shirt_number": 19,
        "position": "Defender"
      },
      {
        "name": "Trent SAINSBURY",
        "captain": False,
        "shirt_number": 20,
        "position": "Defender"
      },
      {
        "name": "Tom ROGIC",
        "captain": False,
        "shirt_number": 23,
        "position": "Midfield"
      }
    ]
  }
]
```

Let's take a look at some properties of this nested data structure:


```python
# Run this cell without changes

print("Information about soccer_match")
print("Type:", type(soccer_match))
print("Length:", len(soccer_match))
print()

print("Information about soccer_match[0]:")
print("Type:", type(soccer_match[0]))
print("Length:", len(soccer_match[0]))
print("Keys:", soccer_match[0].keys())
print("Values:", soccer_match[1].values())
```
#### Output:
```
Information about soccer_match
Type: <class 'list'>
Length: 2

Information about soccer_match[0]:
Type: <class 'dict'>
Length: 8
Keys: dict_keys(['home_team', 'away_team', 'country', 'num_passes', 'passes_completed', 'fouls_committed', 'colors', 'players'])
Values: dict_values([False, True, 'Australia', 390, 332, 19, ['green', 'gold'], [{'name': 'Mathew RYAN', 'captain': False, 'shirt_number': 1, 'position': 'Goalie'}, {'name': 'Mark MILLIGAN', 'captain': False, 'shirt_number': 5, 'position': 'Defender'}, {'name': 'Mathew LECKIE', 'captain': False, 'shirt_number': 7, 'position': 'Forward'}, {'name': 'Robbie KRUSE', 'captain': False, 'shirt_number': 10, 'position': 'Forward'}, {'name': 'Andrew NABBOUT', 'captain': False, 'shirt_number': 11, 'position': 'Forward'}, {'name': 'Aaron MOOY', 'captain': False, 'shirt_number': 13, 'position': 'Midfield'}, {'name': 'Mile JEDINAK', 'captain': True, 'shirt_number': 15, 'position': 'Midfield'}, {'name': 'Aziz BEHICH', 'captain': False, 'shirt_number': 16, 'position': 'Defender'}, {'name': 'Joshua RISDON', 'captain': False, 'shirt_number': 19, 'position': 'Defender'}, {'name': 'Trent SAINSBURY', 'captain': False, 'shirt_number': 20, 'position': 'Defender'}, {'name': 'Tom ROGIC', 'captain': False, 'shirt_number': 23, 'position': 'Midfield'}]])
```

Before looking at the answer below, try to identify: **what does `soccer_match` represent overall, and what does each record within `soccer_match` represent?**

.

.

.

*`soccer_match` represents a soccer match (game) containing a home team and an away team. Each record within `soccer_match` represents a team that participated in the match, and their associated stats.*

## Countries: A List of Strings

In the cell below, iterate over the `soccer_match` list to create a new list with the name of the country for each team. 

#### Input:
```python
countries = []

# Iterate over each team in soccer_match
for team in soccer_match:
    # Append the country of the current team to the countries list
    countries.append(team["country"])

countries # ['France', 'Australia']
```
#### Output:
```
['France', 'Australia']
```

## Colors: Another List of Strings!

In the cell below, iterate over the `soccer_match` list to create a new list with the colors for each team.

This should be only one list containing strings for each of the country's colors, not a list of lists.

#### Input:
```python
colors = []

# Iterate over each team in the soccer_match
for team in soccer_match:
    # Iterate over each color in the current team's colors
    for color in team["colors"]:
        # Append each color to the colors list
        colors.append(color)

colors  # ['blue', 'white', 'red', 'green', 'gold']
```
#### Output:
```
['blue', 'white', 'red', 'green', 'gold']
```

## Players: A List of Dictionaries

This time, iterate over the `soccer_match` list to create a new list with the players from each team. `players` should be a single list containing the dictionaries for each of the country's players.

#### Input:
```python
# Iterate over each team in soccer_match
for team in soccer_match:
    # Iterate over each player in the current team's players
    for player in team["players"]:
        # Append each player dictionary to the players list
        players.append(player)

print(players)
```
#### Output:
```
[{'name': 'Hugo LLORIS', 'captain': True, 'shirt_number': 1, 'position': 'Goalie'}, {'name': 'Benjamin PAVARD', 'captain': False, 'shirt_number': 2, 'position': 'Defender'}, {'name': 'Raphael VARANE', 'captain': False, 'shirt_number': 4, 'position': 'Defender'}, {'name': 'Samuel UMTITI', 'captain': False, 'shirt_number': 5, 'position': 'Defender'}, {'name': 'Paul POGBA', 'captain': False, 'shirt_number': 6, 'position': 'Midfield'}, {'name': 'Antoine GRIEZMANN', 'captain': False, 'shirt_number': 7, 'position': 'Forward'}, {'name': 'Kylian MBAPPE', 'captain': False, 'shirt_number': 10, 'position': 'Forward'}, {'name': 'Ousmane DEMBELE', 'captain': False, 'shirt_number': 11, 'position': 'Forward'}, {'name': 'Corentin TOLISSO', 'captain': False, 'shirt_number': 12, 'position': 'Midfield'}, {'name': 'Ngolo KANTE', 'captain': False, 'shirt_number': 13, 'position': 'Midfield'}, {'name': 'Lucas HERNANDEZ', 'captain': False, 'shirt_number': 21, 'position': 'Defender'}, {'name': 'Mathew RYAN', 'captain': False, 'shirt_number': 1, 'position': 'Goalie'}, {'name': 'Mark MILLIGAN', 'captain': False, 'shirt_number': 5, 'position': 'Defender'}, {'name': 'Mathew LECKIE', 'captain': False, 'shirt_number': 7, 'position': 'Forward'}, {'name': 'Robbie KRUSE', 'captain': False, 'shirt_number': 10, 'position': 'Forward'}, {'name': 'Andrew NABBOUT', 'captain': False, 'shirt_number': 11, 'position': 'Forward'}, {'name': 'Aaron MOOY', 'captain': False, 'shirt_number': 13, 'position': 'Midfield'}, {'name': 'Mile JEDINAK', 'captain': True, 'shirt_number': 15, 'position': 'Midfield'}, {'name': 'Aziz BEHICH', 'captain': False, 'shirt_number': 16, 'position': 'Defender'}, {'name': 'Joshua RISDON', 'captain': False, 'shirt_number': 19, 'position': 'Defender'}, {'name': 'Trent SAINSBURY', 'captain': False, 'shirt_number': 20, 'position': 'Defender'}, {'name': 'Tom ROGIC', 'captain': False, 'shirt_number': 23, 'position': 'Midfield'}]
```

## Captains: Another List of Dictionaries!

Iterate over the `soccer_match` list to create a new list with the captains from each team.

This should be a single list containing the dictionaries for each of the countries' captains.

#### Input:
```python
captains = []

for team in soccer_match: #iteriate through each team in soccer_match
  for player in team["players"]: # iteriate player in each team
    if player["captain"] == True: #Only append each player that is labeld True on Captain 
      captains.append(player)

captains # One captain per team:

# [{'name': 'Hugo LLORIS',
#   'captain': True,
#   'shirt_number': 1,
#   'position': 'Goalie'},
#  {'name': 'Mile JEDINAK',
#   'captain': True,
#   'shirt_number': 15,
#   'position': 'Midfield'}]
```
#### Output:
```
[{'name': 'Hugo LLORIS',
  'captain': True,
  'shirt_number': 1,
  'position': 'Goalie'},
 {'name': 'Mile JEDINAK',
  'captain': True,
  'shirt_number': 15,
  'position': 'Midfield'}]
```

## Home Team Players: A Third List of Dictionaries

Iterate over the `soccer_match` list to create a new list with the players from ONLY the home team.

Do not "hard-code" which team this is; use the `'home_team'` key.

#### Input:
```python
home_team_players = []

for team in soccer_match: # Iterate through teams in soccer_match
  if team["home_team"]: # Make it print out only things related to "home_team"
    for player in team["players"]: # Iterate through players in ONLY home_team
      home_team_players.append(player)

home_team_players


# [{'name': 'Hugo LLORIS',
#   'captain': True,
#   'shirt_number': 1,
#   'position': 'Goalie'},
#  ...
#  {'name': 'Lucas HERNANDEZ',
#   'captain': False,
#   'shirt_number': 21,
#   'position': 'Defender'}]
```
#### Output:
```
[{'name': 'Hugo LLORIS',
  'captain': True,
  'shirt_number': 1,
  'position': 'Goalie'},
 {'name': 'Benjamin PAVARD',
  'captain': False,
  'shirt_number': 2,
  'position': 'Defender'},
 {'name': 'Raphael VARANE',
  'captain': False,
  'shirt_number': 4,
  'position': 'Defender'},
 {'name': 'Samuel UMTITI',
  'captain': False,
  'shirt_number': 5,
  'position': 'Defender'},
 {'name': 'Paul POGBA',
  'captain': False,
  'shirt_number': 6,
  'position': 'Midfield'},
 {'name': 'Antoine GRIEZMANN',
  'captain': False,
  'shirt_number': 7,
  'position': 'Forward'},
 {'name': 'Kylian MBAPPE',
  'captain': False,
  'shirt_number': 10,
  'position': 'Forward'},
 {'name': 'Ousmane DEMBELE',
  'captain': False,
  'shirt_number': 11,
  'position': 'Forward'},
 {'name': 'Corentin TOLISSO',
  'captain': False,
  'shirt_number': 12,
  'position': 'Midfield'},
 {'name': 'Ngolo KANTE',
  'captain': False,
  'shirt_number': 13,
  'position': 'Midfield'},
 {'name': 'Lucas HERNANDEZ',
  'captain': False,
  'shirt_number': 21,
  'position': 'Defender'}]

```


## Away Team Forwards: Yup, a List of Dictionaries

Iterate over the `soccer_match` list to create a new list with the information for each of the away team players whose `position` is `"Forward"`.

#### Input:
```python

# Iterate through teams in soccer_match
for team in soccer_match:
    # Check if the current team is the away team
    if team["away_team"]:
        # Iterate through players in the away team
        for player in team["players"]:
            # Check if the player's position is "Forward"
            if player["position"] == "Forward":
                # Append player to the list if they are a Forward
                away_team_forwards.append(player)

# Output the list of away team forwards
print(away_team_forwards)


away_team_forwards
# [{'name': 'Mathew LECKIE',
#   'captain': False,
#   'shirt_number': 7,
#   'position': 'Forward'},
#  {'name': 'Robbie KRUSE',
#   'captain': False,
#   'shirt_number': 10,
#   'position': 'Forward'},
#  {'name': 'Andrew NABBOUT',
#   'captain': False,
#   'shirt_number': 11,
#   'position': 'Forward'}]
```
#### Output:
```
[{'name': 'Mathew LECKIE', 'captain': False, 'shirt_number': 7, 'position': 'Forward'}, {'name': 'Robbie KRUSE', 'captain': False, 'shirt_number': 10, 'position': 'Forward'}, {'name': 'Andrew NABBOUT', 'captain': False, 'shirt_number': 11, 'position': 'Forward'}]
```
## Player with the Highest Number

Iterate over the `soccer_match` list and find the player with the highest `shirt_number`.  
Store this player's information in the `player_with_highest_num` variable.

#### Input:
```python
player_with_highest_num = None

# Iterate through teams in soccer_match

for team in soccer_match:
    # Iterate through players in each team
    for player in team["players"]:
        # Check if player_with_highest_num is None or if the current player's shirt number is higher
        if player_with_highest_num is None or player["shirt_number"] > player_with_highest_num["shirt_number"]:
            # Update player_with_highest_num to the current player
            player_with_highest_num = player

# Output the player with the highest shirt number
player_with_highest_num

# {'name': 'Tom ROGIC',
#  'captain': False,
#  'shirt_number': 23,
#  'position': 'Midfield'}
```
#### Output:
```
{'name': 'Tom ROGIC',
 'captain': False,
 'shirt_number': 23,
 'position': 'Midfield'}
```

## Player Names: A Cleaned List

Notice that the players oddly have their last names in all caps. Create a list of all the names of the players in this match. Be sure to make sure their first and last names are properly capitalized (first letter upper case, proceeding letters lower case), as opposed to how they are currently formatted.

#### Input:
```python
player_names = []

# Iterate through teams in soccer_match
for team in soccer_match:
    # Iterate through players in each team
    for player in team["players"]:
        # Use .title() to format the player's name properly (Capitalizing both letters)
        formatted_name = player["name"].title()

        # Append the formatted name to player_names list
        player_names.append(formatted_name)

# Output the list of formatted player names
player_names

# ['Hugo Lloris',
#  'Benjamin Pavard',
#  'Raphael Varane',
#  'Samuel Umtiti',
#  'Paul Pogba',
#  'Antoine Griezmann',
#  'Kylian Mbappe',
#  'Ousmane Dembele',
#  'Corentin Tolisso',
#  'Ngolo Kante',
#  'Lucas Hernandez',
#  'Mathew Ryan',
#  'Mark Milligan',
#  'Mathew Leckie',
#  'Robbie Kruse',
#  'Andrew Nabbout',
#  'Aaron Mooy',
#  'Mile Jedinak',
#  'Aziz Behich',
#  'Joshua Risdon',
#  'Trent Sainsbury',
#  'Tom Rogic']
```
#### Output:
```
['Hugo Lloris',
 'Benjamin Pavard',
 'Raphael Varane',
 'Samuel Umtiti',
 'Paul Pogba',
 'Antoine Griezmann',
 'Kylian Mbappe',
 'Ousmane Dembele',
 'Corentin Tolisso',
 'Ngolo Kante',
 'Lucas Hernandez',
 'Mathew Ryan',
 'Mark Milligan',
 'Mathew Leckie',
 'Robbie Kruse',
 'Andrew Nabbout',
 'Aaron Mooy',
 'Mile Jedinak',
 'Aziz Behich',
 'Joshua Risdon',
 'Trent Sainsbury',
 'Tom Rogic']
```

## Summary

In this lab, you practiced using nested loops to iterate through a nested data structure using data from a soccer match. Nested data structures can be quite complicated and it can become difficult to access more nested data. With nested loops, you are able to dynamically access this nested data and work with it as you would with a flatter data structure. It is important to think about the structure of the data before and while you're working so you know exactly what data you are working with at each level.

# Creating Functions - Lab

## Introduction

As you know, we can use functions to name snippets of our code, thus making our code more expressive. We can also use functions to allow us to reuse our code. In this lab we will practice using functions for both of those purposes.

## Objectives

You will be able to:

* Declare and use a basic function

## Instructions: 
### Writing our first functions

Imagine we are creating a list of travel destinations -- which can really turn out to be a full time job if we like to travel. We have our list of `travel_destinations` which we assign below. Write a function called `number_of_destinations()` that returns the number of destinations we have on our list.

#### Input:
```python
# List of travel destinations
travel_destinations = ['argentina', 'mexico', 'italy', 'finland', 'canada', 'croatia']
# Function to return the number of destinations
def number_of_destinations():
    return len(travel_destinations)

number_of_destinations() # Expected output: 6
```
> Below, remove the first `#` to uncomment the following line(s) of code and then press `shift` + `enter` to run the cell

#### Output:
```
6
```

Now write another function called `next_up()` that returns our first destination (the destination with the lowest index), in the `list_of_destinations` list.


```python
def next_up():
    return list_of_destinations[0]
```

Next, run your new function


```python
list_of_destinations = ['argentina', 'canada', 'croatia']

next_up()
# Expected output: 'argentina'
```
#### Output:
```
'argentina'
```

Ok, now write a function called `favorite_destination()` that returns the string `'madagascar'`.


```python
def favorite_destination():
    return 'madagascar'
```

Next, run your new function


```python
favorite_destination()
# Expected output:'madagascar'
```
#### Output:
```
'madagascar'
```
Again, let's declare a list called `favorite_destinations`. Write a new function called `add_favorite_destination()` that adds the string `'madagascar'` to the end of `favorite_destinations` and also returns the string `'madagascar'`.


```python
def add_favorite_destination():
    favorite_destinations.append('madagascar')
    return 'madagascar'
```

Next, run your new function

```python
favorite_destinations = ['argentina', 'mexico', 'italy', 'finland', 'canada', 'croatia']

add_favorite_destination()  
print(favorite_destinations)

favorite_destinations[-1] 
```
#### Output:
```
['argentina', 'Mexico', 'italy', 'finland', 'canada', 'croatia', 'madagascar']

'madagascar'
```
Now let's write another function called `capitalize_countries()` which iterates through the list of `capitalized_destinations` and capitalizes the first letter of each word. It should return a list of capitalized destinations.


```python
capitalized_destinations = ['argentina', 'mexico', 'italy', 'finland', 'canada', 'croatia']
# define function here
def capitalize_countries():
    return [country.capitalize() for country in capitalized_destinations] # Use a list comprehension to capitalize each country
```

Next, run your new function


```python
print(capitalize_countries()) # ['Argentina', 'Mexico', 'Italy', 'Finland', 'Canada', 'Croatia']
```
#### Output:
```
['Argentina', 'Mexico', 'Italy', 'Finland', 'Canada', 'Croatia']
```

Great! Now if someone adds a country that is lowercased to our list of destinations, we can simply call our function again to capitalize each of the destinations in the list.

## Summary

Great job! In this lab we were able to get practice both creating and returning values from functions.

# Functions With Arguments - Lab

## Introduction
In this lesson, we have decided to visit one of our travel destinations! This time we have chosen to visit Albuquerque, but we aren't very familiar with this city and are quite hungry after our long flight. We will be working with information we pulled from the Yelp database to help us find a restaurant where we can satisfy our hunger. While Yelp is great for learning about what to do in Albuquerque, it gives us back a lot of information. We'll use what we know about functions and dictionaries to format and read our data more easily. 

## Objectives

You will be able to:

* Declare and use a function with arguments

## Exploring Two Restaurants in Albuquerque

Let's take a quick look at the information Yelp provides for a single restaurant:


```python
# Run this cell without changes
fork_fig = {'categories': [{'alias': 'burgers', 'title': 'Burgers'},
  {'alias': 'sandwiches', 'title': 'Sandwiches'},
  {'alias': 'salad', 'title': 'Salad'}],
 'coordinates': {'latitude': 35.10871, 'longitude': -106.56739},
 'display_phone': '(505) 881-5293',
 'distance': 3571.724649307866,
 'id': 'fork-and-fig-albuquerque',
 'image_url': 'https://s3-media1.fl.yelpcdn.com/bphoto/_-DpXKfS3jv6DyA47g6Fxg/o.jpg',
 'is_closed': False,
 'location': {'address1': '6904 Menaul Blvd NE',
  'address2': 'Ste C',
  'address3': '',
  'city': 'Albuquerque',
  'country': 'US',
  'display_address': ['6904 Menaul Blvd NE', 'Ste C', 'Albuquerque, NM 87110'],
  'state': 'NM',
  'zip_code': '87110'},
 'name': 'Fork & Fig',
 'phone': '+15058815293',
 'price': '$$',
 'rating': 4.5,
 'review_count': 604,
 'transactions': [],
 'url': 'https://www.yelp.com/biz/fork-and-fig-albuquerque?adjust_creative=SYc8R4Gowqru5h4SBKZXsQ&utm_campaign=yelp_api_v3&utm_medium=api_v3_business_search&utm_source=SYc8R4Gowqru5h4SBKZXsQ'}
```

Above is the information provided about `Fork & Fig`, but all restaurants are provided with this information.  For example, here is the information provided by Yelp for another restaurant, `Frontier Restaurant`.


```python
# Run this cell without changes
frontier_restaurant = {'categories': [{'alias': 'mexican', 'title': 'Mexican'},
  {'alias': 'diners', 'title': 'Diners'},
  {'alias': 'tradamerican', 'title': 'American (Traditional)'}],
 'coordinates': {'latitude': 35.0808088832532, 'longitude': -106.619402244687},
 'display_phone': '(505) 266-0550',
 'distance': 4033.6583235266075,
 'id': 'frontier-restaurant-albuquerque-2',
 'image_url': 'https://s3-media4.fl.yelpcdn.com/bphoto/M9L2z6-G0NobuDJ6YTh6VA/o.jpg',
 'is_closed': False,
 'location': {'address1': '2400 Central Ave SE',
  'address2': '',
  'address3': '',
  'city': 'Albuquerque',
  'country': 'US',
  'display_address': ['2400 Central Ave SE', 'Albuquerque, NM 87106'],
  'state': 'NM',
  'zip_code': '87106'},
 'name': 'Frontier Restaurant',
 'phone': '+15052660550',
 'price': '$',
 'rating': 4.0,
 'review_count': 1369,
 'transactions': [],
 'url': 'https://www.yelp.com/biz/frontier-restaurant-albuquerque-2?adjust_creative=SYc8R4Gowqru5h4SBKZXsQ&utm_campaign=yelp_api_v3&utm_medium=api_v3_business_search&utm_source=SYc8R4Gowqru5h4SBKZXsQ'}
```

As we already know, one way to quickly view the attributes of a dictionary is to look at the keys of the dictionary.


```python
# Run this cell without changes
fork_fig.keys()
```
```
dict_keys(['categories', 'coordinates', 'display_phone', 'distance', 'id', 'image_url', 'is_closed', 'location', 'name', 'phone', 'price', 'rating', 'review_count', 'transactions', 'url'])
```

```python
# Run this cell without changes
frontier_restaurant.keys()
```
```
dict_keys(['categories', 'coordinates', 'display_phone', 'distance', 'id', 'image_url', 'is_closed', 'location', 'name', 'phone', 'price', 'rating', 'review_count', 'transactions', 'url'])
```

```python
# Run this cell without changes
fork_fig.keys() == frontier_restaurant.keys()
```
```
True
```

As we can see from our above comparison, Yelp provides us with the same information for both restaurants.  

## Writing Functions to Extract Information

Ok, now let's write our functions.

Write a function called `restaurant_name()` that, provided a dictionary representing a restaurant like you saw above, returns that restaurant's name.

#### Input:
```python
def restaurant_name(restaurant):
    return restaurant['name']
```

```python
# Run this cell without changes
restaurant_name(frontier_restaurant) # 'Frontier Restaurant'
```
#### Output:
```
'Frontier Restaurant'
```

```python
# Run this cell without changes
restaurant_name(fork_fig) # 'Fork & Fig'
```
#### Output:
```
'Fork & Fig'
```

Now write a function called `restaurant_rating()` that returns the rating of the provided restaurant.

#### Input:
```python
def restaurant_rating(restaurant):
    return restaurant['rating']
```


```python
# Run this cell without changes
restaurant_rating(frontier_restaurant) # 4.0
```
#### Output:
```
4.0
```

```python
# Run this cell without changes
restaurant_rating(fork_fig) # 4.5
```
#### Output:
```
4.5
```

## Comparing Restaurants

Now let's write a function called `is_better()` that returns `True` if a restaurant has a higher rating than an alternative restaurant.  The first argument should be called `restaurant` and the second argument should be called `alternative`.  The function returns `False` if the two ratings are equal.

This function should *call* (AKA *invoke*) your existing `restaurant_rating` function. 

# STOP RIGHT HERE
```python
def is_better(restaurant, alternative):
    return restaurant_rating(restaurant) > restaurant_rating(alternative)
```


```python
# Run this cell without changes
is_better(frontier_restaurant, fork_fig) # False
```


```python
# Run this cell without changes
is_better(fork_fig, frontier_restaurant) # True
```


```python
# Run this cell without changes
is_better(fork_fig, fork_fig) # False
```

Now let's write a function called `is_cheaper()` that returns `True` if a restaurant has a lower price, that is the restaurant has fewer `'$'` signs, than an alternative restaurant. The first argument should be called `restaurant` and the second argument should be called `alternative`. The function returns `False` if the two prices are equal.

> **Hint:** *Strings in Python respond to then `len` function.*


```python
def is_cheaper(restaurant, alternative):
    # Replace None with appropriate code
    None
```


```python
# Run this cell without changes
is_cheaper(fork_fig, frontier_restaurant) # False
```


```python
# Run this cell without changes
is_cheaper(frontier_restaurant, fork_fig) # True
```


```python
# Run this cell without changes
is_cheaper(fork_fig, fork_fig) # False
```

Now write a function called `high_rating()` that takes a `restaurant` as a first argument and a rating (in the form of a number) as the second argument and returns `True` if the given restaurant's rating is greater than or equal to the provided rating and returns `False` otherwise.


```python
def high_rating(restaurant, rating):
    # Replace None with appropriate code
    None
```


```python
# Run this cell without changes
high_rating(fork_fig, 4) # True
```


```python
# Run this cell without changes
high_rating(fork_fig, 5) # False
```


```python
# Run this cell without changes
high_rating(frontier_restaurant, 4) # True
```

Awesome! We have built out some pretty cool functions so far. Let's now think about a case where we have more than just two data points to operate on. We have added some more restaurant dictionaries below and are going to add them to our list of restaurants. Don't worry that they have a slightly different amount of data. 

We are going to need a function `mean_review_count()` to give us an idea what the typical value for `review_count` is. This function should take in a list of restaurant dictionaries and return the mean of the review counts for the collection of restaurant dictionaries. 


```python
# Run this cell without changes
dennys = {'categories': [{'alias': 'breakfast', 'title': 'Breakfast'},
  {'alias': 'diners', 'title': 'Diners'},
  {'alias': 'tradamerican', 'title': 'American (Traditional)'}],
 'is_closed': False,
 'name': "Denny's",
 'price': '$',
 'rating': 3.0,
 'review_count': 1200}

ihop = {'categories': [{'alias': 'breakfast', 'title': 'Breakfast'},
  {'alias': 'diners', 'title': 'Diners'},
  {'alias': 'tradamerican', 'title': 'American (Traditional)'}],
 'is_closed': False,
 'name': "IHOP: International House of Pancakes",
 'price': '$',
 'rating': 3.45,
 'review_count': 1588}

mcdonalds = {'categories': [{'alias': 'breakfast', 'title': 'Breakfast'},
  {'alias': 'burgers', 'title': 'Burgers'},
  {'alias': 'fast food', 'title': 'Good Food Fast'}],
 'is_closed': False,
 'name': "McDonalds",
 'price': '$',
 'rating': 3.45,
 'review_count': 2455}

pearl_street_oyster_bar = {'categories': [{'alias': 'seafood', 'title': 'Seafood'},
  {'alias': 'gourmet', 'title': 'Gourmet'},
  {'alias': 'Shellfish', 'title': 'Shellfish'}],
 'is_closed': False,
 'name': "Pear Street Oyster Bar",
 'price': '$$$',
 'rating': 4.75,
 'review_count': 350}
```


```python
# Run this cell without changes
restaurant_list = [pearl_street_oyster_bar, mcdonalds, ihop, dennys, fork_fig, frontier_restaurant]
```


```python
def mean_review_count(list_of_restaurants):
    # Replace None with appropriate code
    None
```


```python
# Run this cell without changes
mean_review_count(restaurant_list) #1261.0
```

Now we have an idea of how many reviews a typical restaurant has, but none of these restaurants have exactly that number of reviews.

Which restaurants have a `review_count` within 150 of the average? ("within 150" meaning exactly average, <= 150 fewer reviews than the average, or <= 150 more reviews than the average)

Return a list of the restaurant names.


```python
def near_average_review_count(list_of_restaurants):
    mean = mean_review_count(list_of_restaurants)
    # Replace None with appropriate code
    None
```


```python
# Run this cell without changes
near_average_review_count(restaurant_list) # ["Denny's", 'Frontier Restaurant']
```

## Summary

Great! In this lab we saw how to pass both single and multiple arguments to functions. Function arguments can make functions more flexible and reusable!

# [Python Loops and Functions - Cumulative Lab](https://colab.research.google.com/gist/bpurdy-ds/d7602f1033cd6474442ec02278403c8c/index.ipynb#scrollTo=3ftWIfaObL35)

## Introduction

You made it through another section — excellent work! This cumulative lab will return to the Amazon product review dataset and allow you to flex your new skills.

## Objectives

You will be able to:

 - Recall what you learned in the previous section
 - Practice writing loops to pull multiple pieces of data from a dataset
 - Practice writing functions for organization and avoiding repetition
 
## Your Task: Dynamically Query Amazon Review Data

Once again, we are going to be working with data collected by Computer Science researchers at the University of California, San Diego. Their full paper citation is here:
> **Justifying recommendations using distantly-labeled reviews and fined-grained aspects**
Jianmo Ni, Jiacheng Li, Julian McAuley
Empirical Methods in Natural Language Processing (EMNLP), 2019
[pdf](http://cseweb.ucsd.edu/~jmcauley/pdfs/emnlp19a.pdf)

We are still using a cleaned-up, coffee-specific, sample version of their [full dataset](https://nijianmo.github.io/amazon/index.html).

![pouring coffee](https://curriculum-content.s3.amazonaws.com/data-science/images/coffee.jpg)
<span>Photo by <a href="https://unsplash.com/@dumdidu?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Philipp Cordts</a> on <a href="https://unsplash.com/s/photos/coffee-pot?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>

In some cases, we will write the function signature for you, e.g. 

```python
def review_sentiment(review):
    # Replace None with appropriate code
    None
```

Then you just need to fill in the relevant logic.

In other cases, you will need to write the function signature yourself, e.g.

```python
# Your code here
```

### Requirements

#### 1. Data Summary
While reusing some code from the previous cumulative lab, write code to loop over all of the records in the dataset to summarize its contents, specifically in terms of overall review sentiment and the years when the reviews were written.

#### 2. Subset Sample
Provide a sample of records that meet particular criteria.

#### 3. Individual Review Summary
Refactor the code from the previous cumulative lab so that it is contained in a function and prompts the user to select which review to summarize.

## Data Summary

Once again, we've opened up the dataset and loaded it into a list of dictionaries called `reviews`.


```python
# Run this cell without changes
import json
with open("coffee_product_reviews.json") as f:
    reviews = json.load(f)
type(reviews)
```
```
list
```

Previously, we found the length of the collection, and looked into the data types of each record's keys and values


```python
# Run this cell without changes
num_reviews = len(reviews)
print("The coffee product review dataset contains {} reviews".format(num_reviews))

first_review = reviews[0]
first_review
```
#### Output:
```
The coffee product review dataset contains 86 reviews
{'rating': 5.0,
 'reviewer_name': 'Sns073194',
 'product_id': 'B00004RFRV',
 'review_title': 'Perfect cafsito every time',
 'review_time': '03 11, 2018',
 'images': ['https://images-na.ssl-images-amazon.com/images/I/71d2cQEgJsL._SY88.jpg'],
 'styles': {'Size:': ' 6-Cup', 'Color:': ' Silver'}}
```

```python
# Run this cell without changes
first_review.keys()
```
#### Output:
```
dict_keys(['rating', 'reviewer_name', 'product_id', 'review_title', 'review_time', 'images', 'styles'])
```


```python
# Run this cell without changes
first_review.values()
```
#### Output:
```
dict_values([5.0, 'Sns073194', 'B00004RFRV', 'Perfect cafsito every time', '03 11, 2018', ['https://images-na.ssl-images-amazon.com/images/I/71d2cQEgJsL._SY88.jpg'], {'Size:': ' 6-Cup', 'Color:': ' Silver'}])
```

This time, let's do something a bit more sophisticated. Specifically:

1. Count of positive, negative, and neutral reviews
2. List of years contained in the dataset

### Count of Positive, Negative, and Neutral Reviews

Previously, we wrote something like this code to determine whether a specific review was positive, negative, or neutral:


```python
# Run this cell without changes
selected_review = reviews[2]
selected_rating = selected_review["rating"]

if selected_rating >= 4:
    print("This is a positive review")
elif selected_rating <= 2:
    print("This is a negative review")
else:
    print("This is a neutral review")
```
#### Output:
```
This is a positive review
```

Now, rewrite that code as a function `review_sentiment`, which takes in a review dictionary as an argument, and returns the string `"positive"`, `"negative"`, or `"neutral"`

#### Input:
```python
def review_sentiment(review):
    rating = review["rating"]
    if rating >= 4:
        return "positive"
    elif rating <= 2:
        return "negative"
    else:
        return "neutral"
```
```python
# Run this cell without changes
review_sentiment(reviews[2]) # 'positive'
```
#### Output:
```
'positive'
```

```python
# Run this cell without changes
review_sentiment(reviews[4]) # 'negative'
```
```
'negative'
```
```python
# Run this cell without changes
review_sentiment(reviews[47]) # 'neutral'
```
```
`neutral`
```
Ok, this is already much cleaner than copying and pasting that `if`/`elif`/`else` sequence like we did before!

Now, write a function to loop over all of the reviews in the list, and count how many are positive, negative, and neutral.

The function should be called `get_sentiment_counts`, take one argument (the list of reviews), and return a dictionary containing the counts. A counter dictionary has been initialized for you with `"positive"`, `"negative"`, and `"neutral"` as the keys and values starting at 0.

#### Input:
```python
def get_sentiment_counts(review_list):

    sentiment_counts = {
        "positive": 0,
        "negative": 0,
        "neutral": 0
    }
    
    for review in review_list:
        sentiment = review_sentiment(review)
        sentiment_counts[sentiment] += 1
    
    return sentiment_counts

get_sentiment_counts(reviews) # {'positive': 67, 'negative': 15, 'neutral': 4}
```
#### Output:
```
{'positive': 67, 'negative': 15, 'neutral': 4}
```


This spread of sentiments seems reasonable. There is a well-known [skew towards positive reviews in general](https://dspace.mit.edu/handle/1721.1/111093), similar to "grade inflation", and people with neutral opinions are less likely to write reviews in the first place.

### List of Years Contained in the Dataset

Previously, we wrote something like this code to extract the year of a review from the review dictionary:


```python
# Run this cell without changes
selected_review = reviews[2]
selected_review_time = selected_review["review_time"]
selected_review_year = int(selected_review_time[-4:])
selected_review_year
```
#### Output:
```
2017
```

Now, rewrite that code as a function `review_year`, which takes in a review dictionary as an argument, and returns the year as an integer:

#### Input:
```python
def review_year(review):
    return int(review["review_time"][-4:])
```

#### Output:
```python
# Run this cell without changes
review_year(reviews[2]) # 2017
```
```
2017
```


```python
# Run this cell without changes
review_year(reviews[4]) # 2017
```
```
2017
```


```python
# Run this cell without changes
review_year(reviews[47]) # 2015
```
```
2015
```

Now, write a function called `get_years` to loop over all of the reviews in the review list and create a list of the years you find. Each year should only appear once, in ascending order. The function should accept one argument (`review_list`) and should return a list of integers representing the years.

Hints:

 - Remember that you can use the `set()` function to keep only the unique elements in a list. Just make sure you use `list()` afterwards to convert it back to a list data type. This is not the only solution, however!
 - There is a list method named `.sort()` ([look it up in the python list documentation here](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)) that will automatically order the years; you don't need to write sorting logic "by hand"

#### Input:
```python
def get_years(review_list):
    years = set()  # Use a set to ensure unique years
    for review in review_list:
        years.add(review_year(review))
    
    return sorted(list(years))  # Convert to list and sort

print(get_years(reviews)) # [2007, 2008, 2009, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018]
print(type(get_years(reviews))) # <class 'list'>
```

#### Output:
```
[2007, 2008, 2009, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018]
<class 'list'>
```

Now we know that we have data spanning 2007-2018, with no data from 2010. In some contexts that absence might be worth investigating — is it a random artifact of our sample, or are we missing 2010 data for a reason that matters? For now we'll just keep moving on to the next section, now that we have a clearer sense of the kinds of reviews in our dataset and the years they were written.

## Subset Sampling

Once you have an overall sense of a dataset, it's a good idea to ask *what are some examples of records in each category?* For example, what are some examples of a negative review?

Although 86 records are few enough that you could technically read through all of them and just mentally note what we see, let's use an approach that will scale better to larger datasets with more categories: **filtering** to a subset of records then **sampling** to achieve a digestible amount of information.

### Filtering

Here we are going to make use of another built-in Python function: `filter()` ([docs here](https://docs.python.org/3/library/functions.html#filter)). To use this function, we first need to write a helper function that returns `True` or `False` based on the value passed in.

So, create a function `is_negative` that takes in a review dictionary as an argument and returns `True` if the review is negative, `False` otherwise:

#### Input:
```python
def is_negative(review):
    return review_sentiment(review) == "negative"

print(is_negative(reviews[2]))  # False (postive review)
print(is_negative(reviews[4]))  # True
print(is_negative(reviews[47])) # False (neutral review)
```

#### Output:
```
False
True
False
```

Now we can use the `filter()` function to create a list of negative reviews:


```python
# Run this cell without changes
list(filter(is_negative, reviews))
```
#### Output:
```
'images': ['https://images-na.ssl-images-amazon.com/images/I/71tRehtvN+L._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/719K20U+MaL._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/71jd6yc1GdL._SY88.jpg'],
  'styles': {'Color:': ' Black/White'}},
 {'rating': 1.0,
  'reviewer_name': 'fifrox',
  'product_id': 'B00005MF9C',
  'review_title': 'Works great for a week then fails!',
  'review_time': '03 10, 2016',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/81QVkUT4hdL._SY88.jpg'],
  'styles': {'Color:': ' Black/Stainless Steel'}},
 {'rating': 1.0,
  'reviewer_name': 'cas',
  'product_id': 'B00005NCWQ',
  'review_title': 'Garbage!!!',
  'review_time': '03 26, 2018',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/71Bxydi3DQL._SY88.jpg'],
  'styles': {'Size:': ' 8-Cup'}},
 {'rating': 1.0,
  'reviewer_name': 'GoClick',
  'product_id': 'B00005OTXM',
  'review_title': 'Returned - produced revolting burnt plastic flavored coffee, and seemed flawed.',
  'review_time': '04 16, 2015',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/71o+7Zru+iL._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/81sbfP4tc8L._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/71vhOebyGaL._SY88.jpg'],
  'styles': {'Style Name:': ' COFFEE MAKER ONLY'}},
 {'rating': 2.0,
  'reviewer_name': 'Picks n Pans',
  'product_id': 'B00006F2LW',
  'review_title': 'Cracked lid out of the box',
  'review_time': '02 27, 2008',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/317fvUiuNDL._SY88.jpg'],
  'styles': {'Color:': ' Black'}},
 {'rating': 2.0,
  'reviewer_name': 'LMM',
  'product_id': 'B00008ELEA',
  'review_title': 'smelled like the cord was burning',
  'review_time': '06 6, 2016',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/51xXENQhIGL._SY88.jpg'],
  'styles': {'Size:': ' 4-Cup'}},
 {'rating': 1.0,
  'reviewer_name': 'Marcia S.',
  'product_id': 'B0000A1ZMS',
  'review_title': 'Look what happened to this once great Cuisinart coffeemaker.',
  'review_time': '11 12, 2016',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/51B8eue4nHL._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/519NziREFIL._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/51v+A1zWqTL._SY88.jpg'],
  'styles': {'Color:': ' Black', 'Style Name:': ' Coffeemaker'}},
 {'rating': 2.0,
  'reviewer_name': 'Jimmie',
  'product_id': 'B0000A1ZMS',
  'review_title': 'Leaks and more',
  'review_time': '01 13, 2011',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/51U4K+PzETL._SY88.jpg'],
  'styles': {'Color:': ' Black', 'Style Name:': ' Coffeemaker'}}]
```

Write a function called `get_negative_reviews` that returns a list of these reviews. It should take the list of all reviews as an argument.

(This can be a one-line function.)

#### Input:
```python
def get_negative_reviews(review_list):
    return list(filter(is_negative, review_list))

len(get_negative_reviews(reviews)) # 15
```
#### Output:
```
15
```

### Sampling

Again, since we have a relatively small dataset, we could just look at all 15 reviews. But let's take a more scalable approach instead, and take a random sample of negative reviews.

Recall the `random` module, which must be imported:


```python
# Run this cell without changes
import random
```

We'll use the `random.sample()` function, which takes in a collection and a number, and returns that number of elements from the collection.

So, for example, if we want 3 negative reviews:


```python
# Run this cell without changes
# You can run as many times as you want, to see different sample examples
random.sample(get_negative_reviews(reviews), 3)
```
```
[{'rating': 1.0,
  'reviewer_name': 'Toni Bautista',
  'product_id': 'B00005IBX9',
  'review_title': 'Great but NOT PERFECT -missing Side water panel',
  'review_time': '02 24, 2017',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/71X5NEjZG5L._SY88.jpg'],
  'styles': {'Color:': ' Brushed Chrome'}},
 {'rating': 1.0,
  'reviewer_name': 'mathman54',
  'product_id': 'B00004RFRV',
  'review_title': "The bottom looks like it has rusted and I don't know how to ...",
  'review_time': '02 15, 2016',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/71qt4Hnra8L._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/71Wkg8MesdL._SY88.jpg'],
  'styles': {'Size:': ' 12-Cup', 'Color:': ' Silver'}},
 {'rating': 1.0,
  'reviewer_name': 'SAinVA',
  'product_id': 'B00005LM0T',
  'review_title': 'Too much waste',
  'review_time': '09 7, 2017',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/71shZggLRHL._SY88.jpg'],
  'styles': {'Size:': ' 34 oz.', 'Package Type:': ' Standard Packaging'}}]
```
Now, put that code into a function `get_negative_review_sample`. This function should take a list of reviews and the number of samples to select, and should return a sample of negative reviews.

(You can assume that `num_samples` is a valid number. The number of samples must be less than or equal to the number of elements in the collection.)

#### Input:
```python
def get_negative_review_sample(review_list, num_samples):
    return random.sample(get_negative_reviews(review_list), num_samples)

get_negative_review_sample(reviews, 4)
```
#### Output:
```
[{'rating': 1.0,
  'reviewer_name': 'EJ',
  'product_id': 'B00004RFRV',
  'review_title': 'Rusted spots everywhere fresh out the box...nasty',
  'review_time': '06 4, 2017',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/71Dbr6X0bYL._SY88.jpg'],
  'styles': {'Size:': ' 9-Cup', 'Color:': ' Silver'}},
 {'rating': 2.0,
  'reviewer_name': 'fred o.',
  'product_id': 'B00005MF9C',
  'review_title': 'Good purchase',
  'review_time': '09 4, 2016',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/71tRehtvN+L._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/719K20U+MaL._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/71jd6yc1GdL._SY88.jpg'],
  'styles': {'Color:': ' Black/White'}},
 {'rating': 1.0,
  'reviewer_name': 'Silicon Valley',
  'product_id': 'B00005LM0T',
  'review_title': 'FRAME RUSTS WITHIN A FEW WEEKS',
  'review_time': '03 10, 2016',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/71FREAeBLIL._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/71qkhDjseuL._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/7143mVMMoCL._SY88.jpg'],
  'styles': {'Size:': ' 34 oz.', 'Package Type:': ' Standard Packaging'}},
 {'rating': 1.0,
  'reviewer_name': 'Toni Bautista',
  'product_id': 'B00005IBX9',
  'review_title': 'Great but NOT PERFECT -missing Side water panel',
  'review_time': '02 24, 2017',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/71X5NEjZG5L._SY88.jpg'],
  'styles': {'Color:': ' Brushed Chrome'}}]
```


Repeat the same process for positive reviews. That means we need:

1. A helper function `is_positive` (this can't just be `not is_negative` since neutral reviews are neither)
2. A function `get_positive_reviews` which returns a list of all positive reviews
3. A function `get_positive_review_sample` which returns a sample of positive reviews with the specified length

#### Input:
```python
# Function to check if a review is positive based on rating
def is_positive(review):
    return review["rating"] >= 4  # Returns True if the rating is 4 or higher, otherwise False

# Function to filter and get only positive reviews from a list of reviews
def get_positive_reviews(review_list):
    return [review for review in review_list if is_positive(review)]  # List comprehension to include reviews with rating >= 4

# Function to get a random sample of positive reviews
def get_positive_review_sample(review_list, num_samples):
    # Calls get_positive_reviews to filter positive reviews, then samples 'num_samples' reviews from the result
    return random.sample(get_positive_reviews(review_list), num_samples)

# Example call to get_positive_review_sample to retrieve 4 random positive reviews from the 'reviews' list
get_positive_review_sample(reviews, 4)
```
#### Output
```
[{'rating': 5.0,
  'reviewer_name': 'ArmiWyf',
  'product_id': 'B00004RFRV',
  'review_title': 'LUV IT!!!',
  'review_time': '09 2, 2016',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/61sbRLnd2UL._SY88.jpg'],
  'styles': {'Size:': ' 12-Cup', 'Color:': ' Silver'}},
 {'rating': 5.0,
  'reviewer_name': 'dvrmasik',
  'product_id': 'B00005NCWQ',
  'review_title': 'rich and aromatic coffee',
  'review_time': '05 5, 2016',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/81fgcTsXRwL._SY88.jpg',
   'https://images-na.ssl-images-amazon.com/images/I/81bsfG7k7kL._SY88.jpg'],
  'styles': {'Size:': ' 8-Cup'}},
 {'rating': 5.0,
  'reviewer_name': 'Alexander Lamakin',
  'product_id': 'B00004S8DX',
  'review_title': 'This is my good buy.',
  'review_time': '11 29, 2016',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/7184SwO3X-L._SY88.jpg'],
  'styles': {'Size:': ' Regular-used'}},
 {'rating': 5.0,
  'reviewer_name': 'Thicket',
  'product_id': 'B00009ADDR',
  'review_title': 'This press is stout!',
  'review_time': '12 4, 2007',
  'images': ['https://images-na.ssl-images-amazon.com/images/I/41xt8zREjbL._SY88.jpg'],
  'styles': {'Size:': ' 36-Ounce', 'Color:': ' Polished'}}]
```


## Individual Review Summary

In addition to summarizing the dataset overall and sampling based on criteria, we want the user to be able to query any given record in order to view a summary. Before, we created a variable called `review_index` that the user could modify. Now, let's write some reusable code that doesn't require the user to write any Python at all!

Recall that before, our final code looked something like this:


```python
# Run this cell without changes

review_index = 2

# Extract review from list of reviews
selected_review = reviews[review_index]

# Extract title
selected_review_title = selected_review["review_title"]

# Extract rating and format as positive, negative, or neutral
selected_rating = selected_review["rating"]
if selected_rating >= 4:
    selected_sentiment = "positive"
elif selected_rating <= 2:
    selected_sentiment = "negative"
else:
    selected_sentiment = "neutral"
    
# Extract author
selected_author = selected_review["reviewer_name"]

# Extract year (doesn't need to be int for this use case)
selected_year = selected_review["review_time"][-4:]

print(f'"{selected_review_title}": This was a {selected_sentiment} review written by {selected_author} in {selected_year}.')
```
#### Output:
```
"Bialetti is the Best!": This was a positive review written by Karen in 2017.
```

Rewrite that code as a function called `get_review_summary`, which takes a review dictionary as an argument, and returns a string that resembles the previous summary string, e.g.

```
"Bialetti is the Best!": This was a positive review written by Karen in 2017.
```

*Hint: look back at the functions you have previously written to see which ones might be useful to call within this function!*

#### Input:
```python
def get_review_summary(review):
    review_title = review["review_title"]
    rating = review["rating"]
    
    if rating >= 4:
        sentiment = "positive"
    elif rating <= 2:
        sentiment = "negative"
    else:
        sentiment = "neutral"
        
    author = review["reviewer_name"]
    year = review["review_time"][-4:]
    
    return f'"{review_title}": This was a {sentiment} review written by {author} in {year}.'

print(get_review_summary(reviews[2])) 
```
#### Output:
```
"Bialetti is the Best!": This was a positive review written by Karen in 2017.
```

Now, instead of copying and pasting that every time, we can just call it repeatedly!

Write a function that prompts the user to enter a review index, then prints the relevant review summary. The function should be called `review_summary_prompt`, it should take a list of reviews as an argument, and should print information but not return anything.

Display the message `"Please enter a review index: "` when prompting for input. You can assume that the user will enter a valid index between 0 and 85.

Hints:

 - Use the built-in `input()` function ([check the documentation here to see how to use it!](https://docs.python.org/3/library/functions.html#input))
 - Remember that this function always returns a string, so you will have to convert the user-supplied index into an integer, otherwise you'll get the error `TypeError: list indices must be integers or slices, not str`
 - If you're wondering about the type of a given variable, you can use the built-in `type()` function


```python
def review_summary_prompt(list_of_reviews):
    index = int(input("Please enter a review index: "))
    review_summary = get_review_summary(list_of_reviews[index])
```

Run this cell, and try entering 2, 4, 52 (examples of positive, negative, neutral reviews)

You can also try any index you want, between 0 and 85!


```python
# Run this cell without changes
review_summary_prompt(reviews)
```

## Putting It All Together

In this section, we are just calling several of the previously-created functions to double-check that they are working as expected. You do not need to write any more code, although if you notice something wrong with one of your functions you can go back and fix it!  Just make sure that you re-run the cell declaring the function if you want the behavior of calling the function to change.

### Data Summary


```python
# Run this cell without changes

print(f"The coffee product review dataset contains {len(reviews)} reviews")
print()
print("Review sentiment:")
for key, value in get_sentiment_counts(reviews).items():
    print(f"{value} {key} reviews")
print()
print("Review years:")
print(get_years(reviews))
```
#### Output:
```
The coffee product review dataset contains 86 reviews

Review sentiment:
67 positive reviews
15 negative reviews
4 neutral reviews

Review years:
[2007, 2008, 2009, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018]
```

### Subset Samples


```python
# Run this cell without changes

print("Examples of positive reviews:")
positive_samples = get_positive_review_sample(reviews, 5)
for review in positive_samples:
    print(get_review_summary(review))
print()
print("Examples of negative reviews:")
negative_samples = get_negative_review_sample(reviews, 5)
for review in negative_samples:
    print(get_review_summary(review))
```
#### Output:
```
Examples of positive reviews:
"This thing is awesome!": This was a positive review written by Joseph P. Long in 2008.
"Intoxicating aroma": This was a positive review written by Patrick523 in 2015.
"12 years of heavy use - lasted longer than ex-husband": This was a positive review written by Alice Wakefield in 2007.
"If you want to keep it hot, get this one.": This was a positive review written by KMac in 2016.
"Well made with a charming nostalgic design.": This was a positive review written by Jean-Claude Van Darn in 2017.

Examples of negative reviews:
"The bottom looks like it has rusted and I don't know how to ...": This was a negative review written by mathman54 in 2016.
"Look what happened to this once great Cuisinart coffeemaker.": This was a negative review written by Marcia S. in 2016.
"Garbage!!!": This was a negative review written by cas in 2018.
"Good purchase": This was a negative review written by fred o. in 2016.
"Great but NOT PERFECT -missing Side water panel": This was a negative review written by Toni Bautista in 2017.
```
### Summary Prompt


```python
# Run this cell without changes
review_summary_prompt(reviews)
```

## Conclusion

Congratulations, you made it to the end of another cumulative lab! In this lab you practiced refactoring previously-written code to use functions, and using loops to avoid repetition and perform analyses of the whole dataset as well as certain subsets.
