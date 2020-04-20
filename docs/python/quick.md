# quick

## list

```python
l1 = [3,4,5]

# get

# change
l1.append(6)
l1.pop()

```

## dict

```python
d1 = dict(planet='earth')
d2 = {'planet': 'earth' }

d1.get('planet', None)

for k in d1.keys():

for v in d1.values():

for k,v in d1.items():
    print(k,v)  # planet earth

for ind, k in enumerate(d1):
    print(ind, k) # 0 planet
```

## string

## class

### special methods

```python

class Example:

    def __new__(self):
        pass
    def __init__(self, *args, **kwargs):
        """
        用来对对象进行初始化
        """
        pass

    def __str__(self):
        """
        str(example) 函数调用
        """
        pass

    def __iter__():
        """
        """

    def __dict__():

    def __len__():
        """
        len(example) 函数调用
        """
```
