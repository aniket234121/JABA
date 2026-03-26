# String
A String in Java is an object that represents a sequence of characters, implemented using the **java.lang.String** class.

* String str = "Hello";

* Stored as characters (Unicode)

* Not a primitive → it is a reference type

* Stored in String Constant Pool (SCP) for memory optimization

* mutable → safe for multithreading & security

* JVM gives special treatment (unlike normal objects)

## Internal Representation (Important)

Before Java 9:

    private final char[] value;
Java 9+:

    private final byte[] value;
    private final byte coder;

👉 Java optimized memory using Compact Strings:

Uses byte[] instead of char[]
Saves memory for ASCII strings

## Types of Strings in Java

Technically, Java has only one String class, but based on creation and behavior, we categorize them into types:

## 1. String Literal (Stored in SCP)
    String s1 = "Hello";
Characteristics:
Stored in String Constant Pool (SCP)
JVM reuses memory if value already exists

    String s1 = "Hello";
    String s2 = "Hello";

👉 Both refer to same object in memory

## 2. String Object (Heap Memory)
    String s2 = new String("Hello");
Characteristics:

Stored in Heap

Always creates a new object

Even if same value exists in SCP

## Interned String

    String s3 = new String("Hello").intern();
What happens:

Forces string into SCP

Returns reference from pool

## Immutable

A String is immutable means once an object is created, its value cannot be changed. Any modification results in a new object creation, not modification of the existing one.

🔍 Example

    String s = "Hello";
    s.concat(" World");

👉 Result:

s still points to "Hello"

"Hello World" is created but not referenced

## Memory Map (Important check it)
[Memory Map ](memoryMap.md)


## Ways to compare the strings

### 1 == (Reference Comparison)
What it does:

Compares memory addresses (references), NOT actual content.

🔍 Example

    String s1 = "Hello";
    String s2 = "Hello";

    System.out.println(s1 == s2);
**output:** true  

Both point to same object in String Constant Pool (SCP)

Important Case

    String s1 = new String("Hello");
    String s2 = new String("Hello");

    System.out.println(s1 == s2);

👉 Output: false

✔ Why?
Two different objects in Heap

### 2 .equals() (Content Comparison)
✅ What it does:

Compares actual character data (value)

🔍 Example

    String s1 = new String("Hello");
    String s2 = new String("Hello");

    System.out.println(s1.equals(s2));

👉 Output: true

🧠 Internal Working:

Compares character-by-character

### 3 .equalsIgnoreCase()

Compares strings ignoring case differences

🔍 Example

    String s1 = "hello";
    String s2 = "HELLO";

    System.out.println(s1.equalsIgnoreCase(s2));

👉 Output: true

✔ Use Case:

User input validation

Case-insensitive matching

### 4 .compareTo() (Lexicographical Comparison)

Compares strings based on Unicode values

🔍 Example

    String s1 = "Apple";
    String s2 = "Banana";

    System.out.println(s1.compareTo(s2));

👉 Output: negative value

Return Values

    0 if equal

    < 0 if s1 < s2

    > 0 if s1 > s2

### 5 .compareToIgnoreCase()
Same as compareTo() but ignores case

    s1.compareToIgnoreCase(s2);

### 5  Objects.equals() (Null-Safe Comparison) 
this will only compare the references not the actual values

    import java.util.Objects;

    Objects.equals(s1, s2);
✅ Advantage:

Handles null safely
🔍 Example

    String s1 = null;
    String s2 = "Hello";

    System.out.println(Objects.equals(s1, s2));

👉 Output: false (no exception)

⚠️ Null Pointer Trap

    String s = null;
    s.equals("Hello");   // ❌ NullPointerException

✔ Safe way:

    "Hello".equals(s);

## Concatenation

### 1 Using + Operator

    String s = "Hello" + " World";

compile time concatenation and runtime concatenation checkout in memory map.


### 2 Using concat() Method

    String s1 = "Hello";
    String s2 = s1.concat(" World");

✔ Features:

Belongs to String class

Always creates new object

⚠️ Important Behavior

    String s = "Hello";
    s.concat(" World");

    System.out.println(s);

👉 Output: "Hello" (unchanged)

✔ Because String is immutable

### 3 Using StringBuilder (Recommended for Performance)

    StringBuilder sb = new StringBuilder();
    sb.append("Hello");
    sb.append(" World");

    String result = sb.toString();
✔ Features:

Mutable

Faster

Used internally by JVM for + operator

### 4 Using StringBuffer
    StringBuffer sb = new StringBuffer();
    sb.append("Hello");
    sb.append(" World");
✔ Features:

Thread-safe (synchronized)

Slower than StringBuilder

### 5 Using String.join() (Java 8+)
    String result = String.join("-", "A", "B", "C");

👉 Output: "A-B-C"

Use Case:
Joining multiple strings with delimiter