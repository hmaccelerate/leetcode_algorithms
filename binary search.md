## 367. Valid Perfect Square

### Description

Given a positive integer *num*, write a function which returns True if *num* is a perfect square else False.

**Note:** **Do not** use any built-in library function such as `sqrt`.

### **Example 1:**

```
Input: 16
Output: true
```

**Example 2:**

```
Input: 14
Output: false
```



### Resolution:

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
            // if(num/mid==mid){return true;} 
            // else if(num/mid>mid){start=mid+1;} 
            // else{end=mid-1;} 
    }
        // if(num/start==start) 
        //     return true;
        // else if(num/end==end) 
        //     return true;
        // else 
            return false;
}}
```

