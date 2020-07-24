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

--------------------------------------------------------------------------

* scripts vs modules vs packages

	- script is any .py file with python commands
	- the same is true for module (just saved in a .py file)
	- when python reads source file, it assigns __name__ variable
	- if the .py file is run as a main program, the __name__ (inside its namespace) is assigned to __main__
	- if the .py file is imported as module (like ```import foo```) elsewhere -- __name__ is assigned to the module name
	- a package is a generalization of module to having multiple files : it's put in a folder with __init__ file that can import necessary tools 
	from the other files in the folder
	- when ```import``` is run with a package (rather than single file module) -- actually it's __init__.py is imported
	- both modules and packages (and scripts - since internally they are just .py files, same as modules) can be used both as libs for import and 
	the main programs:
		- for modules need to add ```if __name__ == "__main__":``` section with code that will only be run when module is run as a main program (via python or python -m by OS, not import), 
		the other parts typically only contain function and constant declarations
		- for packages need to specify __main__.py inside a package
		- module can be run in the same way using ```python file_name.py``` and ```python -m file_name```
		- package can only be run with ```-m``` option
	- when running script (__main__.py file) the relative imports will not work, for this need to run module



* command line python command

```
python [-c command | -m module-name | script | - ] [args]
```
	- -c is used to run command (or multiple commands, put in a string with \n), further arguments are treated as strings and are passed to sys.argv[1], sys.argv[2] etc
	(cwd is automatically added to sys.path)

	- -m is used to run file as module (don't put .py in this case, will get error otherwise) -- will get the same results as running it as script, or to run a package 
	(in this case the code in __main__.py will be run), args are passed to sys.argv[1:], cwd is automatically added to sys.path

	- run script : may be a file, a dir or a zip file containing __main__.py


* it's possible to really run python script of module as main only from cmd (or its emulator inside python), inside other .py file can only use import

* can debug any function or cell inside vsdode, using cell debug;
to debug module or script in vscode use F5-ShiftF5 (choose to debug as script, or as module if contains relative imports -- it will autostop at any error or exception)

* if need to debug remotely using cmd
	- debug inside ipython:
		- use %pdb to sell ipdb-drop at any error or exception
		- use %debug to debug post-mortem right after a failed command
	- debug module or script from command line use ```python -m pdb -m module_name``` or ```python -m pdb script.py```