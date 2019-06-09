
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

