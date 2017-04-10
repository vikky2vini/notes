# Python

## Virtual Environments

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

## Packages
* Packages are nothing more than a folder, with a special file: `__init__.py`. This file doesn't need to hold any code, but its presence in this directory tells python that the folder is actually a package.
* The book "Learning Python" has a great writeup of what a package is and how it looks from a directory tree in the first chapter, in the section "How is Python code organized."

## Classes
* Classes are a way of packaging variables and functions together.
* Inside a class, `__init__` is executed first.

###### Example:

    class Enemy():
        life = 3

        def attack(self):
            print("Was attacked")
            self.life -= 1

        def checkLife(self):
            print(str(self.life))

    enemy1 = Enemy()
    enemy1.attack()
    enemy1.checkLife()

###### Example with instance and class variables:

    class Hero:
        profession = 'Hero'  # Class variable

        def __init__(self, name):
            self.name = name  # Instance variable

    t = Hero("Terra")
    c = Hero("Cloud")
    print(t.name)
    print(t.profession)
    print(c.name)
    print(c.profession)

###### Antoher example:
In the example below, every Hero created from this class will always start with 100 health.

    class Hero:
        def __init__(self, name):
            self.name = name
            self.health = 100

        def eat(self, food):
            if (food == 'apple'):
                self.health -= 50
            elif (food == 'ham'):
                self.health -= 20

    my_hero = Hero("Bob")
    print my_hero.name
    print my_hero.health

    my_hero.eat("apple")
    print my_hero.health

    my_hero.eat("ham")
    print my_hero.health

###### Another example, using `__init__`:

    class Enemy:
        def __init__(self, x): # Every class will set up the energy variable for the object.
            self.energy = x

        def get_energy(self):
            print(self.energy)

    jason = Enemy(5)  # Create an instance of enemy, pass 5 to self.energy for that object
    boss = Enemy(18)

    jason.get_energy()
    boss.get_energy)

## Inheritance:
To Do: Add description and some notes here

###### Basic Example:

    class Parent():
        def print_last_name(self):
            print("Smith")

    class Child(Parent): <---- This class is inheriting from Parent
        def print_first_name(self):
            print("Jason")

    r = Child()
    r.print_first_name()
    r.print_last_name() <---- We can do this, because class Child inherits from Parent

###### Overriding:

We can override something from another class, using the same function and same name. Like this.

    Class Child(Parent):
        def print_last_name(self):
            print("Williams")

## Multiple Inheritance:

###### Inheriting from more than one class:

    class Mario():
        def move(self):
            print("I am moving")

    class Mushroom():
        def eat_mushroom(self):
            print("Mario got big")

    class BigMario(Mario, Mushroom):  # Inheriting from both
        pass  # We don't need to do anything in order to inherit

    bm = BigMario()
    bm.move()
    bm.eat_mushroom()

## Threading

Example:

    import threading

    class InstantMessenger(threading.Thread):
        def run(self):
            for _ in range(16):
                print(threading.currentThread().getName())

    x = InstantMessenger(name = 'Send out messages')  # we can give names to threads.
    y = InstantMessenger(name = 'Receive messages')
    x.start()  # the start function looks for a function named run
    y.start()

## os module

###### Example of os.name:

    import os

    print(os.name)
    print(list(os.environ.items())) # Not very pretty
    for param in os.environ.keys(): # For loop iterates through items and prints them, prettier
        print(param, os.environ[param])

###### Example of path.join:

    import os

    p = os.path.join('/' 'home')

    print(p)

    print(os.listdir(p))

###### Print the current working directory:

		currentdir = os.getcwd() # Give us our current working directory
		print(currentdir)

###### List contents of current dir:

    print(os.listdir(os.curdir))

###### Change working directory:

    os.chdir('/home/jlacroix/music')
    print(os.listdir(os.curdir))

###### Output of Music folder, iterated into a print statement, to make it look better:
    musicdir = os.chdir('/home/jlacroix/Music')
    for artist in os.listdir():
        print(artist)

###### Rename a file or folder:

		os.rename('oldname', 'newname')

###### Delete a file:

		os.remove('filename.txt')

## File Handling
###### Open a file for reading:

    mf = open('python.py', 'r')

###### Open a file for writing (replaces current content):

    mf = open('python.py', 'w')

###### Open a file for appending new content:

    mf = open('python.py', 'a')

###### Open a file for writing an use the unversal newline character:

    mf = open('python.py', 'U')

###### Write to the file:

    mf.write('hello\v')

###### Read individual lines in a file:

    mf.readline()

###### Reads files into list of stings:

    mf.readlines()

###### Close file handle when finished:

    mf.close()

## tuples
* tuples are immutable
* In a tuple, items are separated by commas
* Sometimes tuples are used implicitly, for example to set up multiple variables on one line, or to allow a function to return multiple different objects.
* You still need the comma in a tuple, even when only declaring a single element: t = (42, )
* The braces are actually optional when creating a tuple, but possibly look better

###### Creating a tuple:
    my_tuple = ("item1", "item2", "item3")
 Note: Parenthesis aren't necessary, but look better.
 Note 2: If creating a tuple with just a single value, it must end with a comma

###### Creating an empty tuple:
    t = tuple()  # or: t = ()

###### Tuple with three objects:

    t = (1, 3, 5)

## Lists
* Lists are mutable

###### Creating a list:

    mylist = [1, 2, 1, 3]

###### Appending to an existing list:

		mylist.append(13)

###### Other list examples:

		mylist.count(1)  # How may '1' are in the array

		mylist.index(13)  # Position of '13' in the list

		mylist.insert(0, 17)  # Insert '17' at position 0, current values shift to the right

		mylist.pop()  # Pop (remove and return) last element

		mylist.pop(3)  # pop element at position 3

		mylist.remove(17)  # Remove '17' from the list

		mylist.sort()  # Sort the list, this actually changes the list to a sorted version

## dictionaries
* dictionaries are mutable
* It maps keys to values.
* The keys are hashable.
* They are the backbone of every Python object.

###### Creating a dictionary:
    mydict = {'key1':'value1', 'key2':'value2'}
		mydict = {}
    mydict = dict(A=1, z=-1)
    mydict = {'A': 1, 'a': -1}

###### Creating an empty dictionary:
    d = dict()

###### Add a new value to the dictionary:

    mydict['a'] = 1

###### Fetch the value of 'a' from a dictionary:

    mydict['a']

###### Fetch the entire dictionary:

    mydict

###### Is an item in the dictionary?

    'e' in mydict

###### Clear out the dictionary:

    mydict.clear()

###### View only the values in a dictionary:

    mydict.values()

###### View only the keys in a dictionary:

    mydict.keys()

###### View only the items in the dictionary:

    mydict.items()  # This is the same as 'mydict' executed by itself so how is it different?

###### Example of iterating through dictionaries:
    for k,v in my_dict.items():
        print(k + ":" + v)

## namespaces
* If you do not create a namespace, the object is within the global namespace.

## Immutability
* Integer data types are immutable.
* Immutable sequences are strings, tuples, and bytes.
* If you create age = 42, then age = 43, you created two objects with the values of 42 and 43, but changed age to point to a different object. Their id's would be different. So basically, first age pointed to an int object with value 42, but now points to a different int object with a value of 43

# string data type
* Accessing a string at a precise character is known as indexing. Selecting a group of characters is known as slicing.
* You can declare a string of multiple lines with ''' or """
* If you use s[:] to call a string, it will print the entire string. Reason being, it uses the default start point (the beginning) and the default stop point (the end) as well as the default step (stepping 1 character at a time)

# bool data type
* If a bool value is anything other than 0, it is true

# fractions
* You can use the Fraction class to deal with fractions. f = Fraction(10, 6)
* You can call the numerator and denominator of a fraction directly.

    `f.numerator`
		
    `f.denominator`

# misc notes
* When an object is created, it gets an id.
* Python integers have unlimited range, limited only by the available virtual memory
* Using / in division is true division. Using // is floored division
* Integer division in Python is always rounded towards minus infinity

[More info on lists, tuples, and dictionaries](    http://www.wellho.net/solutions/python-python-list-python-tuple-python-dictionary.html)
