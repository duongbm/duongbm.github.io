---
title: Python Decorators and Closures
date: 2021-11-14 22:00:00 +0700
---

## Decorator 101
> Decorator là 1 callable object có argument là 1 function.(function này gọi là decorated function)

```python
def deco(func):
    def inner():
        print('run inner()')
        func()
    return inner

@deco # -> decorator func
def target(): # -> decorated func
    print('run target()')

>>> target()
... 'run inner()'
... 'run target()'
```

> Decorator được execute ngay sau khi decorated được define. (hay còn gọi là import time)

## Closures
> Là function có thể giữ lại được các binding variables được define trong chính nó cho các lần call tiếp theo.

```python
def calculate_avg():
    series = []

    def avenger(new_value):
        series.append(new_value)
        total = sum(series)
        return total / len(series)
    
    return avenger

>>> avg = calculate_avg()
>>> avg(10) 
... 10
>>> avg(20)
... 20
```

Bình thường sau khi call các function thì các local variable trong function đó sẽ được khởi tạo lại từ đầu cho các lần gọi tiếp. Tuy nhiên với `closure`, thì ngược lại, các biến local variale vẫn được lưu trữ và sử dụng lại với các lần gọi tiếp theo.

## SingleDispatch decorator

```python
from functools import singledispatch

def greeting(obj: object) -> str:
    return 'greeting'

@greeting.register
def _(message: str) -> str:
    return 'hello ' + message

@greeting.register
def _(messages: list) -> str:
    return 'hello ' + ','.join(messages)


>>> greeting('Mr.Dungo')
... hello Mr.Dungo

>>> greeting(['Dungo', 'Gango'])
... hello Dungo, Gango
```

