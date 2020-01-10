# Description
Once upon a time, on a way through the old wild mountainous west,…
… a man was given directions to go from one point to another. The directions were "NORTH", "SOUTH", "WEST", "EAST". Clearly "NORTH" and "SOUTH" are opposite, "WEST" and "EAST" too.

Going to one direction and coming back the opposite direction right away is a needless effort. Since this is the wild west, with dreadfull weather and not much water, it's important to save yourself some energy, otherwise you might die of thirst!

How I crossed a mountain desert the smart way.
The directions given to the man are, for example, the following (depending on the language):

`["NORTH", "SOUTH", "SOUTH", "EAST", "WEST", "NORTH", "WEST"].`

You can immediatly see that going "NORTH" and immediately "SOUTH" is not reasonable, better stay to the same place! So the task is to give to the man a simplified version of the plan. A better plan in this case is simply:

`["WEST"]`

Other examples:
In `["NORTH", "SOUTH", "EAST", "WEST"]`, the direction `"NORTH"` + `"SOUTH"` is going north and coming back right away.

The path becomes `["EAST", "WEST"]`, now `"EAST"` and `"WEST" `annihilate each other, therefore, the final result is `[]` (nil in Clojure).

In ` ["NORTH", "EAST", "WEST", "SOUTH", "WEST", "WEST"]`, `"NORTH"` and `"SOUTH"` are not directly opposite but they become directly opposite after the reduction of "EAST" and "WEST" so the whole path is reducible to ["WEST", "WEST"].

# Task
Write a function dirReduc which will take an array of strings and returns an array of strings with the needless directions removed (W<->E or S<->N side by side).

The Haskell version takes a list of directions with data Direction = North | East | West | South.
The Clojure version returns nil when the path is reduced to nothing.
The Rust version takes a slice of enum Direction {NORTH, SOUTH, EAST, WEST}.
See more examples in "Sample Tests:"

# Notes
Not all paths can be made simpler. The path ["NORTH", "WEST", "SOUTH", "EAST"] is not reducible. "NORTH" and "WEST", "WEST" and "SOUTH", "SOUTH" and "EAST" are not directly opposite of each other and can't become such. Hence the result path is itself : ["NORTH", "WEST", "SOUTH", "EAST"].
if you want to translate, please ask before translating.
# Tests
```java
@Test
  public void testSimpleDirReduc() {        
    assertArrayEquals("\"NORTH\", \"SOUTH\", \"SOUTH\", \"EAST\", \"WEST\", \"NORTH\", \"WEST\"",
          new String[]{"WEST"},
          DirReduction.dirReduc(new String[]{"NORTH", "SOUTH", "SOUTH", "EAST", "WEST", "NORTH", "WEST"}));
    assertArrayEquals("\"NORTH\",\"SOUTH\",\"SOUTH\",\"EAST\",\"WEST\",\"NORTH\"",
          new String[]{},
          DirReduction.dirReduc(new String[]{"NORTH","SOUTH","SOUTH","EAST","WEST","NORTH"}));
  }
```
# Solutions
```java
import java.util.Stack;

public class DirReduction {
    public static String[] dirReduc(String[] arr) {
        final Stack<String> stack = new Stack<>();

        for (final String direction : arr) {
            final String lastElement = stack.size() > 0 ? stack.lastElement() : null;

            switch(direction) {
                case "NORTH": if ("SOUTH".equals(lastElement)) { stack.pop(); } else { stack.push(direction); } break;
                case "SOUTH": if ("NORTH".equals(lastElement)) { stack.pop(); } else { stack.push(direction); } break;
                case "EAST":  if ("WEST".equals(lastElement)) { stack.pop(); } else { stack.push(direction); } break;
                case "WEST":  if ("EAST".equals(lastElement)) { stack.pop(); } else { stack.push(direction); } break;
            }
        }
        return stack.stream().toArray(String[]::new);
    }
}
```
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class DirReduction {
    public static String[] dirReduc(String[] arr) {
      List<String> dirs = new ArrayList<String>(Arrays.asList(arr));
      for (int i = 0; i + 1 < dirs.size(); i++) {
        if ("NORTHSOUTH,SOUTHNORTH,EASTWEST,WESTEAST".contains(dirs.get(i) + dirs.get(i + 1))) {
          dirs.remove(i + 1);
          dirs.remove(i);
          i = -1;
        }
      }
      return dirs.toArray(new String[dirs.size()]);
    }
}
```
```java
import java.util.*;

public class DirReduction {

  private static final Map<String, Integer> dirs = new HashMap<>();
  static {
    dirs.put("NORTH", 1);
    dirs.put("SOUTH", -1);
    dirs.put("EAST", 2);
    dirs.put("WEST", -2);
  }
  
  public static String[] dirReduc(String[] a) {
    Deque<String> list = new ArrayDeque<>();
    for (String d: a) {
      Integer c = dirs.get(d);
      Integer p = dirs.get(list.peekLast());
      if (p == null || p + c != 0) list.addLast(d);
      else list.removeLast();
    }
    return list.toArray(new String[list.size()]);
  }
}
```
```java
public class DirReduction {
    public static final String NORTH_SOUTH = "NORTH SOUTH ";
    public static final String WEST_EAST = "WEST EAST ";
    public static final String SOUTH_NORTH = "SOUTH NORTH ";
    public static final String EAST_WEST = "EAST WEST ";
    public static String[] dirReduc(String[] arr) {
        String s = "";
        for (String string: arr) s += string + " ";
        for (int i = 0; i < arr.length; i++){
          s = s.contains(NORTH_SOUTH) ? s.replace(NORTH_SOUTH, "") : s;
          s = s.contains(WEST_EAST)   ? s.replace(WEST_EAST, "")   : s;
          s = s.contains(SOUTH_NORTH) ? s.replace(SOUTH_NORTH, "") : s;
          s = s.contains(EAST_WEST)   ? s.replace(EAST_WEST, "")   : s;      
        }
        return s.isEmpty() ? new String[] {} : s.split(" ");
    }
}
```
