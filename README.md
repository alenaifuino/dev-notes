# Python Notes

## Logging
Python provides logging through the ```logging``` module. It can be used in two broad ways and both share the same principles:
* **Basic interface**: simple to set up, useful for scripts and mid-size applications
* **Logger Objects**: complex to set up, far more powerful. Scales to any size

### Basic Interface
##### Usage
```python
import logging
logging.warning('Watch out!')
logging.error('Watch out!')
```
##### Output
```shell
> WARNING:root:Watch Out!
> ERROR:root:Watch Out!
```

#### Log Level signals
The following are the log level signals supported by the `logging` module from lowest to highest severity. The order matters in the list below; *debug* is considered strictly less severe than *info*, and so on.

* **debug**: detailed information, should be used when diagnosing problems (shouldn't be used in production)
* **info**: confirmation that everything is working as expected (might be used in production depending on the application)
* **warning**: something unexpected happened or a potential problem in the near future (eg. filesystem full)
* **error**: the application has not been able to perform a function
* **critical**: a serious error, the application is unable to continue running

Each level has a corresponding uppercased constant in the library (e.g., `logging.WARNING` for `logging.warning()`) and are used when defining the log level threshold. The default is `logging.WARNING` and it it can be changed with `logging.basicConfig(level=logging.INFO)`

The phrase *log level* has two different meanings depending on the context. It can mean the **severity** of the message, which can be set by choosing which of the functions to use (e.g., `logging.warning()`). Or it can mean the **threshold** for ignoring a message which is signaled by the constants (e.g., `logging.WARNING`)

Constants can also be used in the more general `logging.log` function
```python
logging.log(logging.DEBUG, "Small detail, useful for troubleshooting")
```
This is useful to modify the log level dynamically at runtime:
```python
def log_results(message, level=logging.INFO):
    logging.log(level, 'Results: ' + message)
```

#### Configuring the Basic Interface

The `logging.basicConfig()` function has to be called exactly once and it must happen before the first logging event. Additionally if the program has several threads, it must be called from the main thread and *only* the main thread.

##### Basic Configuration Arguments
* **level**: the log level threshold as shown above
* **format**: the format of the log records, by default <levelname>:<name>:<message> (name = name of the logger object, by default root)
* **filename**: filename to write log messages, by default writes to stderr
* **filemode**: "a" to append to the log file (default), "w" to overwrite



##### Production vs Development Example
```shell
> export MODE=development
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
