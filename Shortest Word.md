# Description
Simple, given a string of words, return the length of the shortest word(s).

String will never be empty and you do not need to account for different data types.

# Solutions
```java
import java.util.stream.*;
public class Kata {
    public static int findShort(String s) {
        return Stream.of(s.split(" "))
          .mapToInt(String::length)
          .min()
          .getAsInt();
    }
}
```

```java
import java.util.Arrays;

public class Kata {
    public static int findShort(String s) {
        int min = Integer.MAX_VALUE;
        for(String each : s.split(" "))
        {
        if(each.length() < min)
        min = each.length();
        }
         return min;
    }
}
```
