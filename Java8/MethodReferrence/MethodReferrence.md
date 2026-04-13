# Method Reference

Method Reference provides a shortcut for invoking a function or method. 

It allows you to call a function or method by using its name instead of writing a lambda expression. Method Reference is particularly useful when working with functional interfaces.

* **Can I use Method reference without functional interface??**

No, you cannot use a method reference without a functional interface.

**Types of Method Reference**
1. Static Method Reference
2. Non-Static method Reference
3. Constructor Reference
4. Arbitrary Object Method Reference.

### <div style='color:skyblue'>Static Method Reference<div>
Refer to Static Method of a particular class.
* syntax :-
`ClassName :: MethodName`.

### <div style='color:skyblue'> Non-static Method Reference with Object<div>(Bounded)
reference to an instance method of particular Object.

Syntax :-
`Obj reference variable :: methodName`

### <div style='color:skyblue'>Arbitrary Object Method Reference (Unbounded).</div>


## Bounded vs Unbounded Types
| Type        | Syntax                  | Requires Object? | Description                                                      |
|-------------|-------------------------|------------------|------------------------------------------------------------------|
| **Bound**   | `object::methodName`    | ✅ Yes            | Method is tied (bound) to a specific object.                     |
| **Unbound** | `ClassName::methodName` | ❌ No             | Method is tied to the class, and object is passed at invocation. |



✅ 1. Bound Method Reference

A bound method reference points to an instance method of a specific object (already available).

✅ Syntax:

`instance::instanceMethod`

Think of it as:

The object is already known; you're just referring to the method.

✅ Example:

    class Printer {
    void print(String message) {
    System.out.println(message);
     }
    }

    `Printer printer = new Printer();
     Consumer<String> consumer = printer::print; // Bound reference
     consumer.accept("Hello!"); // Internally calls: printer.print("Hello!")`


✅ 2. Unbound Method Reference
📌 Definition:
An unbound method reference points to an instance method of a class. The object is not yet known — it will be provided when the method is invoked.

✅ Syntax:
`ClassName::instanceMethod`
 Think of it as:

The object is passed later during execution.

✅ Example:

    class Printer {
    void print(String message) {
    System.out.println(message);
      }
     }

    BiConsumer<Printer, String> biConsumer = Printer::print; // Unbound reference
    Printer printer = new Printer();
    biConsumer.accept(printer, "Hi there!"); // Internally calls: printer.print("Hi there!")


###  <div style='color:skyblue'>Constructor Reference<div>
Constructor Introduced in Java 8, constructor references are specialized form of method references which refer to the constructors of a class. Constructor References can be created using the Class Name and the keyword new with the following 
syntax.
* Syntax of Constructor References:
 `<ClassName>::new`.

Constructor Reference Example: If you want reference to the constructor of wrapper class Integer.

then you can write something like this -
* `Supplier<Integer> integerSupplier = Integer::new`