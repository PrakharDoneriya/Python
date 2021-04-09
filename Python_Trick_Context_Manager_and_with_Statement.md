# Python Trick :: Context Manager & with Statement 

## Context Manger
* It's a simple interface that your object needs to follow in order to support the with statement.
* You only need to add \_\_enter__ and \_\_exit__ methods to an object, if you want it to function as context manager.
    * **\_\_enter__** &nbsp;-> &nbsp; python calls **\_\_enter__** when execution enters in context with statement
    * **\_\_exit__** &nbsp; &nbsp; -> &nbsp; python calls **\_\_exit__** to free the allocated resources
* Using with effectively can help you avoid leaks and increase your codes readability
* decorator -> @contextmanager

## File handling
* most of us open file as
```python
f = open('file.txt', 'w')
f.write('hello, world!')
f.close()
```
Above implementation won't guarantee file is closed or not, Suppose there is some exception raised while calling f.write() then the code may leak file descriptor ☹️.

* Quick Fix
```python
with open('file.txt', 'w') as f:
    f.write('hello, world!')
```
Opening file using with statement is recommended because it make sure that open file descriptor are closed automatically 😃.
* How it works internally?
```python
f = open('file.txt', 'w')
    try:
        f.write('hello, world')
    finally:
        f.close()
```

## Support with in your Own Objects
Let's implement our own object which supports *with statement*
```python
class ManagedFile:
    def __init__(self, name):
        self.name = name

    def __enter__(self):
        self.file = open(self.name, 'w')
        return self.file

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()

if __name__ == "__main__" :
    with ManagedFile('hello.txt') as f:
        f.write('hello, world!')
        f.write('BYE :)')            
```
 &nbsp; &nbsp; Have you noticed its looks like implementing *open()* context manager😊?

*  Writing a class-based context manager isn’t the only way to support the with statement in Python
* You can also use contextlib's contextmanager decorator for defining generator-based factory function that will automatically support *with statement*.
```python
from contextlib import contextmanager

@contextmanager
def ManagedFile(name):
    try:
        f = open(name, 'w')
        yield f
    finally:
        f.close()

if __name__ == "__main__" :
    with ManagedFile('hello.txt') as f:
        f.write('hello, world!')
        f.write('BYE :)')
```
In this case ManageFile() is generator that first acquires the resource and temporarily suspends its execution and yield resource, that can used by the caller. Once caller leaves the *with* context, generator continues execution to clean-up steps if any needed and finally resource get released to the system.

### Let's have some fun with context manager
* Implementing our own indenter that will take care of indentation while printing something in output 🤪
```python
class Indenter:
    def __init__(self):
        self.level = 0

    def __enter__(self):
        self.level += 1
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        self.level -= 1
    
    def print(self, text):
        print('\t' * self.level + text)

if __name__ == "__main__" :
    with Indenter() as indent:
        indent.print('Hi')
        with indent:
            indent.print('Have')
            with indent:
                indent.print('Some')
        indent.print('Fun')
```
* Output
```
    Hi
        Have
            Some
    Fun
```
