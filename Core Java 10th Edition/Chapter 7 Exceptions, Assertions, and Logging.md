# Chapter 7

## 7.1 Dealing with Errors
- ```Throwable``` is the ancestor of all Exceptions and Errors
- Errors refer to java runtime system, which should not be thrown by our code.
- RuntimeException - programming error
    - If it is a RuntimeException, it is your fault.
- Other exception - bad things happened
- When an exception is thrown:
    - call a method that throws a checked exception
    - you dectect an error and ```throw``` it
    - you make programming error - unchecked
    - internal error occurs in VM or runtime library
- For the first two cases, you need to declare the possibility of throwing some exceptions.
- As a rule of thumb, a method must declare all the checked exceptions that it might throw. Unchecked exceptions are either beyond your control (Error) or result from conditions that you should not have allowed in the first place (RuntimeException).

## 7.2 Catching Exceptions
- You should catch those exceptions that you know how to handle and propagate those that you do not know how to handle.
- You are not allowed to add more throws specifiers to a subclass method than are present in the superclass method.
- The value of the return statement in the finally clause could mask the return value in the try clause.
- Try-with-Resource Statement
```
// in.close() will be called automatically when the try block exits
try (Scanner in = new Scanner(new FileInputStream(path), "UTF-8"))
{
    in.next();
    ...
}
```

## 7.3 Tips for Using Exceptions
- Exception handling is not supposed to replace a simple test. Use exceptions for exceptional circumstances only.
- Do not micromanage exceptions.
- Make good use of the exception hierarchy.
- Do not squelch exceptions.
- When you detect an error, "tough love" works better than indulgence.
- Propagating exceptions is not a sign of shame
- Throw early, catch late.

## 7.4 Using Assertions 
- ``` assert x >= 0;```
- ``` assert x >= 0 : x; \\ Will pass the actual value of x into AssertionError object```
- By default, assertions are disabled.
- use ``` java -ea MyApp ``` to enable assertion.
- When to use assertions:
    - Assertion failures are intended to be fatal, unrecoverable errors.
    - Assertion checks are turned on only during development and testing.

## 7.5 Logging
- Basic Logging:
    - ```Logger.getGlobal().info("something");```
    - ```Logger.getGlobal().setLevel(Level.OFF);```
- Advanced Logging:
    - Create or retrieve:```private static final Logger myLogger = Logger.getLogger("com.mycompany.myapp");```
    - 7 logging levels:
        - SEVERE
        - WARNING
        - INFO
        - CONFIG
        - FINE
        - FINER
        - FINEST
    - Each level has its own method:
        - ```logger.warning(msg);```
        - ```logger.fine(msg);```
        - Or ```logger.log(Level.FINE, msg);```
    