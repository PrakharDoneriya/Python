# Python Trick :: *args & **kwargs Parameters

## What are *args & **kwargs Parameters?
* Allows function to accept numbers of arguments without specifying the arguments
* You can create flexible functions using these parameters
* args & kwargs are the used for the naming convention
    * ***args**  &nbsp; &nbsp; &nbsp; &nbsp; -> &nbsp; * represents **Tuple**
    * ***\*kwargs** &nbsp; -> &nbsp;  ** represents Dictionary

```python
def test_argument(mandatory_argument, *args, **kwargs):
    print(mandatory_argument, args, kwargs)

if __name__ == "__main__":
    test_argument("Hello", 1, 2, 3, key1="1", key2="2", key3="3")
    test_argument("Hello", 1, 2, 3)
    test_argument("Hello", key1="1", key2="2", key3="3")
    test_argument("Hello")
    test_argument()
```
* Output
```python
Hello (1, 2, 3) {'key1': '1', 'key2': '2', 'key3': '3'}
Hello (1, 2, 3) {}
Hello () {'key1': '1', 'key2': '2', 'key3': '3'}
Hello () {}
Traceback (most recent call last):
  File <file_name>, line 9, in <module>
    test_argument()
TypeError: test_argument() missing 1 required positional argument: 'mandatory_argument'
```
### You can also add more arguments to args & kwargs and can pass to another functions also
```python
def test_argument(mandatory_argument, *args, **kwargs):
    args += ("extra1",)
    kwargs["key4"] = "4"
    print(mandatory_argument, args, kwargs)

    # args & kwargs can be passes do another function like
    # function_name(*args, **kwargs)

if __name__ == "__main__":
    test_argument("Hello", 1, 2, 3, key1="1", key2="2", key3="3")
    test_argument("Hello", 1, 2, 3)
    test_argument("Hello", key1="1", key2="2", key3="3")
    test_argument("Hello")
    test_argument()
```
* Output
```python
Hello (1, 2, 3, 'extra1') {'key1': '1', 'key2': '2', 'key3': '3', 'key4': '4'}
Hello (1, 2, 3, 'extra1') {'key4': '4'}
Hello ('extra1',) {'key1': '1', 'key2': '2', 'key3': '3', 'key4': '4'}
Hello ('extra1',) {'key4': '4'}
Traceback (most recent call last):
  File <file_name>, line 11, in <module>
    test_argument()
TypeError: test_argument() missing 1 required positional argument: 'mandatory_argument'
```