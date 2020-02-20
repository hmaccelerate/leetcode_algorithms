## 总结

1. while(conditional)和candidates
   - while(left<right)：left和right会停止在同一个位置，只有一个candidate讨论
   - while(left+1<right)：left会停在前一个位置，right会停在后一个位置，有两个个candidate讨论
<<<<<<< HEAD
   - while(left+1<=right) or while(left<=right)：right会停在前一个位置，left会停在后一个位置，有两个个candidate讨论
2.  left/right = mid/mid+1/mid-1
=======
   - while(left+1<=right) or while(left<=right)：right会停在前一个位置，left会停在后一个位置，没有candidate讨论
2.  left/right = mid/mid+1/mid-1
   - while(left+1<right)：使用 left/right = mid
3. 边界讨论

## [704. Binary Search](https://leetcode.com/problems/binary-search/)

### Analysis

## [First Position of Target]()

### Analysis

## [Last Position of Target]()

### Analysis

## [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

### Analysis

1. 这题是典型的two times binary search 题目
2. 首先使用第一次binary search 找到first position，然后第二次使用binary search 找到last position

```java
class Solution {
    public int findFirstPosition(int[] nums, int target){
//         int left =0;
//         int right =nums.length-1;
//         //         让mid向最左边的target逼近
//         while(left<right){
//             int mid =(left+right)/2;
//             if(nums[mid]<target){
//                 left = mid+1;
//             }else{
//                 right = mid;
//             }
//         }
        
//         if(nums[left]!=target){
//             return -1;
//         }else{
//             return left;
//         }
        
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                end = mid;
            } else if (nums[mid] < target) {
                start = mid;
                // or start = mid + 1
            } else {
                end = mid;
                // or end = mid - 1
            }
        }
        
        if (nums[start] == target) {
            return start;
        }
        if (nums[end] == target) {
            return end;
        }
        return -1;
    
        
    }
    
     public int findLastPosition(int firstPosition,int[] nums, int target){
//          //         让mid向最右边的target逼近
//         int left = firstPosition;
//         int right= nums.length-1;
//         while(left<right){
//             int mid =(left+right)/2+1;// 为啥这个跟上面不同
//             if(nums[mid]>target){
//                 right = mid-1;
//             }else{
//                 left = mid;
//             }
//         }
        
//         return right;
         int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                start = mid;
            } else if (nums[mid] < target) {
                start = mid;
                // or start = mid + 1
            } else {
                end = mid;
                // or end = mid - 1
            }
        }
        
        
        if (nums[end] == target) {
            return end;
        }
         if (nums[start] == target) {
            return start;
        }
        return -1;
         
    }

    
    public int[] searchRange(int[] nums, int target) {
        int[] result = {-1,-1};
        if(nums==null|| nums.length==0){
            return result;
        }
        
        int firstPosition = findFirstPosition(nums, target);
        if (firstPosition==-1)
            return result;
        result[0]=firstPosition;
        
        int lastPositon = findLastPosition(firstPosition, nums,  target);
        result[1]=lastPositon;
        return result;
}
}
```


>>>>>>> add Two Pointers.md

## 367. Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/)

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



## [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

### Analysis

1. 先判断mid是在rotated array的左边还是右边
2. 判断target是mid左边还是右边
3. while loop没找到，处理start和end这两个candidates

#### Binary Search

```java
class Solution {
    public int search(int[] nums, int target) {
        if(nums==null||nums.length==0){
            return -1;
        }
        int start=0, end= nums.length-1;
        while(start+1<end){
            int mid = start+(end-start)/2;
            if(nums[mid]==target)
                return mid;
            if(nums[mid]>nums[start])
                if(nums[mid]>=target&&target>nums[start])
                    end=mid;
                else
                    start=mid;
            else
                if(nums[mid]<=target&&target<nums[end])
                    start=mid;
                else
                    end=mid;
        }
        if(nums[start]==target)
            return start;
        else if(nums[end]==target)
            return end;
        return -1;
    }
}
```

<<<<<<< HEAD
## [\34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

### Analysis

1. 这题是典型的two times binary search 题目
2. 首先使用第一次binary search 找到first position，然后第二次使用binary search 找到last position

```java
class Solution {
    public int findFirstPosition(int[] nums, int target){
//         int left =0;
//         int right =nums.length-1;
//         //         让mid向最左边的target逼近
//         while(left<right){
//             int mid =(left+right)/2;
//             if(nums[mid]<target){
//                 left = mid+1;
//             }else{
//                 right = mid;
//             }
//         }
        
//         if(nums[left]!=target){
//             return -1;
//         }else{
//             return left;
//         }
        
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                end = mid;
            } else if (nums[mid] < target) {
                start = mid;
                // or start = mid + 1
            } else {
                end = mid;
                // or end = mid - 1
            }
        }
        
        if (nums[start] == target) {
            return start;
        }
        if (nums[end] == target) {
            return end;
        }
        return -1;
    
        
    }
    
     public int findLastPosition(int firstPosition,int[] nums, int target){
//          //         让mid向最右边的target逼近
//         int left = firstPosition;
//         int right= nums.length-1;
//         while(left<right){
//             int mid =(left+right)/2+1;// 为啥这个跟上面不同
//             if(nums[mid]>target){
//                 right = mid-1;
//             }else{
//                 left = mid;
//             }
//         }
        
//         return right;
         int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                start = mid;
            } else if (nums[mid] < target) {
                start = mid;
                // or start = mid + 1
            } else {
                end = mid;
                // or end = mid - 1
            }
        }
        
        
        if (nums[end] == target) {
            return end;
        }
         if (nums[start] == target) {
            return start;
        }
        return -1;
         
    }

    
    public int[] searchRange(int[] nums, int target) {
        int[] result = {-1,-1};
        if(nums==null|| nums.length==0){
            return result;
        }
        
        int firstPosition = findFirstPosition(nums, target);
        if (firstPosition==-1)
            return result;
        result[0]=firstPosition;
        
        int lastPositon = findLastPosition(firstPosition, nums,  target);
        result[1]=lastPositon;
        return result;
}
}
```

=======
>>>>>>> add Two Pointers.md
