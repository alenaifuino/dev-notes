# Python Notes

### Logging
It can be used in two broad ways and both share the same principles:
* **Basic interface**: simple to set up, useful for scripts and mid-size applications
* **Logger Objects**: complex to set up, far more powerful. Scales to any size

#### Basic Interface
##### Usage
```python
import logging
logging.warning('Watch out!')
```
##### Output
```
~ $: WARNING:root:Watch Out!
```
