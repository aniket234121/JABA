# memory map
**Case 1:** Literal Reuse

    String s1 = "Hello";
    String s2 = "Hello";
Memory:

    SCP:
    "Hello"  ← s1, s2

👉 Only 1 object

**Case 2:** Using new

    String s1 = new String("Hello");
Memory:

    SCP:   "Hello"
    Heap:  new String("Hello") ← s1
👉 2 objects

**Case 3:** Concatenation

    String s = "Hello";
    s = s.concat(" World");
Memory:

    SCP:
    "Hello"
    "Hello World"

    s → "Hello World"

👉 Old object remains (eligible for GC if no reference)

**Case 4:** Compile-Time Optimization

    String s = "Hello" + "World";

👉 JVM converts to:

    String s = "HelloWorld";
Memory:

    SCP:
    "HelloWorld"

👉 Only 1 object

referring to:

    String s = "Hello" + "World";

and asking:

Why NOT 3 objects in SCP?

("Hello", "World", "HelloWorld")

🔥 Core Answer (Short & Precise)

Because this is a compile-time constant expression, the Java compiler performs constant folding and converts it into:

    String s = "HelloWorld";

👉 So only ONE object ("HelloWorld") is created in the String Constant Pool (SCP).

🧠 Step-by-Step Internal Working
✅ Step 1: Compiler Optimization (Constant Folding)

At compile time, the compiler sees:

    "Hello" + "World"

Both are string literals, so it evaluates them before runtime.

👉 Bytecode becomes:

    String s = "HelloWorld";

🗺️ Memory Map (Actual)

    SCP:

    "HelloWorld"  ← s

👉 Only 1 object

## ❗ Why "Hello" and "World" are NOT created?

Because:

They never exist as separate variables

They are only part of a compile-time expression

Compiler does not store intermediate literals unless needed

⚠️ Compare with This Case (Very Important)

    String a = "Hello"; //1st object scp
    String b = "World"; //2nd object scp
    String s = a + b;

🚨 Now what happens?

This is runtime concatenation, NOT compile-time.

🧠 Internal Working:

    StringBuilder temp = new StringBuilder();3rd object heap
    temp.append(a);
    temp.append(b);
    String s = temp.toString(); //4th object heap
so total 4 objects will be created 

**Case 4:** Compile-Time Optimization

    String s = "Hello" + "World";

👉 JVM converts to:

    String s = "HelloWorld";
Memory:

    SCP:
    "HelloWorld"

👉 Only 1 object

### Note
    final String a = "Hello";
    final String b = "World";
    String s = a + b;

only 1 object created 

why?

In Java, a variable of primitive type or type String that is declared as final and initialized with a constant expression is a "constant variable". String literals (like "Hello" and "World") are also constant expressions.