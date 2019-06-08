# OS Module 

The `OS` module is a standard library module that gives us access to the underlying operating system. 

- To get current working directory (where our script is located):

```py
import os

print(os.getcwd())  # prints /home/orjwan

```
- To change current working directory:

```py
import os

print(os.getcwd())  # prints /home/orjwan

os.chdir('/home/orjwan/Downloads')

print(os.getcwd())  # prints /home/orjwan/Downloads
```

- To get a list of files and folders on the current directory:

```py
import os

print(os.getcwd())  # prints /home/orjwan

os.chdir('/home/orjwan/Downloads')

print(os.listdir())  # prints list of all files and folders on /home/orjwan/Downloads
```
-To create a folder/folders on current directory:

```py
import os

print(os.getcwd())  # prints /home/orjwan

# makes newFolder on current working directory
# throws an error if folder already exists
os.mkdir('newFolder')

# To make a folder that is a couple of levels deep, we use
# throws an error if folder already exists
os.makedirs('newNewFolder/new-4-folder/new-5-folder')

# prints list of all files and folders on /home/orjwan/Downloads
print(os.listdir())
```
- To remove a folder/folders on current working directory:
```py
import os

print(os.getcwd())  # prints /home/orjwan

# removes newFolder on current working directory
# throws an error if folder doesn't exist
os.rmdir('newFolder')

# To remove a folder that is a couple of levels deep, we use
# throws an error if folder doesn't exist
os.removedirs('newNewFolder/new-4-folder/new-5-folder')

# prints list of all files and folders on /home/orjwan/Downloads
print(os.listdir())
```
-To rename a file/folder in current working directory:

```py
import os

print(os.getcwd())  # prints /home/orjwan

# to rename a file/folder, we use:
# first arg is the target's name, 2nd arg is the new name
os.rename('3hd', '3HD')

# prints list of all files and folders on /home/orjwan/Downloads
print(os.listdir())
```
- To get a file/folder's information, we can do:

```py
import os
from datetime import datetime

print(os.getcwd())  # prints /home/orjwan

# to get info on a specific file/folder, we use:

print(os.stat('test.py'))  # prints info about test.py file

size_bytes = os.stat('test.py').st_size

print(size_bytes)  # prints file's size in bytes

# last modified timestamp
modified_time = os.stat('test.py').st_mtime

human_readable_modified_time = datetime.fromtimestamp(modified_time)

# prints modified_time in a human readable text (2019-06-08 16:11:53.241706)
print(human_readable_modified_time)
```






