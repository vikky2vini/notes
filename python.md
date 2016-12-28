## Python

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
	1. sudo pip install virtualenv
	2. virtualenv /env/teamcity_env
	3. source /env/teamcity_env/bin/activate
	4. pip install -r requirements.txt (install list of packages listedin file)
	5. virtualenv-2.7 /env/teamcity_env2

[More info on lists, tuples, and dictionaries](    http://www.wellho.net/solutions/python-python-list-python-tuple-python-dictionary.html)
