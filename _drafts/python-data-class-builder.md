---
title: Python Data Class Builder
---

## Overview

Thông thường để tạo một class trong python. Chúng ta có thể code như sau:

1. Sử dụng boilerpate sau, tuy nhiên nó khá là old fashion. Các sepecial method `__repr__` hoặc `__eq__` đều không cung cấp nhiều value.

    ```python
    class Coordinate:
        def __init__(self, lat, lon):
            self.lat = lat
            self.lon = lon

    coordinate = Coordinate(44, 33)
    ```

2. Sử dụng `namedtuple` - 1 factory function - sẽ build ra 1 class là subclass của `tuple`. Tùy ý định nghĩa class name & field.

    ```python
    from collections import namedtuple
    Coordinate = namedtuple('Coordinate', 'lat lon')

    coordinate = Coordinate(44, 33)
    ```

    Cách mới hơn, đó là sử dụng `typing.NamedTuple`, về bản chất vẫn giống với `collections.namedtuple`. 
        
    ```python
    import typing
    Coordinate = typing.NamedTuple('Coordinate', [('lat', float), ('lon', float)])

    coordinate = Coordinate(44, 33)
    ```

3. Sử dụng `dataclass`. Cách này dễ đoc, dễ viết và modern hơn các cách trước đó.

    ```python
    from dataclasses import dataclass

    @dataclass
    class Coordinate:
        lat: float
        lon: float

        def __str__(self):
            ns = 'N' if self.lat >= 0 else 'S'
            we = 'E' if self.lon >= 0 else 'W'
            return f'{abs(self.lat):.1f}°{ns}, {abs(self.lon):.1f}°{we}'
    ```

## About `@dataclass`

