# Identity HashMap

This class implements the Map interface. The Map interface mandates the use of the equals() method on the key comparison. 
However, the IdentityHashMap class violates that contract. 

**Instead, it uses reference equality (==) on key search operations.**

During search operations, HashMap uses the hashCode() method for hashing,

 **whereas IdentityHashMap uses the System.identityHashCode() method.** 

It also uses the linear probe technique of the hashtable for search operations.

The use of reference equality, System.identityHashCode(), and the linear probe technique give the IdentityHashMap class a better performance

```java
import java.util.IdentityHashMap;
import java.util.Map;

public class IdentityExample {
    public static void main(String[] args) {
        Map<String, String> map = new IdentityHashMap<>();

        String a = new String("key");
        String b = new String("key");

        map.put(a, "Value1");
        map.put(b, "Value2");

        System.out.println(map.size()); // Output: 2
    }
}
```
Although a.equals(b) is true, they are different objects in memory, so IdentityHashMap treats them as distinct keys.