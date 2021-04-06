# Python Trick :: Lambda Functions 

### **Read Time : 7 mins 🕒**

## Lambda Function
* These function behaves like regular functions but are single expression.
* Provides deceleration of anonymous functions.
* Allow to write inline functions.
* It automatically return the value after evaluating.

Add function using Lambda Function
```python
add = lambda x, y : x + y

print(add(5, 3))
```
* Output
```
8
```

You can also write function as
```python
def add(x, y):
    return x + y

print(add(5, 3))
```
* Output
```
8
```
It seems like writing functions without def keyword ? Right

* You can call the function while writing it, instead of giving name to the function
```python
>>> (lambda x, y: x + y)(5, 3)
8
```

## When to use Lambda Function?
* Whenever you need to pass function object you can use a lambda function
### Example ->
* Example 1 -> Sorting 2d list according to the 2nd element of sub-list
```python
list1 = [
    [1, 6],
    [2, 3],
    [5, 4]
]
print(sorted(list1, key = lambda l: l[1]))
```
*  Output
```
[[2, 3], [5, 4], [1, 6]]
```
* Example 2 -> Sorting list by the square of elements
```python
list1 = [-4, -3, -2, -1, 0, 1, 2, 3, 4]
print(sorted(list1, key = lambda x : x*x))
```
*  Output
```
[0, -1, 1, -2, 2, -3, 3, -4, 4]
```
* Example 3 -> Find squares of of elements of a list
```python
list1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(list(map(lambda ele: ele * ele, list1)))
```
* Output
```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```