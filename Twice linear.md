# 4ku
# Description:
Consider a sequence u where u is defined as follows:

The number u(0) = 1 is the first one in u.  
For each x in u, then y = 2 * x + 1 and z = 3 * x + 1 must be in u too.  
There are no other numbers in u.

Ex:u = [1, 3, 4, 7, 9, 10, 13, 15, 19, 21, 22, 27, ...]

1 gives 3 and 4, then 3 gives 7 and 10, 4 gives 9 and 13, then 7 gives 15 and 22 and so on...

# Task:
Given parameter n the function dbl_linear (or dblLinear...) returns the element u(n) of the ordered (with <) sequence u (so, there are no duplicates).

# Example:
dbl_linear(10) should return 22

# Note:
Focus attention on efficiency

# Solutions
```java
import java.util.*;
class DoubleLinear {
    
    public static int dblLinear(int n) {
        int[] res = new int[n+1];
        res[0] = 1;
        int xi=0, yi=0;
        for(int i=1;i<=n;i++){
            res[i] = Math.min(2*res[xi]+1,3*res[yi]+1);
            if(res[i]==2*res[xi]+1)  xi++;
            if(res[i]==3*res[yi]+1)  yi++;
        }
        return res[n];
    }
}
```
```java
import java.util.*;

class DoubleLinear {
    
    public static int dblLinear(int n) {
        if (n == 0) return 1;
        SortedSet<Integer> u = new TreeSet<>();
        u.add(1);
        for(int i=0; i<n; i++) {
            int x = u.first();
            u.add(x*2+1);
            u.add(x*3+1);
            u.remove(x);
        }
        return u.first();
    }
    
}
```
