* script to get python package version in the current env

```
#!/bin/bash

PACKAGE=$1
python -c "import $PACKAGE; print($PACKAGE.__version__)"
```

* the error 
```
Bash script and /bin/bash^M: bad interpreter: No such file or directory
```
is related to creation of linux scripts on windows remotely, they use different line endings (try re-saving it from linux using vim; if using rmate with sublime -- in sublime View -> Line endings -> Unix)