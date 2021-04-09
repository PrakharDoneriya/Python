# Meaning of Underscore & Dunders

## Patterns of Underscore used in Python
* Single Leading Underscore : _var
* Single Trailing Underscore : var_
* Double Leading Underscore : __var
* Double Leading and Trailing Underscore : \_\_var__
* Single Underscore : _

## 1.  Single Leading Underscore : "_var"
* This is used for naming convention only.
* It does not affect the behavior of program.
```python
class Test:
    def __init__(self):
        self.num1  = 11
        self._num2 = 23

if __name__ == "__main__" :
    t = Test()
    print(t.num1, t._num2)
```
* Output
```
11  23
```
As you have noticed _num2 didn't give any error, its just a naming convention

### Let's see how this impact if get imported from module
```python
# sample.py

def fun1():
    return "fun1"

def _fun2():
    return "fun2"

_name = "Python"
```
* Trying to import the *sample module* and use function and variable
```python
from sample import *

if __name__ == "__main__":
    print("fun1() -> ", fun1())
    print("_fun2() -> ", _fun2())
    print("_name -> ", _name)
```
* Output
```python
fun1() ->  fun1
Traceback (most recent call last):
  File <file_name>, line 5, in <module>
    print("_fun2() -> ", _fun2())
NameError: name '_fun2' is not defined
```
Similar error it will raise for *_name*. Wildcard import for importing all from the module, Python will not import names with leading underscore
We can use the names with leading underscore by two ways.

### a) Using *\_\_all__* list in the module
```python
# sample.py

__all__ = ["fun1", "_fun2", "_name"]

def fun1():
    return "fun1"

def _fun2():
    return "fun2"

_name = "Python"
```
* Trying to import the *sample module* and use function and variable
```python
from sample import *

if __name__ == "__main__":
    print("fun1() -> ", fun1())
    print("_fun2() -> ", _fun2())
    print("_name -> ", _name)
```
* Output
```python
fun1() ->  fun1
_fun2() ->  fun2
_name ->  Python
```
### b) By importing module
```python
# sample.py

def fun1():
    return "fun1"

def _fun2():
    return "fun2"

_name = "Python"
```
* Trying to import the *sample module* and use function and variable
```python
import sample

if __name__ == "__main__":
    print("fun1() -> ", sample.fun1())
    print("_fun2() -> ", sample._fun2())
    print("_name -> ",sample. _name)
```
* Output
```python
fun1() ->  fun1
_fun2() ->  fun2
_name ->  Python
```

## 2.  Single Trailing Underscore : "var_"
* Most of the times it happens the most fitting name of a variable is already taken by the Python Keywords, so we can't use them.
* Example -> def or class can't be used as a variable
* For avoiding the conflict a trailing underscore is used
```python
#   It will give syntax error
def make_object(name, class):
    pass

#   This will work fine
def make_object(name, class_):
    pass
```

## 3.  Double Leading Underscore : "__var"
* Double leading underscore force Python interpreter to rewrite the attribute name in order to avoid naming conflict in subclass, called as name mangling
```python
class Test:
    def __init__(self):
        self.num1   = 1
        self._num2  = 2
        self.__num3 = 3

if __name__ == "__main__" :
    print(dir(Test()))
```
* Output
```python
['_Test__num3', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', '_num2', 'num1']
```
Have you noticed __num3 in the output? (it is written as _Test__num3)
* Python does this to protect the variable from getting overridden in subclasses
Let's try to extend the class & try to override the exiting attributes
```python
class DerivedTest(Test):
    def __init__(self):
        super().__init__()
        self.num1   = 4
        self._num2  = 5
        self.__num3 = 6

if __name__ == "__main__" :
    dt = DerivedTest()
    print(dt.num1, dt._num2)
    print(dt.__num3)
```
* Output
```python
4 5
Traceback (most recent call last):
  File <file_name>, line 16, in <module>
    print(dt.__num3)
AttributeError: 'DerivedTest' object has no attribute '__num3'
```
AttributeError for dt.__num3
* Name mangling strikes again
```python
>>> dir(DerivedTest())
['_DerivedTest__num3', '_Test__num3', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', '_num2', 'num1']
```
Still there is a way to access __num3 of Test & DerivedTest
```python
>>> dt._DerivedTest__num3
6
>>> dt._Test__num3
3
```
### Some Examples related to name mangling
* Example 1 : Mangled Method
```python
class MangledMethod:
    def __method(self):
        return 42
    def call_method(self):
        return self.__method()

>>> MangledMethod().call_method()
42
>>> MangledMethod().__method()
AttributeError:
"'MangledMethod' object has no attribute '__method'"
```
* Example 2 : Surprising Example of name mangling
```python
_MangledGlobal__mangled = 23

class MangledGlobal:
    def test(self):
        return __mangled

>>> MangledGlobal().test()
23
```
If you are wondering about it, This is due to name mangling (__mangled will be written as _MangledGlobal__mangled), I was just able to take the reference

## 4.  Double Leading and Trailing Underscore : "\_\_var__"
* Name mangling is not applicable
* Names that have both leading an trailing double underscores are reserved for special use like *\_\_init__* for constructors and *\_\_call__* for object callable.
```python
class PrefixPostfixTest:
    def __init__(self):
        self.__bam__ = 42

>>> PrefixPostfixTest().__bam__
42
```

## 5.   Single Underscore : "_"
* Used to indicate that variable is temporary or insignificant
* Internally it is used as temporary variable, represents result of the last expression evaluated by interpreter.

### Some examples
* Example 1 : In a loop if we are interested in accessing index
```python
for _ in range(10):
    print("Do Something")
```
* Example 2 : In unpacking a tuple
```python
>>> car = ('red', 'auto', 12, 120)
>>> color, _, _, top_speed = car

>>> color
red
>>> top_speed
120
>>> _
12
```
* Example 3 :
```python
>>> 1 + 2
3
>>> _
3
>>> print(_)
3
```

## Dunders
* In Python Community, Dunders is referred as another name for double underscore
* Example :
    * ***__num*** is pronounce as ***dunder num*** instead of ***underscore underscore num***
    * ***\_\_init__*** is pronounce as ***dunder init*** instead of ***dunder init dunder***
