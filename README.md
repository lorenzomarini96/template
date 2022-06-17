# template
Minimal template for a decent repo

# Basic commands

## Initial setup

- ```git clone https://github.com/lorenzomarini96/template.git```
- ```cd template```
- ```mkdir template tests docs .circle```
- ```touch requirements.txt template/module_template.py template/__init__.py tests/__init__.py tests/test_module_template.py test/Makefile .circle/config.yml setup.py```

## Module template

```python
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

**Suggestion**: run *pylint* before to commit!

links:
- https://pylint.pycqa.org/en/latest/
- https://peps.python.org/pep-0008/
- https://docs.python-guide.org/writing/style/

## Unittest

```python
import sys
import os
from pathlib import Path

import unittest

# Get the absolute path to the parent dir.
sys.path.insert(0, str(Path(os.getcwd()).parent))

# Import my function in my module.
from template.module_template import func1

class TestFunc1(unittest.TestCase):
“””Unittest for the module_template”””

    def test_int(self):
        """Test with integers"""
        self.assertAlmostEqual(func1(2, 2), 4) 
    
    def test_float(self):
        """Test with floats"""
        self.assertAlmostEqual(func1(2.5, 2.5), 5.0) 


if __name__ == "__main__":
    unittest.main()

```

**Info on assertEqual**

Info about ```assertEqual```(https://docs.python.org/3/library/unittest.html)


**CAUTION: Import modules into Python**

[Where does Python look for modules?](https://bic-berkeley.github.io/psych-214-fall-2016/sys_path.html)

Useful links: 
- https://bic-berkeley.github.io/psych-214-fall-2016/sys_path.html
- https://docs.python.org/3.5/library/sys.html#sys.path
- https://pymotw.com/3/sys/imports.html#import-path
- https://stackoverflow.com/questions/5137497/find-current-directory-and-files-directory
- https://stackoverflow.com/questions/2860153/how-do-i-get-the-parent-directory-in-python
- https://docs.python.org/3/library/pathlib.html


### Circle CI

link: https://app.circleci.com/pipelines/github/lorenzomarini96


```code /home/lorenzomarini/Desktop/template/.circle/config.yml```


## Requirements

See: https://note.nkmk.me/en/python-package-version/

From the shell: pip ```freeze```

The output will be something like follows:

```python
alabaster==0.7.12
apturl==0.5.2
argon2-cffi==20.1.0
astroid==2.11.6
atomicwrites==1.1.5
attrs==19.3.0
Babel==2.10.3
backcall==0.2.0
wrapt==1.14.1
xkit==0.0.0
xlrd==1.1.0
xlwt==1.3.0
zipp==1.0.0
```





