# conditionals-and-booleans

conditionals `if, elif, else` behave similarly as `if, else if, else` in JS. Here's an example:

```py
my_name_is = "Slim Shady"

# prints Hi! My name is chika chika Slim Shady

if my_name_is == "Eminem":
    print("Be careful of losing yourself!")
elif my_name_is == "Marshal Mathers":
    print("Don't forget to clean out your closet!")
elif my_name_is == "Rabbit":
    print("Go back to 8 Mile!")
elif my_name_is == "Slim Shady":
    print("Hi! My name is chika chika " + my_name_is)
else:
    print("No M&M was found")
```

## Using and, or, and not operators:

- `and/or`
```py
username = "Admin"
logged_in = True

if username == "Admin" and logged_in:
    print("You're already logged in")  # prints when logged_in==True
```
```py
fav_fruit = "Oranges"

if fav_fruit == "Apples" or fav_fruit == "Oranges":
    print("That's one of my favorite fruits!")
else:
    print("Nah, don't like it.")
```
- `not`

```py
my_name_is = ""

# prints Not shady

if not my_name_is:
    print("Not shady")
elif my_name_is == "Eminem":
    print("Be careful of losing yourself!")
elif my_name_is == "Marshal Mathers":
    print("Don't forget to clean out your closet!")
elif my_name_is == "Rabbit":
    print("Go back to 8 Mile!")
elif my_name_is == "Slim Shady":
    print("Hi! My name is chika chika " + my_name_is)
else:
    print("No M&M was found")
```

### Things that evaluate to false in Python:

- `False` duh.
- `None`.
- Zero of any numeric type - int or decimal. 
- Any empty sequence (empty strings, empty lists, empty tuples or empty sets).
- Any empty mapping. For example, and empty dict`{}`.

## Equals `==` and `is` operators:

- To check if two objects are equal in python, we would do:

 ```py
my_list = [1, 2, 3, 4, 5]
your_list = [1, 2, 3, 4, 5]

print(my_list == your_list)  # prints True
 ```
 - To check if they have the same id (aka same reference in memory we would do:
 
```py
my_list = [1, 2, 3, 4, 5]
your_list = [1, 2, 3, 4, 5]

print(my_list is your_list)  # prints False

```
- To view the id of a variable, you can use the `id()` function on the var, like this:

```py
my_list = [1, 2, 3, 4, 5]
your_list = [1, 2, 3, 4, 5]
our_list = my_list

print(id(my_list))  # prints 140432176522632
print(id(your_list))  # prints 140432176522696
print(id(our_list))  # prints 140432176522632
print(my_list is our_list)  # prints True
```









