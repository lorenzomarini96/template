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
"""Docstrings of the module1"""

def func1(arg1, arg2):
    """
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
    """

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
"""Unittest"""
import sys
import os
from pathlib import Path

import unittest

# Get the absolute path to the parent dir.
sys.path.insert(0, str(Path(os.getcwd()).parent))

# Import my function in my module.
from template.module_template import func1

class TestFunc1(unittest.TestCase):
    """Unittest for the module_template"""

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


#### Example of *config.yml*

```python
# Use the latest 2.1 version of CircleCI pipeline process engine.
# See: https://circleci.com/docs/2.0/configuration-reference
version: 2.1

# Orbs are reusable packages of CircleCI configuration that you may share across projects, enabling you to create encapsulated, parameterized commands, jobs, and executors that can be used across multiple projects.
# See: https://circleci.com/docs/2.0/orb-intro/
orbs:
  # The python orb contains a set of prepackaged CircleCI configuration you can use repeatedly in your configuration files
  # Orb commands and jobs help you with common scripting around a language/tool
  # so you dont have to copy and paste it everywhere.
  # See the orb documentation here: https://circleci.com/developer/orbs/orb/circleci/python
  python: circleci/python@1.5.0

# Define a job to be invoked later in a workflow.
# See: https://circleci.com/docs/2.0/configuration-reference/#jobs
jobs:
  build-and-test: # This is the name of the job, feel free to change it to better match what you're trying to do!
    # These next lines defines a Docker executors: https://circleci.com/docs/2.0/executor-types/
    # You can specify an image from Dockerhub or use one of the convenience images from CircleCI's Developer Hub
    # A list of available CircleCI Docker convenience images are available here: https://circleci.com/developer/images/image/cimg/python
    # The executor is the environment in which the steps below will be executed - below will use a python 3.10.2 container
    # Change the version below to your required version of python
    docker:
      - image: cimg/python:3.7
    # Checkout the code as the first step. This is a dedicated CircleCI step.
    # The python orb's install-packages step will install the dependencies from a Pipfile via Pipenv by default.
    # Here we're making sure we use just use the system-wide pip. By default it uses the project root's requirements.txt.
    # Then run your tests!
    # CircleCI will report the results back to your VCS provider.
    steps:
      - checkout
      - python/install-packages:
          pkg-manager: pip
          # app-dir: ~/project/package-directory/  # If you're requirements.txt isn't in the root directory.
          # pip-dependency-file: test-requirements.txt  # if you have a different name for your requirements file, maybe one that combines your runtime and test requirements.
      - run:
          name: Run tests
          # This assumes pytest is installed via the install-package step above
          command: python -m unittest tests.test_module1

# Invoke jobs via workflows
# See: https://circleci.com/docs/2.0/configuration-reference/#workflows
workflows:
  sample: # This is the name of the workflow, feel free to change it to better match your workflow.
    # Inside the workflow, you define the jobs you want to run.
    jobs:
      - build-and-test
```

**Attention!** 

command: python -m unittest tests.test_module_template


## Requirements

Create a .txt file called ```requirements.txt``` to add to the repository root directory. (will contain installation dependencies, but can also be empty for now).

See: https://note.nkmk.me/en/python-package-version/

From the shell: ```pip freeze```

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



# Documentation

<img src="https://user-images.githubusercontent.com/55988954/103821412-62d9d600-506e-11eb-9a0b-6f699743ef71.jpeg" width="250" />

web site: [SPHINX - Python Documentatio Generator](https://www.sphinx-doc.org/en/master/)

- Enter the docs folder: ```$ cd docs```
- Type: ```$ sphinx-quickstart```
- ```Separate source and build directories (y / n) [n]: n```
- Complete the documentation setup.

Sphinx will create a series of files. For now, don't pay too much attention to it.

- Type: ```$ make html```

At this point, sphinx will create various folders.

- The file of our interest, and that we will open, will be: ```index.html```

- Then type: ```$ open _build/html/index.html```.

Very beautiful! But for now there isn't much ... (by clicking, nothing happens yet)

Let's move on to configuring sphinx with our project, and to do that, we work on the ```conf.py``` file

- Open the file created by sphinx ```conf.py```
- Add the following to the file:

```python
# -- Path setup ---------------------------------------------------------------
# If extensions (or modules to document with autodoc) are in another directory,
# add these directories to sys.path here. If the directory is relative to the
# documentation root, use os.path.abspath to make it absolute, like shown here.
import os
import sys
package_name = 'modules'
package_root = os.path.abspath('..')
sys.path.insert(0, package_root)
sys.path.insert(0, os.path.join(package_root, package_name))
```

**CAUTION**: In the package_name insert the name of the folder containing the modules!

Now, insert the Extensions for autodoc:

```python
# -- General configuration ---------------------------------------------------
# Add any Sphinx extension module names here, as strings. They can be # extensions coming with Sphinx (named 'sphinx.ext.*') or your custom # ones.
extensions = [
    'sphinx.ext.napoleon',
    'sphinx.ext.autodoc',
    'sphinx.ext.doctest',
    'sphinx.ext.todo',
    'sphinx.ext.coverage',
    'sphinx.ext.mathjax',
    'sphinx.ext.ifconfig',
    'sphinx.ext.viewcode',
]
```


```python
# Add any paths that contain templates here, relative to this directory.
templates_path = ['_templates']
# The suffix(es) of source filenames.
# You can specify multiple suffix as a list of string:
#
# source_suffix = ['.rst', '.md']
source_suffix = '.rst'

# The master toctree document.
master_doc = 'index'

# The language for content autogenerated by Sphinx. Refer to documentation
# for a list of supported languages.
#
# This is also used if you do content translation via gettext catalogs.
# Usually you set "language" from the command line for these cases.
language = None

# List of patterns, relative to source directory, that match files and # directories to ignore when looking for source files.
# This pattern also affects html_static_path and html_extra_path .
exclude_patterns = [u'_build', 'Thumbs.db', '.DS_Store']

# The name of the Pygments (syntax highlighting) style to use.
pygments_style = 'sphinx'

# -- Options for LaTeX output ------------------------------------------------
latex_elements = {
# The paper size ('letterpaper' or 'a4paper'). #
# 'papersize': 'letterpaper',
# The font size ('10pt', '11pt' or '12pt').
#
    # 'pointsize': '10pt',
# Additional stuff for the LaTeX preamble.
#
    # 'preamble': '',
    # Latex figure (float) alignment
#
# 'figure_align': 'htbp', }
# Grouping the document tree into LaTeX files. List of tuples # (source start file, target name, title,
# author, documentclass [howto, manual, or own class]).
latex_documents = [
(master_doc, 'operazione.tex', u'operazione Documentation', u'Lorenzo Marini', 'manual'),
]
```

- Now, create an ```api.rst``` file.
- Save it in the ```docs``` folder.

```
API documentation
=================

module1
-------

.. automodule:: module1
   :members:
   
```
- Open ```index.rst``` and add
```
packagemodel's documentation
============================

packagemodel is a Python-based package that allows you to compute the sum of two integer/floats.

.. toctree::
    :maxdepth: 2
    :caption: Contents:
    
    api
```
**CAUTION**: leave a blank line between one and the other!

- Then, type: ```$ make html```
- $ ```open _build/html/index.html```

It should work!

See also some inspirational sites for very cool documentation:
- [Sphinx and RST syntax guide (0.9.3)](https://thomas-cokelaer.info/tutorials/sphinx/index.html#)
- [Restructured Text (reST) and Sphinx CheatSheet](https://thomas-cokelaer.info/tutorials/sphinx/rest_syntax.html#restructured-text-rest-and-sphinx-cheatsheet)
- [Example on how to document your Python docstrings](https://thomas-cokelaer.info/tutorials/sphinx/docstring_python.html)
- [How to include test in your Python docstrings using doctest](https://thomas-cokelaer.info/tutorials/sphinx/doctest.html)
- [Sphinx Themes](https://sphinx-themes.org)



# Read the Docs

1. Go to [Read the Docs](https://readthedocs.org) to add the link (badge) to the documentation to our repository
2. We import our project.
3. click on +

**CAUTION**: before compiling the version, go to ```Administration``` and then to ```Advance Settings``` and select ```main```
as the default branch.

4. Now we can compile the version
5. Once the compilation is complete, click on ```Show documents``` to check the result of the compilation.
6. Then click on ```Overview```.

The badge is ready and once you click on the circled we can copy the link (in Markdown version) and paste it on the ```README.md``` file


# Insert Badges to the Repo - Shields IO

That's not all ...

- Go to the site: (https://shields.io)
- Here we will find many badges that you can insert in our ```README.md``` file in order to enrich the information on our repository.
- Click on the desired badge and complete the link generation operation.
- By clicking on ```Copy Markdown``` it is sufficient to copy the link copied to the ```README.md``` file

