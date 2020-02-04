## [367. Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/)

### Analysis

#### Binary Search

1. When num<2, it always return 1;
2. Initializing variables, using long type not int type
3. For  num>2 the square root a , a is always less than num/2 and greater than 1: 1 < x <<num/2
4. Set the left boundary to 2, and the right boundary to num / 2.
5. While using  (start<=end), use start=mid+1 and end=mid-1, not start=mid and end=mid

### Solution:

```java
class Solution {
    public boolean isPerfectSquare(int num) {
        if(num<2){return true;} 
        long start=2,end=num/2,guessSquared,mid;
        while(start<=end){
            mid = start+(end-start)/2;
            guessSquared = mid * mid;
            if(guessSquared == num) return true;
            else if(guessSquared < num){start=mid+1;} 
            else {end=mid-1;} 
    }
            return false;
}}
```