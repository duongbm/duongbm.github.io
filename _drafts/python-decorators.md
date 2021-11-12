---
title: Decorator trong python
---

## Cơ bản
1. Function trong python được hiểu là `first-class objects`. Có thể hiểu nôm na function trong python là 1 instance của object function. Object này được: 
    ```
    - tạo tại thời điểm runtime
    - có thể gán cho 1 variable
    - dùng như 1 argument cho function khác
    - dùng để return trong 1 function.
    ```

    Example:
    ```python
    >>> def factional(n):
    ...     return 1 if n < 2 else n * factional(n - 1)
    ...
    >>> type(factional)
    <class 'function'>
    ```

2. High Order Function: là function nhận argument là 1 function khác hoặc return 1 function như một variable bình thường.

3. callable object là 1 một object dùng `()` để call và thưc execute. ví dụ: function, classes, ...

## Decorators 101
Decorator trong python là 1 callable, mà argument truyền vào là 1 function khác (decorated function). Ví dụ.

```python
def deco(func):
    def inner():
        print('running ineer')
    return inner # return inner function object

@deco
def target():
    print('running target')

target() # invoking decorated target func

```

## Closures
Là 1 function, gọi là f, được binding giữ lại variable khai báo trong f, nên có thể sử dụng các variable này cho các lần gọi tiếp theo. Ví dụ:

```python
def make_avenger():
    count = 0
    total = 0

    def avenger(new_value):
        nonlocal count, total 
        count += 1
        total += new_value
        return total / count

    return avenger


avg = make_avenger()
avg(10) # return 10
avg(20) # return 15
```