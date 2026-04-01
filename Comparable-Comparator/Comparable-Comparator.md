# Comparable
Comparable is an interface defining a strategy of comparing an object with other objects of the same type. This is called the class’s **“natural ordering.”**

In order to be able to sort, we must define our Player object as comparable by i**mplementing the Comparable interface**:


### Example:
Let’s use an example of a football team, where we want to line up the players by their rankings.

We’ll start by creating a simple Player class with natural ordering:

Next, we’ll create a PlayerSorter class to create our collection, and attempt to sort it using Collections.sort:

```java

public class Player implements Comparable<Player> {

    private int ranking;
    private String name;
    private int age;

    @Override
    public int compareTo(Player otherPlayer) {
        return Integer.compare(getRanking(), otherPlayer.getRanking());
    }

}
```
The sorting order is decided by the return value of the compareTo() method. 

The Integer.compare(x, y) 

* returns -1 if x is less than y,

 * 0 if they’re equal, 
 
 * and 1 otherwise.



```java
public static void main(String[] args) {
    List<Player> footballTeam = new ArrayList<>();
    Player player1 = new Player(59, "John", 20);
    Player player2 = new Player(67, "Roger", 22);
    Player player3 = new Player(45, "Steven", 24);
    footballTeam.add(player1);
    footballTeam.add(player2);
    footballTeam.add(player3);

    System.out.println("Before Sorting : " + footballTeam);
    Collections.sort(footballTeam);
    System.out.println("After Sorting : " + footballTeam);
}
```

# Comparator
The Comparator interface defines a compare(arg1, arg2) method with two arguments that represent compared objects, and works similarly to the Comparable.compareTo() method.

 ## Creating Comparators
To create a Comparator, we have to implement the Comparator interface.

**we’ll create a Comparator to use the ranking attribute of Player to sort the players:**
```java
public class PlayerRankingComparator implements Comparator<Player> {

    @Override
    public int compare(Player firstPlayer, Player secondPlayer) {
       return Integer.compare(firstPlayer.getRanking(), secondPlayer.getRanking());
    }

}
```

**to use age to sort players**
```java
public class PlayerAgeComparator implements Comparator<Player> {

    @Override
    public int compare(Player firstPlayer, Player secondPlayer) {
       return Integer.compare(firstPlayer.getAge(), secondPlayer.getAge());
    }

}
```

#### Using this approach, we can override the natural ordering:
```java
PlayerRankingComparator playerComparator = new PlayerRankingComparator();
Collections.sort(footballTeam, playerComparator);
```

## Java 8 Comparators
Java 8 provides new ways of defining Comparators by using lambda expressions, and the comparing() static factory method.

Let’s see a quick example of how to use a lambda expression to create a Comparator:

```java
Comparator byRanking = 
  (Player player1, Player player2) -> Integer.compare(player1.getRanking(), player2.getRanking());
  ```
The Comparator.comparing method takes a method calculating the property that will be used for comparing items, and returns a matching Comparator instance:

```java
Comparator<Player> byRanking = Comparator.comparing(Player::getRanking);
Comparator<Player> byAge = Comparator.comparing(Player::getAge);
  ```

## Avoiding the Subtraction Trick

Integer.compare() method to compare two integers. However, one might argue that we should use this clever one-liner instead:

    Comparator<Player> comparator = (p1, p2) -> p1.getRanking() - p2.getRanking();

Although it’s much more concise than other solutions, it can be a victim of integer overflows in Java:
```java

Player player1 = new Player(59, "John", Integer.MAX_VALUE);
Player player2 = new Player(67, "Roger", -1);

List<Player> players = Arrays.asList(player1, player2);
players.sort(comparator);
```

Since -1 is much less than the Integer.MAX_VALUE, “Roger” should come before “John” in the sorted collection.

 However, due to integer overflow, the “Integer.MAX_VALUE – (-1)” will be less than zero.

 So based on the Comparator/Comparable contract, the Integer.MAX_VALUE is less than -1, which is obviously incorrect.

Therefore, despite what we expected, “John” comes before “Roger” in the sorted collection: