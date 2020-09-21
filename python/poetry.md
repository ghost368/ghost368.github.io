
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
--------

## Questions:

- how to install specific version from folder with various tar.gz files (e.g. like qmspy was distributed)
- learn other ways for package distribution (e.g. setup.py, distutils) - how they interact with poetry?? e.g. install local package distributed using another system to poetry package?
