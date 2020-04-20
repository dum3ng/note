# flask practice

## project structure

```python
from flask import Flask
app = Flask(__name__)

if __name__ == '__main__':
  app()
```

### enviroment variables

Define run parameters in `.flaskenv` file:

A common config file would contains some basic parameters:

```toml
FLASK_APP=my_app
FLASK_ENV=development
FLASK_RUN_PORT=5040
FLASK_RUN_HOST=0.0.0.0
```

To run the flask app, simply run `flask run`.

### setup meta data

Create a `__version__.py` in package root folder, and define

```python
# __version__.py
__version__ = '0.1.0'
__author__ = 'awesome'
```

and in `setup.py`, load the file content:

```python
# setup.py

```

## test

Use `pytest` framework for test.

Create a `tests` folder at project root,

To import our working package for use in test files, we need to install the current package locally in edit mode.

```py
# setup.py
from setup import find_packages

setup(
  # ...
  package=find_packages(), # our package
)

```

then run `pip install -e .`
