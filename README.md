# initify.py
The missing magical python decorator for simplifying your ```__init__(self, ...)``` function.

---
## Quick usage
```python
class Dog(Animal):
	@init_args  # The missing magical decorator
	def __init__(self, name, color)
		# No more yucky self.name self.color!!!
		pass
```

```python
d = Dog(name="Bobby", color="Blue")
# d.name   `Bobby`
# d.color  `Blue`
```
## Introduction
Rule of thumb, ```DRY``` (Don't Repeat Yourself). We've all been tired of doing variable assignments like this:

```python
class MyClass:
	def __init__(self, var1, var2, ...):
		self.var1 = var1
		self.var2 = var2
		...
```

Yikes! We're constantly repeating ourselves in typing self... self... Wonder if there's any better ways of writing initializer for python classes?

Now you have! ```initify.py``` is a simple decorator function attached to ```__init__(self, ...)``` and auto-magically sets the instance variable for you during runtime! No more pain in the... ```__init__``` :)

## Default values supported
Wanted to have default values for your initializer? No problem just throw it in!

```python
...
@init_args  # Magical decorator
def __init__(self, name="Lovely Lucy", age=10):
	# just do whatever other initialization you may need here
	pass  # Put a pass here if nothing to do
...
```
```python
p = Person()
p.name  # "Lovely Lucy"
p.age   # 10
```
Sweet!

## Inherited variables from super class
If you have polymorphism structured classes, you'd love initify.

```python
class Animal:
	def __init__(self, obj):  # REQUIRED reserve "obj" for super class injecting
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
```

```python
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
```
---

That's dull :/ Don't judge until you see this:
### Exclused variables
```python
class Animal:
	def __init__(self, obj):  # REQUIRED reserve "obj" for super class injecting
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
```

```python
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
```

Now this is neat hey?

## Installation
Download this repo using ```git``` or HTTP.

```bash
git clone https://github.com/prankymat/initify.py.git
```
Change directory into the repo

```bash
cd initify.py
```
Install using setup.py

```bash
python3 setup.py install
```

Then whichever class you're using initify, do an import before using. Example:

```python
from initify import init_args
```

Now you can attach the decorator ```@init_args``` right before the class's initializer ```def ___init___(self, ...)```. Enjoy your effort.

## Support
Hope this decorator can help you with your ```DRY``-iness in your python project!

If you have any suggestion, please don't hesistate to give a post on the issue page.

Cheers and happy hacking!
