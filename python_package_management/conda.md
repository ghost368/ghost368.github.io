* conda is an environment management for any programming language

* anaconda is a distribution of conda and comes with a lot of python datascience packages

* miniconda is pure conda without any install packages (should be used in most cases)

* ```conda update conda``` to get the most recent version

* install miniconda

```
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
bash ~/miniconda.sh
export PATH=$PATH:~/miniconda3/bin
conda init bash
```

(might need to reopen terminal in between the commands)


* can create conda environment 
	- manually
	- using env.yml file

* example of environment.yml file

```
name: playenv
channels:
- conda-forge
dependencies:
- python=3.6
- pip
- pip:
    - pyjokes
```

use ```conda env create --file environment.yml``` to create conda env from it, 
then ```source activate playenv``` to activate 


* create manually, e.g.

```
conda create -c conda-forge -n test_env python=3.8 numpy matplotlib pandas
```

(can skip package, or add their version etc)


* to export current env use ```conda env export -f test_env.yml -n test_env```

* clone another env 

```
conda create --name live_env --clone test_env
```

* delete named env

```
conda env remove -n live_env
```

* above ```-n``` stands for name, named envs are placed in ~/anaconda/envs or smth like that, 
can use ```-p``` and env path (like ./.env) - then env will be created in that path, and won't have name

* manual package install
```
conda install -c conda-forge rasterio=0.35
``` 
(-c is used for channel, conda-forge here, can permanently add channel ```conda config --add channels conda-forge```)

* various channels can have different versions of the same package
* PyPI is standard python package repo, conda channels are multiple, and can have non-standardized packages
* some packages are not in PyPI, but can be in some conda channel


* script to get conda version of a single package

conda-v.py

```
import subprocess
import re
import sys
out = subprocess.Popen(['conda', 'list'], 
                        stdout=subprocess.PIPE, 
                        stderr=subprocess.STDOUT)
stdout,stderr = out.communicate()
package_name = sys.argv[1]
version = re.match(f'(?:.*\n)*{package_name}\s*(\S*)(?:.*\n.*)*', stdout.decode('utf-8')).group(1)
print(re.sub(' +', '  ', f'{package_name} {version}'))
```

conda-v

```
#!/bin/bash

python conda-v.py "$1"
```