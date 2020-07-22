* more modern tool than unittest (so prefer to use it)

* pytest expects tests to be in .py files starting with ```test_``` or ending with ```_test.py```

* pytest expects function to be run as tests also to start with ```test_```

* unlike unittest, pytest supports built-in ```assert``` statement

* ```pytest``` command will run all test functions in all files, 
can run '''pytest -k pattern``` where pattern is file ending or function ending, and pytest will check only selected functions

* can set markers for test function like ```@pytest.mark.some_name``` then run 
```pytest -m some_name``` to run only marked tests

* pytest fixtures allow to run some code in each test without having to repeat it, e.g.

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
