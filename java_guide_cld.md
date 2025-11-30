Complete Core Java and Advanced Java Guide
## SECTION 1: JAVA FUNDAMENTALS
### 1.1 JVM, JDK, and JRE
**Explanation:**

JVM (Java Virtual Machine): Runtime engine that executes Java bytecode. Provides platform independence by abstracting hardware/OS differences. Contains class loader, bytecode verifier, interpreter, and JIT compiler.
JRE (Java Runtime Environment): JVM + core libraries needed to run Java applications. Does not include development tools.
JDK (Java Development Kit): JRE + development tools (javac, jar, javadoc, debugger).

Relationship: JDK âŠƒ JRE âŠƒ JVM
Code Example:
```java
// Compile: javac HelloWorld.java (creates .class bytecode)
// Run: java HelloWorld (JVM executes bytecode)
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

Interview Q&A:

**Q: What is platform independence in Java?**
A: Java code compiles to bytecode (.class files) that runs on any platform with a JVM. "Write Once, Run Anywhere" (WORA). The JVM handles platform-specific execution.

**Q: What happens during java MyClass execution?**
A: 1) ClassLoader loads MyClass.class, 2) Bytecode Verifier checks for security violations, 3) JIT compiler converts hot bytecode to native machine code, 4) main() method executes.

### 1.2 Variables, Data Types, and Operators
**Explanation:**
Variables: Named memory locations storing data.

Local variables: Declared inside methods, must be initialized.
Instance variables: Declared in class, initialized to default values.
Static/Class variables: Shared across all instances.

Primitive Data Types:

Integer: byte (8-bit), short (16-bit), int (32-bit), long (64-bit)
Floating: float (32-bit), double (64-bit)
Character: char (16-bit Unicode)
Boolean: boolean (true/false)

Operators:

Arithmetic: +, -, *, /, %
Relational: ==, !=, >, <, >=, <=
Logical: &&, ||, !
Bitwise: &, |, ^, ~, <<, >>, >>>
Assignment: =, +=, -=, *=, /=
Ternary: condition ? expr1 : expr2

Code Example:
```java
public class DataTypesDemo {
    static int classVar = 100; // static variable
    int instanceVar = 50;      // instance variable
    
    public void method() {
        int localVar = 10;     // local variable (must initialize)
        
        // Primitive types
        byte b = 127;
        short s = 32000;
        int i = 2147483647;
        long l = 9223372036854775807L;
        float f = 3.14f;
        double d = 3.14159265359;
        char c = 'A';
        boolean bool = true;
        
        // Operators
        int a = 10, b = 20;
        int sum = a + b;              // Arithmetic
        boolean result = a > b;       // Relational
        int max = (a > b) ? a : b;    // Ternary
        
        // Bitwise
        int bitAnd = 5 & 3;           // 0101 & 0011 = 0001 (1)
        int leftShift = 5 << 1;       // 0101 << 1 = 1010 (10)
    }
}
```

Interview Q&A:

**Q: What's the difference between == and .equals()?**
A: == compares references (memory addresses) for objects, primitive values for primitives. .equals() compares object content. String s1="a", s2="a" â†’ s1==s2 true (string pool). String s3=new String("a") â†’ s1==s3 false, s1.equals(s3) true.

**Q: What's the default value of instance variables?**
A: Numeric types: 0, boolean: false, char: '\u0000', references: null. Local variables have no defaultâ€”must initialize explicitly.

### 1.3 Control Statements
**Explanation:**
Decision Making:

if-else
switch (traditional and enhanced from Java 12+)

Loops:

for, enhanced for (for-each)
while, do-while

Jump Statements:

break, continue, return

Code Example:
```java
public class ControlFlow {
    public static void main(String[] args) {
        // If-else
        int score = 85;
        if (score >= 90) {
            System.out.println("A");
        } else if (score >= 80) {
            System.out.println("B");
        } else {
            System.out.println("C");
        }
        
        // Traditional switch
        int day = 3;
        switch (day) {
            case 1:
                System.out.println("Monday");
                break;
            case 2:
                System.out.println("Tuesday");
                break;
            default:
                System.out.println("Other day");
        }
        
        // Enhanced switch (Java 12+, switch expression)
        String dayName = switch (day) {
            case 1 -> "Monday";
            case 2 -> "Tuesday";
            case 3 -> "Wednesday";
            default -> "Other";
        };
        
        // For loop
        for (int i = 0; i < 5; i++) {
            System.out.println(i);
        }
        
        // Enhanced for loop
        int[] numbers = {1, 2, 3, 4, 5};
        for (int num : numbers) {
            System.out.println(num);
        }
        
        // While loop
        int count = 0;
        while (count < 3) {
            System.out.println(count);
            count++;
        }
        
        // Do-while
        int x = 0;
        do {
            System.out.println(x);
            x++;
        } while (x < 3);
        
        // Break and continue
        for (int i = 0; i < 10; i++) {
            if (i == 5) break;      // Exit loop
            if (i == 3) continue;   // Skip iteration
            System.out.println(i);
        }
    }
}
```

Interview Q&A:

**Q: What's the difference between break and continue?**
A: break exits the loop entirely. continue skips the current iteration and proceeds to the next iteration.

**Q: When to use switch vs if-else?**
A: Use switch for multiple discrete values of a single variable (better performance and readability). Use if-else for complex conditions, range checks, or multiple variables.

## SECTION 2: OBJECT-ORIENTED PROGRAMMING (OOP)
### 2.1 Abstraction
**Explanation:**
Hiding implementation details and showing only essential features. Achieved through abstract classes and interfaces.
Abstract Class:

Cannot be instantiated
Can have abstract methods (no body) and concrete methods
Can have constructors, instance variables
Supports single inheritance

Code Example:
```java
// Abstract class
abstract class Animal {
    String name;
    
    // Constructor
    public Animal(String name) {
        this.name = name;
    }
    
    // Abstract method
    abstract void sound();
    
    // Concrete method
    void sleep() {
        System.out.println(name + " is sleeping");
    }
}

class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    
    @Override
    void sound() {
        System.out.println(name + " barks");
    }
}

public class AbstractionDemo {
    public static void main(String[] args) {
        Animal dog = new Dog("Buddy");
        dog.sound();  // Buddy barks
        dog.sleep();  // Buddy is sleeping
    }
}
```

Interview Q&A:

**Q: Why can't we instantiate abstract classes?**
A: Abstract classes are incompleteâ€”they contain abstract methods without implementation. Instantiation would create objects that can't fulfill their contract.

**Q: Can abstract classes have constructors?**
A: Yes. Constructors are called when subclasses are instantiated to initialize the abstract class's state.

### 2.2 Encapsulation
**Explanation:**
Bundling data (variables) and methods that operate on data into a single unit (class). Restricting direct access to object components using access modifiers.
Access Modifiers:

private: Accessible only within the class
default (no modifier): Accessible within the package
protected: Accessible within package and subclasses
public: Accessible everywhere

Code Example:
```java
public class BankAccount {
    // Private data members
    private String accountNumber;
    private double balance;
    
    // Constructor
    public BankAccount(String accountNumber, double initialBalance) {
        this.accountNumber = accountNumber;
        this.balance = initialBalance;
    }
    
    // Public getter
    public double getBalance() {
        return balance;
    }
    
    // Public setter with validation
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }
    
    // Private helper method
    private void logTransaction(String type, double amount) {
        System.out.println(type + ": " + amount);
    }
}

public class EncapsulationDemo {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("12345", 1000);
        account.deposit(500);
        System.out.println("Balance: " + account.getBalance()); // 1500
        // account.balance = 5000; // Compile error - private field
    }
}
```

Interview Q&A:

**Q: What are the benefits of encapsulation?**
A: 1) Data hidingâ€”prevents unauthorized access, 2) Flexibilityâ€”change implementation without affecting clients, 3) Maintainabilityâ€”localized changes, 4) Validationâ€”control data modification through setters.

**Q: Difference between encapsulation and abstraction?**
A: Encapsulation is about data hiding (how to achieve itâ€”access modifiers). Abstraction is about hiding complexity (what to showâ€”interfaces/abstract classes).

### 2.3 Inheritance
**Explanation:**
Mechanism where a new class (child/subclass) acquires properties and behaviors of an existing class (parent/superclass). Promotes code reuse.
Types:

Single: Class B extends Class A
Multilevel: Class C extends B extends A
Hierarchical: Classes B, C extend A
Multiple (via interfaces): Class implements Interface1, Interface2

Code Example:
```java
// Parent class
class Vehicle {
    protected String brand;
    protected int speed;
    
    public Vehicle(String brand) {
        this.brand = brand;
    }
    
    public void start() {
        System.out.println(brand + " starting");
    }
}

// Child class
class Car extends Vehicle {
    private int doors;
    
    public Car(String brand, int doors) {
        super(brand); // Call parent constructor
        this.doors = doors;
    }
    
    @Override
    public void start() {
        super.start(); // Call parent method
        System.out.println("Car with " + doors + " doors");
    }
    
    public void honk() {
        System.out.println("Beep beep!");
    }
}

public class InheritanceDemo {
    public static void main(String[] args) {
        Car car = new Car("Toyota", 4);
        car.start();  // Toyota starting \n Car with 4 doors
        car.honk();   // Beep beep!
    }
}
Method Overriding Rules:

Same method signature as parent
Return type: same or covariant (subtype)
Access modifier: same or less restrictive
Cannot override final, static, or private methods

Code Example (Multilevel Inheritance):
```java
class Animal {
    void eat() {
        System.out.println("Eating");
    }
}

class Mammal extends Animal {
    void walk() {
        System.out.println("Walking");
    }
}

class Dog extends Mammal {
    void bark() {
        System.out.println("Barking");
    }
}

public class MultilevelDemo {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();   // From Animal
        dog.walk();  // From Mammal
        dog.bark();  // From Dog
    }
}
```

Interview Q&A:

**Q: Why doesn't Java support multiple inheritance with classes?**
A: Diamond problemâ€”if classes B and C extend A, and both override a method, and D extends B and C, which method should D inherit? Java resolves this with interfaces (default methods use explicit resolution).

**Q: What's the difference between IS-A and HAS-A relationships?**
A: IS-A (inheritance): Dog IS-A Animal. HAS-A (composition): Car HAS-A Engine. Composition is preferred over inheritance for flexibility.

### 2.4 Polymorphism
**Explanation:**
Ability of objects to take multiple forms. "Many forms."
Types:

Compile-time (Static) Polymorphism: Method overloading, operator overloading
Runtime (Dynamic) Polymorphism: Method overriding

Method Overloading:
Same method name, different parameters (number, type, or order).
Method Overriding:
Subclass provides specific implementation of method declared in parent.
Code Example (Overloading):
```java
class Calculator {
    // Overloaded methods
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
    }
    
    int add(int a, int b, int c) {
        return a + b + c;
    }
    
    // Compile error: return type alone doesn't differentiate
    // double add(int a, int b) { return a + b; }
}
Code Example (Overriding - Runtime Polymorphism):
```java
class Shape {
    void draw() {
        System.out.println("Drawing shape");
    }
    
    double area() {
        return 0;
    }
}

class Circle extends Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    void draw() {
        System.out.println("Drawing circle");
    }
    
    @Override
    double area() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    private double width, height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    @Override
    void draw() {
        System.out.println("Drawing rectangle");
    }
    
    @Override
    double area() {
        return width * height;
    }
}

public class PolymorphismDemo {
    public static void main(String[] args) {
        // Runtime polymorphism
        Shape shape1 = new Circle(5);
        Shape shape2 = new Rectangle(4, 6);
        
        shape1.draw();  // Drawing circle
        shape2.draw();  // Drawing rectangle
        
        System.out.println(shape1.area()); // 78.54...
        System.out.println(shape2.area()); // 24.0
        
        // Dynamic method dispatch
        Shape[] shapes = {new Circle(3), new Rectangle(2, 3), new Circle(4)};
        for (Shape shape : shapes) {
            shape.draw();
            System.out.println("Area: " + shape.area());
        }
    }
}
```

Interview Q&A:

**Q: What is dynamic method dispatch?**
A: Runtime determination of which overridden method to call based on the actual object type, not reference type. JVM uses the object's vtable (virtual method table) to resolve the method at runtime.

**Q: Can we override static methods?**
A: No. Static methods belong to the class, not instances. Redeclaring a static method in subclass is method hiding, not overriding. No runtime polymorphism.

**Q: Difference between overloading and overriding?**
A: Overloading: same method name, different parameters, resolved at compile-time, within same class. Overriding: same signature, different implementation in subclass, resolved at runtime.

### 2.5 Interfaces
**Explanation:**
Blueprint of a class containing abstract methods and constants. Achieves 100% abstraction and multiple inheritance.
Features (Java 8+):

Abstract methods (implicitly public abstract)
Default methods (concrete methods with default keyword)
Static methods
Private methods (Java 9+)
Constants (implicitly public static final)

Code Example:
```java
interface Flyable {
    // Abstract method (implicitly public abstract)
    void fly();
    
    // Default method (Java 8+)
    default void land() {
        System.out.println("Landing safely");
    }
    
    // Static method (Java 8+)
    static void checkWeather() {
        System.out.println("Weather is clear");
    }
    
    // Private method (Java 9+)
    private void log(String message) {
        System.out.println("Log: " + message);
    }
}

interface Swimmable {
    void swim();
}

// Multiple inheritance via interfaces
class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Duck flying");
    }
    
    @Override
    public void swim() {
        System.out.println("Duck swimming");
    }
}

public class InterfaceDemo {
    public static void main(String[] args) {
        Duck duck = new Duck();
        duck.fly();           // Duck flying
        duck.swim();          // Duck swimming
        duck.land();          // Landing safely (default method)
        Flyable.checkWeather(); // Weather is clear (static method)
    }
}
Functional Interface:
Interface with exactly one abstract method (SAMâ€”Single Abstract Method). Used with lambda expressions.
java@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
    
    // Default/static methods allowed
    default void display() {
        System.out.println("Calculator");
    }
}

public class FunctionalInterfaceDemo {
    public static void main(String[] args) {
        // Lambda expression
        Calculator add = (a, b) -> a + b;
        Calculator multiply = (a, b) -> a * b;
        
        System.out.println(add.calculate(5, 3));       // 8
        System.out.println(multiply.calculate(5, 3));  // 15
    }
}
```

Interview Q&A:

**Q: Difference between abstract class and interface?**
A: Abstract class: single inheritance, can have constructors/instance variables, can have any access modifier for methods. Interface: multiple inheritance, no constructors/instance variables, methods implicitly public. Use interface for "can-do" relationships (Flyable), abstract class for "is-a" with shared implementation.

**Q: What happens if a class implements two interfaces with same default method?**
A: Compilation error. Must override the method explicitly to resolve ambiguity.
```java
interface A {
    default void show() { System.out.println("A"); }
}
interface B {
    default void show() { System.out.println("B"); }
}
class C implements A, B {
    @Override
    public void show() {
        A.super.show(); // Explicitly call A's version
        // Or provide own implementation
    }
}

```

2.6 Abstract Classes vs Interfaces
Code Example (Comparison):
```java
// Abstract class - "is-a" relationship with shared state
abstract class Employee {
    protected String name;
    protected double baseSalary;
    
    public Employee(String name, double baseSalary) {
        this.name = name;
        this.baseSalary = baseSalary;
    }
    
    // Abstract method
    abstract double calculateSalary();
    
    // Concrete method
    void displayInfo() {
        System.out.println("Name: " + name);
    }
}

// Interface - "can-do" relationship
interface Bonus {
    double calculateBonus();
}

interface TaxPayer {
    double calculateTax();
}

// Class can extend one abstract class and implement multiple interfaces
class Manager extends Employee implements Bonus, TaxPayer {
    private double bonusPercentage;
    
    public Manager(String name, double baseSalary, double bonusPercentage) {
        super(name, baseSalary);
        this.bonusPercentage = bonusPercentage;
    }
    
    @Override
    double calculateSalary() {
        return baseSalary + calculateBonus();
    }
    
    @Override
    public double calculateBonus() {
        return baseSalary * bonusPercentage;
    }
    
    @Override
    public double calculateTax() {
        return calculateSalary() * 0.3;
    }
}

public class AbstractVsInterfaceDemo {
    public static void main(String[] args) {
        Manager manager = new Manager("John", 5000, 0.2);
        manager.displayInfo();           // Name: John
        System.out.println("Salary: " + manager.calculateSalary()); // 6000
        System.out.println("Tax: " + manager.calculateTax());       // 1800
    }
}

```

SECTION 3: STRINGS, STRINGBUILDER, AND STRINGBUFFER
### 3.1 String Immutability
**Explanation:**
String objects are immutableâ€”once created, cannot be modified. Any operation creates a new String object.
Why Immutable?

Security: Strings used in sensitive operations (database connections, file paths)
Thread Safety: Immutable objects are inherently thread-safe
Caching: String pool enables memory efficiency
Hashing: Immutable hashCode ensures HashMap integrity

String Pool:
JVM maintains a pool of String literals in heap memory. When creating a String literal, JVM checks the pool first. If exists, returns reference; otherwise, creates new String and adds to pool.
Code Example:
```java
public class StringImmutabilityDemo {
    public static void main(String[] args) {
        // String literals - stored in String pool
        String s1 = "Hello";
        String s2 = "Hello";
        System.out.println(s1 == s2);  // true (same reference)
        
        // String object - heap memory
        String s3 = new String("Hello");
        System.out.println(s1 == s3);  // false (different references)
        System.out.println(s1.equals(s3)); // true (same content)
        
        // Immutability demonstration
        String original = "Java";
        String modified = original.concat(" Programming");
        System.out.println(original);  // Java (unchanged)
        System.out.println(modified);  // Java Programming (new object)
        
        // intern() method - adds to string pool
        String s4 = new String("Test").intern();
        String s5 = "Test";
        System.out.println(s4 == s5);  // true (both reference pool)
        
        // String concatenation in loop (inefficient)
        String result = "";
        for (int i = 0; i < 1000; i++) {
            result += i; // Creates 1000 String objects!
        }
    }
}
```

Interview Q&A:

**Q: Why are Strings immutable?**
A: Security (prevent modification of sensitive data), thread safety (no synchronization needed), caching (String pool), hashCode consistency (safe for HashMap keys).

**Q: What's the difference between String s = "Hello" and String s = new String("Hello")?**
A: First uses String pool (checks pool first). Second always creates new object in heap. Use literals for efficiency.

### 3.2 StringBuilder and StringBuffer
**Explanation:**
Mutable alternatives to String for efficient string manipulation.
StringBuilder:

Mutable
Not thread-safe
Faster (no synchronization overhead)
Introduced in Java 5

StringBuffer:

Mutable
Thread-safe (synchronized methods)
Slower than StringBuilder
Legacy class (Java 1.0)

When to Use:

Use String for immutable, small concatenations
Use StringBuilder for single-threaded mutable operations
Use StringBuffer for multi-threaded mutable operations

Code Example:
```java
public class StringBuilderBufferDemo {
    public static void main(String[] args) {
        // StringBuilder - not thread-safe, faster
        StringBuilder sb = new StringBuilder("Hello");
        sb.append(" World");
        sb.insert(5, ",");
        sb.replace(0, 5, "Hi");
        sb.delete(2, 3);
        sb.reverse();
        System.out.println(sb); // dlroW ,iH
        
        // Chaining methods
        StringBuilder builder = new StringBuilder()
            .append("Java")
            .append(" ")
            .append("Programming")
            .insert(4, " 17");
        System.out.println(builder); // Java 17 Programming
        
        // StringBuffer - thread-safe, slower
        StringBuffer sbf = new StringBuffer("Thread");
        sbf.append("-Safe");
        System.out.println(sbf); // Thread-Safe
        
        // Performance comparison
        long start, end;
        
        // String concatenation (slow)
        start = System.currentTimeMillis();
        String str = "";
        for (int i = 0; i < 10000; i++) {
            str += i;
        }
        end = System.currentTimeMillis();
        System.out.println("String: " + (end - start) + "ms");
        
        // StringBuilder (fast)
        start = System.currentTimeMillis();
        StringBuilder sb2 = new StringBuilder();
        for (int i = 0; i < 10000; i++) {
            sb2.append(i);
        }
        end = System.currentTimeMillis();
        System.out.println("StringBuilder: " + (end - start) + "ms");
    }
}
Common Methods:
javapublic class StringMethodsDemo {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder(50); // Initial capacity
        
        // Capacity management
        System.out.println("Capacity: " + sb.capacity()); // 50
        System.out.println("Length: " + sb.length());     // 0
        
        sb.append("Hello");
        sb.ensureCapacity(100); // Increase capacity
        
        // Methods
        sb.append(" World");     // Add to end
        sb.insert(5, ",");       // Insert at index
        sb.delete(5, 6);         // Delete range
        sb.deleteCharAt(5);      // Delete at index
        sb.replace(0, 5, "Hi");  // Replace range
        sb.reverse();            // Reverse
        
        // Extract substring
        String sub = sb.substring(0, 5);
        
        // Character access
        char ch = sb.charAt(0);
        sb.setCharAt(0, 'X');
    }
}
```

Interview Q&A:

**Q: Difference between StringBuilder and StringBuffer?**
A: StringBuilder is not thread-safe but faster. StringBuffer is thread-safe (synchronized) but slower. Use StringBuilder in single-threaded scenarios, StringBuffer in multi-threaded.

**Q: How does StringBuilder improve performance over String concatenation?**
A: String concatenation creates new objects for each operation. StringBuilder modifies the same object, avoiding object creation overhead and garbage collection pressure.

**Q: What's the default capacity of StringBuilder?**
A: 16 characters. When exceeded, capacity becomes (oldCapacity * 2) + 2.

## SECTION 4: ARRAYS, ENUMS, AND WRAPPER CLASSES
### 4.1 Arrays
**Explanation:**
Fixed-size, contiguous memory structure storing elements of the same type. Can be single or multi-dimensional.
Code Example:
```java
import java.util.Arrays;

public class ArrayDemo {
    public static void main(String[] args) {
        // Declaration and initialization
        int[] arr1 = new int[5];              // Default values (0)
        int[] arr2 = {1, 2, 3, 4, 5};         // Initialization
        int[] arr3 = new int[]{10, 20, 30};   // Anonymous array
        
        // Access and modification
        arr1[0] = 100;
        System.out.println(arr1[0]); // 100
        
        // Length
        System.out.println(arr2.length); // 5
        
        // Iteration
        for (int i = 0; i < arr2.length; i++) {
            System.out.print(arr2[i] + " ");
        }
        
        // Enhanced for loop
        for (int num : arr2) {
            System.out.print(num + " ");
        }
        
        // Multi-dimensional arrays
        int[][] matrix = {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
        };
        System.out.println(matrix[1][2]); // 6
        
        // Jagged array (irregular)
        int[][] jagged = new int[3][];
        jagged[0] = new int[]{1, 2};
        jagged[1] = new int[]{3, 4, 5};
        jagged[2] = new int[]{6};
        
        // Arrays utility class
        int[] numbers = {5, 2, 8, 1, 9};
        
        // Sort
        Arrays.sort(numbers);
        System.out.println(Arrays.toString(numbers)); // [1, 2, 5, 8, 9]
        
        // Binary search (requires sorted array)
        int index = Arrays.binarySearch(numbers, 5);
        System.out.println("Index of 5: " + index); // 2
        
        // Fill
        int[] filled = new int[5];
        Arrays.fill(filled, 10);
        System.out.println(Arrays.toString(filled)); // [10, 10, 10, 10, 10]
        
        // Copy
        int[] copy = Arrays.copyOf(numbers, 7); // Extend length
        System.out.println(Arrays.toString(copy)); // [1, 2, 5, 8, 9, 0, 0]
        
        int[] rangeCopy = Arrays.copyOfRange(numbers, 1, 4);
        System.out.println(Arrays.toString(rangeCopy)); // [2, 5, 8]
        
        // Equals
        int[] arr4 = {1, 2, 3};
        int[] arr5 = {1, 2, 3};
        System.out.println(arr4 == arr5);           // false (different refs)
        System.out.println(Arrays.equals(arr4, arr5)); // true (same content)
        
        // Stream operations (Java 8+)
        int sum = Arrays.stream(numbers).sum();
        double avg = Arrays.stream(numbers).average().orElse(0);
    }
}
```

Interview Q&A:

**Q: How is array stored in memory?**
A: Arrays are objects stored in heap memory. The array variable holds a reference to the first element. Elements are stored contiguously in memory.

**Q: What happens when accessing an index out of bounds?**
A: ArrayIndexOutOfBoundsException is thrown at runtime.

**Q: Can array size change after creation?**
A: No. Arrays are fixed size. Use ArrayList for dynamic sizing.

### 4.2 Enums
**Explanation:**
Special type for representing a fixed setof constants. Type-safe alternative to integer constants.
Code Example:
```java
// Simple enum
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

// Enum with fields, constructors, and methods
enum Planet {
    MERCURY(3.303e+23, 2.4397e6),
    EARTH(5.976e+24, 6.37814e6),
    MARS(6.421e+23, 3.3972e6);
    
    private final double mass;   // in kilograms
    private final double radius; // in meters
    
    // Constructor
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }
    
    // Methods
    public double getMass() { return mass; }
    public double getRadius() { return radius; }
    
    public double surfaceGravity() {
        final double G = 6.67300E-11;
        return G * mass / (radius * radius);
    }
}

// Enum with abstract method
enum Operation {
    PLUS {
        @Override
        public double apply(double x, double y) {
            return x + y;
        }
    },
    MINUS {
        @Override
        public double apply(double x, double y) {
            return x - y;
        }
    },
    MULTIPLY {
        @Override
        public double apply(double x, double y) {
            return x * y;
        }
    };
    
    public abstract double apply(double x, double y);
}

public class EnumDemo {
    public static void main(String[] args) {
        // Basic usage
        Day today = Day.MONDAY;
        System.out.println(today); // MONDAY
        
        // Switch with enum
        switch (today) {
            case MONDAY:
                System.out.println("Start of work week");
                break;
            case FRIDAY:
                System.out.println("TGIF!");
                break;
            default:
                System.out.println("Midweek");
        }
        
        // Enum methods
        System.out.println(today.name());      // MONDAY
        System.out.println(today.ordinal());   // 0 (position)
        
        // values() - returns all enum constants
        for (Day day : Day.values()) {
            System.out.println(day);
        }
        
        // valueOf() - string to enum
        Day day = Day.valueOf("TUESDAY");
        System.out.println(day); // TUESDAY
        
        // Enum with fields
        Planet earth = Planet.EARTH;
        System.out.println("Earth mass: " + earth.getMass());
        System.out.println("Earth gravity: " + earth.surfaceGravity());
        
        // Enum with abstract method
        double result = Operation.PLUS.apply(5, 3);
        System.out.println(result); // 8.0
        
        // EnumSet and EnumMap
        java.util.EnumSet<Day> weekend = java.util.EnumSet.of(Day.SATURDAY, Day.SUNDAY);
        java.util.EnumMap<Day, String> activities = new java.util.EnumMap<>(Day.class);
        activities.put(Day.MONDAY, "Work");
        activities.put(Day.SATURDAY, "Relax");
    }
}
```

Interview Q&A:

**Q: Can we extend enums?**
A: No. All enums implicitly extend java.lang.Enum and Java doesn't support multiple inheritance.

**Q: Can enums implement interfaces?**
A: Yes. Enums can implement interfaces.

**Q: Why use enums over constants?**
A: Type safety (can't assign int to Day), namespace (Day.MONDAY vs MONDAY constant), methods and fields, switch case completeness checking, can implement interfaces.

### 4.3 Wrapper Classes, Autoboxing, and Unboxing
**Explanation:**
Wrapper classes convert primitives to objects. Required for Collections (which only store objects), generics, and utility methods.
Wrapper Classes:

byte â†’ Byte
short â†’ Short
int â†’ Integer
long â†’ Long
float â†’ Float
double â†’ Double
char â†’ Character
boolean â†’ Boolean

Autoboxing: Automatic conversion of primitive to wrapper object.
Unboxing: Automatic conversion of wrapper object to primitive.
Code Example:
```java
public class WrapperDemo {
    public static void main(String[] args) {
        // Boxing (primitive to object) - manual
        Integer obj1 = Integer.valueOf(10);
        
        // Autoboxing (automatic)
        Integer obj2 = 10; // Compiler: Integer.valueOf(10)
        
        // Unboxing (object to primitive) - manual
        int num1 = obj1.intValue();
        
        // Auto-unboxing (automatic)
        int num2 = obj2; // Compiler: obj2.intValue()
        
        // Usage in collections
        java.util.ArrayList<Integer> list = new java.util.ArrayList<>();
        list.add(10);    // Autoboxing
        int value = list.get(0); // Auto-unboxing
        
        // Wrapper utility methods
        // Parsing
        int parsed = Integer.parseInt("123");
        double d = Double.parseDouble("3.14");
        
        // Conversion
        String str = Integer.toString(100);
        String binary = Integer.toBinaryString(10); // "1010"
        String hex = Integer.toHexString(255);      // "ff"
        
        // Comparison
        Integer a = 100, b = 200;
        System.out.println(Integer.compare(a, b)); // -1 (a < b)
        
        // Min/Max values
        System.out.println(Integer.MAX_VALUE); // 2147483647
        System.out.println(Integer.MIN_VALUE); // -2147483648
        
        // Caching demonstration
        Integer x1 = 127;
        Integer x2 = 127;
        System.out.println(x1 == x2); // true (cached)
        
        Integer y1 = 128;
        Integer y2 = 128;
        System.out.println(y1 == y2); // false (not cached)
        System.out.println(y1.equals(y2)); // true (value comparison)
        
        // valueOf vs constructor
        Integer i1 = Integer.valueOf(10);   // Uses cache
        Integer i2 = new Integer(10);        // Always new object (deprecated)
        
        // NullPointerException risk with auto-unboxing
        Integer nullInt = null;
        // int primitive = nullInt; // NullPointerException!
        
        // Character wrapper
        Character ch = 'A';
        System.out.println(Character.isDigit(ch));      // false
        System.out.println(Character.isLetter(ch));     // true
        System.out.println(Character.toUpperCase('a')); // A
        System.out.println(Character.toLowerCase('B')); // b
    }
}
```

**Caching:**
Java caches wrapper objects for:
- Integer, Short, Byte, Character: -128 to 127
- Boolean: true, false

**Interview Q&A:**


**Q: What's the output of: Integer a = 1000; Integer b = 1000; System.out.println(a == b);?**
A: false. Values outside -128 to 127 aren't cached, so new objects are created. Use .equals() for value comparison.


**Q: Why can't Collections store primitives?**
A: Collections are designed for objects (references). Primitives aren't objects. Generics (e.g., List<T>) require reference types due to type erasure.


**Q: Performance cost of autoboxing?**
A: Object creation overhead and memory consumption. In tight loops, use primitives to avoid unnecessary boxing/unboxing.

---

## SECTION 5: COLLECTIONS FRAMEWORK

### 5.1 Overview

**Explanation:**
Unified architecture for storing and manipulating groups of objects. Provides interfaces (contracts), implementations (classes), and algorithms (methods).

**Core Interfaces Hierarchy:**
```
Collection (interface)
â”œâ”€â”€ List (ordered, allows duplicates)
â”‚   â”œâ”€â”€ ArrayList
â”‚   â”œâ”€â”€ LinkedList
â”‚   â””â”€â”€ Vector (legacy, synchronized)
â”œâ”€â”€ Set (no duplicates)
â”‚   â”œâ”€â”€ HashSet
â”‚   â”œâ”€â”€ LinkedHashSet
â”‚   â””â”€â”€ TreeSet (sorted)
â””â”€â”€ Queue (FIFO)
    â”œâ”€â”€ PriorityQueue
    â””â”€â”€ Deque (double-ended queue)
        â””â”€â”€ ArrayDeque

Map (key-value pairs, not in Collection hierarchy)
â”œâ”€â”€ HashMap
â”œâ”€â”€ LinkedHashMap
â”œâ”€â”€ TreeMap (sorted by keys)
â””â”€â”€ Hashtable (legacy, synchronized)
Code Example (Overview):
```java
import java.util.*;

public class CollectionsOverview {
    public static void main(String[] args) {
        // List - ordered, duplicates allowed
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Apple"); // Duplicate allowed
        System.out.println(list); // [Apple, Banana, Apple]
        
        // Set - no duplicates
        Set<String> set = new HashSet<>();
        set.add("Apple");
        set.add("Banana");
        set.add("Apple"); // Duplicate ignored
        System.out.println(set); // [Apple, Banana] (unordered)
        
        // Queue - FIFO
        Queue<String> queue = new LinkedList<>();
        queue.offer("First");
        queue.offer("Second");
        System.out.println(queue.poll()); // First (remove and return)
        
        // Map - key-value pairs
        Map<String, Integer> map = new HashMap<>();
        map.put("Apple", 10);
        map.put("Banana", 20);
        System.out.println(map.get("Apple")); // 10
    }
}

```

5.2 List Interface
**Explanation:**
Ordered collection that allows duplicates. Elements accessible by index.
Implementations:

ArrayList: Resizable array, fast random access, slow insertion/deletion in middle
LinkedList: Doubly-linked list, fast insertion/deletion, slow random access
Vector: Legacy, synchronized, similar to ArrayList

Code Example:
```java
import java.util.*;

public class ListDemo {
    public static void main(String[] args) {
        // ArrayList
        List<String> arrayList = new ArrayList<>();
        arrayList.add("Java");
        arrayList.add("Python");
        arrayList.add("C++");
        arrayList.add(1, "JavaScript"); // Insert at index
        System.out.println(arrayList); // [Java, JavaScript, Python, C++]
        
        // Access by index
        System.out.println(arrayList.get(0)); // Java
        
        // Modify
        arrayList.set(0, "Kotlin");
        
        // Remove
        arrayList.remove(1);              // Remove by index
        arrayList.remove("Python");       // Remove by object
        
        // Search
        int index = arrayList.indexOf("C++");
        boolean contains = arrayList.contains("Java");
        
        // Size
        System.out.println(arrayList.size());
        
        // Iteration
        for (String lang : arrayList) {
            System.out.println(lang);
        }
        
        // Iterator
        Iterator<String> it = arrayList.iterator();
        while (it.hasNext()) {
            System.out.println(it.next());
        }
        
        // ListIterator (bidirectional)
        ListIterator<String> listIt = arrayList.listIterator();
        while (listIt.hasNext()) {
            System.out.println(listIt.next());
        }
        while (listIt.hasPrevious()) {
            System.out.println(listIt.previous());
        }
        
        // Sublist
        List<String> sublist = arrayList.subList(0, 2);
        
        // LinkedList specific methods
        LinkedList<String> linkedList = new LinkedList<>();
        linkedList.addFirst("First");
        linkedList.addLast("Last");
        linkedList.removeFirst();
        linkedList.removeLast();
        System.out.println(linkedList.getFirst());
        System.out.println(linkedList.getLast());
        
        // Sorting
        List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 9);
        Collections.sort(numbers);
        System.out.println(numbers); // [1, 2, 5, 8, 9]
        
        // Custom sorting with Comparator
        Collections.sort(numbers, Collections.reverseOrder());
        System.out.println(numbers); // [9, 8, 5, 2, 1]
        
        // Java 8+ List.sort()
        numbers.sort(Comparator.naturalOrder());
    }
}
```

Interview Q&A:

**Q: ArrayList vs LinkedList?**
A: ArrayList: backed by array, O(1) random access, O(n) insertion/deletion in middle, better for read-heavy. LinkedList: doubly-linked nodes, O(n) random access, O(1) insertion/deletion at ends, better for frequent modifications.

**Q: When does ArrayList resize?**
A: When size exceeds capacity. New capacity = (oldCapacity * 3/2) + 1. Resizing involves creating new array and copying elements (expensive operation).

**Q: Is ArrayList thread-safe?**
A: No. Use Collections.synchronizedList() or CopyOnWriteArrayList for thread safety.

### 5.3 Set Interface
**Explanation:**
Collection that doesn't allow duplicates. No index-based access.
Implementations:

HashSet: Backed by HashMap, O(1) operations, unordered
LinkedHashSet: Maintains insertion order, slightly slower than HashSet
TreeSet: Sorted (natural or custom), O(log n) operations, backed by TreeMap

Code Example:
```java
import java.util.*;

public class SetDemo {
    public static void main(String[] args) {
        // HashSet - unordered, no duplicates
        Set<String> hashSet = new HashSet<>();
        hashSet.add("Apple");
        hashSet.add("Banana");
        hashSet.add("Cherry");
        hashSet.add("Apple"); // Duplicate ignored
        System.out.println(hashSet); // [Apple, Cherry, Banana] (unordered)
        
        // LinkedHashSet - maintains insertion order
        Set<String> linkedHashSet = new LinkedHashSet<>();
        linkedHashSet.add("Apple");
        linkedHashSet.add("Banana");
        linkedHashSet.add("Cherry");
        System.out.println(linkedHashSet); // [Apple, Banana, Cherry]
        
        // TreeSet - sorted order
        Set<String> treeSet = new TreeSet<>();
        treeSet.add("Banana");
        treeSet.add("Apple");
        treeSet.add("Cherry");
        System.out.println(treeSet); // [Apple, Banana, Cherry]
        
        // TreeSet with custom comparator
        Set<String> reverseSet = new TreeSet<>(Collections.reverseOrder());
        reverseSet.add("Banana");
        reverseSet.add("Apple");
        System.out.println(reverseSet); // [Banana, Apple]
        
        // Set operations
        Set<Integer> set1 = new HashSet<>(Arrays.asList(1, 2, 3, 4));
        Set<Integer> set2 = new HashSet<>(Arrays.asList(3, 4, 5, 6));
        
        // Union
        Set<Integer> union = new HashSet<>(set1);
        union.addAll(set2);
        System.out.println("Union: " + union); // [1, 2, 3, 4, 5, 6]
        
        // Intersection
        Set<Integer> intersection = new HashSet<>(set1);
        intersection.retainAll(set2);
        System.out.println("Intersection: " + intersection); // [3, 4]
        
        // Difference
        Set<Integer> difference = new HashSet<>(set1);
        difference.removeAll(set2);
        System.out.println("Difference: " + difference); // [1, 2]
        
        // TreeSet specific methods
        TreeSet<Integer> numbers = new TreeSet<>(Arrays.asList(5, 2, 8, 1, 9));
        System.out.println(numbers.first());     // 1
        System.out.println(numbers.last());      // 9
        System.out.println(numbers.headSet(5));  // [1, 2] (< 5)
        System.out.println(numbers.tailSet(5));  // [5, 8, 9] (>= 5)
        System.out.println(numbers.subSet(2, 8)); // [2, 5] (>= 2 and < 8)
    }
}
```

Interview Q&A:

**Q: How does HashSet ensure uniqueness?**
A: Uses HashMap internally. Element stored as key (value is dummy PRESENT object). HashMap doesn't allow duplicate keys. Relies on hashCode() and equals().

**Q: Why is TreeSet slower than HashSet?**
A: TreeSet maintains sorted order using Red-Black tree (self-balancing BST), requiring O(log n) for operations vs O(1) for HashSet.

**Q: What happens if we add null to TreeSet?**
A: NullPointerException (unless custom comparator handles null). HashSet allows one null element.

### 5.4 Map Interface
**Explanation:**
Key-value pairs. No duplicate keys.
Implementations:

HashMap: Unordered, O(1) operations, allows one null key
LinkedHashMap: Maintains insertion order
TreeMap: Sorted by keys, O(log n) operations
Hashtable: Legacy, synchronized, no null keys/values

Code Example:
```java
import java.util.*;

public class MapDemo {
    public static void main(String[] args) {
        // HashMap
        Map<String, Integer> hashMap = new HashMap<>();
        hashMap.put("Apple", 10);
        hashMap.put("Banana", 20);
        hashMap.put("Cherry", 30);
        hashMap.put("Apple", 15); // Updates value
        System.out.println(hashMap); // {Apple=15, Cherry=30, Banana=20}
        
        // Access
        System.out.println(hashMap.get("Apple")); // 15
        System.out.println(hashMap.getOrDefault("Orange", 0)); // 0
        
        // Check existence
        System.out.println(hashMap.containsKey("Apple"));   // true
        System.out.println(hashMap.containsValue(20));      // true
        
        // Remove
        hashMap.remove("Banana");
        
        // Size
        System.out.println(hashMap.size());
        
        // Iteration methods
        // 1. Key set
        for (String key : hashMap.keySet()) {
            System.out.println(key + ": " + hashMap.get(key));
        }
        
        // 2. Values
        for (Integer value : hashMap.values()) {
            System.out.println(value);
        }
        
        // 3. Entry set (most efficient)
        for (Map.Entry<String, Integer> entry : hashMap.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
        
        // Java 8+ forEach
        hashMap.forEach((key, value) -> 
            System.out.println(key + ": " + value));
        
        // Java 8+ methods
        hashMap.putIfAbsent("Date", 40);
        hashMap.compute("Apple", (k, v) -> v + 5);
        hashMap.merge("Apple", 10, Integer::sum);
        
        // LinkedHashMap - maintains insertion order
        Map<String, Integer> linkedHashMap = new LinkedHashMap<>();
        linkedHashMap.put("C", 3);
        linkedHashMap.put("A", 1);
        linkedHashMap.put("B", 2);
        System.out.println(linkedHashMap); // {C=3, A=1, B=2}
        
        // TreeMap - sorted by keys
        Map<String, Integer> treeMap = new TreeMap<>();
        treeMap.put("C", 3);
        treeMap.put("A", 1);
        treeMap.put("B", 2);
        System.out.println(treeMap); // {A=1, B=2, C=3}
        
        // TreeMap specific methods
        TreeMap<String, Integer> sortedMap = new TreeMap<>(treeMap);
        System.out.println(sortedMap.firstKey());      // A
        System.out.println(sortedMap.lastKey());       // C
        System.out.println(sortedMap.headMap("B"));    // {A=1}
        System.out.println(sortedMap.tailMap("B"));    // {B=2, C=3}
        System.out.println(sortedMap.subMap("A", "C")); // {A=1, B=2}
    }
}
```

Interview Q&A:

**Q: How does HashMap work internally?**
A: Uses array of Node objects (buckets). Key's hashCode() determines bucket index. If collision, uses linked list (Java 8+: converts to balanced tree after 8 elements). get/put: O(1) average, O(n) worst case.

**Q: What's the default capacity and load factor?**
A: Capacity: 16, Load factor: 0.75. When size > capacity * load factor, rehashing occurs (capacity doubles).

**Q: HashMap vs Hashtable?**
A: HashMap: not synchronized, allows null key/values, faster. Hashtable: synchronized, no nulls, legacy. Use ConcurrentHashMap for thread-safe alternative.

### 5.5 Queue and Deque
**Explanation:**
Queue: FIFO (First-In-First-Out) structure.
Deque (Double-Ended Queue): Insert/remove from both ends.
Code Example:
```java
import java.util.*;

public class QueueDequeDemo {
    public static void main(String[] args) {
        // Queue - FIFO
        Queue<String> queue = new LinkedList<>();
        queue.offer("First");   // Add to tail (returns boolean)
        queue.offer("Second");
        queue.offer("Third");
        
        System.out.println(queue.peek());   // First (doesn't remove)
        System.out.println(queue.poll());   // First (removes and returns)
        System.out.println(queue);          // [Second, Third]
        
        // PriorityQueue - natural ordering or comparator
        Queue<Integer> priorityQueue = new PriorityQueue<>();
        priorityQueue.offer(5);
        priorityQueue.offer(1);
        priorityQueue.offer(3);
        System.out.println(priorityQueue.poll()); // 1 (min heap)
        System.out.println(priorityQueue.poll()); // 3
        
        // PriorityQueue with custom comparator (max heap)
        Queue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
        maxHeap.offer(5);
        maxHeap.offer(1);
        maxHeap.offer(3);
        System.out.println(maxHeap.poll()); // 5
        
        // Deque - double-ended queue
        Deque<String> deque = new ArrayDeque<>();
        
        // Add to both ends
        deque.offerFirst("First");
        deque.offerLast("Last");
        deque.offerFirst("New First");
        System.out.println(deque); // [New First, First, Last]
        
        // Remove from both ends
        System.out.println(deque.pollFirst()); // New First
        System.out.println(deque.pollLast());  // Last
        
        // Peek both ends
        System.out.println(deque.peekFirst());
        System.out.println(deque.peekLast());
        
        // Use Deque as Stack (LIFO)
        Deque<Integer> stack = new ArrayDeque<>();
        stack.push(1);    // Add to front
        stack.push(2);
        stack.push(3);
        System.out.println(stack.pop()); // 3 (remove from front)
        System.out.println(stack.peek()); // 2
    }
}
```

Interview Q&A:

**Q: Difference between offer() and add() in Queue?**
A: offer() returns false if element can't be added (capacity-constrained queue). add() throws IllegalStateException. Prefer offer() for bounded queues.

**Q: Why use ArrayDeque over Stack?**
A: Stack is legacy and synchronized (slower). ArrayDeque is faster, more efficient, and implements Deque interface with richer API.

**Q: How does PriorityQueue maintain order?**
A: Uses min-heap (binary heap) structure. Root is always minimum element (or maximum with reverse comparator). O(log n) insertion/removal.

### 5.6 Collection Internals: HashMap
**Explanation:**
HashMap uses array + linked list + balanced tree (Java 8+).
Internal Structure:

Array of Node objects (buckets)
Each Node contains: key, value, hash, next reference
Collision handling: linked list â†’ balanced tree (threshold: 8 elements)

Operations:

put(key, value):

Calculate hash: hash = key.hashCode() ^ (hash >>> 16) (reduce collisions)
Find bucket: index = hash & (capacity - 1) (bitwise AND with capacity-1)
If empty, create node
If collision, traverse list/tree, update if key exists, else add new node
If size > threshold, resize (double capacity)


get(key):

Calculate hash and bucket index
Compare keys using equals()
Return value if found, else null



Code Example:
```java
import java.util.*;

public class HashMapInternals {
    public static void main(String[] args) {
        // HashMap with initial capacity and load factor
        Map<String, Integer> map = new HashMap<>(16, 0.75f);
        
        // Demonstrating collision
        // Keys with same hashCode will collide
        map.put("FB", 1);  // hashCode: 2236
        map.put("Ea", 2);  // hashCode: 2236 (collision!)
        
        System.out.println(map);
        
        // HashMap statistics
        System.out.println("Size: " + map.size());
        
        // Custom hashCode demonstration
        class Person {
            String name;
            int age;
            
            public Person(String name, int age) {
                this.name = name;
                this.age = age;
            }
            
            @Override
            public int hashCode() {
                return Objects.hash(name, age);
            }
            
            @Override
            public boolean equals(Object obj) {
                if (this == obj) return true;
                if (obj == null || getClass() != obj.getClass()) return false;
                Person person = (Person) obj;
                return age == person.age && Objects.equals(name, person.name);
            }
        }
        
        Map<Person, String> personMap = new HashMap<>();
        Person p1 = new Person("John", 30);
        Person p2 = new Person("John", 30); // Equal to p1
        
        personMap.put(p1, "Engineer");
        System.out.println(personMap.get(p2)); // Engineer (equals works)
        
        // Resize demonstration
        Map<Integer, String> resizeMap = new HashMap<>(2);
        for (int i = 0; i < 20; i++) {
            resizeMap.put(i, "Value" + i);
            // Resize happens at size > capacity * 0.75
        }
    }
}
```

Interview Q&A:

**Q: Why is capacity always a power of 2?**
A: Allows fast modulo operation using bitwise AND: hash & (capacity - 1) instead of hash % capacity. For capacity=16, capacity-1=15 (binary: 1111), AND operation masks high-order bits.

**Q: What happens if hashCode() returns constant?**
A: All entries go into same bucket, degrading to O(n) linked list/tree traversal. HashMap becomes inefficient.

**Q: When does linked list convert to tree in HashMap?**
A: When bucket size exceeds TREEIFY_THRESHOLD (8) and capacity >= MIN_TREEIFY_CAPACITY (64). Converts to balanced tree for O(log n) operations.

### 5.7 Collection Internals: ConcurrentHashMap
**Explanation:**
Thread-safe alternative to HashMap. Uses segmentation (Java 7) or CAS operations + synchronized blocks (Java 8+).
Java 8+ Implementation:

Array of Node[] (similar to HashMap)
Fine-grained locking: locks only specific bucket during write
Read operations don't require locks (using volatile)
Uses CAS (Compare-And-Swap) for atomic operations

Code Example:
```java
import java.util.concurrent.*;

public class ConcurrentHashMapDemo {
    public static void main(String[] args) throws InterruptedException {
        ConcurrentHashMap<String, Integer> concurrentMap = new ConcurrentHashMap<>();
        
        // Thread-safe operations
        concurrentMap.put("A", 1);
        concurrentMap.put("B", 2);
        
        // Atomic operations
        concurrentMap.putIfAbsent("C", 3);
        concurrentMap.computeIfAbsent("D", k -> 4);
        concurrentMap.computeIfPresent("A", (k, v) -> v + 10);
        concurrentMap.merge("B", 5, Integer::sum);
        
        System.out.println(concurrentMap); // {A=11, B=7, C=3, D=4}
        
        // Multi-threaded usage
        ConcurrentHashMap<Integer, Integer> map = new ConcurrentHashMap<>();
        
        // Multiple threads writing concurrently
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                map.put(i, i);
            }
        });
        
        Thread t2 = new Thread(() -> {
            for (int i = 1000; i < 2000; i++) {
                map.put(i, i);
            }
        });
        
        t1.start();
        t2.start();
        t1.join();
        t2.join();
        
        System.out.println("Size: " + map.size()); // 2000 (thread-safe)
        
        // Bulk operations (Java 8+)
        concurrentMap.forEach((k, v) -> System.out.println(k + ":" + v));
        
        // Search
        String result = concurrentMap.search(1, (k, v) -> v > 5 ? k : null);
        System.out.println("Found: " + result);
        
        // Reduce
        Integer sum = concurrentMap.reduce(1, 
            (k, v) -> v, 
            (v1, v2) -> v1 + v2);
        System.out.println("Sum: " + sum);
    }
}
```

Interview Q&A:

**Q: ConcurrentHashMap vs Hashtable?**
A: ConcurrentHashMap: fine-grained locking (bucket-level), better concurrency, no null keys/values. Hashtable: coarse-grained locking (entire map), poor concurrency, legacy.

**Q: ConcurrentHashMap vs Collections.synchronizedMap()?**
A: ConcurrentHashMap: better performance (fine-grained locking), atomic operations. synchronizedMap: locks entire map for each operation, poor performance under contention.

**Q: Is ConcurrentHashMap iteration thread-safe?**
A: Weakly consistent. Iterator doesn't throw ConcurrentModificationException but may not reflect latest updates made during iteration.

### 5.8 ArrayList vs LinkedList
Code Example (Performance Comparison):
Code Example (Performance Comparison):
```java
import java.util.*;

public class ArrayListVsLinkedList {
    public static void main(String[] args) {
        int size = 100000;
        
        // ArrayList performance
        List<Integer> arrayList = new ArrayList<>();
        
        // Add to end - O(1) amortized
        long start = System.nanoTime();
        for (int i = 0; i < size; i++) {
            arrayList.add(i);
        }
        long end = System.nanoTime();
        System.out.println("ArrayList add to end: " + (end - start) / 1000000 + "ms");
        
        // Add to beginning - O(n) (shift all elements)
        start = System.nanoTime();
        for (int i = 0; i < 1000; i++) {
            arrayList.add(0, i);
        }
        end = System.nanoTime();
        System.out.println("ArrayList add to beginning: " + (end - start) / 1000000 + "ms");
        
        // Random access - O(1)
        start = System.nanoTime();
        for (int i = 0; i < 10000; i++) {
            arrayList.get(i);
        }
        end = System.nanoTime();
        System.out.println("ArrayList random access: " + (end - start) / 1000000 + "ms");
        
        // LinkedList performance
        List<Integer> linkedList = new LinkedList<>();
        
        // Add to end - O(1)
        start = System.nanoTime();
        for (int i = 0; i < size; i++) {
            linkedList.add(i);
        }
        end = System.nanoTime();
        System.out.println("\nLinkedList add to end: " + (end - start) / 1000000 + "ms");
        
        // Add to beginning - O(1)
        start = System.nanoTime();
        for (int i = 0; i < 1000; i++) {
            linkedList.add(0, i);
        }
        end = System.nanoTime();
        System.out.println("LinkedList add to beginning: " + (end - start) / 1000000 + "ms");
        
        // Random access - O(n) (traverse from head/tail)
        start = System.nanoTime();
        for (int i = 0; i < 10000; i++) {
            linkedList.get(i);
        }
        end = System.nanoTime();
        System.out.println("LinkedList random access: " + (end - start) / 1000000 + "ms");
        
        // Memory comparison
        System.out.println("\nMemory overhead:");
        System.out.println("ArrayList: stores only elements + small overhead for capacity");
        System.out.println("LinkedList: stores element + 2 references (next/prev) per node");
    }
}
Time Complexity Comparison:
OperationArrayListLinkedListget(index)O(1)O(n)add(element)O(1) amortizedO(1)add(index, element)O(n)O(n)remove(index)O(n)O(n)remove(element)O(n)O(n)contains(element)O(n)O(n)
```

Interview Q&A:

**Q: When to use ArrayList vs LinkedList?**
A: ArrayList: frequent random access, read-heavy operations, less memory overhead. LinkedList: frequent insertions/deletions at beginning/end, implementing Queue/Deque, when you iterate sequentially.

**Q: Why is ArrayList.add() O(1) amortized?**
A: Most adds are O(1), but occasionally requires resizing (creating new array, copying elements) which is O(n). Amortized over many operations, average is O(1).

### 5.9 Fail-Fast vs Fail-Safe Iterators
**Explanation:**
Fail-Fast: Immediately throws ConcurrentModificationException if collection modified during iteration (except via iterator's own remove()).
Fail-Safe: Works on clone/copy, doesn't throw exception, may not reflect current state.
Code Example:
```java
import java.util.*;
import java.util.concurrent.*;

public class FailFastFailSafeDemo {
    public static void main(String[] args) {
        // Fail-Fast Iterator (ArrayList, HashMap, HashSet)
        List<Integer> failFastList = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
        
        try {
            for (Integer num : failFastList) {
                System.out.println(num);
                if (num == 3) {
                    failFastList.remove(num); // ConcurrentModificationException!
                }
            }
        } catch (ConcurrentModificationException e) {
            System.out.println("Fail-Fast: " + e.getClass().getSimpleName());
        }
        
        // Correct way: use iterator's remove()
        List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
        Iterator<Integer> iterator = list.iterator();
        while (iterator.hasNext()) {
            Integer num = iterator.next();
            if (num == 3) {
                iterator.remove(); // Safe removal
            }
        }
        System.out.println("After safe removal: " + list); // [1, 2, 4, 5]
        
        // Fail-Safe Iterator (ConcurrentHashMap, CopyOnWriteArrayList)
        List<Integer> failSafeList = new CopyOnWriteArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
        
        for (Integer num : failSafeList) {
            System.out.println(num);
            if (num == 3) {
                failSafeList.remove(num); // No exception, works on copy
            }
        }
        System.out.println("Fail-Safe list: " + failSafeList); // [1, 2, 4, 5]
        
        // ConcurrentHashMap - weakly consistent iterator
        ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
        map.put("A", 1);
        map.put("B", 2);
        map.put("C", 3);
        
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
            map.put("D", 4); // No exception
        }
        
        // ModCount demonstration
        List<String> modCountList = new ArrayList<>();
        modCountList.add("A");
        modCountList.add("B");
        
        // modCount incremented on structural modification
        // Iterator stores expected modCount
        // Each next() checks: if (modCount != expectedModCount) throw CME
    }
}
```

Interview Q&A:

**Q: How does fail-fast detection work?**
A: Collection maintains modCount (modification count). Iterator stores expectedModCount on creation. Each operation checks if modCount != expectedModCount, throws ConcurrentModificationException.

**Q: Why use fail-safe iterators?**
A: Thread-safe iteration without explicit synchronization. Useful in concurrent applications. Trade-off: may not reflect latest changes, higher memory overhead (copying).

**Q: Can we modify collection during iteration?**
A: Use iterator.remove() for fail-fast iterators. For fail-safe, direct modification is safe but changes may not be visible in current iteration.

## SECTION 6: GENERICS
### 6.1 Generics Basics
**Explanation:**
Provide type safety at compile-time, eliminate casting, enable writing generic algorithms.
Code Example:
```java
import java.util.*;

// Generic class
class Box<T> {
    private T item;
    
    public void set(T item) {
        this.item = item;
    }
    
    public T get() {
        return item;
    }
}

// Multiple type parameters
class Pair<K, V> {
    private K key;
    private V value;
    
    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }
    
    public K getKey() { return key; }
    public V getValue() { return value; }
}

// Generic method
class Util {
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.print(element + " ");
        }
        System.out.println();
    }
    
    // Generic method with bounded type
    public static <T extends Comparable<T>> T findMax(T[] array) {
        T max = array[0];
        for (T element : array) {
            if (element.compareTo(max) > 0) {
                max = element;
            }
        }
        return max;
    }
}

public class GenericsDemo {
    public static void main(String[] args) {
        // Type safety
        Box<String> stringBox = new Box<>();
        stringBox.set("Hello");
        String str = stringBox.get(); // No casting needed
        
        // Compile error: type safety
        // stringBox.set(123); // Error: incompatible types
        
        // Multiple type parameters
        Pair<String, Integer> pair = new Pair<>("Age", 30);
        System.out.println(pair.getKey() + ": " + pair.getValue());
        
        // Generic method
        Integer[] intArray = {1, 2, 3, 4, 5};
        String[] strArray = {"A", "B", "C"};
        Util.printArray(intArray); // 1 2 3 4 5
        Util.printArray(strArray); // A B C
        
        // Bounded type parameter
        Integer max = Util.findMax(intArray);
        System.out.println("Max: " + max); // 5
        
        // Diamond operator (Java 7+)
        List<String> list = new ArrayList<>(); // Type inference
    }
}
```

Interview Q&A:

**Q: Why use generics?**
A: 1) Type safety at compile-time, 2) Eliminate casting, 3) Enable generic algorithms, 4) Better code readability and maintainability.

**Q: Can we create generic array?**
A: No. T[] array = new T[10]; is compile error due to type erasure. Use T[] array = (T[]) new Object[10]; with unchecked warning, or use ArrayList<T>.

### 6.2 Bounded Type Parameters
**Explanation:**
Restrict types that can be used as type arguments.
Code Example:
```java
import java.util.*;

// Upper bounded type parameter
class NumberBox<T extends Number> {
    private T number;
    
    public void set(T number) {
        this.number = number;
    }
    
    public double doubleValue() {
        return number.doubleValue(); // Number method available
    }
}

// Multiple bounds
class ComparableBox<T extends Number & Comparable<T>> {
    private T value;
    
    public void set(T value) {
        this.value = value;
    }
    
    public boolean isGreaterThan(T other) {
        return value.compareTo(other) > 0;
    }
}

public class BoundedTypesDemo {
    public static void main(String[] args) {
        // Upper bounded
        NumberBox<Integer> intBox = new NumberBox<>();
        intBox.set(100);
        System.out.println(intBox.doubleValue()); // 100.0
        
        NumberBox<Double> doubleBox = new NumberBox<>();
        doubleBox.set(3.14);
        
        // Compile error: String doesn't extend Number
        // NumberBox<String> stringBox = new NumberBox<>();
        
        // Multiple bounds
        ComparableBox<Integer> box = new ComparableBox<>();
        box.set(10);
        System.out.println(box.isGreaterThan(5)); // true
        
        // Bounded method
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        System.out.println(sumOfNumbers(numbers)); // 15.0
    }
    
    // Bounded wildcard method
    public static double sumOfNumbers(List<? extends Number> list) {
        double sum = 0;
        for (Number num : list) {
            sum += num.doubleValue();
        }
        return sum;
    }
}

```

6.3 Wildcards and PECS
**Explanation:**
Wildcards:

? (unbounded wildcard): Unknown type
? extends T (upper bounded): T or any subtype
? super T (lower bounded): T or any supertype

PECS (Producer Extends, Consumer Super):

Use ? extends T when you only read (produce) from structure
Use ? super T when you only write (consume) to structure

Code Example:
```java
import java.util.*;

public class WildcardsDemo {
    public static void main(String[] args) {
        // Unbounded wildcard
        List<?> unknownList = new ArrayList<String>();
        // unknownList.add("Hello"); // Compile error: unknown type
        Object obj = unknownList.get(0); // Can only read as Object
        
        // Upper bounded wildcard (Producer Extends)
        List<Integer> intList = Arrays.asList(1, 2, 3);
        List<Double> doubleList = Arrays.asList(1.1, 2.2, 3.3);
        
        System.out.println(sum(intList));    // 6.0
        System.out.println(sum(doubleList)); // 6.6
        
        // Lower bounded wildcard (Consumer Super)
        List<Number> numbers = new ArrayList<>();
        addIntegers(numbers);
        System.out.println(numbers); // [1, 2, 3]
        
        List<Object> objects = new ArrayList<>();
        addIntegers(objects);
        System.out.println(objects); // [1, 2, 3]
        
        // PECS demonstration
        List<Integer> integers = new ArrayList<>(Arrays.asList(1, 2, 3));
        List<Number> nums = new ArrayList<>();
        copy(integers, nums); // integers is producer, nums is consumer
        System.out.println(nums); // [1, 2, 3]
    }
    
    // Producer Extends: read from source
    public static double sum(List<? extends Number> list) {
        double total = 0;
        for (Number num : list) {
            total += num.doubleValue();
        }
        return total;
    }
    
    // Consumer Super: write to destination
    public static void addIntegers(List<? super Integer> list) {
        list.add(1);
        list.add(2);
        list.add(3);
    }
    
    // PECS: copy from source (producer) to dest (consumer)
    public static <T> void copy(List<? extends T> source, List<? super T> dest) {
        for (T item : source) {
            dest.add(item);
        }
    }
    
    // Real-world example: Collections.copy()
    public static void realWorldExample() {
        List<Integer> source = Arrays.asList(1, 2, 3);
        List<Number> dest = new ArrayList<>(Arrays.asList(0, 0, 0));
        Collections.copy(dest, source);
        // Method signature: copy(List<? super T> dest, List<? extends T> src)
    }
}
```

Interview Q&A:

**Q: What is PECS principle?**
A: Producer Extends, Consumer Super. Use ? extends T when reading (producing values from collection). Use ? super T when writing (consuming/adding values to collection).

**Q: Difference between List<Object> and List<?>?**
A: List<Object> is list of Objects. List<?> is list of unknown type. Can't add elements to List<?> (except null) because type is unknown.

**Q: Why can't we add to List<? extends Number>?**
A: Type safety. List could be List<Integer> at runtime. Adding Double would violate type safety. Compiler prevents this.

### 6.4 Type Erasure
**Explanation:**
Generics are compile-time feature. JVM doesn't have type parameter information at runtime. Compiler removes (erases) type parameters, replacing with bounds or Object.
Process:

Replace type parameters with bounds (or Object if unbounded)
Insert type casts where necessary
Generate bridge methods for polymorphism

Code Example:
```java
import java.util.*;

public class TypeErasureDemo {
    // Before erasure
    public static <T> void genericMethod(T item) {
        System.out.println(item);
    }
    
    // After erasure (compiled bytecode equivalent)
    public static void genericMethodErased(Object item) {
        System.out.println(item);
    }
    
    // Before erasure with bound
    public static <T extends Comparable<T>> T findMax(T a, T b) {
        return a.compareTo(b) > 0 ? a : b;
    }
    
    // After erasure
    public static Comparable findMaxErased(Comparable a, Comparable b) {
        return a.compareTo(b) > 0 ? a : b;
    }
    
    public static void main(String[] args) {
        // Runtime type information lost
        List<String> stringList = new ArrayList<>();
        List<Integer> intList = new ArrayList<>();
        
        // Both have same runtime class
        System.out.println(stringList.getClass() == intList.getClass()); // true
        System.out.println(stringList.getClass()); // class java.util.ArrayList
        
        // Cannot check type at runtime
        // if (stringList instanceof List<String>) {} // Compile error
        if (stringList instanceof List) {} // OK
        
        // Cannot create generic array
        // List<String>[] array = new List<String>[10]; // Compile error
        List<?>[] array = new List<?>[10]; // OK
        
        // Cannot instantiate type parameter
        // T obj = new T(); // Compile error
        
        // Reflection doesn't reveal type parameters
        List<String> list = new ArrayList<>();
        System.out.println(list.getClass().getTypeParameters()[0]); // E
        // Only gets parameter name, not actual type (String)
        
        // Bridge method example
        class Node<T> {
            public T data;
            public void setData(T data) { this.data = data; }
        }
        
        class IntegerNode extends Node<Integer> {
            // After erasure, must bridge to Node.setData(Object)
            @Override
            public void setData(Integer data) { 
                super.setData(data); 
            }
            // Bridge method generated by compiler:
            // public void setData(Object data) { setData((Integer) data); }
        }
    }
}
Limitations due to Type Erasure:
javapublic class TypeErasureLimitations {
    // 1. Cannot instantiate type parameters
    // <T> T create() { return new T(); } // Error
    
    // 2. Cannot create generic array
    // <T> T[] createArray() { return new T[10]; } // Error
    
    // 3. Cannot use primitives
    // List<int> list; // Error, use List<Integer>
    
    // 4. Cannot use instanceof with parameterized types
    // if (obj instanceof List<String>) {} // Error
    
    // 5. Cannot create instances of type parameters
    class Generic<T> {
        // T instance = new T(); // Error
        
        // Workaround: pass Class<T>
        T instance;
        Generic(Class<T> clazz) throws Exception {
            instance = clazz.getDeclaredConstructor().newInstance();
        }
    }
    
    // 6. Cannot have static field of type parameter
    class Container<T> {
        // static T value; // Error: static context
    }
    
    // 7. Cannot overload methods with same erasure
    class Overload {
        void method(List<String> list) {}
        // void method(List<Integer> list) {} // Error: same erasure
    }
}
```

**Interview Q&A:**


**Q: What is type erasure?**
A: Compiler removes generic type information after compilation. Type parameters replaced with bounds (or Object). JVM doesn't have generic type information at runtime. Ensures backward compatibility with pre-Java 5 code.


**Q: Why can't we create generic array?**
A: Arrays are covariant and reified (know their element type at runtime). Generics are invariant and erased. Combining both violates type safety. Example: `Object[] arr = new String[10]; arr[0] = new Integer(1);` would compile but fail at runtime with generics.


**Q: How to get generic type at runtime?**
A: Use reflection with type tokens. Pass Class<T> to methods or use anonymous inner classes to capture type information via `getGenericSuperclass()`.

---

## SECTION 7: EXCEPTION HANDLING

### 7.1 Exception Hierarchy and Types

**Explanation:**
Exception hierarchy:
```
Throwable
â”œâ”€â”€ Error (unchecked) - serious problems, shouldn't catch
â”‚   â”œâ”€â”€ OutOfMemoryError
â”‚   â”œâ”€â”€ StackOverflowError
â”‚   â””â”€â”€ VirtualMachineError
â””â”€â”€ Exception
    â”œâ”€â”€ RuntimeException (unchecked)
    â”‚   â”œâ”€â”€ NullPointerException
    â”‚   â”œâ”€â”€ ArrayIndexOutOfBoundsException
    â”‚   â”œâ”€â”€ ArithmeticException
    â”‚   â””â”€â”€ IllegalArgumentException
    â””â”€â”€ Checked Exceptions
        â”œâ”€â”€ IOException
        â”œâ”€â”€ SQLException
        â””â”€â”€ ClassNotFoundException
Checked vs Unchecked:

Checked: Must handle (try-catch or throws). Compiler enforces. Used for recoverable conditions.
Unchecked: RuntimeException and Error. Not required to handle. Used for programming errors.

Code Example:
```java
import java.io.*;
import java.sql.*;

public class ExceptionDemo {
    // Checked exception - must declare or handle
    public static void readFile(String path) throws IOException {
        FileReader reader = new FileReader(path);
        // IOException is checked, must be declared
    }
    
    // Handling checked exception
    public static void readFileHandled(String path) {
        try {
            FileReader reader = new FileReader(path);
            BufferedReader br = new BufferedReader(reader);
            String line = br.readLine();
            br.close();
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }
    }
    
    // Unchecked exception - no declaration needed
    public static int divide(int a, int b) {
        return a / b; // May throw ArithmeticException (unchecked)
    }
    
    public static void main(String[] args) {
        // Try-catch
        try {
            int result = divide(10, 0);
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero");
        }
        
        // Multiple catch blocks
        try {
            String str = null;
            str.length(); // NullPointerException
            
            int[] arr = new int[5];
            arr[10] = 100; // ArrayIndexOutOfBoundsException
        } catch (NullPointerException e) {
            System.out.println("Null pointer: " + e.getMessage());
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array index: " + e.getMessage());
        } catch (Exception e) {
            // Generic catch - should be last
            System.out.println("General exception: " + e.getMessage());
        }
        
        // Multi-catch (Java 7+)
        try {
            // code
        } catch (IOException | SQLException e) {
            System.out.println("IO or SQL exception: " + e.getMessage());
        }
        
        // Finally block - always executes
        FileReader reader = null;
        try {
            reader = new FileReader("file.txt");
            // read file
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            // Cleanup code - always executes
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
        
        // Throw exception
        try {
            validateAge(-5);
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
    }
    
    public static void validateAge(int age) {
        if (age < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
        }
    }
}
```

Interview Q&A:

**Q: Difference between checked and unchecked exceptions?**
A: Checked: Compiler forces handling, used for recoverable conditions (IOException). Unchecked: RuntimeException/Error, not forced to handle, used for programming errors (NullPointerException).

**Q: When does finally block not execute?**
A: 1) System.exit() called, 2) JVM crashes, 3) Thread dies, 4) Infinite loop in try/catch.

**Q: Can we have try without catch?**
A: Yes. try-finally is valid. Used for cleanup without catching exceptions.

### 7.2 Custom Exceptions and Try-with-Resources
Code Example:
```java
import java.io.*;

// Custom checked exception
class InsufficientFundsException extends Exception {
    private double amount;
    
    public InsufficientFundsException(double amount) {
        super("Insufficient funds: " + amount);
        this.amount = amount;
    }
    
    public double getAmount() {
        return amount;
    }
}

// Custom unchecked exception
class InvalidAccountException extends RuntimeException {
    public InvalidAccountException(String message) {
        super(message);
    }
}

class BankAccount {
    private double balance;
    
    public BankAccount(double balance) {
        this.balance = balance;
    }
    
    public void withdraw(double amount) throws InsufficientFundsException {
        if (amount > balance) {
            throw new InsufficientFundsException(amount - balance);
        }
        balance -= amount;
    }
    
    public double getBalance() {
        return balance;
    }
}

public class CustomExceptionDemo {
    public static void main(String[] args) {
        BankAccount account = new BankAccount(1000);
        
        try {
            account.withdraw(1500);
        } catch (InsufficientFundsException e) {
            System.out.println(e.getMessage());
            System.out.println("Short by: " + e.getAmount());
        }
        
        // Try-with-resources (Java 7+)
        // Automatically closes resources implementing AutoCloseable
        try (FileReader reader = new FileReader("file.txt");
             BufferedReader br = new BufferedReader(reader)) {
            
            String line = br.readLine();
            System.out.println(line);
            
        } catch (IOException e) {
            e.printStackTrace();
        }
        // No finally needed - resources auto-closed
        
        // Multiple resources
        try (FileInputStream fis = new FileInputStream("input.txt");
             FileOutputStream fos = new FileOutputStream("output.txt")) {
            
            int data = fis.read();
            fos.write(data);
            
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // Custom AutoCloseable
        try (MyResource resource = new MyResource()) {
            resource.use();
        } catch (Exception e) {
            e.printStackTrace();
        }
        // close() called automatically
    }
}

// Custom AutoCloseable resource
class MyResource implements AutoCloseable {
    public MyResource() {
        System.out.println("Resource opened");
    }
    
    public void use() {
        System.out.println("Using resource");
    }
    
    @Override
    public void close() throws Exception {
        System.out.println("Resource closed");
    }
}
Suppressed Exceptions:
javapublic class SuppressedExceptionDemo {
    public static void main(String[] args) {
        try (ResourceWithException resource = new ResourceWithException()) {
            throw new Exception("Exception in try block");
        } catch (Exception e) {
            System.out.println("Main exception: " + e.getMessage());
            
            // Get suppressed exceptions
            Throwable[] suppressed = e.getSuppressed();
            for (Throwable t : suppressed) {
                System.out.println("Suppressed: " + t.getMessage());
            }
        }
    }
}

class ResourceWithException implements AutoCloseable {
    @Override
    public void close() throws Exception {
        throw new Exception("Exception in close()");
    }
}
```

Interview Q&A:

**Q: When to create custom exceptions?**
A: When built-in exceptions don't convey specific domain meaning, need additional fields/methods, or want to provide more context for error handling.

**Q: Checked vs unchecked for custom exceptions?**
A: Extend Exception for checked (recoverable conditions). Extend RuntimeException for unchecked (programming errors, validation failures).

**Q: How does try-with-resources work?**
A: Compiler generates finally block that calls close() on all AutoCloseable resources. Exceptions in close() are suppressed if exception occurs in try block.

## SECTION 8: MULTITHREADING AND CONCURRENCY
### 8.1 Thread Creation and Lifecycle
**Explanation:**
Thread states: NEW â†’ RUNNABLE â†’ RUNNING â†’ BLOCKED/WAITING/TIMED_WAITING â†’ TERMINATED
Code Example:
```java
// Method 1: Extend Thread class
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

// Method 2: Implement Runnable interface (preferred)
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Runnable running: " + Thread.currentThread().getName());
    }
}

// Method 3: Lambda expression (Java 8+)
public class ThreadCreationDemo {
    public static void main(String[] args) throws InterruptedException {
        // Method 1: Thread class
        MyThread thread1 = new MyThread();
        thread1.start(); // Starts new thread, calls run()
        
        // Method 2: Runnable interface
        Thread thread2 = new Thread(new MyRunnable());
        thread2.start();
        
        // Method 3: Lambda
        Thread thread3 = new Thread(() -> {
            System.out.println("Lambda thread: " + Thread.currentThread().getName());
        });
        thread3.start();
        
        // Thread methods
        System.out.println("Main thread: " + Thread.currentThread().getName());
        System.out.println("Thread priority: " + thread1.getPriority()); // 1-10
        thread1.setPriority(Thread.MAX_PRIORITY); // 10
        
        System.out.println("Thread state: " + thread1.getState());
        System.out.println("Is alive: " + thread1.isAlive());
        System.out.println("Is daemon: " + thread1.isDaemon());
        
        // Join - wait for thread to complete
        thread1.join(); // Main thread waits
        System.out.println("Thread1 completed");
        
        // Sleep - pause current thread
        Thread.sleep(1000);
        
        // Yield - hint to scheduler
        Thread.yield();
        
        // Daemon threa2 / 2d
Thread daemonThread = new Thread(() -> {
while (true) {
System.out.println("Daemon running");
try {
Thread.sleep(1000);
} catch (InterruptedException e) {
break;
}
}
});
daemonThread.setDaemon(true); // Must set before start()
daemonThread.start();
// JVM exits when only daemon threads remain
    // Thread lifecycle demonstration
    Thread lifecycleThread = new Thread(() -> {
        synchronized (ThreadCreationDemo.class) {
            try {
                ThreadCreationDemo.class.wait(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    });
    
    System.out.println("State: " + lifecycleThread.getState()); // NEW
    lifecycleThread.start();
    Thread.sleep(100);
    System.out.println("State: " + lifecycleThread.getState()); // TIMED_WAITING
    lifecycleThread.join();
    System.out.println("State: " + lifecycleThread.getState()); // TERMINATED
}
}

**Interview Q&A:**

Q: Difference between start() and run()?
A: start() creates new thread and calls run() in that thread. Calling run() directly executes in current thread (no multithreading).

Q: Why implement Runnable instead of extending Thread?
A: 1) Java doesn't support multiple inheritanceâ€”can extend other class, 2) Better separation of task from thread, 3) Can reuse same Runnable with multiple threads, 4) Can use with Executor framework.

Q: What happens if start() is called twice?
A: IllegalThreadStateException. Thread can only be started once.

---

```

### 8.2 Synchronization and Thread Safety

**Explanation:**
Synchronization prevents race conditions by allowing only one thread to access critical section at a time.

**Code Example:**
```java
// Problem: Race condition
class Counter {
    private int count = 0;
    
    public void increment() {
        count++; // Not atomic: read, increment, write
    }
    
    public int getCount() {
        return count;
    }
}

// Solution 1: Synchronized method
class SynchronizedCounter {
    private int count = 0;
    
    public synchronized void increment() {
        count++;
    }
    
    public synchronized int getCount() {
        return count;
    }
}

// Solution 2: Synchronized block
class SynchronizedBlockCounter {
    private int count = 0;
    private final Object lock = new Object();
    
    public void increment() {
        synchronized (lock) {
            count++;
        }
    }
    
    public int getCount() {
        synchronized (lock) {
            return count;
        }
    }
}

// Static synchronization
class StaticCounter {
    private static int count = 0;
    
    public static synchronized void increment() {
        count++; // Locks on class object (StaticCounter.class)
    }
}

public class SynchronizationDemo {
    public static void main(String[] args) throws InterruptedException {
        // Without synchronization - race condition
        Counter unsafeCounter = new Counter();
        
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                unsafeCounter.increment();
            }
        });
        
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                unsafeCounter.increment();
            }
        });
        
        t1.start();
        t2.start();
        t1.join();
        t2.join();
        
        System.out.println("Unsafe count: " + unsafeCounter.getCount()); // < 2000 (race condition)
        
        // With synchronization
        SynchronizedCounter safeCounter = new SynchronizedCounter();
        
        Thread t3 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                safeCounter.increment();
            }
        });
        
        Thread t4 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                safeCounter.increment();
            }
        });
        
        t3.start();
        t4.start();
        t3.join();
        t4.join();
        
        System.out.println("Safe count: " + safeCounter.getCount()); // 2000 (correct)
        
        // Reentrant synchronization
        demonstrateReentrant();
    }
    
    // Reentrant lock - thread can acquire same lock multiple times
    public static synchronized void demonstrateReentrant() {
        System.out.println("Outer method");
        innerSynchronized();
    }
    
    public static synchronized void innerSynchronized() {
        System.out.println("Inner method - same thread can acquire lock again");
    }
}
```

**Deadlock Example:**
```java
public class DeadlockDemo {
    private static final Object lock1 = new Object();
    private static final Object lock2 = new Object();
    
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            synchronized (lock1) {
                System.out.println("Thread 1: Holding lock1...");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                
                System.out.println("Thread 1: Waiting for lock2...");
                synchronized (lock2) {
                    System.out.println("Thread 1: Acquired lock2");
                }
            }
        });
        
        Thread t2 = new Thread(() -> {
            synchronized (lock2) {
                System.out.println("Thread 2: Holding lock2...");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                
                System.out.println("Thread 2: Waiting for lock1...");
                synchronized (lock1) {
                    System.out.println("Thread 2: Acquired lock1");
                }
            }
        });
        
        t1.start();
        t2.start();
        // Deadlock: t1 holds lock1, waits for lock2
        //           t2 holds lock2, waits for lock1
    }
    
    // Solution: Lock ordering
    public static void avoidDeadlock() {
        Thread t1 = new Thread(() -> {
            synchronized (lock1) {
                synchronized (lock2) {
                    System.out.println("Thread 1 completed");
                }
            }
        });
        
        Thread t2 = new Thread(() -> {
            synchronized (lock1) { // Same order
                synchronized (lock2) {
                    System.out.println("Thread 2 completed");
                }
            }
        });
        
        t1.start();
        t2.start();
    }
}
```

**Interview Q&A:**


**Q: What is monitor in Java?**
A: Every object in Java has an intrinsic lock (monitor). When thread enters synchronized block/method, it acquires monitor. Other threads trying to enter must wait.


**Q: Difference between synchronized method and block?**
A: Synchronized method locks entire method (this object). Synchronized block locks specific object, allowing finer granularity and better performance.


**Q: How to detect deadlock?**
A: Use jstack, JVisualVM, or ThreadMXBean. Programmatically: ThreadMXBean.findDeadlockedThreads().

---

### 8.3 Inter-Thread Communication

**Code Example:**
```java
// Producer-Consumer using wait() and notify()
class SharedResource {
    private int data;
    private boolean hasData = false;
    
    public synchronized void produce(int value) throws InterruptedException {
        while (hasData) {
            wait(); // Release lock and wait
        }
        
        data = value;
        hasData = true;
        System.out.println("Produced: " + value);
        notify(); // Wake up one waiting thread
    }
    
    public synchronized int consume() throws InterruptedException {
        while (!hasData) {
            wait(); // Wait for data
        }
        
        hasData = false;
        System.out.println("Consumed: " + data);
        notify(); // Notify producer
        return data;
    }
}

public class InterThreadCommunicationDemo {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();
        
        // Producer thread
        Thread producer = new Thread(() -> {
            try {
                for (int i = 1; i <= 5; i++) {
                    resource.produce(i);
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
        
        // Consumer thread
        Thread consumer = new Thread(() -> {
            try {
                for (int i = 1; i <= 5; i++) {
                    resource.consume();
                    Thread.sleep(1500);
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
        
        producer.start();
        consumer.start();
    }
}
```

**Interview Q&A:**


**Q: Difference between wait() and sleep()?**
A: wait(): releases lock, must be in synchronized block, wakes on notify/notifyAll. sleep(): doesn't release lock, can be called anywhere, wakes after time expires.


**Q: Why must wait() be in synchronized block?**
A: To avoid race condition between checking condition and waiting. Ensures atomicity of check-and-wait operation.


**Q: notify() vs notifyAll()?**
A: notify(): wakes one random waiting thread. notifyAll(): wakes all waiting threads. Use notifyAll() to avoid missed signals, especially with multiple conditions.

---

### 8.4 Locks and ReentrantLock

**Code Example:**
```java
import java.util.concurrent.locks.*;

public class ReentrantLockDemo {
    private final ReentrantLock lock = new ReentrantLock();
    private int count = 0;
    
    public void increment() {
        lock.lock(); // Acquire lock
        try {
            count++;
        } finally {
            lock.unlock(); // Always unlock in finally
        }
    }
    
    // Try lock with timeout
    public void incrementWithTimeout() {
        try {
            if (lock.tryLock(1000, java.util.concurrent.TimeUnit.MILLISECONDS)) {
                try {
                    count++;
                } finally {
                    lock.unlock();
                }
            } else {
                System.out.println("Could not acquire lock");
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
    
    // Fair lock - respects thread waiting order
    private final ReentrantLock fairLock = new ReentrantLock(true);
    
    public void fairIncrement() {
        fairLock.lock();
        try {
            count++;
        } finally {
            fairLock.unlock();
        }
    }
    
    // ReadWriteLock - multiple readers, single writer
    private final ReadWriteLock rwLock = new ReentrantReadWriteLock();
    private int value = 0;
    
    public int read() {
        rwLock.readLock().lock();
        try {
            return value;
        } finally {
            rwLock.readLock().unlock();
        }
    }
    
    public void write(int newValue) {
        rwLock.writeLock().lock();
        try {
            value = newValue;
        } finally {
            rwLock.writeLock().unlock();
        }
    }
    
    // Condition variables
    private final Condition condition = lock.newCondition();
    
    public void awaitCondition() throws InterruptedException {
        lock.lock();
        try {
            condition.await(); // Like wait()
        } finally {
            lock.unlock();
        }
    }
    
    public void signalCondition() {
        lock.lock();
        try {
            condition.signal(); // Like notify()
        } finally {
            lock.unlock();
        }
    }
    
    public static void main(String[] args) {
        ReentrantLockDemo demo = new ReentrantLockDemo();
        
        // Lock information
        System.out.println("Is locked: " + demo.lock.isLocked());
        System.out.println("Hold count: " + demo.lock.getHoldCount());
        System.out.println("Has queued threads: " + demo.lock.hasQueuedThreads());
        
        // Demonstrate reentrant
        demo.lock.lock();
        demo.lock.lock(); // Same thread can acquire multiple times
        System.out.println("Hold count: " + demo.lock.getHoldCount()); // 2
        demo.lock.unlock();
        demo.lock.unlock();
    }
}
```

**Interview Q&A:**


**Q: ReentrantLock vs synchronized?**
A: ReentrantLock: tryLock(), timed lock, interruptible lock, fairness option, multiple conditions, explicit unlock. synchronized: simpler syntax, automatic unlock, no timeout/tryLock.


**Q: When to use ReentrantLock?**
A: When need: timeout on lock acquisition, tryLock without blocking, interruptible locks, fairness, multiple conditions, or lock polling.


**Q: What is lock fairness?**
A: Fair lock respects FIFO order of waiting threads. Default unfair lock may allow thread barging (newly arriving thread acquires lock before queued threads). Fair locks prevent starvation but have lower throughput.

---

### 8.5 Volatile Keyword

**Explanation:**
Ensures visibility of changes across threads. Prevents instruction reordering. Reads/writes are atomic for long/double.

**Code Example:**
```java
public class VolatileDemo {
    // Without volatile - visibility issue
    private static boolean flag = false;
    
    // With volatile - ensures visibility
    private static volatile boolean volatileFlag = false;
    
    public static void main(String[] args) throws InterruptedException {
        // Problem without volatile
        Thread writer = new Thread(() -> {
            try {
                Thread.sleep(1000);
                flag = true; // May not be visible to reader thread
                System.out.println("Flag set to true");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
        
        Thread reader = new Thread(() -> {
            while (!flag) {
                // May loop forever if flag change not visible
            }
            System.out.println("Flag is true - exiting");
        });
        
        // Solution with volatile
        Thread volatileWriter = new Thread(() -> {
            try {
                Thread.sleep(1000);
                volatileFlag = true; // Guaranteed visible to all threads
                System.out.println("Volatile flag set to true");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
        
        Thread volatileReader = new Thread(() -> {
            while (!volatileFlag) {
                // Will exit when flag changes
            }
            System.out.println("Volatile flag is true - exiting");
        });
        
        volatileWriter.start();
        volatileReader.start();
        
        volatileWriter.join();
        volatileReader.join();
    }
}

// Singleton with double-checked locking requires volatile
class Singleton {
    private static volatile Singleton instance;
    
    private Singleton() {}
    
    public static Singleton getInstance() {
        if (instance == null) { // First check (no locking)
            synchronized (Singleton.class) {
                if (instance == null) { // Second check (with locking)
                    instance = new Singleton();
                    // Without volatile, another thread might see partially constructed object
                }
            }
        }
        return instance;
    }
}
```

**Interview Q&A:**


**Q: What does volatile guarantee?**
A: 1) Visibility: changes visible to all threads immediately, 2) Ordering: prevents instruction reordering around volatile variable, 3) Atomicity: reads/writes to volatile long/double are atomic.


**Q: volatile vs synchronized?**
A: volatile: visibility only, no atomicity for compound operations (e.g., count++), lightweight. synchronized: visibility + atomicity + mutual exclusion, heavier.


**Q: When to use volatile?**
A: When: single writer multiple readers, simple flag/status variable, no compound operations needed. Don't use for: count++, check-then-act scenarios requiring atomicity.

---

### 8.6 Atomic Classes

**Code Example:**
```java
import java.util.concurrent.atomic.*;

public class AtomicDemo {
    // AtomicInteger - thread-safe counter
    private AtomicInteger atomicCounter = new AtomicInteger(0);
    
    public void increment() {
        atomicCounter.incrementAndGet(); // Atomic operation
    }
    
    public int get() {
        return atomicCounter.get();
    }
    
    public static void main(String[] args) throws InterruptedException {
        AtomicDemo demo = new AtomicDemo();
        
        // AtomicInteger methods
        AtomicInteger atomic = new AtomicInteger(10);
        
        System.out.println(atomic.get());              // 10
        System.out.println(atomic.incrementAndGet());  // 11
        System.out.println(atomic.decrementAndGet());  // 10
        System.out.println(atomic.addAndGet(5));       // 15
        System.out.println(atomic.getAndIncrement());  // 15 (returns old value)
        
        // Compare and Set (CAS)
        boolean success = atomic.compareAndSet(16, 20);
        System.out.println("CAS success: " + success); // true
        System.out.println("Value: " + atomic.get());  // 20
        
        // AtomicLong
        AtomicLong atomicLong = new AtomicLong(100L);
        atomicLong.incrementAndGet();
        
        // AtomicBoolean
        AtomicBoolean atomicBoolean = new AtomicBoolean(false);
        atomicBoolean.set(true);
        boolean oldValue = atomicBoolean.getAndSet(false);
        
        // AtomicReference
        AtomicReference<String> atomicRef = new AtomicReference<>("Initial");
        atomicRef.set("Updated");
        atomicRef.compareAndSet("Updated", "Final");
        
        // AtomicIntegerArray
        AtomicIntegerArray atomicArray = new AtomicIntegerArray(10);
        atomicArray.set(0, 100);
        atomicArray.incrementAndGet(0);
        
        // Thread-safe counter demonstration
        Thread[] threads = new Thread[10];
        for (int i = 0; i < threads.length; i++) {
            threads[i] = new Thread(() -> {
                for (int j = 0; j < 1000; j++) {
                    demo.increment();
                }
            });
            threads[i].start();
        }
        
        for (Thread t : threads) {
            t.join();
        }
        
        System.out.println("Final count: " + demo.get()); // 10000 (correct)
        
        // Custom atomic operation
        AtomicInteger value = new AtomicInteger(10);
        value.updateAndGet(v -> v * 2); // Custom transformation
        System.out.println(value.get()); // 20
        
        value.accumulateAndGet(5, (current, update) -> current + update);
        System.out.println(value.get()); // 25
    }
}
```

**Interview Q&A:**


**Q: How do atomic classes work?**
A: Use CAS (Compare-And-Swap) operations at CPU level. Lock-free algorithm: read value, compute new value, use CAS to update only if original value unchanged. Retry if CAS fails.


**Q: Atomic classes vs synchronized?**
A: Atomic classes: lock-free, better performance under low/moderate contention, wait-free for reads. synchronized: lock-based, better under high contention, simpler for complex operations.


**Q: When to use atomic classes?**
A: Simple counters, flags, single-variable updates. Not suitable for compound operations involving multiple variables (use locks/synchronized).

---

### 8.7 Thread Pools and Executors

**Code Example:**
```java
import java.util.concurrent.*;
import java.util.*;

public class ExecutorDemo {
    public static void main(String[] args) throws Exception {
        // Fixed thread pool
        ExecutorService fixedPool = Executors.newFixedThreadPool(3);
        
        for (int i = 0; i < 10; i++) {
            final int taskId = i;
            fixedPool.submit(() -> {
                System.out.println("Task " + taskId + " by " + Thread.currentThread().getName());
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            });
        }
        
        fixedPool.shutdown(); // Initiates orderly shutdown
        fixedPool.awaitTermination(1, TimeUnit.MINUTES);
        
        // Cached thread pool - creates threads as needed
        ExecutorService cachedPool = Executors.newCachedThreadPool();
        // Reuses idle threads, creates new if needed
        
        // Single thread executor
        ExecutorService singleExecutor = Executors.newSingleThreadExecutor();
        // Guarantees sequential execution
        
        // Scheduled executor
        ScheduledExecutorService scheduledExecutor = Executors.newScheduledThreadPool(2);
        
        // Schedule with delay
        scheduledExecutor.schedule(() -> {
            System.out.println("Executed after 2 seconds");
        }, 2, TimeUnit.SECONDS);
        
        // Schedule at fixed rate
        scheduledExecutor.scheduleAtFixedRate(() -> {
            System.out.println("Repeating task");
        }, 0, 1, TimeUnit.SECONDS); // Initial delay 0, period 1 second
        
        // Schedule with fixed delay
        scheduledExecutor.scheduleWithFixedDelay(() -> {
            System.out.println("Task with delay");
        }, 0, 1, TimeUnit.SECONDS); // Delay after task completion
        
        Thread.sleep(5000);
        scheduledExecutor.shutdown();
        
        // ThreadPoolExecutor - custom configuration
        ThreadPoolExecutor customExecutor = new ThreadPoolExecutor(
            2,  // corePoolSize
            4,  // maximumPoolSize
            60, TimeUnit.SECONDS, // keepAliveTime
            new LinkedBlockingQueue<>(100), // workQueue
            Executors.defaultThreadFactory(),
            new ThreadPoolExecutor.CallerRunsPolicy() // rejectionHandler
        );
        
        // Submit tasks
        customExecutor.execute(() -> System.out.println("Task 1"));
        
        // Monitoring
        System.out.println("Active threads: " + customExecutor.getActiveCount());
        System.out.println("Pool size: " + customExecutor.getPoolSize());
        System.out.println("Queue size: " + customExecutor.getQueue().size());
        
        customExecutor.shutdown();
    }
}
```

**Rejection Policies:**
```java
public class RejectionPolicyDemo {
    public static void main(String[] args) {
        // AbortPolicy (default) - throws RejectedExecutionException
        ThreadPoolExecutor executor1 = new ThreadPoolExecutor(
            1, 1, 0L, TimeUnit.MILLISECONDS,
            new LinkedBlockingQueue<>(1),
            new ThreadPoolExecutor.AbortPolicy()
        );
        
        // CallerRunsPolicy - runs task in caller's thread
        ThreadPoolExecutor executor2 = new ThreadPoolExecutor(
            1, 1, 0L, TimeUnit.MILLISECONDS,
            new LinkedBlockingQueue<>(1),
            new ThreadPoolExecutor.CallerRunsPolicy()
        );
        
        // DiscardPolicy - silently discards task
        ThreadPoolExecutor executor3 = new ThreadPoolExecutor(
            1, 1, 0L, TimeUnit.MILLISECONDS,
            new LinkedBlockingQueue<>(1),
            new ThreadPoolExecutor.DiscardPolicy()
        );
        
        // DiscardOldestPolicy - discards oldest task in queue
        ThreadPoolExecutor executor4 = new ThreadPoolExecutor(
            1, 1, 0L, TimeUnit.MILLISECONDS,
            new LinkedBlockingQueue<>(1),
            new ThreadPoolExecutor.DiscardOldestPolicy()
        );
    }
}
```

**Interview Q&A:**


**Q: Fixed vs cached thread pool?**
A: Fixed: fixed number of threads, bounded queue, predictable resource usage. Cached: creates threads as needed, 60s timeout for idle threads, unbounded, good for many short-lived tasks.


**Q: What happens when queue is full?**
A: Rejection policy executes: AbortPolicy (exception), CallerRunsPolicy (run in caller), DiscardPolicy (ignore), DiscardOldestPolicy (remove oldest).


**Q: Core vs maximum pool size?**
A: Core: minimum threads kept alive. Maximum: max threads created. When queue full and threads < max, new thread created. When queue not full, tasks queued even if threads < core.

---

### 8.8 Callable, Future, and CompletableFuture

**Code Example:**
```java
import java.util.concurrent.*;
import java.util.*;

public class CallableFutureDemo {
    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newFixedThreadPool(3);
        
        // Callable - returns result, can throw exception
        Callable<Integer> task = () -> {
            Thread.sleep(2000);
            return 42;
        };
        
        // Future - represents result of asynchronous computation
        Future<Integer> future = executor.submit(task);
        
        System.out.println("Task submitted");
        
        // Do other work while task executes
        System.out.println("Doing other work...");
        
        // Check if done
        System.out.println("Is done: " + future.isDone());
        
        // Get result (blocks until available)
        Integer result = future.get(); // Blocks
        System.out.println("Result: " + result);
        
        // Get with timeout
        Future<String> future2 = executor.submit(() -> {
            Thread.sleep(5000);
            return "Hello";
        });
        
        try {
            String result2 = future2.get(1, TimeUnit.SECONDS); // Timeout
        } catch (TimeoutException e) {
            System.out.println("Task timed out");
            future2.cancel(true); // Cancel task
        }
        
        // invokeAll - execute multiple tasks
        List<Callable<Integer>> tasks = Arrays.asList(
            () -> { Thread.sleep(1000); return 1; },
            () -> { Thread.sleep(1000); return 2; },
            () -> { Thread.sleep(1000); return 3; }
        );
        
        List<Future<Integer>> futures = executor.invokeAll(tasks);
        for (Future<Integer> f : futures) {
            System.out.println(f.get());
        }
        
        // invokeAny - returns result of first completed task
        Integer firstResult = executor.invokeAny(tasks);
        System.out.println("First result: " + firstResult);
        
        executor.shutdown();
        
        // CompletableFuture (Java 8+)
        demonstrateCompletableFuture();
    }
    
    public static void demonstrateCompletableFuture() throws Exception {
        // Create CompletableFuture
        CompletableFuture<String> cf1 = CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            return "Hello";
        });
        
        // Chain operations
        CompletableFuture<String> cf2 = cf1.thenApply(s -> s + " World");
        
        CompletableFuture<Void> cf3 = cf2.thenAccept(s -> 
            System.out.println("Result: " + s));
        
        cf3.get(); // Wait for completion
        
        // Combine multiple futures
        CompletableFuture<Integer> future1 = CompletableFuture.supplyAsync(() -> 10);
        CompletableFuture<Integer> future2 = CompletableFuture.supplyAsync(() -> 20);
        
        CompletableFuture<Integer> combined = future1.thenCombine(future2, (a, b) -> a + b);
        System.out.println("Combined: " + combined.get()); // 30
        
        // Compose - chain dependent futures
        CompletableFuture<Integer> cf4 = CompletableFuture.supplyAsync(() -> 5)
            .thenCompose(n -> CompletableFuture.supplyAsync(() -> n * 2));
        System.out.println("Composed: " + cf4.get()); // 10
        
        // Handle exceptions
        CompletableFuture<String> cf5 = CompletableFuture.supplyAsync(() -> {
            if (true) throw new RuntimeException("Error");
            return "Success";
        }).exceptionally(ex -> "Recovered from: " + ex.getMessage());
        
        System.out.println(cf5.get());
        
        // allOf - wait for all
        CompletableFuture<Void> allOf = CompletableFuture.allOf(future1, future2);
        allOf.get(); // Waits for all to complete
        
        // anyOf - wait for any
        CompletableFuture<Object> anyOf = CompletableFuture.anyOf(future1, future2);
        System.out.println("First completed: " + anyOf.get());
        
        // Complete manually
        CompletableFuture<String> manual = new CompletableFuture<>();
        manual.complete("Manual completion");
        System.out.println(manual.get());
    }
    
    private static void sleep(long millis) {
        try {
            Thread.sleep(millis);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}
```

**Interview Q&A:**


**Q: Callable vs Runnable?**
A: Callable: returns result, can throw checked exceptions, call() method. Runnable: no return value, can't throw checked exceptions, run() method.


**Q: Future vs CompletableFuture?**
A: Future: blocking get(), limited operations, can't combine futures. CompletableFuture: non-blocking callbacks, chainable, combinable, exception handling, manual completion.


**Q: When to use CompletableFuture?**
A: Asynchronous pipelines, combining multiple async operations, non-blocking result handling, complex async workflows, better than Future's blocking get().

---

### 8.9 Java Memory Model and Happens-Before

**Explanation:**
Java Memory Model defines how threads interact through memory and what behaviors are legal in concurrent execution.

**Happens-Before Rules:**
1. **Program order**: Each action happens-before every subsequent action in same thread
2. **Monitor lock**: Unlock happens-before every subsequent lock on same monitor
3. **Volatile**: Write to volatile happens-before every subsequent read of that volatile
4. **Thread start**: Thread.start() happens-before any action in started thread
5. **Thread termination**: Action in thread happens-before any thread detects that thread has terminated (join)
6. **Transitivity**: If A happens-before B, and B happens-before C, then A happens-before C

**Code Example:**
```java
public class HappensBeforeDemo {
    private int normalVariable = 0;
    private volatile int volatileVariable = 0;
    
    // Problem: without synchronization
    public void unsafeWrite() {
        normalVariable = 42; // May not be visible to other threads
    }
    
    public int unsafeRead() {
        return normalVariable; // May see stale value
    }
    
    // Solution 1: volatile (happens-before guarantee)
    public void volatileWrite() {
        volatileVariable = 42; // Happens-before any subsequent read
    }
    
    public int volatileRead() {
        return volatileVariable; // Sees latest write
    }
    
    // Solution 2: synchronized (happens-before via monitor lock)
    private final2 / 2Object lock = new Object();
public void synchronizedWrite() {
    synchronized (lock) {
        normalVariable = 42;
    } // Unlock happens-before any subsequent lock
}

public int synchronizedRead() {
    synchronized (lock) { // Lock happens-after unlock above
        return normalVariable; // Sees write from synchronizedWrite
    }
}

// Thread start happens-before
public static void demonstrateThreadStart() {
    int[] sharedArray = new int[1];
    sharedArray[0] = 42;
    
    Thread t = new Thread(() -> {
        // This sees sharedArray[0] = 42 because thread start happens-before
        System.out.println(sharedArray[0]);
    });
    
    t.start(); // Happens-before any action in thread t
}

// Thread termination happens-before join
public static void demonstrateJoin() throws InterruptedException {
    int[] result = new int[1];
    
    Thread t = new Thread(() -> {
        result[0] = 42;
    });
    
    t.start();
    t.join(); // Actions in t happen-before join() returns
    
    System.out.println(result[0]); // Guaranteed to see 42
}

public static void main(String[] args) throws InterruptedException {
    demonstrateThreadStart();
    demonstrateJoin();
}
}

**Interview Q&A:**


**Q: What is happens-before relationship?**
A: Guarantee that memory writes by one specific statement are visible to another specific statement. If A happens-before B, A's effects are visible to B.


**Q: How does volatile ensure visibility?**
A: Volatile write happens-before every subsequent volatile read. Prevents caching in CPU registers, forces read/write from main memory. Establishes happens-before relationship.


**Q: Why is happens-before important?**
A: Without happens-before guarantees, compiler and CPU can reorder operations for optimization, causing visibility and ordering issues in multithreaded code.

---

### 8.10 Concurrency Utilities

**Code Example:**
```java
import java.util.concurrent.*;

public class ConcurrencyUtilitiesDemo {
    public static void main(String[] args) throws Exception {
        // CountDownLatch - wait for N operations to complete
        CountDownLatch latch = new CountDownLatch(3);
        
        for (int i = 0; i < 3; i++) {
            final int id = i;
            new Thread(() -> {
                System.out.println("Task " + id + " starting");
                sleep(1000);
                System.out.println("Task " + id + " done");
                latch.countDown(); // Decrement count
            }).start();
        }
        
        latch.await(); // Wait until count reaches 0
        System.out.println("All tasks completed");
        
        // CyclicBarrier - threads wait for each other at barrier
        CyclicBarrier barrier = new CyclicBarrier(3, () -> {
            System.out.println("All threads reached barrier");
        });
        
        for (int i = 0; i < 3; i++) {
            final int id = i;
            new Thread(() -> {
                try {
                    System.out.println("Thread " + id + " doing work");
                    sleep(id * 1000);
                    System.out.println("Thread " + id + " waiting at barrier");
                    barrier.await(); // Wait for others
                    System.out.println("Thread " + id + " proceeding");
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }).start();
        }
        
        // Semaphore - limit concurrent access
        Semaphore semaphore = new Semaphore(2); // Only 2 permits
        
        for (int i = 0; i < 5; i++) {
            final int id = i;
            new Thread(() -> {
                try {
                    semaphore.acquire(); // Acquire permit
                    System.out.println("Thread " + id + " acquired permit");
                    sleep(2000);
                    System.out.println("Thread " + id + " releasing permit");
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } finally {
                    semaphore.release(); // Release permit
                }
            }).start();
        }
        
        // Phaser - flexible barrier (Java 7+)
        Phaser phaser = new Phaser(1); // Register main thread
        
        for (int i = 0; i < 3; i++) {
            final int id = i;
            phaser.register(); // Register thread
            new Thread(() -> {
                System.out.println("Phase 0: Thread " + id);
                phaser.arriveAndAwaitAdvance(); // Wait for phase 0
                
                System.out.println("Phase 1: Thread " + id);
                phaser.arriveAndAwaitAdvance(); // Wait for phase 1
                
                phaser.arriveAndDeregister(); // Done
            }).start();
        }
        
        phaser.arriveAndAwaitAdvance(); // Phase 0
        phaser.arriveAndAwaitAdvance(); // Phase 1
        phaser.arriveAndDeregister(); // Main thread done
        
        // Exchanger - exchange data between two threads
        Exchanger<String> exchanger = new Exchanger<>();
        
        new Thread(() -> {
            try {
                String data = "Data from thread 1";
                String received = exchanger.exchange(data);
                System.out.println("Thread 1 received: " + received);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
        
        new Thread(() -> {
            try {
                String data = "Data from thread 2";
                String received = exchanger.exchange(data);
                System.out.println("Thread 2 received: " + received);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
    }
    
    private static void sleep(long millis) {
        try {
            Thread.sleep(millis);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}
```

**Interview Q&A:**


**Q: CountDownLatch vs CyclicBarrier?**
A: CountDownLatch: one-time use, countdown from N to 0, threads wait at await(). CyclicBarrier: reusable, threads wait for each other at barrier, can execute action when all arrive.


**Q: When to use Semaphore?**
A: Limit concurrent access to resource (e.g., connection pool with max 10 connections), implement bounded blocking structures, control rate limiting.


**Q: Phaser vs CyclicBarrier?**
A: Phaser: dynamic registration/deregistration, multiple phases, more flexible, termination support. CyclicBarrier: fixed parties, single barrier point, simpler API.

---

## SECTION 9: SERIALIZATION

### 9.1 Java Serialization

**Explanation:**
Converting object state to byte stream for storage/transmission. Object must implement Serializable (marker interface).

**Code Example:**
```java
import java.io.*;

class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    
    private String name;
    private int age;
    private transient String password; // Not serialized
    private static String country = "USA"; // Static not serialized
    
    public Person(String name, int age, String password) {
        this.name = name;
        this.age = age;
        this.password = password;
    }
    
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + 
               ", password='" + password + "', country='" + country + "'}";
    }
}

public class SerializationDemo {
    public static void main(String[] args) {
        // Serialization
        Person person = new Person("John", 30, "secret123");
        
        try (ObjectOutputStream oos = new ObjectOutputStream(
                new FileOutputStream("person.ser"))) {
            oos.writeObject(person);
            System.out.println("Object serialized: " + person);
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // Deserialization
        try (ObjectInputStream ois = new ObjectInputStream(
                new FileInputStream("person.ser"))) {
            Person deserializedPerson = (Person) ois.readObject();
            System.out.println("Object deserialized: " + deserializedPerson);
            // password is null (transient)
            // country retains current static value
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

### 9.2 Custom Serialization

**Code Example:**
```java
import java.io.*;

class Employee implements Serializable {
    private static final long serialVersionUID = 1L;
    
    private String name;
    private transient int salary; // Don't serialize directly
    
    public Employee(String name, int salary) {
        this.name = name;
        this.salary = salary;
    }
    
    // Custom serialization
    private void writeObject(ObjectOutputStream oos) throws IOException {
        oos.defaultWriteObject(); // Serialize non-transient fields
        
        // Encrypt salary before writing
        int encryptedSalary = salary ^ 0xFACE; // Simple XOR encryption
        oos.writeInt(encryptedSalary);
    }
    
    // Custom deserialization
    private void readObject(ObjectInputStream ois) 
            throws IOException, ClassNotFoundException {
        ois.defaultReadObject(); // Deserialize non-transient fields
        
        // Decrypt salary
        int encryptedSalary = ois.readInt();
        salary = encryptedSalary ^ 0xFACE; // Decrypt
    }
    
    @Override
    public String toString() {
        return "Employee{name='" + name + "', salary=" + salary + "}";
    }
}

// Externalizable - complete control over serialization
class CustomSerialization implements Externalizable {
    private String data;
    private int value;
    
    public CustomSerialization() {} // Must have no-arg constructor
    
    public CustomSerialization(String data, int value) {
        this.data = data;
        this.value = value;
    }
    
    @Override
    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeUTF(data);
        out.writeInt(value);
    }
    
    @Override
    public void readExternal(ObjectInput in) throws IOException {
        data = in.readUTF();
        value = in.readInt();
    }
}

public class CustomSerializationDemo {
    public static void main(String[] args) {
        try {
            Employee emp = new Employee("Alice", 75000);
            
            // Serialize
            ObjectOutputStream oos = new ObjectOutputStream(
                new FileOutputStream("employee.ser"));
            oos.writeObject(emp);
            oos.close();
            
            // Deserialize
            ObjectInputStream ois = new ObjectInputStream(
                new FileInputStream("employee.ser"));
            Employee deserializedEmp = (Employee) ois.readObject();
            ois.close();
            
            System.out.println(deserializedEmp);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**Interview Q&A:**


**Q: What is serialVersionUID?**
A: Unique identifier for Serializable class version. Used during deserialization to verify sender and receiver have compatible versions. If not specified, JVM generates one (riskyâ€”changes with class modifications).


**Q: transient vs static in serialization?**
A: transient: field explicitly excluded from serialization. static: belongs to class, not instance, so not serialized. Both fields will be null/default after deserialization.


**Q: Serializable vs Externalizable?**
A: Serializable: automatic, uses reflection, writes all non-transient fields. Externalizable: manual control, better performance, must implement writeExternal/readExternal, requires no-arg constructor.

---

## SECTION 10: JAVA I/O AND NIO

### 10.1 Java I/O Streams

**Code Example:**
```java
import java.io.*;

public class IODemo {
    public static void main(String[] args) {
        // File operations
        File file = new File("example.txt");
        System.out.println("Exists: " + file.exists());
        System.out.println("Is file: " + file.isFile());
        System.out.println("Is directory: " + file.isDirectory());
        System.out.println("Absolute path: " + file.getAbsolutePath());
        System.out.println("Can read: " + file.canRead());
        System.out.println("Can write: " + file.canWrite());
        System.out.println("Length: " + file.length() + " bytes");
        
        // Create file
        try {
            boolean created = file.createNewFile();
            System.out.println("File created: " + created);
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // FileOutputStream - write bytes
        try (FileOutputStream fos = new FileOutputStream("output.txt")) {
            String data = "Hello World";
            fos.write(data.getBytes());
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // FileInputStream - read bytes
        try (FileInputStream fis = new FileInputStream("output.txt")) {
            int content;
            while ((content = fis.read()) != -1) {
                System.out.print((char) content);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // BufferedOutputStream - buffered writing (faster)
        try (BufferedOutputStream bos = new BufferedOutputStream(
                new FileOutputStream("buffered.txt"))) {
            String data = "Buffered data";
            bos.write(data.getBytes());
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // BufferedInputStream - buffered reading
        try (BufferedInputStream bis = new BufferedInputStream(
                new FileInputStream("buffered.txt"))) {
            int content;
            while ((content = bis.read()) != -1) {
                System.out.print((char) content);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // FileWriter - write characters
        try (FileWriter fw = new FileWriter("characters.txt")) {
            fw.write("Character data\n");
            fw.append("Appended line");
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // FileReader - read characters
        try (FileReader fr = new FileReader("characters.txt")) {
            int ch;
            while ((ch = fr.read()) != -1) {
                System.out.print((char) ch);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // BufferedReader - efficient character reading
        try (BufferedReader br = new BufferedReader(
                new FileReader("characters.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // BufferedWriter - efficient character writing
        try (BufferedWriter bw = new BufferedWriter(
                new FileWriter("bufferedchars.txt"))) {
            bw.write("Line 1");
            bw.newLine();
            bw.write("Line 2");
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // PrintWriter - formatted output
        try (PrintWriter pw = new PrintWriter("formatted.txt")) {
            pw.println("Formatted output");
            pw.printf("Number: %d, String: %s%n", 42, "Hello");
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // Directory operations
        File dir = new File("myDirectory");
        dir.mkdir(); // Create directory
        
        File[] files = dir.listFiles();
        if (files != null) {
            for (File f : files) {
                System.out.println(f.getName());
            }
        }
        
        file.delete(); // Delete file
        dir.delete(); // Delete empty directory
    }
}
```

**Interview Q&A:**


**Q: Difference between InputStream and Reader?**
A: InputStream: reads raw bytes, for binary data. Reader: reads characters, handles character encoding, for text data. Similar relationship between OutputStream and Writer.


**Q: Why use buffered streams?**
A: Reduce I/O operations by reading/writing chunks of data instead of single bytes/characters. Significantly improves performance for file operations.


**Q: What is try-with-resources?**
A: Automatically closes resources implementing AutoCloseable after try block. Ensures cleanup even if exception occurs. Replaces explicit finally blocks for closing resources.

---

### 10.2 Java NIO (New I/O)

**Explanation:**
NIO provides buffer-oriented, non-blocking I/O operations. Key components: Channels, Buffers, Selectors.

**Code Example:**
```java
import java.nio.*;
import java.nio.file.*;
import java.nio.channels.*;
import java.io.*;

public class NIODemo {
    public static void main(String[] args) throws IOException {
        // ByteBuffer - container for data
        ByteBuffer buffer = ByteBuffer.allocate(1024);
        
        // Buffer properties
        System.out.println("Capacity: " + buffer.capacity()); // Total size
        System.out.println("Position: " + buffer.position()); // Current position
        System.out.println("Limit: " + buffer.limit());       // Read/write limit
        
        // Write to buffer
        buffer.put((byte) 10);
        buffer.put((byte) 20);
        buffer.put((byte) 30);
        System.out.println("After put - Position: " + buffer.position()); // 3
        
        // Flip - switch from writing to reading mode
        buffer.flip();
        System.out.println("After flip - Position: " + buffer.position()); // 0
        System.out.println("After flip - Limit: " + buffer.limit());       // 3
        
        // Read from buffer
        while (buffer.hasRemaining()) {
            System.out.println(buffer.get());
        }
        
        // Clear - reset for reuse
        buffer.clear();
        
        // FileChannel - file I/O with buffers
        try (FileChannel fileChannel = FileChannel.open(
                Paths.get("nio-example.txt"), 
                StandardOpenOption.CREATE,
                StandardOpenOption.WRITE)) {
            
            ByteBuffer writeBuffer = ByteBuffer.allocate(64);
            writeBuffer.put("Hello NIO".getBytes());
            writeBuffer.flip();
            
            fileChannel.write(writeBuffer);
        }
        
        // Read with FileChannel
        try (FileChannel fileChannel = FileChannel.open(
                Paths.get("nio-example.txt"),
                StandardOpenOption.READ)) {
            
            ByteBuffer readBuffer = ByteBuffer.allocate(64);
            int bytesRead = fileChannel.read(readBuffer);
            
            readBuffer.flip();
            while (readBuffer.hasRemaining()) {
                System.out.print((char) readBuffer.get());
            }
        }
        
        // Direct buffer - allocated outside JVM heap
        ByteBuffer directBuffer = ByteBuffer.allocateDirect(1024);
        // Faster for I/O, but expensive to create
        
        // Memory-mapped file - map file to memory
        try (RandomAccessFile raf = new RandomAccessFile("mapped.txt", "rw");
             FileChannel channel = raf.getChannel()) {
            
            MappedByteBuffer mappedBuffer = channel.map(
                FileChannel.MapMode.READ_WRITE, 0, channel.size());
            
            // Direct memory access
            mappedBuffer.put(0, (byte) 'A');
        }
        
        // Files utility (Java 7+)
        Path path = Paths.get("test.txt");
        
        // Write
        Files.write(path, "Hello Files API".getBytes());
        
        // Read all lines
        java.util.List<String> lines = Files.readAllLines(path);
        lines.forEach(System.out::println);
        
        // Copy
        Files.copy(path, Paths.get("copy.txt"), 
            StandardCopyOption.REPLACE_EXISTING);
        
        // Move
        Files.move(path, Paths.get("moved.txt"), 
            StandardCopyOption.REPLACE_EXISTING);
        
        // Delete
        Files.deleteIfExists(Paths.get("moved.txt"));
        
        // Directory stream
        try (DirectoryStream<Path> stream = 
                Files.newDirectoryStream(Paths.get("."))) {
            for (Path entry : stream) {
                System.out.println(entry.getFileName());
            }
        }
        
        // Walk file tree
        Files.walk(Paths.get("."), 2)
            .filter(Files::isRegularFile)
            .forEach(System.out::println);
    }
}
```

**Interview Q&A:**


**Q: Difference between IO and NIO?**
A: IO: stream-oriented, blocking, byte/character streams. NIO: buffer-oriented, non-blocking (with Selector), channels and buffers, direct memory access, better for scalable server applications.


**Q: What is buffer flip()?**
A: Switches buffer from writing to reading mode. Sets limit to current position and resets position to 0. Prepares buffer for reading data that was just written.


**Q: Direct vs heap buffer?**
A: Direct: allocated outside JVM heap, faster I/O (no copying between JVM and native), expensive creation. Heap: inside JVM heap, slower I/O, cheaper creation, garbage collected.

---

## SECTION 11: REFLECTION AND ANNOTATIONS

### 11.1 Reflection API

**Code Example:**
```java
import java.lang.reflect.*;

class Person {
    private String name;
    public int age;
    
    public Person() {}
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    private void privateMethod() {
        System.out.println("Private method called");
    }
    
    public void publicMethod(String message) {
        System.out.println("Public method: " + message);
    }
}

public class ReflectionDemo {
    public static void main(String[] args) throws Exception {
        // Get Class object
        Class<?> clazz = Person.class;
        Class<?> clazz2 = Class.forName("Person");
        Person person = new Person();
        Class<?> clazz3 = person.getClass();
        
        // Class information
        System.out.println("Class name: " + clazz.getName());
        System.out.println("Simple name: " + clazz.getSimpleName());
        System.out.println("Package: " + clazz.getPackage().getName());
        System.out.println("Modifiers: " + Modifier.toString(clazz.getModifiers()));
        
        // Constructors
        Constructor<?>[] constructors = clazz.getDeclaredConstructors();
        for (Constructor<?> constructor : constructors) {
            System.out.println("Constructor: " + constructor);
        }
        
        // Create instance using reflection
        Constructor<?> constructor = clazz.getConstructor(String.class, int.class);
        Person newPerson = (Person) constructor.newInstance("John", 30);
        
        // Fields
        Field[] fields = clazz.getDeclaredFields();
        for (Field field : fields) {
            System.out.println("Field: " + field.getName() + 
                             ", Type: " + field.getType());
        }
        
        // Access private field
        Field nameField = clazz.getDeclaredField("name");
        nameField.setAccessible(true); // Bypass access control
        nameField.set(newPerson, "Jane");
        System.out.println("Private field value: " + nameField.get(newPerson));
        
        // Public field
        Field ageField = clazz.getField("age");
        ageField.set(newPerson, 25);
        System.out.println("Public field value: " + ageField.get(newPerson));
        
        // Methods
        Method[] methods = clazz.getDeclaredMethods();
        for (Method method : methods) {
            System.out.println("Method: " + method.getName());
            System.out.println("Return type: " + method.getReturnType());
            System.out.println("Parameters: " + method.getParameterCount());
        }
        
        // Invoke public method
        Method publicMethod = clazz.getMethod("publicMethod", String.class);
        publicMethod.invoke(newPerson, "Hello Reflection");
        
        // Invoke private method
        Method privateMethod = clazz.getDeclaredMethod("privateMethod");
        privateMethod.setAccessible(true);
        privateMethod.invoke(newPerson);
        
        // Check annotations (if any)
        Annotation[] annotations = clazz.getAnnotations();
        for (Annotation annotation : annotations) {
            System.out.println("Annotation: " + annotation);
        }
        
        // Generic information
        demonstrateGenerics();
    }
    
    public static void demonstrateGenerics() throws Exception {
        class Container<T> {
            private T value;
            public void setValue(T value) { this.value = value; }
        }
        
        Field field = Container.class.getDeclaredField("value");
        Type genericType = field.getGenericType();
        System.out.println("Generic type: " + genericType);
        
        if (genericType instanceof TypeVariable) {
            TypeVariable<?> typeVar = (TypeVariable<?>) genericType;
            System.out.println("Type parameter: " + typeVar.getName());
        }
    }
}
```

**Interview Q&A:**


**Q: What is reflection?**
A: Ability to inspect and modify class structure, fields, methods, constructors at runtime. Used for frameworks, serialization, dependency injection, testing.


**Q: Performance impact of reflection?**
A: Slower than direct code due to runtime type checking, security checks, no JIT optimization. Use sparingly in performance-critical code. Cache reflected objects when possible.


**Q: When to use reflection?**
A: Frameworks (Spring DI), ORM (Hibernate), testing (mocking), serialization, dynamic class loading, accessing private members (testing). Avoid in regular application code.

---

### 11.2 Annotations

**Code Example:**
```java
import java.lang.annotation.*;
import java.lang.reflect.*;

// Built-in annotations
@Deprecated
class LegacyClass {
    @Deprecated(since = "2.0", forRemoval = true)
    public void oldMethod() {}
}

class Child extends LegacyClass {
    @Override
    public void oldMethod() {}
    
    @SuppressWarnings("unchecked")
    public void methodWithWarnings() {
        java.util.List list = new java.util.ArrayList();
        list.add("item");
    }
}

// Custom annotation - marker annotation
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@interface Test {
}

// Annotation with elements
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE, ElementType.METHOD})
@interface Info {
    String author();
    String date();
    int version() default 1;
    String[] tags() default {};
}

// Meta-annotations
@Retention(RetentionPolicy.RUNTIME) // When available
@Target(ElementType.TYPE)           // Where applicable
@Inherited                          // Inherited by subclasses
@Documented                         // Include in Javadoc
@interface CustomAnnotation {
    String value();
}

@Info(author = "John", date = "2024-01-01", version = 2, tags = {"important", "stable"})
class AnnotatedClass {
    @Test
    public void testMethod1() {
        System.out.println("Test 1");
    }
    
    @Test
    public void testMethod2() {
        System.out.println("Test 2");
    }
    
    public void regularMethod() {
        System.out.println("Not a test");
    }
}

public class AnnotationDemo {
    public static void main(String[] args) throws Exception {
        // Process annotations
        Class<?> clazz = AnnotatedClass.class;
        
        // Class-level annotation
        if (clazz.isAnnotationPresent(Info.class)) {
            Info info = clazz.getAnnotation(Info.class);
            System.out.println("Author: " + info.author());
            System.out.println("Date: " + info.date());
            System.out.println("Version: " + info.version());
            System.out.println("Tags: " + String.join(", ", info.tags()));
        }
        
        // Method-level annotations - run all @Test methods
        Object instance = clazz.getDeclaredConstructor().newInstance();
        
        for (Method method : clazz.getDeclaredMethods()) {
            if (method.isAnnotationPresent(Test.class)) {
                System.out.println("Running test: " + method.getName());
                method.invoke(instance);
            }
        }
    }
}

// Repeatable annotation (Java 8+)
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@Repeatable(Schedules.class)
@interface Schedule {
    String day();
    int hour();
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@interface Schedules {
    Schedule[] value();
}

@Schedule(day = "Monday", hour = 9)
@Schedule(day = "Friday", hour = 17)
class ScheduledTask {
}
```

**Interview Q&A:**


**Q: Retention policies?**
A: SOURCE: discarded by compiler (e.g., @Override). CLASS: in .class file, not at runtime (default). RUNTIME: available at runtime via reflection.


**Q: @Target values?**
A: TYPE (class/interface), FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE, ANNOTATION_TYPE (meta-annotation), PACKAGE, TYPE_PARAMETER, TYPE_USE.


**Q: When to create custom annotations?**
A: Mark methods for processing (like @Test), configuration (@RequestMapping), validation (@NotNull), code generation, aspect-oriented programming.

---

## SECTION 12: CLASSLOADERS AND JVM INTERNALS

### 12.1 Classloaders

**Explanation:**
ClassLoader loads .class files into JVM.

**Hierarchy:**
1. **Bootstrap ClassLoader**: Loads core Java classes (rt.jar), native code
2. **Extension ClassLoader**: Loads extensions (jre/lib/ext)
3. **Application/System ClassLoader**: Loads application classes (classpath)

**Delegation Model**: Child delegates to parent before loading itself.

**Code Example:**
```java
public class ClassLoaderDemo {
    public static void main(String[] args) {
        // Get classloaders
        ClassLoader appClassLoader = ClassLoaderDemo.class.getClassLoader();
        ClassLoader extClassLoader = appClassLoader.getParent();
        ClassLoader bootstrapClassLoader = extClassLoader.getParent();
        
        System.out.println("Application ClassLoader: " + appClassLoader);
        System.out.println("Extension ClassLoader: " + extClassLoader);
        System.out.println("Bootstrap ClassLoader: " + bootstrapClassLoader); // null (native)
        
        // Which classloader loaded a class?
        System.out.println("String loaded by: " + String.class.getClassLoader()); // null (bootstrap)
        System.out.println("ArrayList loaded by: " + java.util.ArrayList.class.getClassLoader());
        
        // Load class dynamically
        try {
            Class<?> clazz = Class.forName("java.util.HashMap");
            System.out.println("Loaded: " + clazz.getName());
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}

// Custom ClassLoaderclass CustomClassLoader extends ClassLoader {
@Override
protected Class<?> findClass(String name) throws ClassNotFoundException {
try {
// Read .class file
byte[] classData = loadClassData(name);
        // Define class from bytes
        return defineClass(name, classData, 0, classData.length);
    } catch (Exception e) {
        throw new ClassNotFoundException(name, e);
    }
}

private byte[] loadClassData(String name) throws Exception {
    // Load class file from custom location
    String path = name.replace('.', '/') + ".class";
    java.io.InputStream is = getClass().getClassLoader().getResourceAsStream(path);
    
    if (is == null) {
        throw new ClassNotFoundException(name);
    }
    
    java.io.ByteArrayOutputStream baos = new java.io.ByteArrayOutputStream();
    byte[] buffer = new byte[1024];
    int bytesRead;
    
    while ((bytesRead = is.read(buffer)) != -1) {
        baos.write(buffer, 0, bytesRead);
    }
    
    return baos.toByteArray();
}
}

**Interview Q&A:**


**Q: How does class loading work?**
A: 1) Loading: find and load binary data, 2) Linking: verify bytecode, prepare static fields, resolve references, 3) Initialization: execute static initializers.


**Q: What is parent delegation model?**
A: When classloader receives request, delegates to parent first. Only loads if parent can't find class. Ensures core classes loaded by bootstrap, prevents duplicate loading.


**Q: When to use custom classloader?**
A: Load classes from non-standard sources (network, database), hot deployment, class isolation, bytecode manipulation, plugin systems.

---

### 12.2 JVM Architecture

**Explanation:**

**Components:**
1. **Class Loader Subsystem**: Loads, links, initializes classes
2. **Runtime Data Areas**:
   - Method Area: Class metadata, static variables
   - Heap: Objects, instance variables
   - Stack: Method frames, local variables
   - PC Register: Current instruction address
   - Native Method Stack: Native method calls
3. **Execution Engine**:
   - Interpreter: Executes bytecode
   - JIT Compiler: Compiles hot code to native
   - Garbage Collector: Reclaims memory

**Interview Q&A:**


**Q: Heap vs Stack?**
A: Heap: stores objects, shared among threads, garbage collected, slower access. Stack: stores method frames/local variables, thread-private, LIFO, faster access, automatic cleanup.


**Q: What is JIT compiler?**
A: Just-In-Time compiler. Converts frequently executed bytecode (hot spots) to native machine code for faster execution. Balances interpretation speed with compiled performance.


**Q: Method area vs heap?**
A: Method area: class metadata, static variables, constant pool, method code. Heap: instance objects, arrays. Method area is logically part of heap but often implemented separately.

---

### 12.3 Garbage Collection

**Explanation:**

**GC Algorithms:**
1. **Serial GC**: Single-threaded, stop-the-world, simple
2. **Parallel GC**: Multiple threads, throughput-focused
3. **CMS (Concurrent Mark Sweep)**: Low pause times, concurrent marking
4. **G1 GC**: Region-based, predictable pause times (default Java 9+)
5. **ZGC**: Ultra-low latency (<10ms), large heaps
6. **Shenandoah**: Low pause times, concurrent compaction

**Heap Generations:**
- **Young Generation**: Eden + 2 Survivor spaces. Minor GC.
- **Old Generation**: Long-lived objects. Major GC.
- **Metaspace** (Java 8+): Class metadata (replaced PermGen).

**Code Example:**
```java
public class GCDemo {
    public static void main(String[] args) {
        // Enable GC logging: -XX:+PrintGCDetails -Xlog:gc
        
        // Create many objects
        for (int i = 0; i < 1000000; i++) {
            String str = new String("Object " + i);
            // str becomes garbage after iteration
        }
        
        // Request GC (hint, not guaranteed)
        System.gc();
        
        // Finalize method (deprecated, avoid using)
        class Resource {
            @Override
            protected void finalize() throws Throwable {
                // Called before GC (unreliable timing)
                System.out.println("Finalize called");
                super.finalize();
            }
        }
        
        // Weak reference - collected if no strong references
        java.lang.ref.WeakReference<String> weakRef = 
            new java.lang.ref.WeakReference<>(new String("Weak"));
        
        // Soft reference - collected when memory low
        java.lang.ref.SoftReference<byte[]> softRef = 
            new java.lang.ref.SoftReference<>(new byte[1024]);
        
        // Phantom reference - notification after GC
        java.lang.ref.ReferenceQueue<String> queue = 
            new java.lang.ref.ReferenceQueue<>();
        java.lang.ref.PhantomReference<String> phantomRef = 
            new java.lang.ref.PhantomReference<>(new String("Phantom"), queue);
    }
}
```

**GC Tuning Parameters:**
-Xms2g             # Initial heap size
-Xmx4g             # Maximum heap size
-Xmn1g             # Young generation size
-XX:+UseG1GC       # Use G1 GC
-XX:+UseZGC        # Use ZGC
-XX:MaxGCPauseMillis=200  # Target pause time
-XX:+PrintGCDetails       # GC logging

**Interview Q&A:**


**Q: Minor vs Major GC?**
A: Minor GC: cleans Young Generation, fast, frequent. Major/Full GC: cleans entire heap including Old Generation, slower, less frequent, stop-the-world.


**Q: How does G1 GC work?**
A: Divides heap into regions. Prioritizes regions with most garbage (hence "Garbage First"). Concurrent marking, predictable pause times, good for large heaps (>4GB).


**Q: Memory leak in Java?**
A: Objects that are no longer needed but still referenced (not garbage). Common causes: static collections, listeners not removed, unclosed resources, ThreadLocal not cleaned.

---

## SECTION 13: JAVA MODULES (JPMS)

**Explanation:**
Java Platform Module System (JPMS) introduced in Java 9. Organizes code into modules with explicit dependencies.

**Benefits:**
- Strong encapsulation
- Reliable configuration
- Smaller runtime images
- Improved performance

**Code Example:**
```java
// module-info.java
module com.example.myapp {
    // Exports package to other modules
    exports com.example.myapp.api;
    
    // Doesn't export (internal package)
    // com.example.myapp.internal stays private
    
    // Requires another module
    requires java.sql;
    requires java.logging;
    
    // Transitive dependency
    requires transitive java.xml;
    
    // Opens package for reflection (e.g., frameworks)
    opens com.example.myapp.model to com.fasterxml.jackson.databind;
    
    // Provides service implementation
    provides com.example.service.MyService 
        with com.example.myapp.impl.MyServiceImpl;
    
    // Uses service
    uses com.example.service.MyService;
}
```

**Interview Q&A:**


**Q: Why use modules?**
A: Strong encapsulation (hide internal packages), explicit dependencies (no classpath hell), smaller deployments (jlink custom runtime), better security.


**Q: Unnamed module?**
A: Code not in a module. Can read all modules, exports all packages. For backward compatibility with pre-Java 9 code.


**Q: exports vs opens?**
A: exports: makes package accessible at compile and runtime. opens: makes package accessible for reflection only (runtime). Used by frameworks needing deep reflection.

---

## SECTION 14: MODERN JAVA FEATURES (Java 8-21)

### 14.1 Lambda Expressions and Functional Interfaces

**Code Example:**
```java
import java.util.*;
import java.util.function.*;

@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

public class LambdaDemo {
    public static void main(String[] args) {
        // Lambda syntax
        Calculator add = (a, b) -> a + b;
        Calculator multiply = (a, b) -> a * b;
        
        System.out.println(add.calculate(5, 3));      // 8
        System.out.println(multiply.calculate(5, 3)); // 15
        
        // Multi-line lambda
        Calculator complex = (a, b) -> {
            int result = a + b;
            result *= 2;
            return result;
        };
        
        // Built-in functional interfaces
        
        // Predicate<T> - takes T, returns boolean
        Predicate<Integer> isEven = n -> n % 2 == 0;
        System.out.println(isEven.test(4)); // true
        
        // Function<T, R> - takes T, returns R
        Function<String, Integer> stringLength = s -> s.length();
        System.out.println(stringLength.apply("Hello")); // 5
        
        // Consumer<T> - takes T, returns void
        Consumer<String> printer = s -> System.out.println(s);
        printer.accept("Hello Consumer");
        
        // Supplier<T> - takes nothing, returns T
        Supplier<Double> randomSupplier = () -> Math.random();
        System.out.println(randomSupplier.get());
        
        // BiFunction<T, U, R> - takes T and U, returns R
        BiFunction<Integer, Integer, Integer> adder = (a, b) -> a + b;
        System.out.println(adder.apply(10, 20)); // 30
        
        // UnaryOperator<T> - takes T, returns T
        UnaryOperator<Integer> square = n -> n * n;
        System.out.println(square.apply(5)); // 25
        
        // BinaryOperator<T> - takes two T, returns T
        BinaryOperator<Integer> max = (a, b) -> a > b ? a : b;
        System.out.println(max.apply(10, 20)); // 20
        
        // Method reference
        List<String> list = Arrays.asList("a", "b", "c");
        
        // Static method reference
        list.forEach(System.out::println);
        
        // Instance method reference
        String prefix = "Item: ";
        list.forEach(prefix::concat);
        
        // Constructor reference
        Supplier<ArrayList<String>> listSupplier = ArrayList::new;
        ArrayList<String> newList = listSupplier.get();
    }
}
```

---

### 14.2 Streams API

**Code Example:**
```java
import java.util.*;
import java.util.stream.*;

public class StreamsDemo {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
        
        // Filter and collect
        List<Integer> evenNumbers = numbers.stream()
            .filter(n -> n % 2 == 0)
            .collect(Collectors.toList());
        System.out.println("Even numbers: " + evenNumbers);
        
        // Map - transform elements
        List<Integer> squared = numbers.stream()
            .map(n -> n * n)
            .collect(Collectors.toList());
        System.out.println("Squared: " + squared);
        
        // FlatMap - flatten nested structures
        List<List<Integer>> nested = Arrays.asList(
            Arrays.asList(1, 2),
            Arrays.asList(3, 4),
            Arrays.asList(5, 6)
        );
        List<Integer> flattened = nested.stream()
            .flatMap(List::stream)
            .collect(Collectors.toList());
        System.out.println("Flattened: " + flattened);
        
        // Reduce - combine elements
        int sum = numbers.stream()
            .reduce(0, (a, b) -> a + b);
        System.out.println("Sum: " + sum);
        
        Optional<Integer> product = numbers.stream()
            .reduce((a, b) -> a * b);
        product.ifPresent(System.out::println);
        
        // Sorted
        List<String> words = Arrays.asList("banana", "apple", "cherry");
        List<String> sorted = words.stream()
            .sorted()
            .collect(Collectors.toList());
        System.out.println("Sorted: " + sorted);
        
        // Distinct
        List<Integer> duplicates = Arrays.asList(1, 2, 2, 3, 3, 3, 4);
        List<Integer> unique = duplicates.stream()
            .distinct()
            .collect(Collectors.toList());
        System.out.println("Unique: " + unique);
        
        // Limit and skip
        List<Integer> limited = numbers.stream()
            .limit(5)
            .collect(Collectors.toList());
        
        List<Integer> skipped = numbers.stream()
            .skip(5)
            .collect(Collectors.toList());
        
        // Terminal operations
        long count = numbers.stream().count();
        Optional<Integer> max = numbers.stream().max(Integer::compareTo);
        Optional<Integer> min = numbers.stream().min(Integer::compareTo);
        
        boolean anyMatch = numbers.stream().anyMatch(n -> n > 5);
        boolean allMatch = numbers.stream().allMatch(n -> n > 0);
        boolean noneMatch = numbers.stream().noneMatch(n -> n < 0);
        
        // forEach
        numbers.stream().forEach(System.out::println);
        
        // Collectors
        String joined = words.stream()
            .collect(Collectors.joining(", "));
        System.out.println("Joined: " + joined);
        
        Map<Boolean, List<Integer>> partitioned = numbers.stream()
            .collect(Collectors.partitioningBy(n -> n % 2 == 0));
        System.out.println("Partitioned: " + partitioned);
        
        Map<Integer, List<Integer>> grouped = numbers.stream()
            .collect(Collectors.groupingBy(n -> n % 3));
        System.out.println("Grouped by mod 3: " + grouped);
        
        // Parallel stream
        int parallelSum = numbers.parallelStream()
            .reduce(0, Integer::sum);
        System.out.println("Parallel sum: " + parallelSum);
        
        // IntStream, LongStream, DoubleStream
        IntStream.range(1, 11)
            .forEach(System.out::println);
        
        IntStream.of(1, 2, 3, 4, 5)
            .average()
            .ifPresent(System.out::println);
    }
}
```

---

### 14.3 Optional

**Code Example:**
```java
import java.util.*;

public class OptionalDemo {
    public static void main(String[] args) {
        // Create Optional
        Optional<String> optional = Optional.of("Hello");
        Optional<String> empty = Optional.empty();
        Optional<String> nullable = Optional.ofNullable(null);
        
        // Check if present
        if (optional.isPresent()) {
            System.out.println(optional.get());
        }
        
        // ifPresent with lambda
        optional.ifPresent(value -> System.out.println("Value: " + value));
        
        // orElse - default value
        String value1 = empty.orElse("default");
        System.out.println(value1); // default
        
        // orElseGet - lazy default
        String value2 = empty.orElseGet(() -> "computed default");
        
        // orElseThrow
        try {
            String value3 = empty.orElseThrow(() -> 
                new IllegalStateException("No value"));
        } catch (IllegalStateException e) {
            System.out.println(e.getMessage());
        }
        
        // map - transform value
        Optional<Integer> length = optional.map(String::length);
        System.out.println(length.get()); // 5
        
        // flatMap - avoid nested Optional
        Optional<Optional<String>> nested = Optional.of(Optional.of("Nested"));
        Optional<String> flattened = Optional.of("Value")
            .flatMap(v -> Optional.of(v.toUpperCase()));
        System.out.println(flattened.get()); // VALUE
        
        // filter
        Optional<String> filtered = optional
            .filter(v -> v.length() > 3);
        System.out.println(filtered.isPresent()); // true
        
        // Java 9+: ifPresentOrElse
        optional.ifPresentOrElse(
            value -> System.out.println("Present: " + value),
            () -> System.out.println("Empty")
        );
        
        // Java 9+: or
        Optional<String> result = empty.or(() -> Optional.of("alternative"));
        
        // Java 10+: orElseThrow() without parameter
        // String value4 = empty.orElseThrow();
        
        // Java 11+: isEmpty
        System.out.println("Is empty: " + empty.isEmpty());
        
        // Avoid
        // if (optional.isPresent()) {
        //     String val = optional.get(); // Don't do this
        // }
        // Use: optional.ifPresent() or orElse()
    }
}
```

---

### 14.4 Records (Java 14+)

**Code Example:**
```java
// Simple record
record Person(String name, int age) {}

// Record with custom methods
record Point(int x, int y) {
    // Canonical constructor validation
    public Point {
        if (x < 0 || y < 0) {
            throw new IllegalArgumentException("Coordinates must be positive");
        }
    }
    
    // Custom method
    public double distanceFromOrigin() {
        return Math.sqrt(x * x + y * y);
    }
    
    // Static method
    public static Point origin() {
        return new Point(0, 0);
    }
}

// Record with custom constructor
record Employee(String name, int id, double salary) {
    // Compact constructor
    public Employee {
        if (salary < 0) {
            throw new IllegalArgumentException("Salary cannot be negative");
        }
    }
    
    // Additional constructor
    public Employee(String name, int id) {
        this(name, id, 0.0);
    }
}

public class RecordDemo {
    public static void main(String[] args) {
        // Create record
        Person person = new Person("John", 30);
        
        // Automatic getters
        System.out.println(person.name()); // John
        System.out.println(person.age());  // 30
        
        // Automatic equals, hashCode, toString
        Person person2 = new Person("John", 30);
        System.out.println(person.equals(person2)); // true
        System.out.println(person.hashCode() == person2.hashCode()); // true
        System.out.println(person); // Person[name=John, age=30]
        
        // Records are immutable
        // person.name = "Jane"; // Compile error
        
        // Custom methods
        Point point = new Point(3, 4);
        System.out.println(point.distanceFromOrigin()); // 5.0
        
        // Records in collections
        List<Person> people = List.of(
            new Person("Alice", 25),
            new Person("Bob", 30),
            new Person("Charlie", 35)
        );
        
        people.stream()
            .filter(p -> p.age() > 28)
            .forEach(System.out::println);
    }
}
```

---

### 14.5 Pattern Matching and Sealed Classes

**Code Example:**
```java
// Pattern matching for instanceof (Java 16+)
public class PatternMatchingDemo {
    public static void main(String[] args) {
        Object obj = "Hello";
        
        // Old way
        if (obj instanceof String) {
            String str = (String) obj;
            System.out.println(str.length());
        }
        
        // Pattern matching
        if (obj instanceof String str) {
            System.out.println(str.length());
        }
        
        // Pattern matching in switch (Java 21+)
        String result = switch (obj) {
            case String s -> "String of length " + s.length();
            case Integer i -> "Integer: " + i;
            case null -> "Null value";
            default -> "Unknown type";
        };
    }
}

// Sealed classes (Java 17+)
sealed interface Shape permits Circle, Rectangle, Triangle {}

final class Circle implements Shape {
    private final double radius;
    public Circle(double radius) { this.radius = radius; }
    public double area() { return Math.PI * radius * radius; }
}

final class Rectangle implements Shape {
    private final double width, height;
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    public double area() { return width * height; }
}

final class Triangle implements Shape {
    private final double base, height;
    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }
    public double area() { return 0.5 * base * height; }
}

public class SealedClassDemo {
    public static void main(String[] args) {
        Shape shape = new Circle(5.0);
        
        // Pattern matching with sealed classes
        double area = switch (shape) {
            case Circle c -> c.area();
            case Rectangle r -> r.area();
            case Triangle t -> t.area();
            // No default needed - compiler knows all subtypes
        };
        
        System.out.println("Area: " + area);
    }
}
```

---

### 14.6 Virtual Threads (Project Loom - Java 21+)

**Code Example:**
```java
import java.time.*;
import java.util.concurrent.*;

public class VirtualThreadsDemo {
    public static void main(String[] args) throws Exception {
        // Platform thread (traditional)
        Thread platformThread = new Thread(() -> {
            System.out.println("Platform thread: " + Thread.currentThread());
        });
        platformThread.start();
        
        // Virtual thread
        Thread virtualThread = Thread.ofVirtual().start(() -> {
            System.out.println("Virtual thread: " + Thread.currentThread());
        });
        
        // ExecutorService with virtual threads
        try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
            IntStream.range(0, 10_000).forEach(i -> {
                executor.submit(() -> {
                    Thread.sleep(Duration.ofSeconds(1));
                    return i;
                });
            });
        } // Auto-close waits for completion
        
        // Scalability demonstration
        long start = System.currentTimeMillis();
        
        try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
            for (int i = 0; i < 100_000; i++) {
                executor.submit(() -> {
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        Thread.currentThread().interrupt();
                    }
                });
            }
        }
        
        long end = System.currentTimeMillis();
        System.out.println("Time: " + (end - start) + "ms");
        // Virtual threads: lightweight, millions possible
        // Platform threads: heavy, thousands maximum
    }
}
```

---

### 14.7 Other Modern Features

**Code Example:**
```java
public class ModernFeaturesDemo {
    public static void main(String[] args) {
        // var keyword (Java 10+) - local variable type inference
        var list = new ArrayList<String>();
        var map = new HashMap<String, Integer>();
        var stream = list.stream();
        
        // Text blocks (Java 15+)
        String json = """
            {
                "name": "John",
                "age": 30,
                "city": "New York"
            }
            """;
        
        String html = """
            <html>
                <body>
                    <h1>Hello World</h1>
                </body>
            </html>
            """;
        
        // Switch expressions (Java 14+)
        int day = 3;
        String dayName = switch (day) {
            case 1 -> "Monday";
            case 2 -> "Tuesday";
            case 3 -> "Wednesday";
            default -> "Other";
        };
        
        // Switch with yield
        String result = switch (day) {
            case 1, 2, 3, 4, 5 -> {
                System.out.println("Weekday");
                yield "Work";
            }
            case 6, 7 -> {
                System.out.println("Weekend");
                yield "Rest";
            }
            default -> "Invalid";
        };
        
        // Enhanced NullPointerException messages (Java 14+)
        // Shows exactly which variable was null
        try {
            String str = null;
            int length = str.length();
        } catch (NullPointerException e) {
            System.out.println(e.getMessage());
            // Cannot invoke "String.length()" because "str" is null
        }
    }
}
```

**Interview Q&A:**


**Q: Benefits of records?**
A: Concise syntax for data carriers, immutable by default, automatic equals/hashCode/toString, no boilerplate, clear intent.


**Q: When to use sealed classes?**
A: Restrict class hierarchy, exhaustive pattern matching, domain modeling with fixed set of types, better type safety.


**Q: Virtual threads vs platform threads?**
A: Virtual threads: lightweight (1MB â†’ few KB), millions possible, managed by JVM, ideal for I/O-bound tasks. Platform threads: heavyweight, thousands max, OS-managed, better for CPU-bound tasks.

---

This covers Core Java comprehensively. Would you like me to continue with **Advanced Java** topics (JDBC, JPA/Hibernate, Spring, Microservices, etc.)?
