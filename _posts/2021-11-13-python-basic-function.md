---
title: Function trong python
date: 2021-11-13 22:00:00 +0700
---

## Function là objects

```python
>>> def factorial(n):
...     """return n!"""
...     return 1 if n < 2 else n * factorial(n - 1)
...
>>> factorial.__doc__ # __doc__ là 1 attribute của object factorial
'return n!'
>>> type(factorial) # factorial là 1 object của function class
<class 'function'> 
```

## Higher-Order function
> Là function nhận argument là 1 function khác hoặc return 1 function thay cho các biến bình thường.

```python
def say_hello():
    return 'Hello'

def greeting(func): # high-order
    print(func() + ' Mr.Dungo')

>>> greeting(say_hello) # pass function as argument
'Hello Mr.Dungo'
```

## Anonymous function
> Tức là những function khi khởi tạo sẽ không có name.

```python
reverse = lambda x: x[::-1] # anonymous function with lambda keyword is assigned to a variable

>>> a = [1, 2, 3, 4, 5]
>>> reverse(a)
[5, 4, 3, 2, 1]
```

## Callable objects
> Là những object sử dụng () operator để thực thi. 

```text
Có 9 loại callable object:
1. User-defined functions
    Tạo với def hoặc lambda keyword
2. Builtin function
    Ví dụ: len hoặc type
3. Builtin method
    Ví dụ: dict.get hoặc list.append
4. Methods
    Ví dụ: function được khai báo trong class
5. Classes
    Ví dụ: khi khởi tạo 1 object
6. Class instances
    Nếu __call__ được implement trong 1 class thì có thể dùng instance như function.
7. Native coroutine function
    Ví dụ: async def
8. Generator functions
    Ví dụ: function or method sử dụng yield
9. Asynchronous generator function
    Ví dụ: async for
```

```python
"""Implement số 6"""
import random

class Dice:
    def __init__(self):
        self.dice = list(range(1,7))
    
    def roll(self):
        random.shuffle(self.dice)
        return self.dice[0]   

    def __call__(self):
        return self.roll()    

>>> dice = Dice()
>>> dice.roll()
... 5
>>> dice()
... 2 
```