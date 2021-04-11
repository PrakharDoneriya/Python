# Everything is Object in Python
* Functions are objects
    * Can be assigned to variables
    * Can store in data structures
    * Can pass as an argument
```python
def yell(text):
    print(text.upper())

if __name__ == "__main__" :
    yell("hi, python programmer")
```
* Output
```python
HI, PYTHON PROGRAMMER
```
### Assigning function to a variable
```python
bark = yell
bark("woof")

print("bark function is pointing to {}".format(bark.__name__))
```
* Output
```
WOOF
bark function is pointing to yell
```
### What if we delete yell function?
```python
def yell(text):
    print(text.upper())

bark = yell

if __name__ == "__main__" :
    del yell
    bark("hi")
    print("bark function is pointing to {}".format(bark.__name__))
    yell("hey")
```
* Output
```python
HI
bark function is pointing to yell
Traceback (most recent call last):
  File <file_name>, line 10, in <module>
    yell("hey")
NameError: name 'yell' is not defined
```
In this case we deleted yell function but still we are able to use bark function, Why?
* Actually function & variable pointing to a function are two separate identity.
## How to store Functions in Data Structures
```python
def my_fun(string):
    return string.upper()

funcs = [my_fun, str.lower, str.capitalize]
for func in funcs:
    print(func, func("hI pytHon!"))

print(funcs[0]("hello"))
```
* Output
```python
<function my_fun at 0x01CE03D8> HI PYTHON!
<method 'lower' of 'str' objects> hi python!
<method 'capitalize' of 'str' objects> Hi python!
HELLO
```
* In the above example, first add functions in list
* Using loop assign function from funcs list to func variable and call them
* You can also call without assigning function to a variable, can call directly as <data_structure_name>[index]
## Functions can be passed to other functions
```python
def greet(function):
    result = function("Hi, Python Programmer")
    print(result)

def my_fun1(string):
    return string.upper()

def my_fun2(string):
    return string.lower()

greet(my_fun1)
greet(my_fun2)
```
* Output
```python
HI, PYTHON PROGRAMMER
hi, python programmer
```
* You may write different functions as per your need.

## Nested functions
```python
def greet(text):
    def calm(string):
        return string.lower()
    return calm(text)

print(greet("Hello, pyTHon proGRAMMER"))
```
* Output
```
hello, python programmer
```
If you try to call calm function or try to access through greet.calm then it will gave error as calm function is available only inside greet function
* If you want to access a nested function
```python
def greet(volume):
    def calm(string):
        return string.lower()
    def loud(string):
        return string.upper()
    if(volume > 0.7):
        return loud
    else:
        return calm

loud_function = greet(0.75)
print(loud_function, loud_function("hi, Python Programmer"))
```
* Output
```python
<function greet.<locals>.loud at 0x016504F8> HI, PYTHON PROGRAMMER
```
## Trick ⇒
* Suppose an example, you need to call a function with different arguments
```python
def my_fun(string):
    return string.upper()

arguments_list = ["hi", "python", "programmer"]

'''
Most probably you call the above arguments as
print(my_fun(arguments_list[0]))
print(my_fun(arguments_list[1]))
print(my_fun(arguments_list[2]))

Or you may use loop for doing same task
for argument in arguments_list:
    print(my_fun(argument))

There is one simplest way of doing this using map & list
'''
print(list(map(my_fun, arguments_list)))
```
* Output
```python
['HI', 'PYTHON', 'PROGRAMMER']
```
In this example map iterate over the entire arguments_list and apply my_fun function on them
* If you want to print the output in different lines you may use the following:
```python
print("\n".join(list(map(my_fun, arguments_list))))
```