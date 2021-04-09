# Python Trick :: Assertion (assert Keyword)

## Assertion
* Assert statement is helpful for debugging the code, it allows to test condition
* If the condition is true then program works fine else it will fail and raise AssertionError

## Syntax
```python
assert expression1 ["," expression2]
```
* expression1 -> condition for test
* expression2 -> error message (optional)
## How it works
```python
if (not expression1):
    raise AssertionError(expression2)
```
## Code
### Suppose a function for applying discount :
```python
def apply_discount(product_price, discount):
    price = int(product_price * (100 - discount) / 100)
    assert 0 <= price <= product_price, "Invalid Discount"
    return price
```
### Example 1 : Calling function with valid discount
```python
if __name__ == "__main__" :
    # Valid discount of 25%
    selling_price = apply_discount(2000, 25)
    print(selling_price)
```
* Output
```python
1500
```
#### In this case assert condition is true, code runs fine

### Example 2 : Calling function with Invalid discount
```python
if __name__ == "__main__" :
    # Valid discount of 150%
    selling_price = apply_discount(2000, 150)
    print(selling_price)
```
* Output
```python
Traceback (most recent call last):
  File <file_name>, line 14, in <module>
    selling_price = apply_discount(2000, 150)
  File <file_name>, line 5, in apply_discount
    assert 0 <= price <= product_price, "Invalid Discount"
AssertionError: Invalid Discount
```
In this case assert condition is false as price = -1000, code fails with AssertionError and prints Message

## Assertion that Never Fails
Never pass tuple to condition
```python
assert (10 > 20, "Fail")
```
The above condition will always pass 😵