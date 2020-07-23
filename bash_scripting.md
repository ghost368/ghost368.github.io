* script to get python package version in the current env

```
#!/bin/bash

PACKAGE=$1
python -c "import $PACKAGE; print($PACKAGE.__version__)"
```