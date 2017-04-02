=====
About
=====

This modules provides functionality to create classes with the intention
of mimicking another module or classes API and then invoking a dispatch
function to implement some desired, alternate behaviour.


Installation
============

Supported Python versions are: 2.7, 3.4, 3.5 and 3.6.

To install using pip:

::

    pip install git+https://github.com/aubreystarktoller/api-mimic.git

You can obtain the source from:

::

    https://github.com/aubreystarktoller/lite-boolean-formulae


Usage
=====

`api_mimic.mimic_factory(api_dict)`

This function takes a dictionary of string/function key/value pairs
and uses them to create a class with methods whose names and function
signatures exactly match those in the dictionary.

The created class takes a callback function as it's sole initialization.
This function must take take a string and a dictionary as it's only
positional arguments. This function is called whenever a method on
generated class is called, and the name of method called is used as
the callback function's first argument, the and the arguments that the
method was invoked with as the second.

The method's arguments are passed as a dictionary with the argument name
as the key for that argument's value. If the method can be invoked with
unbound positional arguments (e.g. *args) then the argument name and a 
tuple of all unbound arguments form a key pair.

Example usage
=============

::

    In [1]: from api_mimic import mimic_factory
       ...:
       ...: def func1(a, b, c):
       ...:     pass
       ...:
       ...:
       ...: def func2(a, *b, c, **kwargs):
       ...:     pass
       ...:
       ...:
       ...: def callback(name, args):
       ...:   print('function name: ' + name)
       ...:   print('function called with: ' + str(args))
       ...:
       ...:
       ...: cls = mimic_factory({'func1': func1, 'func2': func2})
       ...:
       ...: cls(callback).func2(1, 2, 3, 4, 5, c=6, d=7)
    
    Out[1]: function name: func2
       ...: function called with: {'a': 1, 'b': (2, 3, 4, 5), 'c': 6, 'd': 7}

 
Testing
=======

It is recommend that you use `mak`e and `tox` to run the tests. First clone
the git repository and then enter the cloned repository:

::

    git clone https://github.com/aubreystarktoller/api-mimic
    cd api-mimic

If you are using `make` and `tox` just run:

::

     tox

To run the tests for Python 3 in the current environment using make:

::
    make test3

Or for Python 2:

::
    make test2

If you're not using `make`, then to run the tests in the current environment:

::

    setup.py test

Coverage
--------

If you have `make` and the `coverage` package installed code coverage
for Python 3 can be tested by running:

::

    make coverage3

And for Python 2 it can be tested using:


::

    make coverage2


Authors
=======
* Aubrey Stark-Toller


License
=======
lite-boolean-formula is licensed under the BSD license. See
LICENSE for the full license.