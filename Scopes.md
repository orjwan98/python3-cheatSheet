
# Python variable scope 

Python follows `LEGB` abbreviation rules when it comes to scoping. And it stands for `L`ocal, `E`nclosing, `G`lobal, `B`uilt-ins. 

Python follows the below order when looking for variables:

 **Local**: Local scope of a function.
 **Enclosing**: Enclosing scope of a function. (nested functions)
 **Global**: Global scope - defined at the top levle of a module or declared explicitly global by using the `global` keyword.
 **Built-ins**: built in functions/method e.g `min()`. 
 
 ## Local and Global scopes:
 
 ```py
 x = 'global x'


def test():
    y = 'local y'
    print(y)  # looks for y in local scope, finds it and prints it.
    print(x)
    # looks for x in local scope, doesn't find it so looks outside for it, finds it and prints it.


print(y)  # looks for y in current scope (global), doesn't find it and throws an error
print(x)  # looks for x in the global scope, finds it and prints it
test()
 ```
 
 
 - vars in functions don't overwrite higher-level-vars (unless explicitly told to). The x var in the function only lives in that space and anything outside of the function can still see and use the global x. 
 
 ```py
 x = 'global x'


def test():
    x = 'local x'
    print(x)
    # looks for x in local scope,finds it and prints it.


test()
print(x)  # looks for x in the global scope, finds it and prints it


# var x in the func won't overwrite global x.
 ```
 
 - To tell Python that you're referring to the same x defined in your global scope to be used in the local scope of your function:
 
 ```py
 x = 'global x' #you don't need this. You can comment it out and your code would still work. Try it.


def test():
    global x  # I am referring to the same x in my func as the global one.
    x = 'local x'
    print(x)
    # looks for x in local scope,finds it and prints it.


test()
print(x)  # looks for x in the global scope, finds it and prints it.
# (it's been overwritten in the test function => prints local x)
 ```
 
 NOTE: something to note is that global statements shouldn't be overused as it can make the code very hard to maintain because you'll constantly be worried about your functions overwriting values outside that can affect other functions. 
 
 - Function paramteres/arguments only live inside that funciton's scope, example:
 
 ```py
 def test(z):

    print(z)
    # looks for z in local scope,finds it and prints it.


test('local z')
print(z)  # looks for z in global scope, doesn't find it, throws an error.

 ```
 
 ## Built-ins
 
 Python doesn't prevent us from overwriting built-ins so we need to understand how to prevent ourselves from overwriting them. Here's an example on how this works:
 
 ```py
 
import builtins

print(dir(builtins))  # prints out a list of attributes on a given object


def min():
    print('You reached our new defined min')


mini = min([1, 2, 3, 4, 5])
# throws an err because we already have a min function 
# defined in the global scope (which takes priority over built-ins)
# which takes priority and overwrites the built-in min() function.
# we can either comment out the built-in min function or
# rename the min() function we defined in the global scope

print(mini)
 
 ```
 ## Enclosing 
 
 Enclosing is the Global scope for child functions of a parent function. And behaves in a similar way. Local - Enclosing - Global - Builtins. 
 
 ```py
 def outer():
    x = 'outer enclosed x'

    def inner():
        x = 'inner enclosed x'  # if this was commented out, it would print 'outer enclosed x'
        print(x)  # looks for x in its inner scope, finds it and prints it.
    inner()
    print(x)  # prints what it can see in its scope, the outer enclosed x


outer()  # if outer enclosed x was commented out, it would throw an error
 ```
 To force our code to use the Enclosing variable of a parent function in a child function, we can do: 
 
 ```py
 def outer():
    x = 'outer enclosed x'

    def inner():
        nonlocal x  # allows us to refer to outer enclosed x
        x = 'inner enclosed x'  # overwrties outer enclosed x
        print(x)  # prints inner enclosed x
    inner()
    print(x)  # prints inner enclosed x


outer()
 ```
 ### Basically the more inner it is , the more it takes priority and the less acessible it is for the outers. The outer it is, the more accessible it is to the inners. 
 
 ```py
 
x = 'global x'


def outer():
    # x = 'outer enclosed x'

    def inner():
        # x = 'inner enclosed x'
        print(x)  # prints global x
    inner()
    print(x)  # prints global x


outer()
print(x)  # prints global
 
 ```
 
 
 
 
 
 
 
 
 
