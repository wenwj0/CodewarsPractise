# Description
Complete the method/function so that it converts dash/underscore delimited words into camel casing. The first word within the output should be capitalized only if the original word was capitalized (known as Upper Camel Case, also often referred to as Pascal case).

# Examples
```
toCamelCase("the-stealth-warrior"); // returns "theStealthWarrior"

toCamelCase("The_Stealth_Warrior"); // returns "TheStealthWarrior"

```
# Solution
```java
import java.lang.StringBuilder;
class Solution{

  static String toCamelCase(String s){
    String[] words = s.split("[_\\-]");
    StringBuilder sb = new StringBuilder();
    for(String word:words)
        sb.append(word.substring(0,1).toUpperCase()).append(word.substring(1).toLowerCase());
    return sb.toString();
  }
}
```

```
import java.util.Arrays;

class Solution{

  static String toCamelCase(String str){
    String[] words = str.split("[-_]");
    return Arrays.stream(words, 1, words.length)
            .map(s -> s.substring(0, 1).toUpperCase() + s.substring(1))
            .reduce(words[0], String::concat);
  }
}
```
```

import java.util.regex.Matcher;
import java.util.regex.Pattern;
import java.lang.StringBuilder;

class Solution{

  static String toCamelCase(String s){
    Matcher m = Pattern.compile("[_|-](\\w)").matcher(s);
    StringBuffer sb = new StringBuffer();
    while (m.find()) {
        m.appendReplacement(sb, m.group(1).toUpperCase());
    }
    return m.appendTail(sb).toString();
  }
}
```