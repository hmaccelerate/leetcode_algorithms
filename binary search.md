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

## [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)

### Analysis

#### Binary Search

1. When nums.length == 0, return 0;
2. you have to compare with nums[start] and nums[end], and decide what you should return

### Solution:

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        if(nums.length == 0)
            return 0;
        int start=0, end=nums.length-1;
        while(start+1<end){
            int mid = start+(end-start)/2;
            if(nums[mid]==target)
                return mid;
            else if(nums[mid]>target)
                end=mid;
            else
                start=mid;
        }
        if(nums[start]<target&&target<nums[end])
            return start+1;
        else if(nums[start]>target)
            return start;
        else if(nums[end]<target)
            return end+1;
        else if(nums[end]==target)
            return end;
        else
            return start;
        
    }
}
```

## [374. Guess Number Higher or Lower](https://leetcode.com/problems/guess-number-higher-or-lower/)

### Analysis

#### Binary Search

We can apply Binary Search to find the given number. We start with the mid number. We pass that number to the guess function. If it returns a -1, it implies that the guessed number is larger than the required one. Thus, we use Binary Search for numbers lower than itself. Similarly, if it returns a 1, we use Binary Search for numbers higher than itself.

```java
/* The guess API is defined in the parent class GuessGame.
   @param num, your guess
   @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
      int guess(int num); */

public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int start=1, end= n;
        while(start+1<end){
            int mid =start+(end-start)/2;
            if(guess(mid)==0)
                return mid;
            else if(guess(mid)==-1)
                end=mid;
            else 
                start=mid;
        }
        if(guess(start)==0)
            return start;
        else
            return end;
        
    }
}
```



## [744. Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/)

### Analysis

1. In the while loop, we must deal with comparison between target, letters[mid], there are there judgement: =,<,>. 
2. we must deal with candidates after exit the loop, and candidates ' numbers are associated with while(condition).

#### Binary Search

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int start =0 ;
        int end = letters.length-1;
        while(start+1<end){
            int mid = start+(end-start)/2;
            if(letters[mid]<=target) start =mid;
            else end =mid;
        }
        if(letters[start]>target)
            return letters[start];
        else if(letters[end]>target)
            return letters[end];
        return letters[0];
        // return letters[start%letters.length];
    }
}
```



