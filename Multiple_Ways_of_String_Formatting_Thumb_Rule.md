# Multiple Ways of String Formatting & Thumb Rule

## String formatting ways :
* Old Style String Formatting (printf style)
* New Style String Formatting (using format)
* Literal String Interpolation (Python 3.6+)
* Template Strings

We will take the following variable for the reference
```python
name = "Python"
num  = 31
```
Try ro format output as
```python
'Hello Python user, Hexadecimal value of 31 is 0x1F'
```

## 1. Old Style String Formatting (printf style)
* It's easier to used format specifier as we usually start programming with C Language, for this example we use following format specifier
    * %s -> String
    * %x -> Hexadecimal value with lower alphabet
    * %X -> Hexadecimal value with upper alphabet
```python
>>> 'Hello %s user' % name
'Hello Python user'
>>> 'Hello %s user, Hexadecimal value of %d is 0x%X' % (name, num, num)
'Hello Python user, Hexadecimal value of 31 is 0x1F'
```
* You can also refer to variable substitution by name in formatting string
```python
>>> 'Hello %(name)s user, Hexadecimal value of %(num)d is 0x%(number)X' % {"name" : name, "num" : num, "number" : num}
'Hello Python user, Hexadecimal value of 31 is 0x1F'
>>> 'Hello %(name)s user, Hexadecimal value of %(num)d is 0x%(num)X' % {"name" : name, "num" : num}
'Hello Python user, Hexadecimal value of 31 is 0x1F'
```

## 2. New Style String Formatting (using format)
* It's similar with Old Style, the only difference is instead of format specifier we use {}
```python
>>> 'Hello {} user'.format(name)
'Hello Python user'
>>> 'Hello {name} user, Hexadecimal value of {num} is 0x{number:X}'.format(name=name, num=num, number=num)
'Hello Python user, Hexadecimal value of 31 is 0x1F'
>>> 'Hello {name} user, Hexadecimal value of {num} is 0x{num:X}'.format(name=name, num=num)
'Hello Python user, Hexadecimal value of 31 is 0x1F'
```

## 3. Literal String Interpolation (Python 3.6+)
* Python 3.6 adds new way of formatting called Formatted String Literals.
* This way allow to use embedded Python expression inside string constants.
* The new formatting syntax is powerful as you can use the expressions inside {}.
```python
>>> f'Hello {name} user'
'Hello Python user'
>>> f'Hello {name} user, Hexadecimal value of {num} is 0x{num:X}'
'Hello Python user, Hexadecimal value of 31 is 0x1F'
>>> a = 5
>>> b = 10
>>> f'Five plus ten is {a + b} and not {2 * (a + b)}.'
'Five plus ten is 15 and not 30.'
>>>
>>> def greet(name, question):
        return f"Hello {name}!, How is it {question}?"

>>> greet("Python", "working")
"Hello Python!, How's it going?"
```
* How f-string works internally, trying to explain with ***greet*** function
```python
def greet(name, question):
    return ("Hello " + name + "!, How's it " +
question + "?")
```

## 4. Template Strings
* By this technique string formatting is done using Python Template Strings
```python
>>> from string import Template
>>> t = Template('Hello $name!')
>>> t.substitute(name=name)
'Hello Python'
>>> t2 = Template('Hello $name user, Hexadecimal value of $num is $number')
>>> t2.substitute(name=name, num=num, number=hex(num))
'Hello Python user, Hexadecimal value of 31 is 0x1f'
```

## **Dan’s Python String Formatting Rule of Thumb**
* If your format strings are user-supplied, use Template Strings to avoid security issues
* Otherwise, use Literal String Interpolation if you’re on Python 3.6+, and “New Style” String Formatting.