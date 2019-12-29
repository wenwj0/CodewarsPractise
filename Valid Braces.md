# Description:
Write a function that takes a string of braces, and determines if the order of the braces is valid. It should return true if the string is valid, and false if it's invalid.

This Kata is similar to the Valid Parentheses Kata, but introduces new characters: brackets [], and curly braces {}. Thanks to @arnedag for the idea!

All input strings will be nonempty, and will only consist of parentheses, brackets and curly braces: ()[]{}.

What is considered Valid?
A string of braces is considered valid if all braces are matched with the correct brace.

# Examples
```
"(){}[]"   =>  True
"([{}])"   =>  True
"(}"       =>  False
"[(])"     =>  False
"[({})](]" =>  False
```

# Solutions
```java
public class BraceChecker {

  public boolean isValid(String braces) { 
    String b = braces;
    System.out.println(braces);   
    for(int i=0;i<braces.length()/2;i++)
    {
      b = b.replaceAll("\\(\\)", "");
      b = b.replaceAll("\\[\\]", "");
      b = b.replaceAll("\\{\\}", "");
      if(b.length() == 0)
        return true;
    }
    return false;
  }
}
```
```java
import java.util.Stack;

public class BraceChecker {
  
  public boolean isValid(String braces) {
    Stack<Character> s = new Stack<>();
    for (char c : braces.toCharArray()) 
      if (s.size() > 0 && isClosing(s.peek(), c)) s.pop(); 
      else s.push(c);
    return s.size() == 0;
  }
  
  public boolean isClosing(char x, char c) {
    return (x == '{' && c == '}') || (x == '(' && c == ')') || (x == '[' && c == ']');
  }
  
}
```
```java
public class BraceChecker {

  public boolean isValid(String s) {
    String lastIteration = s;
    String currentIteration = s;
    do {
        lastIteration = currentIteration;
        currentIteration = lastIteration.replace("[]" , "").replace("{}", "").replace("()" , "");
    } while(currentIteration.length() < lastIteration.length());
    return currentIteration.equals("");
  }

}
```
```java
public class BraceChecker {
  public boolean isValid(String s) {
    int x = s.length();
    s = s.replaceAll("\\(\\)|\\[\\]|\\{\\}","");
    return s.length() == x ? false : s.length() == 0 || isValid(s);
  }
}
```
