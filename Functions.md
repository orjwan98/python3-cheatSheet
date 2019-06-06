
# Functions

To deifne and call a function in python, we do: 

```py
def sayHi(greeting, name):
    print('{} {}!'.format(greeting, name)) #prints Hey Mark!

sayHi('Hey', 'Mark')
```
Returning a value out of a function:

```py
def sayHi(greeting, name):
    return('{} {}!'.format(greeting, name))  


print(sayHi('Hey', 'Mark').upper()) #prints HEY MARK!
```
To pass a default value to the parameters in case no arguements is supplied, we can do:

```py
def sayHi(greeting='Hi', name='Jack'):
    return('{} {}!'.format(greeting, name))


print(sayHi(greeting='Hello')) #prints Hello Jack!
```
To pass a number of arguements and key values, we can use `*args` (stands for arguements) and `**kwargs` (stands for keyword arguements) placeholders in functions, like the following:

```py
def studentInfo(*args, **kwargs):
    my_name = args[0].format(kwargs['name'])  # My name is Mark
    my_age = args[1].format(kwargs['age'])  # and I am 25
    last_course = kwargs['courses'].pop().lower()  # physics
    courses_string = ', '.join(kwargs['courses']).lower()  # history, science, biology
    my_courses = args[2].format(courses_string)  # and I am taking history, science, biology
    intro = f'{my_name} {my_age} {my_courses} & {last_course} courses.'
    # My name is Mark and I am taking history, science, biology & physics courses.
    print(intro)


studentInfo('My name is {}', 'and I am {}', 'and I am taking {}',
            name='Mark', age=25,
            courses=['History', 'Science', 'Biology', 'Physics'])
```
