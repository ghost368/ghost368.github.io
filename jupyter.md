* %cd : get current directory

* %reset : reset all variables

* %conda : apply conda operations on current python env
	- %conda install package_name

* %debug
	- post-mortem (run w/o arguments)
	- or %debug -b file:line statement
	```
	%debug myfunction(arg1, arg2)
	%debug
	```
* %load file_path (or url, module, etc)
	- will copy the contents of the file to the next cell that we can run
	- can add arguments such as the lines to copy etc
	- workings in terminal ipython, but not in VSCode

* %matploblib inline : move matplotlib backend to inline 

* %pylab : import matplotlib and numpy (backend is set to agg, need to run 
	%matplotlib inline)

* from jupyter cell (instead of terminal):
```
!jupyter nbconvert --to pdf filename.ipynb --no-prompt
```

* %config InlineBackend.figure_format = 'svg'  :  use svg image output format in jupyter

* to automatically reload module when it was changed elsewhere in the editor (very useful): 	
```
%load_ext autoreload
%autoreload 2
```

# (!) make a full list of useful ipython magic commands (!!!)


* to output every line - run
```
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```

* run jupyter magics from modules and scripts
```
from IPython import get_ipython

ipython = get_ipython()
# If in ipython, run some magics
if 'ipython' in globals():
    print('\nWelcome to IPython!')
    ipython.magic('load_ext autoreload')
    ipython.magic('autoreload 2')
```

* to use all of the page width in jupyter
```
from IPython.core.display import display, HTML
display(HTML("<style>.container { width:100% !important; }</style>"))
```


-------------------------------

### Jupyter remote connection

* create ssh tunnel (typically port will be 8888 or 8889)
* from ssh terminal run ```jupyter notebook --no-browser```
* this will create a link that can be accessed from the client (and will open client's browser)



----------------------------------



## Creating environment and project with jupyter notebooks, JupyterLab

* jupyter notebooks typically won't directly be used for production, but useful to make reports or store some tests
* jupyter notebooks maybe
	- python library guides
	- data exploration
	- signal backtests and reports

* to use jupyter lab:
	* create venv or conda env (e.g. called jupyter);
	it must contain only jupyter, jupyter lab etc

	* I will them specify env (i.e. kernel) for each jupyter notebook separately anyway, those kernels are absolutely not
	related to the env (kernel) which run the jupyterlab
	**(would be useful to have a big research env with all necessary packages, including local if they're compatible, to easily do research on everything -- but this env should be different from the env which runs the jupyterlab)**

	* extensions (to add to the jupyter environment)
		- install nodejs via conda (not pypi) ```conda install -c conda-forge nodejs```
		- ```jupyter labextension install @axlair/jupyterlab_vim``` vim (modification to work with jupyterlab 2.0.x)
		- ```jupyter labextension install jupyterlab-plotly``` using plotly 
		- install pypath_magic via pip or poetry add (```pip install pypath_magic```), used to easily add smth to pythonpath inside notebook
		(pypath_magic has to be added as --dev dependency to all envs with which I want to use it)

	* to run jupyterlab : 
		- go to any folder, activate jupyter env
		- run ```jupyter lab --no-browser```
		- copy the link, then run it with ```google-chrome --app=<link_url>```
		(chrome.exe path in Windows)
		- this will run jupyterlab, and by default the cwd of the kernels will be the dir where I ran 
		jupyter lab
		-typically I will either use an env of some project (to make research on the functions in that project), or a big research env, which will contain a lot of projects (e.g. installed via poetry using tar.gz and path or git-url and tag), the problem here mightly the different projects envs compatibility; 
		or a specifically created env for a particular research in a notebook
		- it's quite convenient to store all notebooks in one place since I'll access them all mostly through jupyter lab, and thus I can have the common folder simply open in jupyter lab, and check notebooks that're needed
		(though some notebooks with descriptive tests for a particular package may be stored directly in that package - will be supposed that notebook runs well in the package env specified in pyproject.toml)

	* dependencies
		- one option for a notebook is to run in a specific env (e.g. large research env) that have everything needed installed, including local packages (e.g. via poetry path or git installation);
		in this case we don't care about the cwd
		- it may be the case that notebooks goes together with a package and we suppose that it runs from the package env and from the package main dir;
		so basically the notebook is a set of valid commands (tests) that run well if I go to the package, activate env and run them 
		(and I'm not suppose to run them in a separate env with the package installed, just like tests inside the package used for pytest);
		- for this second option the best is to add current local folder with the package to path
		- use pypath magic : run 
		```
		%load_ext pypath_magic
		%pypath -a /path/to/package
		```
		- this approach is good because I can make changes in the package and the notebook at the same time (even more useful with autoreload)
		- also maybe used if during development I modify the package and the notebook at the same time, but later can create an env with the package properly installed to run the notebook in


* to make conda env appear in the jupyter lab kernels need run 
```
python -m ipykernel install --user --name=envNameToShow
```
(need ipykernel installed in the env, it usually is naturally)



### jupyterlab setup

* add this to keyboard shortcut settings
```
{"shortcuts": [
    {
        "command": "application:toggle-left-area",
        "keys": [
            "Accel B"
        ],
        "selector": "body",
        "disabled": true
    },
    {
        "command": "application:toggle-left-area",
        "keys": [
            "Accel X"
        ],
        "selector": "body"
    },
    {
            "command": "application:activate-next-tab",
            "keys": [
                "Ctrl PageDown"
            ],
            "selector": "body"
        },
    {
            "command": "application:activate-previous-tab",
            "keys": [
                "Ctrl PageUp"
            ],
            "selector": "body"
        }
    ]
}
```

* jupyterlab-vim 
	- allows vim keybindings on cell level and also additional vim-like shortcuts on the cell level
	- check https://github.com/jwkvam/jupyterlab-vim for list of keybindings
	- cannot have key map config; the only one I need is jk instead of Esc: in normal mode inside cell do ```: imap jk <Esc>``` at the start of each session
	- use :q to go from vim cell to vim jupyter mode, Enter to go vim-cell mode for the selected cell
	- simplify going to jupyter mode (:q) can use ```: imap qq :q<cr>``` (press qq from insert mode, in jupytervim not really possible to map anything in normal mode)





* close tab is Alt+w in jupyter lab (not Ctrl+W which closes the whole thing - inherited from chrome)
* jupyter supports autocompletion using tab (similar to plain ipython), but won't show option list automatically

* use %prun magic to profile a cell run
