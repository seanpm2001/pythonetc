The module [array](https://t.me/pythonetc/124) is helpful if you want to be memory efficient or interoperate with C. However, working with array can be actually slower than with list:

```python
In [1]: import random
In [2]: import array
In [3]: lst = [random.randint(0, 1000) for _ in range(100000)]
In [4]: arr = array.array('i', lst)

In [5]: %timeit for i in lst: pass
1.05 ms ± 1.61 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)

In [6]: %timeit for i in arr: pass
2.63 ms ± 60.2 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)

In [7]: %timeit for i in range(len(lst)): lst[i]
5.42 ms ± 7.56 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)

In [8]: %timeit for i in range(len(arr)): arr[i]
7.8 ms ± 449 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
```

The reason is that because `int` in Python is a [boxed object](https://en.wikipedia.org/wiki/Object_type#Boxing), and wrapping raw integer value into Python `int` takes some time.