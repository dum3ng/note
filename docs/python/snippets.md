# python snippets

## create a generator using list comprehension

when wrap list comprehension in square bracket, will generate a list;
while wrap list comprehension in bracket, will generate a generator(lazy list).

```python
generator = (x for x in range(10))
_list = [x for x in range(10)]
```

## check generator instance

```python
generator = (x for x in range(10))
isinstance(generator, collections.Generator) # True
ininstance(generator, types.GeneratorType)
```

**traps**:

- In python3.6, the `isinstance(generator, typing.Generator)` is `True`, while in
  python3.7 and later version, the result is `False`
