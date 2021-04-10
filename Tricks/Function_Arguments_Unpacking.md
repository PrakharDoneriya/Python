# Python Trick :: Function Arguments Unpacking

### Lets start with a simple function 
```python
def vector(x, y, z):
    print('<{}, {}, {}>'.format(x, y, z))

vector(1, 1, 0)
```
* Output
```python
<1, 1, 0>
```
### Lets suppose we are storing vector in List or Tuple & calling the vector function
```python
vector_list = [0, 1, 1]
vector_tuple = (1, 0, 1)

vector(vector_list[0], vector_list[1], vector_list[2])
vector(vector_tuple[0], vector_tuple[1], vector_tuple[2])
```
* Output
```python
<0, 1, 1>
<1, 0, 1>
```
### There is a better way for unpacking using *
```python
vector(*vector_list)
vector(*vector_tuple)
```
* Output
```python
<0, 1, 1>
<1, 0, 1>
```
### Dictionary can also be unpacked using **
```python
vector_dictionary = {'z' : 0, 'y' : 1, 'x' : 0}
vector(**vector_dictionary)
```
* Output
```python
<0, 1, 0>
```