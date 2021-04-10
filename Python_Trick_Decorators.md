# Python Trick :: Decorators

## Decorators
* Allows to modify and extend behavior of function, method or classes without permanently modifying.
* Syntax -> only need to put @<decorator_name> before the definition.

```python
def my_decorator(function):
    print("Hi,")
    return function

@my_decorator
def fun():
    return "Python Programmer"

if __name__ == "__main__" :
    string = fun()
    print(string)
```
* Output
```python
Hi,
Python Programmer
```
## If you are wondering what happens here & How it works ?
* It is just like passing function to another function & return from some another function
```python
def my_decorator(function):
    print("Hi,")
    return function

def fun():
    return "Python Programmer"

if __name__ == "__main__" :
    my_function = my_decorator(fun)
    print(my_function())
```
* Output
```python
Hi,
Python Programmer
```
* ### Simplest decorator can be written as
```python
def my_decorator(function):
    return function

@my_decorator
def fun():
    return "Python Programmer"

if __name__ == "__main__" :
    print(fun())
```
* Output
```python
Python Programmer
```
## How to change the behavior using decorators
* ### Changing string to upper case
```python
def change_to_upper_case(function):
    def update_case():
        function_data = function()
        updated_data  = function_data.upper()
        return updated_data
    return update_case

@change_to_upper_case
def fun():
    return "hi, python programmer"

if __name__ == "__main__":
    string = fun()
    print(string)
```
* Output
```python
HI, PYTHON PROGRAMMER
```
### We can change the behavior of decoration by defining function inside function & use them for modifying
For the above example
* we call fun function that calls the change_to_upper_case decorator
* Decorator is returning a function defined inside, decorator called update_case function
* update_case function stores the data returned by fun function then change its case & returned it

## How to use multiple decorators & How it works
* You can use multiple decorators, it applied from bottom to top order
```python
def decorator1(function):
    print("In Decorator 1")
    return function

def decorator2(function):
    print("In Decorator 2")
    return function

@decorator1
@decorator2
def my_decorator():
    return "In My Decorator"

if __name__ == "__main__":
    print(my_decorator())
```
* Output
```python
In Decorator 2
In Decorator 1
In My Decorator
```
*   You can also modify the behavior as explained in previous example