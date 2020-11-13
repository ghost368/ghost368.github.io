# Debugging in VSCode

* cell debug

|command| action|
|------------|--------------|
|Shift+Alt+D| to start cell debug|
| F10| step over|
 |F11| step into|
| Shift+F11 |step out|
|Ctrl+Shift+F10| disconnect debugger|
|F5| continue until breakpoint or end|
|Alt+Shift+F10| run until cursor (if in vim -- should be in insert mode)|
|F9| set breakpoint|

* debug of script or module
	- run F5
	- choose to debug current file as script or a module
	- if module is selected then input it's name (can be relative path), add to python path in terminal if necessary using ```. cwd-to-pypath```
	- set breakpoints using F9 in advance
	- confirm debug and use the same shortcuts as for cell to go through

* use Shift+Alt+B to remove all breakpoints

* use Ctrl+; to open/close debug console (where I can check variables and type code)


# Debugging in terminal with pdb (ipdb)

* variable autocomplete using tab works inside pdb

* general pdb (ipdb) navigation commands

|command| action|
|------------|--------------|
|n or next| step over|
|s or step| step into|
|c or continue| continue until breakpoint or end|
|j line_nb| jump to line number in the current file (without running code in-between)|
|b file_path: line_nb| create breakpoint in any file|
|r| move to the current function return (useful since there's no step out in pdb)|
|q| quit debugger|

* if the code fails : the post-mortem session will open - will still be possible to 
check variable at the point of failure (!!)
 

* install pdbpp (a better version of pdb that's supported by running python -m pdb ...), ipdb that can be used in ipython to replace pdb

* pdb is not able to import from cwd (the output of os.getcwd()) unlike ipython, 
will need to add it to PYTHONPATH using export

------------------------------

* to debug a script use 

```
python -m pdb script.py
```

can debug a module in python 3.7+ using 

```
python -m pdb -m module
```

* either of this commands with open pdb debugger at the start of the script
	
----------------------------------

* to debug a command in ipython
	- after failed command run %debug : this will open post-mortem ipdb
	- before running commands run %pdb on : this will auto drop to ipdb if error (%pdb off to turn off)
	- import ipdb and run ```ipdb.run('any_command'); 
	then run s(step) first -> this will put the debugger at the beginning of the function call in the command -> navigate as usual

------------------------------

* remote debug if error in production files:
	* when debugging using ipdb remotely from terminal and w/o vscode -- useful to use tmux to 
	open code files in vim in one window and pdb debug in the other
	* can use post-mortem for terminal commands with ```-m pdb``` if that's enough (run and press continue)
	* or go to ipython -> run command that breaks -> use pdb post-mortem with %debug to check variables
	* in ipython use %debug with arguments
	```
	%debug -b file_path:line_nb statement
	```
	(can omit breakpoint -b, statement is any python function call or command)
	* otherwise can use ipdb.run(..) and go step-by-step -- useful to look at file in vim and see the line numbers :
	
		can use them to run ```j line_mb``` and ```b file_path: line_nb``` to jump or set breakpoints to stop 