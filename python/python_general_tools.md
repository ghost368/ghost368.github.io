* pip 

```
sudo apt-get install python3-pip
```

* pipx

```
python3 -m pip install --user pipx
python3 -m pipx ensurepath
```


* venv

```
sudo apt-get install python3-venv
```

* to check python version inside environment 
``` python --version```

* if run ```python -m ... ``` or ```python -c ...``` from cmd, the python version interpreter will be chosen from the current env, but can 
use e.g. ```python2 -m ... ``` to run with the latest python2 version (won't ever use)


* tab variable autocomplete works in ipython (!)


* can debug any function or cell inside vsdode, using cell debug;
to debug module or script in vscode use F5-ShiftF5 (choose to debug as script, or as module if contains relative imports -- it will autostop at any error or exception)

* if need to debug remotely using cmd
	- debug inside ipython:
		- use %pdb to sell ipdb-drop at any error or exception
		- use %debug to debug post-mortem right after a failed command
	- debug module or script from command line use ```python -m pdb -m module_name``` or ```python -m pdb script.py```


* profiling tools:
	- install KCacheGrind ```sudo apt-get install -y kcachegrind```
	- install ```pyprof2calltree``` from PyPI via pip (poetry)
	- run in bash (which supports X11 if ssh is used)
	```
	python -m cProfile -o myscript.cprof myscript.py
	pyprof2calltree -k -i myscript.cprof
	```

* if a module will be called from command line with arguments (e.g. in production) use argparse standard module, here is a code example
```
import argparse

parser = argparse.ArgumentParser(description='Process some integers.')
parser.add_argument('integers', metavar='N', type=int, nargs='+',
                    help='an integer for the accumulator')
parser.add_argument('--sum', dest='accumulate', action='store_const',
                    const=sum, default=max,
                    help='sum the integers (default: find the max)')

args = parser.parse_args()
print(args.accumulate(args.integers))
```

