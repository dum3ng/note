#

## setup file template

```python
# setup.py
from setuptools import find_packages, setup
import os
about = {}

with open(os.path.abspath(os.path.join(__file__,'../my_package/__version__.py')), encoding='utf-8') as f:
    exec(f.read(), about)

setup(
    version=about['__version__'],
    packages=find_packages()
)
```

Create a `__version__.py` and put package meta info, i.e. description, version, etc, in this file, and
exec the source to load info in a `dict`.

## workflow

### pypi

config file of `pip` is `~/config/pip/pip.conf`

## test

Use `pytest` framework.

All test function starts with `test_`, and will be collected by `pytest`.

### pytest config

The config file is `pytest.ini`:

```ini
[pytest]
...=...
```

### print content in test function

By default `pytest` capture all output to stdin/stdout, to ensure a clean test result report.

To enable the print to stdout temporarily, use the `capsys.disabled()`:

```python
def test_my_function(capsys):
    with capsys.disabled():
        print("yeah, you can see me now.")
```
