# Chapter 5
## 5.1 Classes, Superclasses and Subclasses
- Java use keyword ```super``` to call a superclass method.
- Subclass Constructor
    - The call using ```super``` must be the first statement in the constructor for the subclass.
    - If the subclass constructor does not call a superclass constructor explicitly, the no-argument constructor of the superclass is invoked.
- Abstract Classes
    - A class with one or more abstract methods must itself be declared abstract
- Protected fields or methods can be used by 
    - subclasses 
    - other classes in the same package

## 5.2 Object: The Cosmic Superclass
- Every class is subclass of Object
- Only values of primitive types (numbers, char, boolean) are not objects.
- Arrays are class types that extend the Object class
- Implement ```equals()``` method:
    - Name the explicit parameter ```otherObject```
    - Short cut: ```if (this == otherObject) return true;```
    - Test null: ```if (otherObject == null) return false;```
    - Compare classes: 
        - ```if (getClass() != otherObject.getClass()) return false;```
        - ```if (!(otherObject instanceof ClassName)) return false;```
    - Cast otherObject: ```ClassName other = (ClassName) otherObject;```
    - Compare fields.
- Implement ```hashCode()``` method for inserting into a HashTable
    - If ```x.equals(y)``` is true, then ```x.hashCode()``` must equals to ```y.hashCode()```
- Get class name string: ```getClass().getName()```
- Print an array: ```Arrays.toString(array);```
- Print multidimensional array: ```Arrays.deepToString(array);```

## 5.5 Varargs
- ```printf(String fmt, Object... args)```, compiler will transform the call of such a function, bundling the parameters into an array and autoboxing as necessary.
- To some extent, ```Object...``` is like ```Object[]```, only that the compiler will do the conversion.

## 5.6 Enumeration Classes
- The type defined by enum is actually a class, with one instance for each type.
- All enumerated types are subclasses of the class Enum.
- Constructor:
```
public enum Size {
    // Calling the constructor for each instance.
    SMALL("S"), MEDIUM("M"), LARGE("L"), EXTRA_LARGE("XL");
    
    private String abbr;
    private Size(String abbr) {this.abbr = abbr;}
    public String getAbbr(return abbr;)
}
```
- Return an array of all values of the enumeration: ```Size[] values = Size.values(); ```
- Conversion between String and type:
    - ```Size.SMALL.toString(); // Returns "SMALL"```
    - ```Size s = Enum.valueOf(Size.class, "SMALL");```

## 5.7 Reflection
- Will study when acutally used.

## 5.8 Design Hints for Inheritance
- Place common operations and fields in the superclass.
- Don't use protected fields.
    - But protected methods can be used.
- Use inheritance to model "is-a" relationship.
- Don't use inheritance unless all inherited methods make sense.
- Don't change the expected behavior when you override a method.
- Use polymorphism, not type information.
- Don't overuse reflection.

