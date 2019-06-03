
# Integers and Floats

To find the type of a variable we can do:

```
num = 1
name = 'Mark'

print(num, ' is a ', type(num)) #prints "1  is a  <class 'int'>"

print(name, ' is a ', type(name)) #prints "Mark  is a  <class 'str'>"

```
### Arithmetic operators: 

All Arithemetic operators in Python are the same as normal Maths (and JS), but some stuff to take note of are:

#### Division & Floor Division

```
# Division

division = 5 / 2

print(division) #prints 2.5

# Floor Division
 
floor_division = 5 // 2

print(floor_division) #prints 2

```
#### Exponent (something to power of something else)

```
num = 3

print(num ** num) #prints 27
print(num ** 4) #prints 81
```
#### Modulus (return the remainder)

```
print(2 % 2) #prints 0
print(5 % 2) #prints 1

```

### Arithmetic happens from left to right with the following order `( () >>> * or / >>> + or - )` 

```
print (45 / 3 * 5 + 5 * 2 - 1 ) #prints 84.0
print (45 / (3 * 5) + 5 * (2 - 1) ) #prints 8.0
```

### Increment, decrement, multiply, divide:


increment:

```
num = 3 

num += num

print(num) #prints 6

```

decrement:

```
num = 3 

num -= num

print(num) #prints 0

```
multiply:

```
num = 3 

num *= num

print(num) #prints 9

```
divide:

```
num = 3 

num /= num

print(num) #prints 1

```

### Some methods to apply to numbers:

- `abs()` => returns the absolute value of a number. Example `print(abs(-3)) #prints 3`
- `round()` => round number to nearest integer. `print(round(3.75)) #prints 4` but you can pass another arguement and round it a number after the decimal. `print(round(3.75, 1)) #prints 3.8`


### casting strings to numbers:

`print(int('100')) #prints 100`








