# template
Minimal template for a decent repo

# Basic commands

## Initial setup

- ```git clone https://github.com/lorenzomarini96/template.git```
- ```cd template```
- ```mkdir template tests docs .circle```
- ```touch requirements.txt template/module_template.py template/__init__.py tests/__init__.py tests/test_module_template.py test/Makefile .circle/config.yml setup.py```

## Module template

- ```python
“””Docstrings of the module1“””

def func1(arg1, arg2):
    “””
    The func1 function implements the scalar sum between
    two addends given in input.
    Parameters
    ----------
    arg1 : int, float
           Description
    arg1 : int, float
           Description
    Returns
    -------
    sum : int, float
          Return the sum of arg1 with arg2.
    “””

    return arg1 + arg2


if __name__ == "__main__":
    func1(None, None)

```

## Unittest









