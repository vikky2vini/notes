## Python

###### Creating a virtual environment:
	1. Make sure the required virtualenv package is installed:
          (i.e. python-virtualenv python3-virtualenv)
    2. Create a directory for that project, cd into that project
          `$ mkdir projects/myproject && cd projects/myproject`
	3. Create the virtual environment:
          `$ virtualenv .lpenv` (if you want to use system's version of python)
          `$ virtualenv -p /usr/bin/python3 .lpvenv` (for a specific python version)
	3. Activate the virtual environment:
          `$ source /env/teamcity_env/bin/activate`
	4. Perform work
	5. Deactivate the virtual environment
          `$ deactivate`

###### Packages
Packages are nothing more than a folder, with a special file: __init__.py. This file doesn't need to hold any code, but its presense in this directory tells python that the folder is actually a package. The book "Learning Python" has a great writeup of what a package is and how it looks from a directory tree in the first chapter, in the section "How is Python code organized."

###### Creating a tuple:
    my_tuple = ("item1", "item2", "item3")
 Note: Parenthesis aren't necessary, but look better.
 Note 2: If creating a tuple with just a single value, it must end with a comma

###### Creating an empty tuple:
    t = tuple()

###### Creating a list:
    my_list = ["item1", "item2", "item3"]

###### Appending to an existing list:
    my_list.append("item4")

###### Creating a dictionary:
    my_dict = {'key1':'value1', 'key2':'value2'}

###### Creating an empty dictionary:
    d = dict()

###### If statement to check if an item is in a list:
    if "value4" in my_list:
        print("True")

###### Adding a key pair to an existing dictionary:
    my_dict['key3'] = 'value3'

###### Print contents of dictionary:
    my_dict

###### Print keys contained in a dictionary:
    my_dict.keys()

###### Print values contained in a dictionary:
    my_dict.values()

###### Example of iterating through dictionaries:
    for k,v in my_dict.items():
        print(k + ":" + v)

###### Creating a virtual environment:
	1. Make sure the required virtualenv package is installed:
          (i.e. python-virtualenv python3-virtualenv)
    2. Create a directory for that project, cd into that project
          `$ mkdir projects/myproject && cd projects/myproject`
	3. Create the virtual environment:
          `$ virtualenv .lpenv` (if you want to use system's version of python)
          `$ virtualenv -p /usr/bin/python3 .lpvenv` (for a specific python version)
	3. Activate the virtual environment:
          `$ source /env/teamcity_env/bin/activate`
	4. Perform work
	5. Deactivate the virtual environment
          `$ deactivate1


[More info on lists, tuples, and dictionaries](    http://www.wellho.net/solutions/python-python-list-python-tuple-python-dictionary.html)
