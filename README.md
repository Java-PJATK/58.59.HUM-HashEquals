# HUM-HashEquals
58 59 HUM-HashEqua1s/Person.java HUM-HashEqua1s/AHash.java 95 96

Cont. from [57.AAR-EquToString](https://github.com/Java-PJATK/57.AAR-EquToString/)

The next example illustrates the effect of overriding the hashCode method:

## Listing 58 HUM-HashEquals/Person.java

```java
// AXW-ScanExcept/ScanExcept.java
 
import java.io.IOException;
import java.nio.file.Paths;
import java.util.Scanner;

public class ScanExcept {
    public static void main (String[] args) {
          // no checked exception here
        @SuppressWarnings("resource")
        Scanner console = new Scanner(System.in);

        Scanner scfile = null;
        try {
            scfile = new Scanner(Paths.get("file.txt"), "UTF-8");
            int count = 0;
            while (scfile.hasNextLine())
                System.out.printf("%2d: %s%n", ++count,
                                  scfile.nextLine());
        } catch(IOException e) {
            System.out.println("Exception: " + e +
                               "\n**** Now the stack:");
            e.printStackTrace();
            System.out.println("**** CONTINUING...");
        } finally {
            System.out.println("FINALLY executed");
        }

        System.out.println("Enter anything...");
        String s = console.next();
        System.out.println("Read from console: " + s);

          // Active only when run with '-ea' option!
          // Should be used for debugging only.
          // No side effects allowed!
        assert scfile != null : "apparently no file";

        if (scfile != null) scfile.close();
    }
}
```
with `main` as below

## Listing 59 HUM-HashEquals/AHash.java

```java
// HUM-HashEquals/AHash.java
 
import java.util.HashMap;
import java.util.Map;

public class AHash {
    public static void main(String[] args) {
        Map<Person,String> map = new HashMap<>();

        map.put(new Person("Sue","123456"),"Sue");

          // new object, but should be equivalent to
          // the one which has been put into the map
        Person sue = new Person("Sue","123456");

        if (map.containsKey(sue))
            System.out.println(sue + " has been found");
        else
            System.out.println(sue + " has NOT been found");
    }
}
```

As can be easily checked, the program will print

```
      Sue(123456) has been found
```

only when both `hashCode` and `equals` are consistently overridden in the class of keys of the map (i.e., `Person`).

Next [Section 11 Exceptions 60.AXW-ScanExcept](https://github.com/Java-PJATK/60.AXW-ScanExcept)
