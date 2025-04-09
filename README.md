# java-8_features
Java 8 introduced several powerful features that transformed how developers write Java code, making it more concise, expressive, and functional. These features are essential to understand for an interview, as they significantly improve code quality and are frequently used in modern Java development.

Here are **detailed notes on Java 8 features** for an interview:

---

### **1. Lambda Expressions**
Lambda expressions are one of the most important features introduced in Java 8. They allow you to pass functionality as an argument to a method or store it in a variable. Lambdas make the code more concise and expressive, particularly when working with collections and streams.

#### **Syntax:**
```java
(parameters) -> expression
```

- **Example**:
```java
(int a, int b) -> a + b;
```

- **Example 2 (Runnable)**:
```java
Runnable r = () -> System.out.println("Hello from Lambda!");
r.run();
```

#### **Key Points:**
- **Functional Interfaces**: Lambda expressions can be used with functional interfaces (interfaces with one abstract method).
- **Code Simplification**: Helps to eliminate boilerplate code for implementing interfaces like `Runnable`, `Comparator`, etc.
- **Usage with Collections**: Allows easy iteration and filtering operations on collections.

---

### **2. Functional Interfaces**
A **Functional Interface** is an interface with exactly one abstract method. Java 8 provides a set of built-in functional interfaces in the `java.util.function` package.

#### **Key Points:**
- **Functional Interface Annotation**: You can use the `@FunctionalInterface` annotation to indicate that an interface is intended to be a functional interface (though it's not required).
- **Examples of Functional Interfaces**:
  - **`Runnable`**: Represents a task to be executed.
  - **`Predicate<T>`**: Represents a function that takes a parameter of type `T` and returns a boolean.
  - **`Function<T, R>`**: Represents a function that takes an argument of type `T` and returns a result of type `R`.
  - **`Consumer<T>`**: Represents an operation that takes an argument of type `T` and returns no result.
  - **`Supplier<T>`**: Represents a supplier of results, takes no input but returns a result.

#### **Example:**
```java
@FunctionalInterface
public interface MyFunctionalInterface {
    void myMethod();
}
```

---

### **3. Streams API**
The **Stream API** is a new abstraction that allows for functional-style operations on sequences of elements, such as collections. Streams allow you to process data in a more declarative and readable way.

#### **Key Concepts**:
- **Stream**: A sequence of elements supporting aggregate operations.
- **Operations**: Streams support both **intermediate** (e.g., `filter()`, `map()`) and **terminal** (e.g., `collect()`, `forEach()`) operations.

#### **Types of Operations**:
- **Intermediate Operations**: These operations are **lazy** and return a new stream (e.g., `filter()`, `map()`).
- **Terminal Operations**: These operations are **eager** and produce a result or side-effect (e.g., `collect()`, `forEach()`).

#### **Example**:
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> squared = numbers.stream()
                                .map(x -> x * x)
                                .collect(Collectors.toList());
System.out.println(squared);  // Output: [1, 4, 9, 16, 25]
```

#### **Key Methods**:
- **forEach()**: Performs an action for each element.
- **filter()**: Filters elements based on a condition.
- **map()**: Transforms elements.
- **reduce()**: Combines elements into a single result (e.g., sum, max).
- **collect()**: Collects the result into a container, such as a list or set.

---

### **4. Default Methods in Interfaces**
In Java 8, interfaces can have **default methods**, which allow you to add method implementations in interfaces. This was introduced to support backward compatibility with older versions while allowing new methods to be added to interfaces without breaking existing implementations.

#### **Syntax:**
```java
public interface MyInterface {
    default void myDefaultMethod() {
        System.out.println("This is a default method");
    }
}
```

#### **Key Points**:
- **Default Methods**: You can define methods in interfaces with a body. This method is provided by default and can be overridden by the implementing class if needed.
- **Multiple Inheritance of Behavior**: Java 8 allows an interface to provide default methods, thereby allowing multiple inheritance of behavior (unlike before, where interfaces could only have abstract methods).

#### **Example**:
```java
interface Vehicle {
    default void start() {
        System.out.println("Vehicle started");
    }
}

class Car implements Vehicle {
    // Inherits the default start() method
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        car.start();  // Output: Vehicle started
    }
}
```

---

### **5. Optional Class**
The **Optional** class was introduced in Java 8 to handle the problem of `null` values in a more expressive and safer manner. It helps to avoid `NullPointerException` by representing the presence or absence of a value.

#### **Key Methods**:
- **`empty()`**: Creates an empty Optional.
- **`of(T value)`**: Creates an Optional with a non-null value.
- **`ofNullable(T value)`**: Creates an Optional that may or may not contain a value.
- **`isPresent()`**: Returns true if the value is present.
- **`ifPresent()`**: Executes the provided code if the value is present.
- **`orElse()`**: Returns the value if present, otherwise returns a default value.
- **`orElseGet()`**: Returns the value if present, otherwise executes the provided `Supplier`.

#### **Example**:
```java
Optional<String> optional = Optional.of("Hello, Java 8!");
optional.ifPresent(s -> System.out.println(s));  // Output: Hello, Java 8!

Optional<String> emptyOptional = Optional.empty();
System.out.println(emptyOptional.orElse("No Value"));  // Output: No Value
```

---

### **6. Method References**
Method references provide a way to refer to methods directly using the `::` operator. They are shorthand for calling a method with a lambda expression.

#### **Types of Method References**:
- **Static Method Reference**: Refers to a static method.
- **Instance Method Reference**: Refers to an instance method of a specific object.
- **Constructor Reference**: Refers to a constructor.

#### **Example**:
```java
// Static method reference
List<String> names = Arrays.asList("John", "Jane", "Paul");
names.forEach(System.out::println);  // Output: John, Jane, Paul

// Instance method reference
List<String> strings = Arrays.asList("apple", "banana", "cherry");
strings.forEach(String::toUpperCase);  // Output: APPLE, BANANA, CHERRY
```

---

### **7. New Date and Time API (java.time package)**
Java 8 introduced a new `java.time` package to handle date and time, which was a much-needed improvement over the older `Date` and `Calendar` classes.

#### **Key Classes**:
- **LocalDate**: Represents a date without time (e.g., 2025-04-09).
- **LocalTime**: Represents a time without date (e.g., 14:30).
- **LocalDateTime**: Represents both date and time (e.g., 2025-04-09T14:30).
- **ZonedDateTime**: Represents a date and time with timezone (e.g., 2025-04-09T14:30+02:00).
- **Duration**: Represents the amount of time between two temporal objects.

#### **Example**:
```java
LocalDate today = LocalDate.now();
System.out.println("Today's Date: " + today);

LocalTime now = LocalTime.now();
System.out.println("Current Time: " + now);
```

---

### **8. Nashorn JavaScript Engine**
Java 8 introduced the **Nashorn** JavaScript engine, which replaced the previous Rhino engine. Nashorn allows you to embed JavaScript code inside Java applications.

#### **Example**:
```java
import javax.script.*;

public class NashornExample {
    public static void main(String[] args) throws Exception {
        ScriptEngineManager manager = new ScriptEngineManager();
        ScriptEngine engine = manager.getEngineByName("nashorn");
        engine.eval("print('Hello from Nashorn')");
    }
}
```

---

### **9. Parallel Streams**
Java 8 allows easy parallelism using **Streams**. By simply calling `.parallel()` on a stream, you can execute operations in parallel, making it easier to take advantage of multi-core processors.

#### **Example**:
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.parallelStream()
       .forEach(n -> System.out.println(n + " processed by thread: " + Thread.currentThread().getName()));
```

---

### **Conclusion**
Java 8 introduced several significant features that changed how Java developers write code. Understanding **Lambda expressions**, **Streams**, **Functional Interfaces**, **Optional**, and the **new Date/Time API** is essential for modern Java development and interviews. These features help in writing more concise, maintainable, and functional code.
