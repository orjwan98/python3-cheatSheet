
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






