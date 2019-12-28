# Description
Your task is to make a function that can take any non-negative integer as a argument and return it with its digits in descending order. Essentially, rearrange the digits to create the highest possible number.


# Examples
```
Input: 21445 Output: 54421

Input: 145263 Output: 654321

Input: 123456789 Output: 987654321
```

# Solution
```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.stream.Collectors;

public class DescendingOrder {
    public static int sortDesc(final int num) {
        return Integer.valueOf(Arrays
              .stream(String.valueOf(num).split(""))
              .sorted(Comparator.reverseOrder())
              .collect(Collectors.joining()));
    }
}

```
```java
import java.util.Arrays;
import java.util.Collections;

public class DescendingOrder {
    public static int sortDesc(final int num) {
        String[] array = String.valueOf(num).split("");
        Arrays.sort(array, Collections.reverseOrder());
        return Integer.valueOf(String.join("", array));
    }
}
```

```java
import java.util.Comparator;
import java.util.stream.Collectors;

public class DescendingOrder {
    public static int sortDesc(final int num) {
        return Integer.parseInt(String.valueOf(num)
                                      .chars()
                                      .mapToObj(i -> String.valueOf(Character.getNumericValue(i)))
                                      .sorted(Comparator.reverseOrder())
                                      .collect(Collectors.joining()));
    }
}
```
