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

* jupyter supports autocompletion using tab (similar to plain ipython), but won't show option list automatically


## Jupyter Lab

* extensions
	- ```jupyter labextension install @axlair/jupyterlab_vim``` vim (modification to work with jupyterlab 2.0.x)
	- ```jupyter labextension install jupyterlab-plotly``` using plotly 