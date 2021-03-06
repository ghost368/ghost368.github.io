
* easiest way to install is using pipx
(see pipx installation tips in another file)
```
pipx install poetry
```

* to update poetry version 

```
poetry self update
```

* to start a new package : make package dir, cd to it, then run 

```
poetry init
```

and follow the guide 


* add dependencies in the pyproject.toml file, 
```poetry update``` to update all floating dependencies (like "*" or "3.x") and general lock file, 
```poetry install``` only to install dependencies fixed in the lock file to the current environment

* current project is installed in editable mode (similar to pip -e) by default, to only install dependencies use 

```
poetry install --no-root
```

* interactively add and remove packages using ```poetry add some_package```, ```poetry remove some_package```

* editable mode for pip

```
pip install -e path/to/SomeProject
```
(essentially used to develop two related projects at the same time)

* to temporarily use local version of package (e.g. for simultaneous development) add the package build (some recent version of it) via path option to pyproject.toml to install it with dependencies, that use ```pip uninstall package_name``` (this will not uninstall dependencies) and simply add the repo with package to python path in the notebook, together with autoreload this will pull up all the changes every time, and build and install new package version later when dev is done.


* python package egg-info - distribution format for python packages, 

it is similar to java .jar file - contains project data about a specific release, has .egg extension


* to run tests

```
poetry run pytest tests/
```

* to specify git dependency (use ssh rather that http - otherwise poetry will wait for username/password and break)

```
[tool.poetry.dependencies]
python = "3.8.x"
analysis = {git = "git@github.com:ghost368/analysis.git", tag = "v0.4", branch = "master" }
```

use tag in git repo to tag versions, can install a specific version from git, and use specific branch

* local dependency (may be useful during simult. development of two packages)

```
[tool.poetry.dependencies]
# directory
my-package = { path = "../my-package/" }

# file
my-package = { path = "../my-package/dist/my-package-0.1.0.tar.gz" }
```

* poetry assumes that the package folder has the same name as given in pyproject.toml and is in the project root or in root/src - 
highly recommened to use this project template (!)

Full information on python-poetry.org


* when removing a package or changing version need to put ```--dev``` option if the package is in dev-dependencies




* standard dev dependencies
```
jupyter = "^1.0.0"
pytest = "^6.0.1"
black = {version = "^19.10b0", allow-prereleases = true}
jedi = "^0.17.2"
ipdb = "^0.13.3"
rope = "^0.17.0"
pylint = "^2.6.0"
```

* poetry version command (get or adjust version)
	- no argument : get the current version
	- major	1.3.0 -> 2.0.0
	- minor	2.1.4 -> 2.2.0
	- patch	4.1.1 -> 4.1.2
	- specify exact new version number


--------

## Questions:

- how to install specific version from folder with various tar.gz files (e.g. like qmspy was distributed)
- learn other ways for package distribution (e.g. setup.py, distutils) - how they interact with poetry?? e.g. install local package distributed using another system to poetry package?
