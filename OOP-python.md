
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

-----------------------------------

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

-----------------------------------

# ClassMethods and StaticMethods

We'll be looking at regular methods, class methods, and instance methods. 

Regular methods automatically take the instance (`self`) as the first argument, how can we change that to make it take the class argument instead? To do that, we're gonna be using class methods. And to turn a regular method into a class method, we add a **decorator** to the top called `@classmethod`. Let's allow the class to alter it's `raise_amount` variable dynamically by using a class method. 

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

    @classmethod
    # by convention, we use `cls` to refer to class. we can't use `class` bcuz it's a key word in Python
    def set_raise_amount(cls, amount):
        cls.raise_amount = amount #or you can do `Employee.raise_amount = amount`


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 50000)

print(Employee.raise_amount)  # prints 1.04
print(emp1.raise_amount)  # prints 1.04
print(emp2.raise_amount)  # prints 1.04
# cls arg is passed automatically, I only need to specify the `amount` arg
Employee.set_raise_amount(1.06)
print(Employee.raise_amount)  # prints 1.06
print(emp1.raise_amount)  # prints 1.06
print(emp2.raise_amount)  # prints 1.06

```

You can run classmethods from the instances as well, though it's not very heard of. Here's what it looks like nonetheless:

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

    @classmethod
    # by convention, we use `cls` to refer to class. we can't use `class` bcuz it's a key word in Python
    def set_raise_amount(cls, amount):
        Employee.raise_amount = amount


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 50000)

print(Employee.raise_amount)  # prints 1.04
print(emp1.raise_amount)  # prints 1.04
print(emp2.raise_amount)  # prints 1.04
# cls arg is passed automatically, I only need to specify the `amount` arg
emp1.set_raise_amount(1.06) #using an instance to update the class
print(Employee.raise_amount)  # prints 1.06
print(emp1.raise_amount)  # prints 1.06
print(emp2.raise_amount)  # prints 1.06
```

### Class methods as alternative constructors: 

You can use these class methods to provide multiple ways to create our objects. What if we had someone who was using our `Employee` class and they had these strings that hold employees information seperated by hyphens. And they need to constantly parse the string before they create employees. So is there any way to just pass the string and create an employee out of that?

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

    @classmethod
    # by convention, we use `cls` to refer to class. we can't use `class` bcuz it's a key word in Python
    def set_raise_amount(cls, amount):
        Employee.raise_amount = amount

    @classmethod
    # by convention, we use `cls` to refer to class. we can't use `class` bcuz it's a key word in Python
    def from_emps_strings(cls, emp_str):
        first, last, pay = emp_str.split('-')
        return cls(first, last, pay) #return a new Employee object => Employee(self, first, last, pay)


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 50000)

emp_string_list = ['Jack-Jones-90000', 'Jamie-James-100000', 'Mackenzie-Blake-700000']

new_emp_list = list(map(lambda string_ele: Employee.from_emps_strings(string_ele), emp_string_list))

for eachEle in new_emp_list:
    # prints Jack Jones 90000/ Jamie James 100000/ Mackenzie Blake 700000
    print(eachEle.fullname(), eachEle.pay)
```

### Static Methods:

Static methods don't pass anything automtically, neither the class nor the instance. Unlike class and instance methods. They're like regular functions and we include them in our classes because they have a logical connection in our class. Let's make a method that takes in a weekday and returns whether or not it was a weekday. 

```py
import datetime


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

    @classmethod
    # by convention, we use `cls` to refer to class. we can't use `class` bcuz it's a key word in Python
    def set_raise_amount(cls, amount):
        Employee.raise_amount = amount

    @classmethod
    # by convention, we use `cls` to refer to class. we can't use `class` bcuz it's a key word in Python
    def from_emps_strings(cls, emp_str):
        first, last, pay = emp_str.split('-')
        return cls(first, last, pay)

    @staticmethod
    # if you don't access the class or the instance, it should be a staticmethod
    def is_work_day(day):
        if day.weekday() == 5 or day.weekday() == 6:
            return False
        return True


emp1 = Employee('Mark', 'Miles', 50000)
emp2 = Employee('Frank', 'Famous', 50000)

my_date = datetime.date(2019, 6, 9)

print(Employee.is_work_day(my_date))  # prints False

```

------------------------------------

# Inheritance - Creating Subclasses

Ineritance allows us to inherit attributes and methods from a parent class. This is useful because we can create subclasses and get all the functionality of our parent class and then overwrite or add completely new functionality without affecting the parent class at all.  

Throughout this document about OOP, we have been talking about our `Employee` class. Let's say we wanted to create different types of Employees, so developers and managers. Now, developers and managers are still employees, and they definitely have first and last names, emails, and salaries. 

Instead of copying our Employee class in its entirey when making our developers and managers, we can inherit all the attrs and methods directly from `Employee`. Like this:

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

class Developer(Employee):
     pass
```

Now that we have defined our subclass, let's try using some of the parent's attrs and methods on our subclass:

```py
class Employee:
    raise_amount = 1.04
    num_of_emps = 0

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first + '.' + last + '@company.com'
        Employee.num_of_emps += 1  # each time an instance is initialized, this line will run.

    def fullname(self):
        return('{} {}'.format(self.first, self.last))

    def apply_raise(self):
        # this variable can be accessed on the class or the instance
        return (self.pay * self.raise_amount)


class Developer(Employee):
    pass


dev1 = Developer('Mark', 'Miles', 50000)
dev2 = Developer('Frank', 'Famous', 50000)

print(dev1.first)  # prints Mark
print(dev2.email)  # prints Frank.Famous@company.com
print(Developer.fullname(dev1))  # prints Mark Miles

```

To visulaize the relationship between a subclass and the parent class it inherits from, we can use the `help()` function:

```py
class Developer(Employee)
 |  Method resolution order:
 |      Developer
 |      Employee
 |      builtins.object
 |  
 |  Methods inherited from Employee:
 |  
 |  __init__(self, first, last, pay)
 |      Initialize self.  See help(type(self)) for accurate signature.
 |  
 |  apply_raise(self)
 |  
 |  fullname(self)
 |  
 |  ----------------------------------------------------------------------
 |  Data descriptors inherited from Employee:
 |  
 |  __dict__
 |      dictionary for instance variables (if defined)
 |  
 |  __weakref__
 |      list of weak references to the object (if defined)
 |  
 |  ----------------------------------------------------------------------
 |  Data and other attributes inherited from Employee:
 |  
 |  num_of_emps = 2
 |  
 |  raise_amount = 1.04

```

Things to keep note of:

`Methods Resolution Order`:  This is the level of inheritance Python looks at. So, it starts with the subclass itself, then the parent class, then the object class. Which is the base class that other classes inherits from.






























