# Functional Interfaces
A functional interface is an interface that contains only one abstract method (SAM — Single Abstract Method). 

The presence of a single abstract method ensures that the interface can be used with lambda expressions. In other words, functional interfaces serve as the target type for lambda expressions and method references.

There can be any no. of default and static methods in functional Interfaces.


## Predefined Functional Interfaces
There are various types of predefined functional interfaces.

1. **Predicate**
2. **Consumer**
3. **Supplier**
4. **Function**
5. **BiFunction**
6. **BiPredicate**
etc...

### 1. Predicate <<T>T>
Predicate represents a boolean-valued function that takes one argument and returns a boolean result.
```
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T t);
}
```
**Methods**
* test ( ) -> the test method evaluates the predicate with this argument and returns a boolean result.
* and ( ) -> Returns a composed predicate when two predicates are TRUE.
* or ( ) -> Returns a composed predicate when one of the predicates is TRUE
* negate ( ) -> Returns a predicate that represents the logical negation of this predicate.


### 2. Function < T , R >
part of the java.util.function package 

introduced since Java 8, to implement functional programming in Java.

It represents a function that takes in one argument and produces a result. Hence, this functional interface takes in 2 generics, namely as follows:

* T: denotes the type of the input argument
* R: denotes the return type of the function

**Methods**
1. R apply ( T ) --> executes the lambda function given to define Function. T is type of input parameter and R is return type.
2. andThen ( ) --> execute another Function<T,R> after the caller function.
3. compose ( ) --> execute first the Passed Function<T,R> after that caller Function<T,R>.
4. identity ( ) ---> just return the passed value.

### 3. Consumer <T>
It represents a function which takes in one argument and produces a result. 
However, these kind of functions don't return any value.

**Methods**
1. accept (T) --> takes a value and perform operation on that value.
2. andThen ( ) --> It returns a composed Consumer wherein the parameterized Consumer will be executed after the first one. 

### 4. Supplier <T>
It represents a function which does not take in any argument but produces a value of type T. 

**Methods**
* T get ( ) --> returns a value of type T.

```java
package Java8.Functional_Interface;

import java.util.Arrays;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;

public class PredefinedFunctionalinterfacesExample {

    public static void main(String[] args) {
        // Predicate

        Predicate<Integer> predicate=x->x%2==0;

        List<Integer> list= Arrays.asList(1,12,23,43,45,56);
        list.stream().filter(predicate).forEach(System.out::println);

        // OR

        System.out.println("Predicate 24 is even: "+predicate.test(24));


        // Function

        Function<String,Integer> function=str->str.trim().length();

        Function<String,String> function2=str->str.toLowerCase();
        System.out.println("Function : "+function.apply("   ram is a  "));


        System.out.println(function.compose(function2).apply("      hello"));     //  compose

        // Consumer

        Consumer<Integer> consumer=System.out::println;
        consumer.accept(309909);

        //Supplier

        Supplier<Double> supplier =()->Math.random();
        Supplier<String> supplier2=()->"hey you";

        System.out.println(supplier.get());
        System.out.println(supplier2.equals("are awesome"));
        





    }
}
```