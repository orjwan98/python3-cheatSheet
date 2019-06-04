# Lists, Tuples and Sets

## Lists

Lists in python are like arrays in JS. 

All slicing rules applied to strings also apply to lists. Refer to strings.md for more info. 

### Modify (mutate) lists (replace, add, remove)

- To add an element to the end of the list: 
``` py
my_list = ['History','Maths', 'Physics', 'CompSci']

my_list.append('Arts')

print(my_list) #prints ['History','Maths', 'Physics', 'CompSci', Arts]
```
- To add an element **anywhere** in the list: 
``` py
my_list = ['History','Maths', 'Physics', 'CompSci']

my_list.insert(2,'Arts')

print(my_list) #prints ['History','Maths', 'Arts', 'Physics', 'CompSci']

```
- To add elements of another list to the end of our list: 

``` py
my_list = ['History','Maths', 'Physics', 'CompSci']

my_list2 = ['Arts', 'Social Studies']

my_list.extend(my_list2)

print(my_list) #prints ['History','Maths', 'Arts', 'Physics', 'CompSci', 'Arts', 'Social Studies']

```
- To remove a specific element from a list:

``` py
my_list = ['History','Maths', 'Physics', 'CompSci']

my_list.remove('Physics`)

print(my_list) #prints ['History','Maths', 'CompSci']
```
- To remove the last element from a list and return its value:

``` py
my_list = ['History','Maths', 'Physics', 'CompSci']

popped = my_list.pop()

print(popped) #prints 'CompSci'
print(my_list) #prints ['History','Maths', 'Physics']
```

- To reverse a list, we can either do:

```py
my_list = ['History', 'Maths', 'Physics', 'CompSci']


print(my_list[::-1])  # prints ['CompSci', 'Physics', 'Maths', 'History']

```

or use the `reverse()` method:

``` py
my_list = ['History', 'Maths', 'Physics', 'CompSci']

my_list.reverse()

print(my_list)  # prints ['CompSci', 'Physics', 'Maths', 'History']

```

- To sort our list:

Alphabetically if it's strings:

``` py
my_list = ['History', 'Maths', 'Physics', 'CompSci']

my_list.sort()
print(my_list)  # prints ['CompSci', 'History', 'Maths', 'Physics'] => from A to Z

my_list.sort(reverse=True)
print(my_list)  # prints ['Physics', 'Maths', 'History', 'CompSci'] => from Z to A

```
Ascending/Descending if it's numbers:

```py
nums = [1, 4, 7, 2, 5, 9, 3, 8, 6, 0]

nums.sort()
print(nums) #prints [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

nums.sort(reverse=True)
print(nums)  #prints [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

```

- To return a **new** sorted list, we use the `sorted()` function:

```py
my_list = ['History', 'Maths', 'Physics', 'CompSci']

new_list = sorted(my_list)
reverse_list = sorted(my_list, reverse=True)
print(new_list)  # prints ['CompSci', 'History', 'Maths', 'Physics']
print(reverse_list)  # prints ['Physics', 'Maths', 'History', 'CompSci']

```

- To return biggest, smallest, and sum value of a list we can use: 

 => `min()` 
 
 ```py 
 print(min([0,2,7,4,1])) #prints 0
 ```
 
=> `max()`  

```py 
print(max([0,2,7,4,1])) #prints 7
```
=> `sum()` 
```py 
print(sum([0,2,7,4,1])) #prints 14
```

- To find the index of an element in a list, we can use the `index()` method:
```py
my_list = ['History', 'Maths', 'Physics', 'CompSci']

print(my_list.index('Maths')) #prints 1

```

- To check if an element exists a list, we can use the `in` operator (returns True or False):
```py
my_list = ['History', 'Maths', 'Physics', 'CompSci']

print('CompSci' in my_list) #prints True

```
- To loop through a list, we can use a `for...in` loop:

```py
my_list = ['History', 'Maths', 'Physics', 'CompSci']

print('CompSci' in my_list)

for ele in my_list:
    print(ele)  
    
    # prints 
    # History
    # Maths
    # Physics
    # CompSci
    
    #Notes: the loop prints each element on a new line because it executes that way.
```
- To access the `index` and value in a `loop`, we can use the `enumerate()` function:

```py
my_list = ['History', 'Maths', 'Physics', 'CompSci']


for index, ele in enumerate(my_list):
    print(index, ele)
    
    # prints
    # 0 History
    # 1 Maths
    # 2 Physics
    # 3 CompSci
    
 # We can also control the value of starting index by passing a 2nd argument to `enumerate(list, start=number)`, example:
 
 my_list = ['History', 'Maths', 'Physics', 'CompSci']


for index, ele in enumerate(my_list, start=1):
    print(index, ele)
    
    # prints
    # 1 History
    # 2 Maths
    # 3 Physics
    # 4 CompSci
```

- To turn an list into a string, we can use the **string** method `join()`: 

```py

my_list = ['History', 'Maths', 'Physics', 'CompSci']

my_string = ', '.join(my_list)

print(my_string)  # prints 'History, Maths, Physics, CompSci'

```
- To turn a string into a list, we can use the **string** method `split()`:

```py

my_list = ['History', 'Maths', 'Physics', 'CompSci']

my_string = ', '.join(my_list)

new_string = my_string

print(new_string.split(', '))  # prints ['History', 'Maths', 'Physics', 'CompSci']

```


## Tuples

Tuples behave the exact same way as a list, but unlike lists, we can't modify tuples. Meaning that they are **immutable**. However, we can loop through them, access their elements and everything else long as we're not mutating them. 

Example:

```py
my_tuple = ('History', 'Maths', 'Physics', 'CompSci')

my_tuple[0] = 'Arts'

#returns a typeError:'tuple' object does not support item assignment

````
```py

my_tuple = ('History', 'Maths', 'Physics', 'CompSci')

for ele in my_tuple:
    print(ele)
    # prints
    # History
    # Maths
    # Physics
    # CompSci

```

## Sets

Sets are values that are NOT ordered and include no duplicates. They don't support indexing and they throw away duplicate elements. 

if you print your set, each time you'll get a different order of elements. And if you try to print a particular element by indexing, it will throw an error:

```py

my_set = {'History', 'Maths', 'Physics', 'CompSci'}

print(my_set) #throws a TypeError: 'set' object does not support indexing.

```

And if you have duplicates, it will throw them away:

```py

my_set = {'History', 'Maths', 'Physics', 'CompSci', 'Maths'}

print(my_set)  # prints {'History', 'Physics', 'CompSci', 'Maths'}

```
NOTE: Sets are often used for membership tests because they are much optimized for it than tuples and lists. You can check whether an element exists in a set the same way you'd in a list/tuple. 

- To check for values that your set may share with another set, you can use the `intersection()` method:

```py

my_set = {'History', 'Maths', 'Physics', 'CompSci', 'Maths'}
your_set = {'History', 'Maths', 'Design', 'Arts'}

print(my_set.intersection(your_set))  # prints {'History', 'Maths'}

```

- On the contrary, to check values that your set don't share with another set, you can use the `difference()` method:

```py

my_set = {'History', 'Maths', 'Physics', 'CompSci', 'Maths'}
your_set = {'History', 'Maths', 'Design', 'Arts'}

print(my_set.difference(your_set))  # prints {'CompSci', 'Physics'}

```

- To combine both sets, we can use the `union()` method:

```py

my_set = {'History', 'Maths', 'Physics', 'CompSci', 'Maths'}
your_set = {'History', 'Maths', 'Design', 'Arts'}

print(my_set.union(your_set))  # prints {'Physics', 'CompSci', 'Arts', 'History', 'Maths', 'Design'}

```

## Empty lists, tuples, and sets:

```py
# To create an empty list:

empty_list = []
empty_list2 = list()


# To create an empty tuple:
empty_tuple = ()
empty_tuple2 = tuple()

# to create an empty set

empty_set = set()

# An empty {} refers to an empty dictionary.

```






