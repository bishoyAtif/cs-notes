## Python 2 vs 3 ##
- ```print``` became a function instead of statement
```python
    >> print "Hello world"  #Python 2 .. Statement
    >> print("Hello world") #Python 3 .. function
```
- the division of whole numbers gives a fraction instead of whole numbers
```python
    >> 5 / 2   # 2   in python 2
    >> 5 / 2   # 2.5 in python 3
    >> 5.0 / 2 # 2.5 in python 2
```

## Printing Output ##
- use ```print``` statement to output text.
```python
    print 1 + 1 # 2
    print 2 * 20 # 40
    print (2 * 10) + (5 * 20) # 120
```

## Arithmetic expressions ##
- Its basic rule is ```Expression``` = ```Expression``` ```Operator``` ```Expression```.
- The ```operator``` can be ```+```, ```-```, ```/```, ```*``` more operators [here](http://python-reference.readthedocs.io/en/latest/docs/operators/#arithmetic-operators).
- The expression can be literal like ```"Hello"```, variable, number or another expression.
```python
    (3)
    3 + 5
    3 * (5 + 6)
```
- When using Python 2, Division of integers with ```/``` gives only integers. To make it results float numbers, make sure that one from the dominator and numerator is a float number.
```python
    # Python 2
    >> 5 / 2   # 2
    >> 5.0 / 2 # 2.5
    >> 5 / 2.0 # 2.5
```
- In Python 3, All divisions with ```/``` result floats.