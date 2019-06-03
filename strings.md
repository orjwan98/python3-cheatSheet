# python3-cheatSheet
A cheat sheet for python3 through following Corey Schafer's tutorial series. 

### Strings

Strings in python behave a similar way as in JS. For example, you can use either double or single quotes when you define them. But, in some cases you may need to use one or the other depending if the content itself has quotations or not. For example:

```
let_us_go = "let's go!"
```
In some cases, you'd use both single and double quotes and you'd still need to escape the content's single quote, for example:

```
sally_said = 'Sally said, "let\'s go!"'

```

Another way to escape quotation marks in strings in Python is to use three single/double quotes to define the string, this would run with no problems.

```
sally_said = '''Sally said, let's go!'''
```
### To know a string's length, we can use the `len()` function:

```
msg = "Hello World"

print(len(msg)) #prints 11
```
### We can access characters in a string through indexes (often referred to as slicing), like:

```
msg = "Hello World"

print(msg[0]) #prints 'H'

# we can access a range of characters through specifying the start and end of our indexes (start index is inclusive, end index is exclusive), for example:

print(msg[0:7]) #prints 'Hello W' 

#You don't need to specify the start or end, and python would just assume you've meant the start index [0] and end index [len(msg)-1]:

print(msg[:7]) #prints 'Hello W'
print(msg[:]) #prints 'Hello World'
print(msg[1:]) #ptins 'ello World'

#You can also use negative indexing, the last character of the string starts at (-1), for example:

print(msg[-1]) #prints 'd'

#But you can't start with a negative index. However, you can end with one, for example:

print(msg[-1:2]) #doesn't print anything
print(msg[1:-2]) #prints 'ello Wor'

#you can only start with a negative indexing if you specify the step to be negative (it's positive by default):

=> str[start:end:step] A step tells python from where to start indexing based on whether it's negative or positive. If it's positive start from left, if it's negative start from right. And it also tells it how big is the step it's taking. For example, if you set it to -2 it will start at -1 and then jump to include every 2-steps-away character from the starting point on the right. For example:

print(msg[-1:-9:-2]) #prints 'drWo' => started at (-1 > d) then jumped every two steps from there so (-3: r), (W:-5), (o:-7) starting from right (in reverse).

#And you can jump as many steps using a positive number as well, for example: 

print(0:7:2)  #prints 'HloW' (H:0), (l:2), (o:4), (W:6), starting from right (normal direction).

```

### You can use a number of methods on strings in Python, like:

```
To lowercase: print(msg.lower()) #prints 'hello world'

To uppercase: print(msg.upper()) #prints 'HELLO WORLD'
To uppercase cherrypick: print(msg[0:7:2].upper()) #prints 'HLOW'

To count a character's occurence in a string: print(msg.count('o')) #prints 2
To count a string's occurrence in a string:  print(msg.count('Hello')) #prints 1
If count doesn't find an occurence, retruns 0. 

To find where a character's occurrence in a string starts:  print(msg.find('H')) #prints 0
To find where a string's occurrence in a string starts:  print(msg.find('Hello')) #prints 0
If find doesn't find an occurence, it returns a -1. 

To replace a character's occurence in a string: print(msg.replace('o', 'i')) #prints 'Helli Wild'
To replace a string's occurrence in a string:  print(msg.replace('Hello', 'Hi')) #prints 'Hi World'
If replace doesn't find an occurence to replace, it retruns the original string. 

```
### To concatenate strings: 

You can concatenate strings the normal way as you'd usually do:

```
greeting = 'Hi'
name = 'Mark'

msg = greeting + name + '!'

print(msg)   #prints 'Hi Mark!'

```
But that's too much of a headache to do, and isn't clean enough. There is another way to concatenate strings using the `format()` method, like this:

```
person = {'name': 'Mark', 'age': 25}

intro = 'Hi I am {}, and I am {} years old'

intro_person = intro.format(person['name'], person['age'])

print(intro_person) #prints 'Hi I am Mark, and I am 25 years old'
```
Sometimes you may want to specify what goes where, especially if you're using it in more than one place: 

```

heading1 = {'tag': 'h1'}
content = {'text': 'Hello World'}

heading1_element = '<{0[tag]}>{1[text]}</{0[tag]}>'.format(heading1, content)

print(heading1_element) #prints '<h1>Hello World</h1>'

```
### Bonus: without using `format()` method:

```
person = {'name': 'Mark', 'age': 25}

intro = f"Hi I am {person['name'].upper()}, and I am {person['age']} years old" #throws an error if you use single quotes because keys already have them.

print(intro) #prints 'Hi I am MARK, and I am 25 years old'
```
### BONUS STUFF

We have multiple helpful methods that we can use, not necessarily _Just_ on strings, like:

- `dir(var)` => takes a variable for an arguement and displays all methods on that variable's calss. 

- `help(class)` => takes a class for an argument and displays everything available to us on this data type along with information. For example; displays methods and what they do. if we want to display info on a certain method only, we can do:

 ```
 help(class.method())
```

That's it for strings for now :)

