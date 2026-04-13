# Lambda Expression
Lambda Expression -> a short, anonymous way to represent a function (usually where a functional interface is expected).

Introduced in Java 8 (2014).

works with only functional interface.

It allows passing behavior (functions) as data.

Major reason for functional programming support in Java.

**Syntax** `(parameters) -> { body }`

* **Simple Lambda — No parameters:**
 `() -> System.out.println("Hello World")`


* **Lambda with One Parameter:**
`name -> System.out.println("Hello, " + name)`.

     (no parentheses needed for a single parameter)



* **Lambda with Multiple Parameters:**

      (a, b) -> a + b
* **Lambda with Type Declaration (Optional):**

        (int a, int b) -> a + b

* **Multi-line Body (Needs {} and return):**

        (int a, int b) -> {
        int sum = a + b;
        return sum;
        }

since it is an expression it is mandatory to use semicolon at the end of the expression.
      
    Test add=(a,b)->{return a+b;};

examples:- LambdaExpression/LambdaExample.java

```java
package Java8.LambdaExpression;

import java.util.Arrays;

public class LambdaExample {
    public static void main(String[] args) {
        //lambda expression
        Test add=(a,b)->{return a+b;};
        Test sub=(a,b)->a-b;
        Test mul=(a,b)->a*b;
        System.out.println("add "+add.action(10,29)); //calling the method.
        System.out.println(sub.action(100,29));
        System.out.println(mul.action(10,29));



        //example 2.
        Integer[] arr={32,23,453,123,45,3};
        Arrays.sort(arr,(a, b)->a-b); // implementation of comparator into lambda expression form..
        System.out.println(Arrays.toString(arr));

    }
}

//functional interface -- having only one abstract method and n no. of default and static can be present or may not.
interface Test{
    int action(int a,int b);
}
```