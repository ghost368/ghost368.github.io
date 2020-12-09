* virtual env (venv)

	- ``` python -m venv test-env ``` will create test-env folder with env 
	in the current dir, activate using 

	```
	source ./test-env/bin/activate
	```
	(```deactivate``` to deactivate)

	- can install packages inside using pip
	- ```pip list``` to see installed packages


* conda 
	- uses conda channels to install packages


* poetry 
	- can be used with venv or conda environment
	- looks for packages in PyPi (same as pip)
	- but can also add some packages from conda at the start (e.g. those not in PyPi)
