# Chapter 4 
## 4.2 Using Predefined Classes
- Local variables are not automatically initialized to null.
- In Java, all objects live on the heap.

## 4.3 Defining Your Own Classes
- A java file can have only one public class, but the number of non public classes is not limitted.
- Java has a built in make functionality. It will automatically compile the referenced class appears in the java file when compiling it.
- Always use **clone** whenever you need to return a copy of a mutable field.
- A method can access the private data of all objects of its class.
- Final instance fields 
    - Must be initialized when the object is created. Afterwards, it may not be modified again.
    - The final keyword only means that the object reference in the variable will never again refer to a different object. But the object can be mutated. In other words, the **binding** is final.

## 4.4 Static Fields and Methods
- Static fields will be shared by all instances of that class, and can be accessed even without an instance.
- ```System.setOut```
 can modify final field "System.out" because it use native method to bypass the access control mechanisms of Java.
- Static Methods do not operate on objects. But can access static fields.
- Static methods can be used as factory method.

## 4.5 Method Parameters
- Java always uses ==**call by value**==.
- For primitive types, the parameter value is copied inside the method.
- For object references, the reference itself is copied inside the method. But the two still reference the same object. Thus a method can modify the object that is passed to it.


## 4.6 Default Field Initialization
- If no constructor is given, Java will offer you a default constructor that initialize all the fields.
- If there is a constructor, Java won't offer you that default constructor.
- Explicit Field Initialization is carried out before the constructor executes:
```
class Employee {
    private String name = "";
    private static int nextId; 
    private int id = assignId();
}
```
- Calling Another Constructor:
```
public Employee(double s) {
    // calls Employee(String, double) 
    // needs to be the first statement of the constructor
    this("Employee #" + nextId, s); 
    nextId++;
}
```
- Initialization Blocks run before the constructor body.
- To initialize static fields, either supply an initial value or use a static initialization block:
```
static {
    // Only executes once when the class is first loaded.
    ...
}
```
- Use finalize method to perform some action before the object is cleared by the garbage collector. **But do not rely on it since you never know when this method will be called.**
Use ```Runtime.addShutdownHook``` instead.

## 4.7 Packages
- Static Imports:
```
// Import static methods and fields to avoid typing class names.
import static java.lang.System.*;

out.println("hello");
exit(0);
```
- Package name must match directory structure. When running ```java test```, JVM will try to load the class following the package structure.

## 4.10 Class Design Hints
- Always keep data private.
- Always initialize data.
    - Java won't initialize local variables, but it will initialize instance fields.
- Don't use too many basic types in a class
- Not all fields need individual field accessors and mutators.
- Break up classes that have too many responsibilities.
- Make the names of your classes and methods reflect their responsibilities.
- Prefer immutable classes
    - Return a new object instead of modifying the object itself
    - This is for the sake of concurrency. Immutable objects can be safely shared by multiple threads.

