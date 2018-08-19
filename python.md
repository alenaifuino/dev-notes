# Python 3

## Contents
* [Logging](#logging)

---
<div align="right">

[← back to Home](docs/README.md)

</div>
<br>

## Logging
Python provides logging through the ```logging``` module. It can be used in two broad ways and both share the same principles:
* __Basic interface__: simple to set up, useful for scripts and mid-size applications
* __Logger objects__: complex to set up, far more powerful. Scales to any size

### Basic Interface
###### Usage
```python
import logging
logging.warning('Watch out!')
logging.error('Watch out!')
```
###### Output
```shell
$ WARNING:root:Watch Out!
$ ERROR:root:Watch Out!
```

#### Configuring the Basic Interface
The `logging.basicConfig()` method has to be called exactly once and it must happen before the first logging event. Additionally if the program has several threads, it must be called from the main thread and *only* the main thread.

##### Basic Arguments
* __level__: the log level threshold
* __format__: the format of the log records
* __filename__: filename to write log messages, by default writes to stderr
* __filemode__: "a" to append to the log file (default), "w" to overwrite

###### Log Level signals
The following are the log level signals supported by the `logging` module from lowest to highest severity. The order matters in the list below; _debug_ is considered strictly less severe than _info_, and so on.

* __debug__: detailed information, should be used when diagnosing problems (shouldn't be used in production)
* __info__: confirmation that everything is working as expected (might be used in production depending on the application)
* __warning__: something unexpected happened or a potential problem in the near future (eg. filesystem full)
* __error__: the application has not been able to perform a function
* __critical__: a serious error, the application is unable to continue running

Each level has a corresponding uppercased constant in the library (e.g., `logging.WARNING` for `logging.warning()`) and are used when defining the log level threshold. The default is `logging.WARNING` and it it can be changed with `logging.basicConfig(level=logging.INFO)`.

The phrase _log level_ has two different meanings depending on the context. It can mean the __severity__ of the message, which can be set by choosing which of the methods to use (e.g., `logging.warning()`). Or it can mean the __threshold__ for ignoring a message which is signaled by the constants (e.g., `logging.WARNING`).

Constants can also be used in the more general `logging.log` method
```python
logging.log(logging.DEBUG, 'Small detail, useful for troubleshooting')
```
This is useful to modify the log level dynamically at runtime:
```python
def log_results(message, level=logging.INFO):
    logging.log(level, 'Results: ' + message)
```

###### Format Attributes
Named fields are defined in percent-formatting by %(FIELDNAME)x, where "x" is a type code: _s_ for string, _d_ for integer (decimal), and _f_ for floating-point.
The default is `%(levelname)s:%(name)s:%(message)s` where name is the name of the logger object (by default *root*).

Some of the most common attributes:

Attribute | Format        | Description
--------- | ------------- | -----------
asctime   | %(asctime)s   | Human-readable date/time
funcName  | %(funcName)s  | Name of function containing the logging call
lineno    | %(lineno)s    | The line number of the logging call
message   | %(message)s   | The log message
pathname  | %(pathname)s  | Full pathname of the source file of the logging call
levelname | %(levelname)s | Text logging level for the message ('DEBUG', 'INFO', 'WARNING', 'ERROR', 'CRITICAL')
name      | %(name)s      | The logger's name

Full list can be found [here](https://docs.python.org/3/library/logging.html#logrecord-attributes)

__Note__: if the log level threshold is higher than the message itself, the line does nothing. Having this into consideration it's important to consider avoiding formatting the string passed to the logger object in order to avoid using system memory and CPU cycles when no logging will take place.

#### Implementation Example
```shell
$ export MODE=development
```
```python
import os
mode = os.environ.get('MODE', 'production').upper()

log_file = 'myapp.log'

# mode can be set by environment variable, command line option etc.
if mode === 'DEVELOPMENT':
    log_level = logging.DEBUG
    log_mode = 'w'
else:
    log_level = logging.WARNING
    log_mode = 'a'

logging.basicConfig(level = log_level, filename = log_file, filemode = log_mode)
```

### Logger Objects
Larger Python applications tend to have different logging needs. `logging` meets these needs through a richer interface, called _logger objects_ or simplu _loggers_.

When a call to `logging.warning()` (or other log method) is made, they convey messages through what is called the _root logger_, the primary, default logger object.

`logging.basicConfig` operates on this root logger and the actual root logger object can be fetch by calling `logging.getLogger()`
```python
logger = logging.getLogger()
logger.name
```
```shell
> 'root'
```

Logger objects have all the same methods the logging module itself has:
```python
import logging
logger = logging.getLogger()
logger.debug('Small detail. Useful for troubleshooting.')
logger.info('This is informative.')
logger.warning('This is a warning message.')
logger.error('Uh oh. Something went wrong.')
logger.critical('We have a big problem!')
```


