# Chapter 6

## 6.1 Interfaces
- All methods of an interface are automatically public. Therefore it's not necessary to supply the keyword ```public```.
- Interfaces **NEVER** have instance fields.
- But interfaces **CAN** have constants. You don't need to provide ```public static final```, compiler will do it for you.
- Can use ```instanceof``` to test if the class of an object implements some interface.
- Static methods:
```
public interface Path {
    public static Path get(String first, String... more) {
        return FileSystems.getDefault().getPath(first, more);
    }
}
```
- Default methods:
```
public interface Comparable<T> {
    default int compareTo(T other) {
        return 0;
    }
}
```
- If name conflict occurs between interfaces and classes, classes always win.

## 6.3 Lambda Expressions
- Functional Interface: An interface that has only one abstract method.
- ArrayList has a removeIf method whose parameter is a Predicate:
```
list.removeIf(e -> e == null);
```
- Method References:
```
Timer t = new Timer(1000, event -> System.out.println(event));

// x -> System.out.println(x)
Timer t = new Timer(1000, System.out::println);

// (x,y) -> x.compareToIgnoreCase(y)
Arrays.sort(strings, String::compareToIgnoreCase);
```

- Constructor References:
```
ArrayList<String> names = ...;
Stream<Person> stream = names.stream().map(Person::new);
List<Person> people = stream.collect(Collectors.toList());
Person[] people = stream.toArray(Person[]::new);
```
- Closure: a block of code together with the values of the free variable.
- In lambda expression, you can only reference variables whose value doesn't change.
```
public static void countDown(int start, int delay) {
    ActionListener listener = event -> {
        start--; // Error: Can't mutate captured variable System.out.println(start);
    }; 
    new Timer(delay, listener).start(); 
}
```
- It's also illegal to refer to a variable in a lambda expression that is mutated outside.
```
public static void repeat(String text, int count) {
    for (int i = 1; i <= count; i++) {
        ActionListener listener = event -> {
            System.out.println(i + ": " + text); // Error: Cannot refer to changing i
        }; 
        new Timer(1000, listener).start(); 
    } 
}
```
- **The rule is that any captured variable in a lambda expression must be effectively ```final```.**
- More about Comparators:
```
Arrays.sort(people, Comparator.comparing(Person::getName));
Arrays.sort(people, Comparator.comparing(Person::getLastName)
                              .thenComparing(Person::getFirstName));

Arrays.sort(people, Comparator.comparing(Person::getName, 
        (s,t) -> Integer.compare(s.length(), t.length())));

// Same as above, but avoid boxing
Arrays.sort(people, Comparator.comparingInt(p -> p.getName().length()));
```

## Inner Classes
- Why inner classes:
    - Inner class methods can access data (even private) from the enclosing class.
    - Inner class can be hidden from other classes from the same package.
    - Anonymous inner classes are handy when you want to define callbacks without writing a lot of code.
- An object of an inner class always gets an implicit reference to the object that created it. This is done by the compiler, who will add outer class's reference in the constructor of the inner class.
- Only inner classes can be private.
- Inner classes are implemented as regular classes by compiler. The JVM has no idea about them.
- Local Inner classes:
    - Defined inside a method
    - Never declared with an access specifier
    - Only the method itself can see it
- Static Inner classes:
    - Do not have a reference to outer class
    - In a static method, static inner class must be used
    - Unlike regular inner classes, static inner classes can have static fields and methods
    - Inner classes that are declared inside an interface are automatically ```static``` and ```public```
    - Use it whenever the inner class does not need to access an outer class object

## 6.5 Proxies
