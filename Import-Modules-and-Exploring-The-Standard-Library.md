
# Importing a module (code) from another file 

## Importing a file in the same directory: 

- To import a module, you can do:

```py
import testmod

# To access functions/variables:

function = testmod.modFun()
testVar = testmod.test

```

When you import a module, the code in the file is automatically run to define functions and variables. 

- You can use aliases if the name is too long:

```py
import testmod as TM

# To access functions/variables:

function = TM.modFun()
testVar = TM.test

```
- To import functions/vars on their own and access them directly:

```py
from testmod import test, modFun as my_fun

# To access functions/variables:

function = my_fun()
testVar = test

```
- To import everything from a module (bad practice because you can't know what was imported from where):

```py
from testmod import *

# To access functions/variables:

function = modFun()
testVar = test

```

## How does Python know where to find your files?

By default, if the file (module) you're trying to import is in the same directory, then python can import it no problem. Python has a list of directories that contains locations of where to go when looking for imports, and you can show this list by printing paths on the system module, like this:

```py
import sys
print(sys.path)

# prints

# ['/home/orjwan', '/usr/lib/python36.zip',
#  '/usr/lib/python3.6', '/usr/lib/python3.6/lib-dynload',
#  '/home/orjwan/.local/lib/python3.6/site-packages',
#  '/usr/local/lib/python3.6/dist-packages',
#  '/usr/lib/python3/dist-packages']

# first, current working directory path.
# 2nd, it lists paths added to the python path environment variables
# 3rd, standard library directories.
# 4th, site packages directory with third party packages
```
- If your file was in another directory, you can add that path manually to Python's list, like the following example:

```py
import sys
sys.path.append('/home/orjwan/Downloads')
import testmod # noqa: E402  => to prevent python flask linter from rearranging code.
```
Now, this isn't the best approach to solve this problem, mainly because if you had this decalaration in multiple files, you'd need to change them manually which isn't practical. So, we can add this new path in the next place Python looks - the Python path environment variables. 

To do this, we must add the following line to the `~/.bash_profile` file (we can use nano, which is a built in text-editor):

```py
export PYTHONPATH="/home/orjwan/Downloads" #this is an example directory

```
And then, after we save, we must **run** the `~/.bash_profile` file by typing in the terminal:

`source ~/.bash_profile` 

To check if it took effect or not, we fire up Python3 in the terminal and type:

`import testmod`

And it should work now :)

## The standard Library

Python has built in modules that we don't need to install in order to use. And they offer some valueable functionality that we don't need to rewrite again. (think of them as npm packages), here are some useful modules:

- `random` module:

```py
import random

nums = range(1, 11)

random_num = random.choice(nums)

print(random_num) #prints a different number each time
```

- To implement some mathmatical operations, we can use the `math` module:

```py
import math

angle = 90

# convert angle to radians
rads = math.radians(angle)

# find sin of radians
print(math.sin(rads)) #prints 1.0
```
- `datetime` and `calendar` modules:

```py
import datetime
import calendar

today = datetime.date.today()

print(today)  # prints 2019-06-08

print(calendar.isleap(2015))  # prints False
```

### `os` module: gives us access to the underlying operating system. 

```py
import os

print(os.getcwd())
# prints current working directory where this script is located
```
### BONUS STUFF

The standard library modules are python files, and you can take a look at them by opening the directory which they reside in. To do that, you can use the dunder file (dunder file => double underscore file => `__file__`) attribute:

```py
import os

print(os.__file__)
# prints current working directory where this script is located
# /usr/lib/python3.6/os.py
# then you can cd into /usr/lib/python3.6 and open it with atom for example.
```
Once you open the standard library and start exploring it, one of the first modules you'll stumble upon is the `antigravity` module. The `antigravity` module will open a browser page with a comic if you import and run it: 

```py
import antigravity

# run script
#open a web browser window.
```










