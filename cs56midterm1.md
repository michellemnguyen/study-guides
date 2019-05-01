# Cynthia Zhang @ UCSB `CS56` Midterm 1 Study Guide
## Introduction
This is an incomplete midterm study guide. There is probably material missing from here, albeit most information should be valid. Please email me if you'd like something updated or changed.
##### All code blocks are either mine or taken from the course's [lecture notes](https://ucsb-cs56.github.io/s19/)

## Java
- **automatic garbage collection**: background thread that finds unreferenced objects and cleans up the heap for you
- very performant language
- advantage: **portable** and **platform-independent**
    - executed by Java Virtual Machine
    - unlike C/C++, which is platform-dependent
    - “write once, run everywhere”: Java bytecode can be placed onto any platform and run 
- Java = interpreted language
    - Python/Javascript = pure interpreted language
- no manual ways to manage memory (unlike C++)
    - less complexity, usually don’t use pointers etc. 
    - all primitive types live on the stack
    - all objects live on the heap, every variable to an object is a reference (or a “pointer”, use sparingly) to the location of the object on the heap

## Programming
- Build steps
    - (Java)
        1. write source code
        2. compilation into **bytecode** (.class) ← portable, can be executed by Java Virtual Machine, executed on the software level
        3. linking and executable
        4. .jar file = java “executable”, a glorified zip file
    - (C++)
        1. write source code
        2. compilation and linking ← executed on the hardware level
        3. run executable
- **Java Virtual Machine (JVM)**: a piece of software that executes  bytecode and also manages memory for Java applications
- everything derives from Object, the base class for all objects
- x has a size based off of operating system
    - 64-bit OS is 64 bit mapping space

### Identifiers (variable names)
- can start with an underscore, $, or letter and can contain letters, digits or underscore  
    - Examples: `var1`, `_temp`, `$total`, `dogBark`  
- identifiers are case sensitive
- **predefined keywords**: cannot be used as identifiers in your programs 

|           |           |           |           |           |           |           |           |
|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|
| abstract	|  char	    | else      | goto*	    | long	    | return	| this  | while     |
| assert***	| class	    | enum****  | if	    | native	| short	    | throw     | *	 	not used
| boolean	| const*    | extends   | implements | new	    | static	| throws    | **	 	added in 1.2
| break	    | continue	| final     | import	| package	| strictfp**  | transient | ***	 	added in 1.4
| byte	    | default	| finally   | instanceof | private	| super 	| try       | ****	 	added in 5.0
| case	    | do        | float     | int	    | protected	| switch    | void      |
| catch	    | double	| for       | interface	| public	| synchronized | volatile  |


### Numerical Primitive Values
Integers
- byte (1 byte)
- short (2 bytes)
- int (4 bytes)
- long (8 bytes)  

Floating Point Numbers
- float (4 bytes)
- double (8 bytes)  

Characters
- char (2 bytes)  

Boolean 
- boolean (1 byte) 

Similar to C++, Java is strictly typed: must define variables with a type
``` java
int x;
int y;
int a,b;
```
**overflow**: when you exceed the number of bits allocated for the bit representation  
    - Java does not check for overflow
``` java
int i = Integer.MAX_VALUE + 1;  // -2147483648
```
- Integer is an object (not a primitive type) that ints are wrapped in
- every primitive type has an "object wrapper"
- overflow also occurs in C++

### Type-Casting
Type casting is when you assign a value of one primitive data type to another type.
In Java, there are two types of casting:
- Widening Casting (automatically) - converting a smaller type to a larger type size  
    `byte` -> `short` -> `char` -> `int` -> `long` -> `float` -> `double`  
    
- Narrowing Casting (manually) - converting a larger type to a smaller size type  
    `double` -> `float` -> `long` -> `int` -> `char` -> `short` -> `byte`  
    ``` java
    int a = 5;
    int b = 10;
    double c = (double) a/b;
    double d = ((double) a)/b;
    double e = (double) (a/b);
    System.out.println(c + " " + d + " " + e); // 0.5 0.5 0.0
    ```
    
### Escape characters 
`\t` tab  
`\n` newline  
`\'` single quote  
`\"` double quote  
`\\` backslash  

## Strings
**Strings**: wrapped objects like C++ std strings (not C-strings); contains attributes like size, etc.
- all Java strings are **immutable**; must make a new string with modifications of the original
- you **cannot** overload operators in Java
- `==` compares two memory addresses, therefore needs the .equals() method to compare equality of two strings
  - **string pool**: a Java7 optimization
    ``` java
    String s = "Hello";
    String t = "Hello";

    System.out.println(s == t); // returns true
    ``` 
    - Java looks on the stack for a string with the same content, and then has both references point to the same location  

    ``` java
    String s = "Hello";
    String t = new String("Hello");

    System.out.println(s == t); // returns false
    ``` 
    - we must explicitly tell Java to make a new memory location using keyword **new**
- the .compareTo() method:  
    ``` java 
    // == 0 if the same
    // > 0 if s1 > s2
    // < 0 if s1 < s2
    
    String a = "a";
    String b = "b";
    String A = "A";

    System.out.println(a.compareTo(a)); // 0
    System.out.println(a.compareTo(b)); // -1
    System.out.println(a.compareTo(A)); // 32
    ```
- converting a string to an int
``` java
String s = "3";
int i = Integer.parseInt(s);
```
- converting an int to a string
``` java
String t = Integer.toString(5);
System.out.println(t);
```
### String Concatenation
``` java
System.out.println(3 + 4 + "Hi");   // OUTPUT: 7Hi
System.out.println(3 + (4 + "Hi")); // OUTPUT: 34Hi
System.out.println("3" + 4 + "Hi"); // OUTPUT: 34Hi

String u = String.valueOf(4);
System.out.println(u + 3);          // OUTPUT: 43
```

## Java Basics
### If-Else Statements
``` java
if (boolean_expression) 
    statement
else
    statement
```
- curly braces { } are needed if more than one statement

### While loops
``` java
while (boolean_expression) {
    statements;
}
```
- break and continue statements

### Do-while loops
``` java
do {
    statements;
} while (boolean_expression);
```
- must end with a semicolon
- guarantees that a certain bit of code executes at least once
- example: prompting the user with a command

### For loops
``` java
for (initial_action; boolean_expression; update) {
    statements;
}

int i = 0;
for (; i < 10;) {   // this is legal, but dumb
    System.out.println(i);
    i++;    
}
```

### Booleans (primitive types)
- must use keyword `True` or `False`
- cannot use numerical values `0` or `1`, like in C++ --> this causes compiler error

### Relational Operators
`== != < <= > >=`
* left to right precedence

### Logical Operators
`!` not  
`&&` and  
`||` or  
**short-circuit evaluation**: if something evaluates to false in a string of &&s, automatically determine the entire expression false (following order of operations)

### Unreachable Code
- Java will not compile (gives error) if you compile with unreachable code
``` java
public static int f() {
    int a = 0, b = 0;
    if (a < b) {
        System.out.println("a < b");
        return a;
    } else {
        System.out.println("a >= b");
        return b;
    }
    System.out.println("some statement");   // THIS IS UNREACHABLE CODE
}
```

## Classes
Note: all objects are inherited from the object class

* Virtual machine takes class files with functions inside of classes.
* Usually use **public** classes.
    * **protected**: describes a method or field in a superclass that can be accessed only by the subclasses in other package or any class within the package of the protected members' class. 
        * The protected access modifier cannot be applied to class and interfaces. 
        * methods and fields in a interface cannot be declared protected.
    * Private classes can be created inside of public class definitions. 
* No semicolon necessary after a class definition (unlike C++)
* We don't separate header files from class files. Java classes contain the interface, so that all implementation details are part of the class itself.
    * Class members must be declared private or public (unlike C++) 
* In Java, we call the dot operator on `this`. `this` is a memory reference in C++, so we use an arrow operator. `this` refers to the class to itself. Using `this` is only necessary when the parameter in the argument is the same as the class variable name.
* Don't need to "import" Car.java because the JVM will find it in the directory when it's mentioned in Lecture3.java

### Static
* **static variables**: belongs to the class (or all instances of the object) instead of each instance of an object
    * they are shared among ALL instances of the class
    * when modified in one class, changes are reflected in all instances of the class
``` java
private static int staticCounter = 0;
```
* **static methods**: a method that can be called without creating an instance of the class
    * usually something that is always constant and is associated with the class
    * can call using the class name or the name of an instance
    * used when the functionality is not dependent on the state of the object.
``` java
public static double convertMilesToKilometers(double miles) { 
    return miles * 1.60934; 
}
```

### Method Overloading
* methods with the same name but different parameters; different "signature"
``` java
// in Lecture3.java
car.setMaxMPH(1);
car.setMaxMPH(1.0);
short x = 3;
car.setMaxMPH(x);
car.setMaxMPH("1");

// in Car.java
public void setMaxMPH(int x) {
    System.out.println("maxMPH int");
}

public void setMaxMPH(double x) {
    System.out.println("maxMPH double");
}

public void setMaxMPH(short x) {
    System.out.println("maxMPH short");
}

public void setMaxMPH(String x) {
    System.out.println("maxMPH string");
}
```

### Constructors
* a **default constructor** is a constructor without any parameters
    * if no constructor is provided, Java makes one that sets the class variables to default values
    * if any constructor is defined, Java does not supply a default constructor and you must provide one if needed (same as C++)

### Pass-By-Value vs. Pass-By-Reference
* primitive values are pass-by-value by default
* everything in Java is pass-by-value, but for objects, we are making a copy of the memory reference; memory address is passed-by-value; It *looks* like pass-by-reference because we are not changing the memory reference in that stack frame

### Shallow vs. Deep Copies
Shallow copy: copying memory location  
Deep copy: making new memory locations with keyword `new` with exact same content

### Command-line arguments
* `args[0]` is a string
``` java
// if command line is 'java Lecture 10 20'
System.out.println(args[0]);            // 10
System.out.println(args[1]);            // 20
System.out.println(args[0] + args[1]);  // 1020 because of string concatenation
Integer.parseInt(args[1]);              // 30
```

### Import statements
* takes code from Java's API and imports it into your code

### Scanners
* `System.in` refers to C++'s `cin` to take in information
* nextLine() takes in the next line into a string
* next() takes in the next characters until a whitespace or newline
``` java
import java.util.Scanner;

Scanner s = new Scanner(System.in);
String t = s.nextLine();
String first = s.next();
s.close();
``` 

### Random Numbers
* pseudo-random number generator provided by java.util.Random

``` java
import java.util.Random;

Random generator = new Random();
int randomInt = generator.nextInt(4); // [0, 1, 2, 3]
double randomDouble = generator.nextDouble(); // 0 -> 0.99999...
```

### Arrays
* `.length` is a public member of array with the array size
* default instantiation will populate all int elements with 0
* `int[] array3 = array2.clone();` clones a new memory segment with the exact contents of the previous array
``` java 
int[] array;        // declare array
array = new int[100];   // assign array of size 100 ints 
array[0] = 10;
array[1] = 20;
```

### Arraylists
* arraylists are a generic type that is dynamically resizable
    * very similar to C++ vectors
* cannot use primitive types; must use object types (Integer not int)
    * in general, generic types accept objects, not primitive types
* .add(x) enters new value at the end of the arraylist
* .remove(Object o) or .remove(int index) to remove elements from the arraylist

### Stack Overflow
stack overflow: occurs when stack grows into the heap in the memory
``` java
public static int factorial(int n) {
    return n * factorial(n - 1);
}
```
The following does not cause stack overflow because of Java Garbage Collection:
``` java
String s;
while (true) {
    s = new String();
}
```

## Exceptions
* null pointer exceptions: occurs when attempting to access a null object
* may only throw objects that extend from the Exception class
* **cannot** throw primitive types
* shouldn't try catching everything in main, since it is hard to recover from
* **finally block**: will always be executed regardless of what occurs in the rest of the blocks; even occurs if a "return" statement is called (Java-specific; is not in C++)
* how to chain exceptions: `catch(IndexOutOfBoundsException | NullPointerException e) {`

## Testing
* unit testing: makes sure that module of code works
* builds confidence in the system you're building
* complete tests are impossible
* JUnit: Java framework for testing
    * JUnit methods:
    ``` java
    assertEquals(expected_value, result_of_test);
    assertFalse(boolean_result);
    assertTue(boolean_result);
    assertNull(some_object);
    ```
    * JUnit API contains more methods
* **annotations**: 
    * @Before executes before each test in this class
    ``` java
    import org.junit.Before;

    @Before
    public void executeBeforeEachTest()) {
        System.out.println("@Before");
        array = new int[10];
        b = new Example();
    }
    ```
    * @Test indicates to run these tests
    ``` java
    import org.junit.Test;
    import static org.junit.Assert.assertEquals;
    
    @Test 
    public void testInsertItem() {
        array[0] = 0;
        assertEquals(array[0], 0);
    }
    ```
    * reminder: a .jar file is a container with class files
    * the **junit-4.8.2.jar** file 
    * flag **-cp**: "class path", tells Java where to look for certain files
    `javac -cp .:lib/* Example.java Tester.java` tells Java to look in your current directory and in the lib folder for the named files
    * to run: `java -cp Example` (?)
* Google Test Framework for C++: gives platform for easy unit testing

## Inheritance
* inheritance using keyword **extends** `public class Car2 extends Vehicle { }`
* if a default constructor exists, the base class constructor is called first
* Java provides a default constructor if a constructor doesn't exist
* If you create a parameterized constructor and no default constructor, then no default constructor is created
* keyword **super** to reference its direct parent class; `super(100, "blue")` calls the superclass' parameterized constructor
    * super MUST be in the very first line of the method
* **instanceOf** operator: returns if one thing is an instance of another
``` java
Car2 c = new Car2(120, "black", "Pointiac", "GrandAM");

if (c instanceof Vehicle)   // true
            System.out.println("instance of vehicle");  
```
* C++ allows multiple inheritance; Java does **not** allow multiple inheritance (extending from multiple classes)
    * you can implement multiple interfaces

## Polymorphism
- ability to act as different types (base class or subclass)
- memory access always depends on base class 
- java automatically exhibits polymorphic behavior without using **virtual** keyword like in C++
``` java
import java.util.Scanner;
...
Object o = new Car2(120, "black", "Pontiac", "GrandAM"); // can only access methods from the Object type, not the car2 class
Object o2 = new int[100];
Object o3 = new Scanner(System.in);
Car2 c = new Object(); // ERROR, type mismatch

Vehicle[] vehicleArray = new Vehicle[3];
vehicleArray[0] = new Vehicle(100, "blue");
vehicleArray[1] = new Car2(120, "black", "Pontiac", "GrandAM");
vehicleArray[2] = new Truck(120, "black", "Ford", "F150", 400);
for (int i = 0; i < 3; i++) {
    System.out.println(vehicleArray[i]);
    System.out.println("----");
}
```
- overriding the toString() method
``` java
// in Car2.java
public String toString() {
    System.out.println("in Car2.toString()");
    return super.toString() + ", make = " + make + "model = " + model;
}

// in Vehicle.java
public String toString() {
    System.out.println("in Vehicle.toString()");
    return "maxMPH = " + maxMPH + ", color = " + color;
}
```
- keyword **final**:
    - for methods: cannot override
    - for classes: cannot inherit from this class
- **memory slicing**: can exist for primitive types (loss of precision)
    - all objects in Java exist on the heap, so objects don't have the same problem of memory slicing as in C++
    - only primitive types and references to objects are constructed on the stack
    - everything is still accessible, not sliced away
    - depends on visibility of methods from base class
``` java
double x = 2.2;
int y = (int) x;    // int has 4 bytes; valid
int z = x;          // invalid
```

### Casting
- base class cannot be assigned to a subclass type
``` java
Vehicle v1 = (Vehicle) new Object();    // illegal
Vehicle v2 = (Vehicle) new Car(120, "black", "Pontiac", "GrandAM");     // valid
Car2 c = (Car2) v2;     // casting backwards
System.out.println(c.getModel());       // still able to access model, since memory slicing did not occur
```
- as long as it's a valid casting with underlying compatible types, it will be legal

## Abstract Classes/Methods
- abstract classes: a class with one or more abstract methods
    - subclasses must define its' parent class methods
    - cannot have an object constructed of it
    - methods must be overriden in a subclass
**interface**: a purely abstract class
- C++ allows multiple inheritance
- **implements** keyword: to implement an interface

### Switch Statements
- replaces a long if-else chain; switch statements are much cleaner to read 
- useful for menu and inputs
``` java
String status;
switch(studentYear) {   // start switch block
    case 1:
        status = "Freshman";
        break;
    case 2: 
        status = "Sophomore";
        break;
    case 3: 
        status = "Junior";
        break;
    case 4: 
        status = "Senior";
        break;
    default:
        status = "Undefined";
        break;
}   // end switch block
```
- combining switch statements
``` java
switch(studentYear) {
    case 1: case 2: 
        status = "LowerDivision";
        break;
    case 3: case 4:
        status = "UpperDivision";
        break;
    default: 
        status = "Undefined";
        break;
}
```
- String switching
``` java
String studentYear = "junior";
String status;
switch(studentYear) {
    case "freshman" : case "sophomore" :
        status = "LowerDivision";
        break;
    case "junior" : case "senior" :
        status = "UpperDivision";
        break;
    default: 
        status = "Undefined";
        break;
}
```
### Encoding and Decoding
- using bit-form
    - the basis of file i/o
    - ASCII: American standard code for information interchange 
- encode into characters, decode into binary bits
- useful for file conversion
2^8 = 256 possible combinations (ie. IP addresses)
- UTF-8 `System.out.println(System.getProperty("file.encoding"));
    - 1 byte: American characters
    - 4 bytes = 2^32 = ~4 billion: non-American set of characters beyond the ASCII set

## File I/O with Scanners
- .hasNext() : gets everything until a whitespace character
- .hasNextLine() : gets everything until a newline character
``` java
try {
    Scanner inFile = new Scanner(new File("file.txt"));
    String line;
    while (inFine.hasNextLine()) {
        line = inFile.nextLine();
        System.out.println(line);
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    }
}
```
**absolute path**: starts from the root directory; usually only works on your machine
**relative path**: good idea, especially when the file will be shared with others or run on a different machine

**delimiters**: a token that is used to separate different values
``` java
inFile.useDelimiter("l");   // the letter l
```

### Input from a URL
``` java
String line;
Scanner remoteIn = null;
try {
    URL remoteFileLocation = new URL("https://sites.cs.ucsb.edu/~richert/file.txt");

    URLConnection connection = remoteFileLocation.openConnection();
    remoteIn = new Scanner(connection.getInputStream());
} catch (IOException e) {
    e.printStackTrace();
} finally {
    remoteIn.close();
}

```

.split(): a string method that splits a string into an array of values separated by a delimiter
``` java
while (inFile.hasNextLine()) {
    s = inFile.nextLine();
    stringArray = s.split(",");
}
```
