
# Classes and instances:

## Why do we use classes?

They allow us to group our data and functions in an easy to reuse and build upon if we need to. Data and functions associated with a specific class are called functions and attributes. Classes are a blueprint to create instances. Each instance can be unique but what they have in common is that they're all a copy of the same original blueprint aka class.


## Example: Employees in a company.

Let's say we have a company that has employees and each one of them has a name, email, pay and tasks that they perform. Instead of building an employee object from the ground up we can use a blueprint called 'class', whic it covers the common traits but will still allow us to build upon it for each employee. 




#### To define a class

```py
class Employee:
     pass       # pass prevents python from throwing errors when you define a class/function that is empty
     
     
#emp1 and emp2 are instances of the Employee class
emp1 = Employee()  # prints <__main__.Employee object at 0x7f93cb6cf4e0>
emp2 = Employee()  # prints <__main__.Employee object at 0x7f93cb6cf4a8>
```
#### To create instance variables (manually): instance variables are unique data to that specifi instance.

```py
emp1.first = "Mark"
emp1.last = "Miles"
emp1.email = "Mark.Miles@company.com"
emp1.pay = 50000

emp2.first = "Frank"
emp2.last = "Famous"
emp2.email = "Frank.Famous@company.com"
emp2.pay = 80000

print(emp1.email)  # prints "Mark.Miles@company.com"
print(emp2.email)  # prints "Frank.Famous@company.com
```
#### Now this code is repetitive, we can initialize (construct) a class that has these attributes and can pass them down for each instance created:

```py

# Think of __init__  as the constructor/initializer. 
class Employee:
    def __init__(self, first, last, pay): # self is the instance e.g emp1, the other arguments are the methods and attrs.
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'   # email can be constructred from first+last


# Now you can specify the values you passed in your Employee class init method as args:
emp1 = Employee('Mark', 'Miles', 50000)  
emp2 = Employee('Frank', 'Famous', 80000)  

# you can leave 'self' out, because when you create the instance it's passed automatically as an arg to the init method.
# We don't need to pass the attrs (first, last, email, pay) manually since the init method will initialize them automatically for us.
```
### To define a method on our class:

```py

#Say that we wanted to print first and last name, usually we would do:

class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'

emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 80000)

print('{} {}'.format(emp1.first, emp1.last)) # prints out first and last name 'Mark Miles'
print('{} {}'.format(emp2.first, emp2.last)) # prints out first and last name 'Frank Famous'

# BUT a more effecient way of doing it; would be to define a method that does it automatically for us when we call it:

class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'

    def fullname(self): 
        return('{} {}'.format(self.first, self.last))  # we pass self to work with all instances. 
        
#if we forgot to pass self to our method, the instance would still pass it automatically (and the code will run normally long as we don't call the method) but once we call the method, the instance will pass itself as an arguement and our method wouldn't recongnize it.

emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 80000)

# print out first and last name using our new defined method
print(emp1.fullname())  # prints Mark Miles
print(emp2.fullname())  # prints Frank Famous

```

## Calling the method from the class VS calling on the instance:

```py
class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'

    def fullname(self):
        return('{} {}'.format(self.first, self.last))


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 80000)

print(emp1.fullname())  # prints Mark Miles
print(Employee.fullname(emp1))  # prints Mark Miles

```
If you take a look at our piece of code above, when we call the method on the instance, we don't need to pass any `self` argument because it passes itself as the self automatically. 

But if we call the method from the class, we will need to specify which instance do we wish to pass as the `self` argument. 


# Class Variables

## What are class variables?

Class variables are variables that are shared among all instances of a class. So whilst instance variables can be unique for each instance like the first name of an employee, last name, email and pay, class variables should be the same for each instance. 

Instance variables are the variables which are set using the self arguement inside a class. 

### Let's set a class variable: 

Let's say our company gives annual raises every year. So whilst the amount may be different from year to year, it's the same for all employees. 

First, let's hardcode the raise inside our class using a method:

```py
class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'

    def fullname(self):
        return('{} {}'.format(self.first, self.last))

    def apply_raise(self):
        return (self.pay * 1.04)


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 80000)

print(emp1.apply_raise())  # prints 52000.0
print(emp2.apply_raise())  # prints 83200.0

```

### what if we wanted to update the amount of raise easily? Right now the raise is hidden inside the function and it could be all over our code for all we know. Also, what if we wanted to be able to access it on our instances and class like any other attribute? This is where a class variable could be useful. So, let's make our raise into a class variable!

```py
class Employee:
    raise_amount = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'

    def fullname(self):
        return('{} {}'.format(self.first, self.last))

    def apply_raise(self):
        # this variable can be accessed on the class or the instance
        return (self.pay * Employee.raise_amount)


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 80000)

print(emp1.apply_raise())  # prints 52000.0
print(emp2.apply_raise())  # prints 83200.0
```

### But if those are class variables, why can we access them on both the class and instance? 

```py
class Employee:
    raise_amount = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'

    def fullname(self):
        return('{} {}'.format(self.first, self.last))

    def apply_raise(self):
        # this variable can be accessed on the class or the instance
        return (self.pay * Employee.raise_amount)


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 80000)

print(emp1.raise_amount)  # prints 1.04
print(emp2.raise_amount)  # prints 1.04
print(Employee.raise_amount)  # prints 1.04

```
What's going on here is that when we try to access an attribute on one of the instances, it will first check if the instance contains that variable (attribute) or not. It will look for the variable (attribute) in the class or the class it inherits from. `emp1` and `emp2` will look for the attr `raise_amount` in themselves, won't find it, and will look for that variable in the class. 

To understand how this works better, let's print out the headspace of both the instances and class:

```py
class Employee:
    raise_amount = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'

    def fullname(self):
        return('{} {}'.format(self.first, self.last))

    def apply_raise(self):
        # this variable can be accessed on the class or the instance
        return (self.pay * Employee.raise_amount)


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 80000)

# __dict__ method returns the headspace aka the object along with its attrs and methods
# prints {'first': 'Mark', 'last': 'Miles', 'pay': 50000, 'email': 'Mark.Miles @company.com'}
print(emp1.__dict__)
# prints {'first': 'Frank', 'last': 'Famous', 'pay': 80000, 'email': 'Frank.Famous @company.com'}
print(emp2.__dict__)
# prints {'__module__': '__main__', 'raise_amount': 1.04, '__init__': <function Employee.__init__ at 0x7fbf308c8620>, 'fullname': <function Employee.fullname at 0x7fbf308c88c8>, 'apply_raise': <function Employee.apply_raise at 0x7fbf308c8950>, '__dict__': <attribute '__dict__' of 'Employee' objects>, '__weakref__': <attribute '__weakref__' of 'Employee' objects>, '__doc__': None}
print(Employee.__dict__)
```
As you can see, `raise_amount` doesn't exist in `emp1` and `emp2` but it does exist in `Employee`. 

If you were to directly change the `raise_amount` from within the class `Employee`, it would change it for the class and across all instances:

```py
class Employee:
    raise_amount = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'

    def fullname(self):
        return('{} {}'.format(self.first, self.last))

    def apply_raise(self):
        # this variable can be accessed on the class or the instance
        return (self.pay * Employee.raise_amount)


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 80000)

emp1.raise_amount = 1.05  # changed raise_amount value

print(Employee.raise_amount)  # prints 1.05
print(emp1.raise_amount)  # prints 1.05
print(emp2.raise_amount)  # prints 1.05

```

What if we tried to change the `raise amount` variable from within one of the instances? 

```py
class Employee:
    raise_amount = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'

    def fullname(self):
        return('{} {}'.format(self.first, self.last))

    def apply_raise(self):
        # this variable can be accessed on the class or the instance
        return (self.pay * Employee.raise_amount)


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 80000)

emp1.raise_amount = 1.05  # sets a raise_amount variable that only lives on this instance

print(Employee.raise_amount)  # prints 1.04
print(emp1.raise_amount)  # prints 1.05
print(emp2.raise_amount)  # prints 1.04

```
Now the reason this happens is you're not changing anything when you do `emp1.raise_amount = 1.05`, you're only creating a new variable that's specific to the `emp1` instance. If you look at the print statements above, you'll notice that only the `raise_amount` of `emp1` was modified.

Now, this is important to understand because, as we said before, we can access the class variable either using the class or the instance itself. Now, that we have set the `raise_amount` variable for a particular instance, accessing the variable via `self` will allow us to customize the `raise_amount` we want for each Employee. 

Here's an example to illustrate what we mean:

```py
class Employee:
    raise_amount = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'

    def fullname(self):
        return('{} {}'.format(self.first, self.last))

    def apply_raise(self):
        # this variable can be accessed on the class or the instance
        return (self.pay * self.raise_amount)


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 50000)

emp1.raise_amount = 1.05  # sets a raise_amount variable that only lives on this instance

print(emp1.apply_raise())  # prints 52500.0
print(emp2.apply_raise())  # prints 52000.0

```
In this example, we unified the amount of pay for both employees. Also, we accessed the `raise_amount` class variable by using `self` instead of the `class` itself. 


### A use case where it's wiser to use the class name rather than the instance when accessing the class variable: 

Let's assume we have a new class variable called `num_of_emps` that keeps track of the number of employees across the company. Now, it wouldn't make sense to have a different number of employees for each employee since it would be the same across all the company for all employees at all times:

```py
class Employee:
    raise_amount = 1.04
    num_of_emps = 0

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + ' @company.com'
        Employee.num_of_emps += 1  # each time an instance is initialized, this line will run.

    def fullname(self):
        return('{} {}'.format(self.first, self.last))

    def apply_raise(self):
        # this variable can be accessed on the class or the instance
        return (self.pay * self.raise_amount)


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 50000)

print(Employee.num_of_emps)  # prints 2
print(emp1.num_of_emps)  # prints 2
print(emp2.num_of_emps)  # prints 2

```











































