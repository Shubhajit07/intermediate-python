# Logging in python

## Security levels
There are a total of five security levels.

- **DEBUG**: this is the lowest security level.
- **INFO**: this the second level of security, use this to show info messages.
- **WARNING**: this is the default level of security when you log without any modifications, use this level when you want to warn the user that something may happen if the user doesn't do something.
- **ERROR**: use this level when some error happened.
- **CRITICAL**: this is the highest level of security, use this when something very bad happened or may happen that needs immediate attention.

> [!NOTE]
> If you don't set the security level of the logger it will use the default security level of WARNING. Below which the logger won't show any message.

---

## Logging
There are three ways of logging in python.
1. Using default logger
2. Creating custom logger
3. Logging to a file

### How to log using the default logger
To log using the default logger just import the logging package and log.
Here's how to do it.
```python
import logging

# Using the methods with the level name.
# Usage: logging.security_level(message)
logging.debug("This is a debug message...")
logging.critical("Something critical happened...")

# Using the log method
# Usage: logging.log(logging.SECURITY_LEVEL, message)
logging.log(logging.DEBUG, "This is a debug message...")
logging.log(logging.CRITICAL, "Something critical happened...")
```
> [!NOTE]
> You'll see only the critical message will be shown, because you haven't set the security level.
>
> Here's how to set security level.

```python
import logging

logging.basicConfig(level=logging.DEBUG)
```

### Creating custom logger
```python
import logging

# You must set a level for logging or the custom logger won't print anything
logging.basicConfig(level=logging.DEBUG)
my_logger = logging.getLogger(LOGGER_NAME)

# Now you can use the logger just like the previous examples.
```

> [!TIP]
> You can set the security level of your custom logger with the `setLevel` method like `my_logger.setLevel(logging.DEBUG)`

### Logging to a file
To log into a file you'll have to create a handler and then register that to your logger.
```python
import logging

logging.basicConfig(level=logging.DEBUG)

my_logger = logging.getLogger(LOGGER_NAME)

handler = logging.FileHander(FILE_NAME)

my_logger.addHandler(handler)
```

If you open the log file you'll see plain log message without any level or timestamp.
You can define the formatting with the help of Formatter.

```python
# .... previous code ....
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
handler.setFormatter(formatter)
my_logger.addHandler(handler)
```

Here's the list of formatting parameters

- %(asctime)s: Timestamp of the log message.
- %(name)s: The name of the logger.
- %(levelname)s: The severity level of the log (e.g., DEBUG, INFO, WARNING).
- %(message)s: The actual log message.

You can customize the format to include other attributes like the file name, line number, etc., using format specifiers:

- %(filename)s: The name of the file where the logging call was made.
- %(lineno)d: The line number in the file where the logging call was made.
- %(module)s: The module (the file without the .py extension).
- %(funcName)s: The function name where the logging call was made.

You can adjust the formatting string based on what you need to log.