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

# Inbuilt methods in String class

| Category | Method | Return Type | Modifies Original? | Time Complexity* | Key Notes (What Developers Must Know) |
|----------|--------|------------|--------------------|------------------|--------------------------------------|
| Basic | `length()` | `int` | ❌ No | O(1) | Returns character count (not bytes) |
| Basic | `isEmpty()` | `boolean` | ❌ No | O(1) | Checks length == 0 |
| Basic | `isBlank()` (Java 11+) | `boolean` | ❌ No | O(n) | Checks only whitespace (trim-like behavior) |
| Access | `charAt(int)` | `char` | ❌ No | O(1) | No bounds check → can throw `IndexOutOfBoundsException` |
| Access | `toCharArray()` | `char[]` | ❌ No | O(n) | Creates new array copy |
| Comparison | `equals(Object)` | `boolean` | ❌ No | O(n) | Content comparison (case-sensitive) |
| Comparison | `equalsIgnoreCase()` | `boolean` | ❌ No | O(n) | Case-insensitive comparison |
| Comparison | `compareTo(String)` | `int` | ❌ No | O(n) | Lexicographical comparison (Unicode-based) |
| Comparison | `compareToIgnoreCase()` | `int` | ❌ No | O(n) | Case-insensitive ordering |
| Search | `contains(CharSequence)` | `boolean` | ❌ No | O(n) | Internally uses `indexOf()` |
| Search | `indexOf(String)` | `int` | ❌ No | O(n) | Returns first match index or -1 |
| Search | `lastIndexOf(String)` | `int` | ❌ No | O(n) | Searches from end |
| Search | `startsWith(String)` | `boolean` | ❌ No | O(n) | Prefix check |
| Search | `endsWith(String)` | `boolean` | ❌ No | O(n) | Suffix check |
| Substring | `substring(int)` | `String` | ❌ No | O(n) | Creates new String (post Java 7) |
| Substring | `substring(int, int)` | `String` | ❌ No | O(n) | End index exclusive |
| Modify | `toUpperCase()` | `String` | ❌ No | O(n) | Locale-sensitive |
| Modify | `toLowerCase()` | `String` | ❌ No | O(n) | Locale-sensitive |
| Modify | `trim()` | `String` | ❌ No | O(n) | Removes leading/trailing spaces only |
| Modify | `strip()` (Java 11+) | `String` | ❌ No | O(n) | Unicode-aware trimming |
| Modify | `replace(char, char)` | `String` | ❌ No | O(n) | No regex used |
| Modify | `replaceAll(String, String)` | `String` | ❌ No | O(n) | Uses regex → slower |
| Modify | `replaceFirst(String, String)` | `String` | ❌ No | O(n) | Replaces first match (regex) |
| Split/Join | `split(String)` | `String[]` | ❌ No | O(n) | Regex-based split (costly) |
| Split/Join | `join(CharSequence, ...)` | `String` | ❌ No | O(n) | Best for joining multiple values |
| Concat | `concat(String)` | `String` | ❌ No | O(n) | Throws NPE if argument is null |
| Conversion | `valueOf(any)` | `String` | ❌ No | O(n) | Converts primitives/objects safely |
| Formatting | `format(String, ...)` | `String` | ❌ No | O(n) | Similar to printf (slower but readable) |
| Regex | `matches(String)` | `boolean` | ❌ No | O(n) | Full-string regex match |
| Advanced | `intern()` | `String` | ❌ No | O(n) | Moves/returns string from SCP |
| Utility | `repeat(int)` (Java 11+) | `String` | ❌ No | O(n*k) | Repeats string k times |

---

## ⚠️ Important Rules for Developers

- **Strings are immutable** → every method creates a new object
- Always **store the result**:

# Mutable String
A mutable string allows in-place modification of its character sequence without creating a new object.

In Java, mutability is provided by:

#### 1 StringBuilder

#### 2 StringBuffer

### Why Mutable Strings Exist

String is immutable → inefficient for repeated updates:

    String s = "";
    for (int i = 0; i < 1000; i++) {
        s += i; // creates many temporary objects
    }

👉 Leads to:

Excessive heap allocations

GC pressure

Poor performance

Solution: use a mutable buffer.

same methods

| Method | Return Type | Mutates Object? | Complexity | Key Notes |
|--------|-------------|------------------|------------|-----------|
| append(x) | StringBuilder / StringBuffer | ✅ Yes | Amortized O(1) | Central method; overloads for primitives/objects |
| insert(int, x) | same | ✅ Yes | O(n) | Shifts tail to make space |
| delete(int, int) | same | ✅ Yes | O(n) | Removes range |
| replace(int, int, String) | same | ✅ Yes | O(n) | Range replace |
| reverse() | same | ✅ Yes | O(n) | In-place reversal |
| setCharAt(int, char) | void | ✅ Yes | O(1) | Direct mutation |
| charAt(int) | char | ❌ No | O(1) | Read access |
| length() | int | ❌ No | O(1) | Used characters |
| capacity() | int | ❌ No | O(1) | Allocated buffer |
| ensureCapacity(int) | void | ✅ (may grow) | O(n) when grow | Avoid repeated reallocations |
| toString() | String | ❌ (creates new) | O(n) | Produces immutable `String` |

## What is Capacity?

Capacity = total allocated size of the internal buffer

Length (count) = number of characters currently stored

    StringBuilder sb = new StringBuilder("Hello");
    length() → 5
    capacity() → 21

capacity = initial_length + 16

So:

"Hello" → length = 5  
capacity = 5 + 16 = 21

## Final vs Immutability (Deep, Precise Distinction)

🔹 Primitive

    final int x = 10;
    x = 20; // ❌ compile-time error

👉 Value itself cannot change

🔹 Reference Type

    final StringBuilder sb = new StringBuilder("Hello");
    sb.append(" World");   // ✅ allowed
    sb = new StringBuilder(); // ❌ not allowed

👉 Key Insight:

Reference is fixed

Object can still change

### Immutability — What It Really Means

An object is immutable if its internal state cannot change after creation.

🔍 Example (String)

    String s = "Hello";
    s.concat(" World");

👉 New object created → original unchanged