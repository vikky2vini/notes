# Python

## Virtual Environments

###### Creating a virtual environment:
	1. Make sure the required virtualenv package is installed:
          (i.e. python-virtualenv python3-virtualenv)
    2. Create the virtual environment
          `virtualenv my-project-name`
          Note: This should create the project folder for you
          `virtualenv -p /usr/bin/python3 my-project-name` (for python3)
    3. Activate the virtual environment
          `cd <project_dir>`
          `source bin/activate`
	4. Perform work
	5. Deactivate the virtual environment
          `$ deactivate`

###### Freezing a virtual environment:
"Freezing" a virtual environment creates a requirements.txt file containing all the packages that are installed.
	`pip freeze > requirements.txt`

###### Installing packages from a requirements.txt file
    `pip install -r requirements.txt`

## Packages
* Packages are nothing more than a folder, with a special file: `__init__.py`. This file doesn't need to hold any code, but its presence in this directory tells python that the folder is actually a package.
* The book "Learning Python" has a great writeup of what a package is and how it looks from a directory tree in the first chapter, in the section "How is Python code organized."

## Variables
* Variables that are constants should be in upper case
* Variables that are created on "indent level 0" are global variables
* Global variables are a bad thing, because any code anywhere can change their values

## Classes
* A class is a classification of an object
* An object is a particular instance of a class
* Objects have attributes (name, age, etc) and methods
* Classes are a way of packaging variables and functions together.
* Class names should begin with an uppercase letter
* `def__init__(self)` is a special function called a constructor
* The constructor is called first when an object from the class is created
* Inside a class, parameters using self.<whatever> refer specically to the object created from the class
* Inside a class, a variable beginning with self.<whatever> is an instance variable
* A parameter within a class that doesn't include self.* is a static variable
* Instance variables are used when tracking an individual item, for example, a persons age
* A static variable is for tracking something globally, like a counter for how many people there are


###### Example:

    class Address():
        """ Hold all the fields for a mailing address """
        def __init__(self):
            self.name = ""
            self.line1 = ""
            self.line2 = ""
            self.city = ""
            self.state = ""
            self.zip = ""

    home_address = Address()
    home_address.name = "John Doe"
    home_address.line1 = "123 Address st
    print(home_address.name)

###### Example with required parameter
    class Dog():

        def __init__(self, new_name):
            """  Constructor. """
            self.name = new_name
            print("A new dog object was created!")  # just an example, prints when object created

    # To create the dog:
    my_dog = Dog("Spot")

    # This will error (no name provided):
    herDog = Dog()

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

###### Another example:
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
    
    
###### Methods    
* Methods define what an object can do
* A method is a function that exists inside of a class
* method definitions in a class look like any other function declaration,
    but they include self (self is required even if the function doesn't use it):

    class Dog():
        def __init__(self):
            self.age = 0
            self.name = ""
            self.weight = 0

        def bark(self):
            print("Woof")



## Inheritance:
To Do: Add description and some notes here

###### Basic Example:

    class Parent():
        def print_last_name(self):
            print("Smith")

    class Child(Parent): # This class is inheriting from Parent
        def print_first_name(self):
            print("Jason")

    r = Child()
    r.print_first_name()
    r.print_last_name() # We can do this, because class Child inherits from Parent

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
* Dictionaries are also known as "associative arrays"
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

## string data type
* Accessing a string at a precise character is known as indexing. Selecting a group of characters is known as slicing.
* You can declare a string of multiple lines with ''' or """
* If you use s[:] to call a string, it will print the entire string. Reason being, it uses the default start point (the beginning) and the default stop point (the end) as well as the default step (stepping 1 character at a time)

## bool data type
* If a bool value is anything other than 0, it is true

## fractions
* You can use the Fraction class to deal with fractions. f = Fraction(10, 6)
* You can call the numerator and denominator of a fraction directly.

    `f.numerator`

    `f.denominator`

## Debugging
These notes were taken from the April 2017 Penguicon panel. I have yet to test most of these.

###### Start the debugger:
The following will start python in debug mode and allow you to step through the script.

     python -m pdb filename.py

###### Debugger commands:

u,d (move up and down the stack)
n (execute the current statement, goes to the next line)
b (show all break points, with its number)
b linenum (set a break point at linenum)
display <variable> (python3 only, displays variable any time it's changed, undisplay turns it off)
disable number (disable breakpoint number)
enable number (enable breakpoint number)
tbreak linenum (set a temporary breakpoint at lineno, which is removed when first hit)
c (continue exection until a breakpoint is encountered)
s (execute and step into function)
p expr (print expression)
pp expr ("pretty print" the value of expr)
l (list 11 lines of code around the current location)

###### Start the debugger (within the code):

     import pdb
		 pdb.set_trace()

###### pdbpp
pdbpp is a drop-in replacement for pdb, with better features (colorization, tab completion, etc).
Install it with the following command:

     `$ pip install pdbpp`

###### Useful debugging resources
https://github.com/nblock/pdb-cheatsheet/blob/master/pdb-cheatsheet.pdf
https://pymotw.com/3/pdb/
https://docs.python.org/3/library/pdb.html
https://pypi.python.org/pypi/pdbpp/

## misc notes
* When an object is created, it gets an id.
* Python integers have unlimited range, limited only by the available virtual memory
* Using / in division is true division. Using // is floored division
* Integer division in Python is always rounded towards minus infinity
* When you create two objects with the same value, the id's will be different. That is, unless the value is small, in which case Python will map to the same id to save memory.


[More info on lists, tuples, and dictionaries](    http://www.wellho.net/solutions/python-python-list-python-tuple-python-dictionary.html)
