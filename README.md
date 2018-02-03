# Python Notes

## Logging
It can be used in two broad ways and both share the same principles:
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
* **debug**: detailed information, should be used when diagnosing problems
* **info**: confirmation that everything is working as expected
* **warning**: something unexpected happened or a potential problem in the near future (eg. filesystem full)
* **error**: the application has not been able to perform a function
* **critical**: a serious error, the application is unable to continue working
