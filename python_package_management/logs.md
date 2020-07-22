
# ```logging``` standard library (old way)

## basic usage

* start logging into file example.log

```
import logging
logging.basicConfig(filename='example.log',level=logging.DEBUG)
logging.debug('This message should go to the log file')
logging.info('So should this')
logging.warning('And this, too')
```

* if logging is needed for package with multiple modules, follow this example:

```
# myapp.py
import logging
import mylib

def main():
    logging.basicConfig(filename='myapp.log', level=logging.INFO)
    logging.info('Started')
    mylib.do_something()
    logging.info('Finished')

if __name__ == '__main__':
    main()
```

and in other modules do

```
# mylib.py
import logging

def do_something():
    logging.info('Doing something')
```


## more advance details

* logging library has Loggers, Filters, Handlers and Formatters
	- Loggers expose the interface that application code directly uses.
	- Handlers send the log records (created by loggers) to the appropriate destination.
	- Filters provide a finer grained facility for determining which log records to output.
	- Formatters specify the layout of log records in the final output.

* can obtain logger by giving the desired logger name to getLogger

* a good convention to use when naming loggers is to use a module-level logger, in each module which uses logging, named as follows:

``` logger = logging.getLogger(__name__) ```

this means that logger names track the package/module hierarchy, and it’s intuitively obvious where events are logged just from the logger name


* ```sys.stderr``` is the console output destination


* example why logger may need multiple handlers: if an application wants to send all log messages to a log file, all log messages of error or higher to stdout, and all messages of critical to an email address. 
This scenario requires three individual handlers where each handler is responsible for sending messages of a specific severity to a specific location.

-----------------------

# logging ```loguru``` (modern way)

* basic usage:

```
from loguru import logger

logger.info('message')
logger.warning('message')
# etc
```

* instead of this in logging

```
logger.setLevel(logging.DEBUG)

fh = logging.FileHandler("spam.log")
fh.setLevel(logging.DEBUG)

ch = logging.StreamHandler()
ch.setLevel(logging.ERROR)

formatter = logging.Formatter("%(asctime)s - %(name)s - %(levelname)s - %(message)s")
fh.setFormatter(formatter)
ch.setFormatter(formatter)

logger.addHandler(fh)
logger.addHandler(ch)
```

we can use this simplified interface in loguru

```
fmt = "{time} - {name} - {level} - {message}"
logger.add("spam.log", level="DEBUG", format=fmt)
logger.add(sys.stderr, level="ERROR", format=fmt)
```

* so there is no more Handelrs, Formatters etc
* Handlers are added using ```logger.add(...)```
* other things are specified as arguments for .add(...), like level, format, etc


* no need to call ``` logger = logging.getLogger(__name__) ```, 
enough to do ```from loguru import logger```, 
this will automatically apply ```__name__``` value


* when running ```from loguru import logger```
the logger has one handler with id 0, level set to DEBUG, and output to sys.stderr.
--> to change the specification of the console output handler need to remove the default one first, e.g.

```
from loguru import logger
logger.remove()
logger.add(sys.stderr, level='WARN')
```

 * in general ```logger.remove()``` will remove all handlers for the logger created before, in the previous example
 could also use ```logger.remove(0)``` since the single default handler has id 0. 

 * if used in a package with multiple modules enough to add handler somewhere once and it will be applied everywhere after that: 
 all modules share the same logger object (imported from loguru) with a common set of handlers in a single python interpreter process.


