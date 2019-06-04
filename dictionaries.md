
#Dictionaries 

Dictionaries in python are what objects are in JS. Example:

```py
person = {'name':'Mark', 'age':25}

print(person['name']) #prints Mark
```

NOTE: Though values in a dictionary can be mutable or immutable objects, only immutable objects are allowed for keys. like strings, numbers and even **tuples**, example:

```py
person = {('name',): 'Mark', 'age': 25}

print(person[('name',)])  # prints Mark
print(type(('name',)))  # prints tuple

#if you have only one element in a tuple, you must add a comma (,) to tell Python that this is a tuple.
```
- If you try to access a key that doesn't exist, like `phone` for example, python would throw an error:

```py
person = {'name':'Mark', 'age':25}

print(person['phone']) #throws a KeyError: 'phone'
```
Now, you can make it return a none or a defauly value in case a key doesn't exist by using the `get()` method:

```py
person = {'name': 'Mark', 'age': 25}

print(person.get('phone')) #prints None

print(person.get('phone', 'No such key exists!'))  # No such key exists!

```
- To add/update a key in a dictionary, you can do:

```py
person = {'name': 'Mark', 'age': 25}

person['phone'] = '0595408237'

print(person)  #prints {'name': 'Mark', 'age': 25, 'phone': '0595408237'}

person['name'] = 'Mira'

print(person)  #prints {'name': 'Mira', 'age': 25, 'phone': '0595408237'}

```
To update multiple keys in a dictionary, we can use the `update()` method:

```py
person = {'name': 'Mark', 'age': 25}

person['phone'] = '0595408237'

person.update({'name': 'Miles', 'age': 28})

print(person)  # prints {'name': 'Miles', 'age': 28, 'phone': '0595408237'}

```

To remove a key (and its value), we can use `del`:

```py

person = {'name': 'Mark', 'age': 25}

del person['age']

print(person) #prints {'name': 'Mark'}

```

To remove a key (and catch its value), we can use `pop()` method:

```py

person = {'name': 'Mark', 'age': 25}

age = person.pop('age')

print(person) #prints {'name': 'Mark'}
print(age) #prints 25

```

To find out the length of our dictionary (aka how many keys), we can use the `len()` function:

```py
person = {'name': 'Mark', 'age': 25}

print(len(person))  # prints 2 because we only have 2 keys

```
To get the dict's keys or values, we can use `keys()` and `values()` methods:

```py
person = {'name': 'Mark', 'age': 25}

person_keys = person.keys()
person_values = person.values()

print(person_keys)  # prints dict_keys(['name', 'age'])
print(person_values)  # prints dict_values(['Mark', 25])

```

To get the dict's keys AND values, we can use `items()` method:

```py
person = {'name': 'Mark', 'age': 25}

person_keys_values = person.items()

print(person_keys_values)  # prints dict_items([('name', 'Mark'), ('age', 25)])

```
To loop through the dict's keys and values, we can make a `for...in` loop:

```py
person = {'name': 'Mark', 'age': 25}

person_keys_values = person.items()

for key, value in person_keys_values:

    print(key, value)
    # prints
    # name Mark
    # age 25
```
 

