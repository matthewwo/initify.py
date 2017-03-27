initify.py
==========

The missing magical python decorator for simplifying your ``__init__(self, ...)`` function.

.. code:: python

    @init_args # Magical decorator
    def __init__(self, name="Lovely Lucy", age=10):
        pass

    p = Person()
    p.name # "Lovely Lucy"
    p.age  # 10 **Sweet**!

Inherited variables from super class
------------------------------------

If you have polymorphism structured classes, you'd love initify.

.. code:: python

    class Animal(object):
        def __init__(self):
            self.age = 0
            self.name = ""
            self.color = ""
            ...

    class Dog(Animal):
        @init_args
        def __init__(self, pet=True):
            pass
        ...

    class Cat(Animal):
        @init_args
        def __init__(self, wild=False):
            pass
        ...

.. code:: python

    d = Dog(age=3, name="Golfy", color="black")
    d.age    # 3
    d.name   # Golfy
    d.color  # black
    d.pet    # True

    c = Cat()
    c.age   # 0
    c.name  # ""
    c.color # ""
    c.wild  # False

--------------

That's dull :/ Don't judge until you see this:

Exclused variables
------------------

.. code:: python

    # Must declare with new-style class in python 2.7 or earlier
    # ``class Animal:`` is fine if using python 3 or later
    class Animal(object):
        def __init__(self):
            self.age = 0
            self.name = ""
            self.color = ""
            ...
            self.barks = True  # Only dog barks
            self.meows = True  # and only cat meows
            ...

    class Dog(Animal):
        @init_args(exclude=['meows'])  # Don't inherit meows from super class!
        def __init__(self, pet=True):
            pass
        ...

    class Cat(Animal):
        @init_args(exclude=['barks'])  # Don't inherit barks from super class!
        def __init__(self, wild=False):
            pass
        ...

.. code:: python

    d = Dog(age=3, name="Golfy", color="black")
    d.age    # 3
    d.name   # Golfy
    d.color  # black
    d.pet    # True
    ...
    d.barks  # True
    d.meows  # Attribute Error: meows is not defined!

    c = Cat()
    c.age   # 0
    c.name  # ""
    c.color # ""
    c.wild  # False
    ...
    d.meows  # True
    d.barks  # Attribute Error: barks is not defined!

Now this is neat hey?

Installation
------------

Install ``initify`` with pip or pip3.

.. code:: bash

    pip install initify

.. code:: bash

    pip3 install initify

Then whichever class you're using initify, do an import before using.
Example:

.. code:: python

    from initify import init_args

Now you can attach the decorator ``@init_args`` right before the class's
initializer ``def ___init___(self, ...)``. Enjoy your effort.

Support
-------

Hope this decorator can help you with your \`\ ``DRY``-iness in your
python project!

If you have any suggestion, please don't hesistate to give a post on the
issue page.

Cheers and happy hacking!
