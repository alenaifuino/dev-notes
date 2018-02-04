# Python Notes

## Logging

Python provides logging through the ```logging``` module. It can be used in two broad ways and both share the same principles:
* **Basic interface**: simple to set up, useful for scripts and mid-size applications
* **Logger Objects**: complex to set up, far more powerful. Scales to any size

### Basic Interface
#### Usage
```python
import logging
logging.warning('Watch out!')
logging.error('Watch out!')
```
#### Output
```
WARNING:root:Watch Out!
ERROR:root:Watch Out!
```

#### Log Level signals

The following are the log leve signals supported by the `logging` module from lowest to highest severity:
* **debug**: detailed information, should be used when diagnosing problems. Shouldn't be used in production
* **info**: confirmation that everything is working as expected. Might be used in production depending on the application
* **warning**: something unexpected happened or a potential problem in the near future (eg. filesystem full)
* **error**: the application has not been able to perform a function
* **critical**: a serious error, the application is unable to continue running

Loggers have a threshold where the default is `logging.WARNING` and it it can be changed with `logging.basicConfig(level=logging.INFO)`

Log level has two different meanings: **severity** of the message or the **threshold** for ignoring a message:
* `logging.basicConfig(level=logging.INFO)` ignores everything less severe than `logging.INFO`
* `logging.basicConfig(level=logging.DEBUG)` shows everything

#### Basic Configuration Arguments
Basic arguments to configure `logging` object: `logging.basicConfig()`
* **level**: the log level threshold as shown above
* **format**: the format of the log records
* **filename**: filename to write log messages, by default writes to stderr
* **filemode**: "a" to append to the log file (default), "w" to overwrite

##### Production vs Development example
```python
log_file = 'myapp.log'

# mode can be set by environment variable, command line option etc.
if mode === 'development':
  log_level = logging.DEBUG
  log_mode = 'w'
else:
  log_level = logging.WARNING
  log_mode = 'a'

logging.basicConfig(level = log_level, filename = log_file, filemode = log_mode)
```
