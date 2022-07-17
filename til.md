# 2022-07-16

## Interfaces in Python using `ABC` and `@abstractmethod`

```python
from abc import ABC, abstractmethod

class IDatabaseConnector(ABC):

    @abstractmethod
    def write(self):
        raise NotImplementedError
        
class PostgresConnector(IDatabaseConnector):

    def write(self):
        pass

class MysqlConnector(IDatabaseConnector):
    pass


if __name__ == '__main__':
    # instantiation works, b/c all abstract methods implemented
    postgres = PostgresConnector() 

    # instantiation throws error, b/c not all abstract methods implemented 
    mysql = MysqlConnector()  
```

## git command

```console
foo@bar:~$ git reset --hard HEAD
foo@bar:~$ git reset --hard HEAD~1
```

## enums

An enumeration is a set of symbolic names bound to unique, constant values. 

```python
from enum import Enum


class Colors(Enum):
    BLUE = 0
    RED = 0
    GREEN = 2

if __name__ == '__main__':
    print(repr(Colors.BLUE))
    print(Colors.BLUE)
    print(Colors.BLUE.value)
    print(Colors.BLUE.name)

    print()
    for color in Colors:
        print(color)

    # Because BLUE=0 and RED=0, it's like BLUE and RED are the same!
    print()
    print(len(Colors))
    print(color.BLUE == color.RED)
    print(color.BLUE.value == color.RED.value)

    # Enumeration members (BLUE, RED, GREEN) are hashable, hence can be used
    # as keys in dictionaries
    apples = {}
    apples[Colors.RED] = 'red delicious'
    apples[Colors.GREEN] = 'granny smith'
```

Running the script:

```console
foo@bar:~$ python enums.py

<Colors.BLUE: 0>
Colors.BLUE
0
BLUE

Colors.BLUE
Colors.GREEN

2
True
True
```
	
## virtualenv in python

virtuelenv is used to manage Python packages for different projects. Using virtualenv allows you to avoid installing Python packages globally (usually done with `pip install <package>`) which could break system tools or other projects.

You setup a virtualenv for every new project (think: repo) that you start. If you then activate the venv, any package that you install via `pip install <package>` will be installed in that specific virtual environment, and not globally.

You create a virtual environment in your project's directory. This creates a new directory `/path/to/project/env` that contains all the stuff of the virtual environment.

```console
foo@bar:~$ python3 -m venv env
```

Whenever you're working on your project, **activate** the environment:

```console
foo@bar:~$ source env/bin/activate
```

When you're done, **deactivate** the environment:

```console
foo@bar:~$ deactivate
```

## managing different python installations

If you have multiple python installations running, there exist some naming conventions. For example, `usr/bin/python2` is reserved for your installation of Python2.7, and `/usr/bin/python3` is reserved for your installation of Python3.x.

```console
foo@bar:~$ which python
/usr/bin/python

foo@bar:~$ which python2
/usr/bin/python2

foo@bar:~$ which python3
/usr/bin/python3
```