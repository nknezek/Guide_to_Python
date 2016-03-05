# Guide to Scientific Python on Mac
by Nicholas Knezek, March 2016

## Installing Python
### Homebrew
Python on mac is easiest to install using [Homebrew](http://brew.sh), a command-line package manager for OS X. Install homebrew by typing

```bash 
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```bash
brew update && brew upgrade
```

This will install and set up Homebrew on your local machine. Homebrew organizes itself in analogy with brewing beer. It sets itself up in its own directory ( `/usr/local/Cellar` ) that doesn't touch anything you've already installed elsewhere on your machine. Run 

```bash
brew doctor
```

To see if everything is working or if it tells you you need to install anything else. Especially XQuartz or XCode. It'll make a stink about "unbrewed files" in various folders, but feel free to ignore the warnings: Homebrew likes to run everyting it can, and doesn't like other things install into `/usr/local/bin` or other folders it uses.

To see what you've installed with brew:

```bash
brew list```

It shouldn't list anything right now. 

### Install Python using Homebrew
To install python 3, run

```bash
brew install python3``` 

This will install the latest version of python 3 and all its dependencies in `/usr/local/Cellar` and symbolically link them into `/usr/local/bin` which should be listed first on your PATH. Note that `python` usually refers to Python 2 and `python3` refers to Python 3. If your PATH doesn't already list `/usr/local/bin` first, add

```bash
export PATH=/usr/local/bin:$PATH
```

to your ~/.bash_profile.

Homebrew uses it's own Cellar to keep itself apart from the system version of programs. If you ever run into a problem or want to install different versions of a program, you can `brew unlink python3` to remove the symbolic links for any package. This leaves them installed in the Cellar, but not on the path, allowing you to troubleshoot. This also allows you to use multiple versions of packages and switch between them with e.g. `brew switch python3 3.3`

### Install Python Packages Using 'pip'

Python uses its own package manger called `pip`. For python 3, the command is pip3. It's similar to brew, but for python packages instead of system programs. First,

```bash
pip3 install --upgrade pip
```

To make sure you're getting the latest version of everything.

A few python packages that everyone uses are listed below.

```bash
pip3 install numpy # general numerical routines, matrices, etc.
pip3 install scipy # specialized functions, polynomials, statistics, etc. 
pip3 install matplotlib # plotting like matlab
pip3 install ipython # interactive python prompt that adds a lot of great things
pip3 install jupyter # used for notebooks (like this one)
```

Optional python packages:
```bash
pandas # data analysis: data frames, etc. Like R in some ways
sympy # Symbolic math, analytical integrals. Like Mathematica
```

### Tips for Python
1. A good guide for coming to python from other languages can be found here: [https://wiki.python.org/moin/MovingToPythonFromOtherLanguages](https://wiki.python.org/moin/MovingToPythonFromOtherLanguages).
1. most people use numpy as np and scipy as sp:
```python 
import numpy as np
import scipy as sp
```
then sin, cos, exp are accessed by `np.sin(), np.cos(), np.exp()`. You can also import commonly-used functions directly:
```python 
from numpy import sin, cos```
1. Do everyting math using numpy. It just makes it a lot easier and clearer. 
1. Unlike some other languages, Python cares about whitespaces and tabs vs spaces. You have to make sure indentations line up or things won't work properly. This is the equivalent of forgetting a closin bracket in other languages.
1. "Comprehension" is super powerful. They let you do something for each item of a dictionary or list on one line. For example, if you want to get a list of the squares of numbers, you can type:
```python 
squared_list = [x**2 for x in number_list]
```
You can do this with dictionaries (AKA hashes, hash tables, lookup tables, key-value tables) too. zip is just a built-in function that pairs up elements: `zip(a,b) -> (a1, b1), (a2, b2), ...` etc. 
```python
dict_out = {key:value for each key,value in zip(list_of_keys, list_of_values)}
```


### Install Spyder (python version of Matlab)

For some reason, the lastest upgrade to the internal window management in Mac OS X broke the current version of Spyder, so now we have to use the next beta version of Spyder that isn't yet released. First install pyqt5, an open-source window manager. 
```bash
brew install pyqt5
```

Then, install a few python packages spyder needs:
```bash
pip3 install qtconsole # runs python code inside spyder
pip3 install sphinx # documentation reader
pip3 install rope # code tab-completion
pip3 install pyflakes # analyzes code for mistakes (real-time)
pip3 install pylint # analyzes code for mistakes (static)
pip3 install psutil # shows CPU and memory usage```

Then, install the in-development (--pre-release) version of spyder:
```bash 
pip3 install --pre spyder
```

Then, to fix a bug in the spyder beta, run
```bash
pip3 install colorama==0.3.5
```

To run spyder, simply type
```bash
spyder```
and a window should pop up after a bit. 

### Tips for Spyder
1. "`#%%`" at the begining of a line or comment marks a new code "cell". This allows you to split your script into chunks to run individually.
2. "`shift-enter`" runs currently highlighted code or current "cell". 
3. "`cmd-i`" shows documentation on the function or module currently under the cursor. 