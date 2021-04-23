* more modern tool than unittest (so prefer to use it)

* pytest expects tests to be in .py files starting with ```test_``` or ending with ```_test.py```

* pytest expects function to be run as tests also to start with ```test_```

* unlike unittest, pytest supports built-in ```assert``` statement

* ```pytest``` command will run all test functions in all files, 
can run '''pytest -k pattern``` where pattern is file ending or function ending, and pytest will check only selected functions

* can set markers for test function like ```@pytest.mark.some_name``` then run 
```pytest -m some_name``` to run only marked tests;
to avoid warning need to register custom markers in a pytest.ini file placed in the package root, with content like this
```
[pytest]
markers =
    webtest: mark a test as a webtest.
```


* pytest fixtures allow to run some code in each test without having to repeat it (must use fixtures instead of global variables), e.g.

```
import pytest
@pytest.fixture
def supply_AA_BB_CC():
	aa=25
	bb =35
	cc=45
	return [aa,bb,cc]

def test_comparewithAA(supply_AA_BB_CC):
	zz=35
	assert supply_AA_BB_CC[0]==zz,"aa and zz comparison failed"

def test_comparewithBB(supply_AA_BB_CC):
	zz=35
	assert supply_AA_BB_CC[1]==zz,"bb and zz comparison failed"

def test_comparewithCC(supply_AA_BB_CC):
	zz=35
	assert supply_AA_BB_CC[2]==zz,"cc and zz comparison failed"
```

* parametrized tests : running the same test for multiple groups of input parameters, e.g.

```
import pytest
@pytest.mark.parametrize("input1, input2, output",[(5,5,10),(3,5,12)])
def test_add(input1, input2, output):
	assert input1+input2 == output,"failed"
```

* ```@pytest.mark.xfail``` decorator will run the test but skip the fail

* ```@pytest.mark.skip``` will skip the test (better way for temp skipping than commenting)


* pytest is commonly used for testing python APIs, there are tutorials available online on the topic

* if some pre-saved is needed for tests: create subfolder in the tests folder with the same name as test .py module and store the expected input/output there, 
if those data will be used for testing multiple function - write a fixture (!) for loading it just once!


* running ```pytest --pdb``` will drop to pdf on any error during tests

* can use ```pytest.set_trace()``` to set breakpoints in test code, that will later be used if ```pytest --pdb``` is run

* install ```pdbpp``` package (add to poetry dev dependencies) to get better console debugger when using ```pytest --pdb```


* to mock absent context (like plot backend, running JVM, etc) use ```unittest.mock```, e.g.
```
from unittest.mock import patch 
import pytest 
import matplotlib.pyplot as plt 

def plot_fn():
    plt.plot([1,2,3])
    plt.show()

@patch("matplotlib.pyplot.show")
def test_plot_fn(mock_show):
    plot_fn()
```
(**learn more on this**)

* to test failure with exception (that's expected) - use ```pytest.raises```

* pytest >= 6.0 maybe buggy with poetry and toml files, using ^5.0 for now

* to run tests for a given package run ```python -m pytest [...]``` from cmd
(running simply ```pytest [...]``` is similar but may have problems with import modules, it won't add current dir to path, etc)

* to debug pytest run use
```
python -m pytest --pdb
```
if any errors occur, pdf will stop at error and it's possible to access variables; can also set trace in the code using
pytest.set_trace() (to stop pdb there and then continue using usual commands s, n, c)

* use ```--capture=no``` to show logs in command line run
