[TOC]

## [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/solution/)

### Analysis

#### Two pointers

1. Since the array is already sorted, we can keep two pointers i and j, where i is the slow-runner while j is the fast-runner. As long as nums[i] = nums[j], we increment j to skip the duplicate.

### Solution

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int i=0;
        for(int j=1;j<nums.length;j++){
            if(nums[i]!=nums[j])
                i++;
                nums[i]=nums[j];
        }
        return i+1;
    }
}
```

## [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/)

### Analysis

#### Two pointers

1. J 遇到不是0的停止，然后跟i比对。i如果是0的，那就交换。无论是不是0，i到往前移动一位
2. 由于置换元素的特殊性（等于0），所以其实不需要单独存个tmp
   时间复杂度：O(n);
   空间复杂度：常数2

### Solution

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int i=0,j=0;
        while(j<nums.length){
            if(nums[j]!=0){
                if(nums[i]==0){
                    nums[i]=nums[j];
                    nums[j]=0;
                }
                // if(nums[i]!=0&&nums[j]!=0) 这种写法会让i不是0的情况，停止移动
                // i不是0的情况，也要向前移动
                i++;
            }
            j++;
        }
    }
}
```

## [344. Reverse String](https://leetcode.com/problems/reverse-string/)

### Analysis

- Two pointers

  - Set pointer left at index 0, and pointer right at index `n - 1`, where n is a number of elements in the array.

  - While left < right:

    - Swap `s[left]` and `s[right]`.

    - Move left pointer one step right, and right pointer one step left.

      https://leetcode.com/problems/reverse-string/Figures/344/two.png

- Binary Search

  - Here is an example. Let's implement recursive function `helper` which receives two pointers, left and right, as arguments.
    - Base case: if `left >= right`, do nothing.
    - Otherwise, swap `s[left]` and `s[right]` and call `helper(left + 1, right - 1)`.
  - **Complexity Analysis**
    - Time complexity : O(*N*) time to perform N/2*N*/2 swaps.
    - Space complexity :O(*N*) to keep the recursion stack.

### Solution

- ​	Two pointers

```
class Solution {
    public void reverseString(char[] s) {
        int left=0,right=s.length-1;
        while(left<right){
            char temp = s[left];
            s[left]=s[right];
            s[right]=temp;
            left++;
            right--;
        }
    }
}
```



- Binary Search

```java
class Solution {
    public void reverseString(char[] s) {
        int left= 0,right=s.length-1;
        helper(s,left,right);
    }
    
    public void helper(char[] s,int left, int right){
//         Base: 奇数个元素，最后left==right；偶数个元素，最后left>right;
        if (left >= right) return;
        char temp= s[left];
        s[left]=s[right];
        s[right]=temp;
        helper(s,left+1,right-1);
    }
    
}
```

## [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

### Analysis
- Two pointers（Reverse类）
  - 消除所有标点符号
  - 相向双指针

### Solution

```java
class Solution {
    public boolean isPalindrome(String s) {
        if(s=="")
            return true;
        String s1= s.replaceAll("\\W","").toLowerCase();
        int left=0,right=s1.length()-1;
        while(left<right){
            if(s1.charAt(left)!=s1.charAt(right))
                return false;
            left++;
            right--;
        }
        return true;
    }
}
```

## [1. Two Sum](https://leetcode.com/problems/two-sum/)

### Analysis

- **Complexity Analysis:**
  - Time complexity : O(n)*O*(*n*). We traverse the list containing n*n* elements only once. Each look up in the table costs only O(1)*O*(1) time.
  - Space complexity : O(n)*O*(*n*). The extra space required depends on the number of items stored in the hash table, which stores at most n*n* elements.

### Solution

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result={0,0};
        Map<Integer,Integer> map= new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            if(map.containsKey(target-nums[i])){
                result[0]=i;
                result[1]=map.get(target-nums[i]);
                return result;
            }
            map.put(nums[i],i);
        }
        return result;
        
    }
}
```

## [15. 3Sum](https://leetcode.com/problems/3sum/)

### Analysis

- 数组要先排序
- 使用传统的三指针：最外层一个for loop + 里层的while lopp的left/ right。最外层的代表一个数，里层使用two sum(sorted array)思路，确保三个数加在一起是等于target
- 遇到重复元素，向前移动，否则会出现重复答案
- Complexity Analysis:
  - Time complexity : O(n)*O*(*n*). 
  - Space complexity : O(n)

### Solution

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        if(nums==null || nums.length<3)
            return result;
        Arrays.sort(nums);
        int target=0;
        for(int i=0;i<nums.length;i++){
            if(nums[i]>0)break;
             //遇到重复元素，向前移动，否则会出现重复答案
            if(i>0 && nums[i]==nums[i-1])continue;
            int left=i+1;
            int right=nums.length-1;
            while(left<right){
                if(nums[i]+nums[left]+nums[right]==target){
                    List<Integer> subResult=new ArrayList<Integer>();
                    subResult.add(nums[i]);
                    subResult.add(nums[left]);
                    subResult.add(nums[right]);
                    result.add(subResult);
                    left++;
                    right--;
                    //while loop 确保不越界&&遇到重复元素，向前移动，否则会出现重复答案
                    while (left < right && nums[left] == nums[left - 1]){
                        left ++;
                    }
                    
                    while (left < right && nums[right]  == nums[right + 1]){
                        right --;
                    }
                }
                else if(nums[i]+nums[left]+nums[right]<target){
                    left=left+1;
                }
                else{
                    right=right-1;
                }
            }
        }
        return result;
    }
}
```

## [18. 4Sum](https://leetcode.com/problems/4sum/)

### Analysis

- 数组要先排序

- If you have already read and implement the 3sum and 4sum by using the sorting approach: reduce them into 2sum at the end, you might already got the feeling that, all ksum problem can be divided into two problems:

  - 2sum Problem
  - Reduce K sum problem to K – 1 sum Problem

  Therefore, the ideas is simple and straightforward. We could use recursive to solve this problem. Time complexity is O(N^(K-1)).

- 遇到重复元素，向前移动，否则会出现重复答案

- Complexity Analysis:

  - Time complexity : O(n∧3). 
  - Space complexity : O(n)

### Solution

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        List<List<Integer>> result=ksum( nums,  target,4, 0);
        return result;
    }
    
    public List<List<Integer>> ksum(int[] nums, int target,int k,int start){
        List<List<Integer>> result= new ArrayList<>();
        if(k==2){
            //注意这里left=start
            int left=start,right=nums.length-1;
            while(left<right){
            int sum =nums[left]+nums[right];
            if(sum==target){
                List<Integer> path = new ArrayList<Integer>();
                path.add(nums[left]);
                path.add(nums[right]);
                result.add(path);
                left++;
                right--;    
                while(left<right&&nums[left]==nums[left-1]) left++;
                while(left<right&&nums[right]==nums[right+1]) right--;
            }
            else if(sum<target) left++;
            else right--;}
        }else{
            for(int i=start;i<nums.length-(k-1);i++){
                //start和k的作用：遇到重复元素，向前移动，否则会出现重复答案
                //注意这里的k。如果是4sum，那就从循环元素中减去(k-2)个元素
                if(i>start&&nums[i]==nums[i-1]) continue;
                List<List<Integer>> temp=ksum(nums,target-nums[i],k-1,i+1);
                for(List<Integer> item:temp){
                    item.add(0, nums[i]);
                }
                result.addAll(temp);
            }
        }
        return result;

    }
}
```

## [16. 3Sum Closest](https://leetcode.com/problems/3sum-closest/)

### Analysis

- 数组要先排序

- 遇到重复元素，向前移动，否则会出现重复答案

- Complexity Analysis:

  - Time complexity : O(n∧2). 
  - Space complexity : O(n)

### Solution

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        if (nums == null || nums.length < 3) {
            return -1;
        }
        Arrays.sort(nums);
        int result=nums[0] + nums[1] + nums[2];
        for(int i=0;i<nums.length-2;i++){
            if(i>0&&nums[i]==nums[i-1]) continue;
            // left 应该从i+1开始，避免重复
            int left=i+1, right= nums.length-1;
            while(left<right){
                int sum=nums[i]+nums[left]+nums[right];
                //比较target与sum的差值：求min(target-sum)
                if (Math.abs(target - sum) < Math.abs(target - result)) {
                    result = sum;
                }
               if(target>sum){
                    left++;
               }else{
                   right--;
               }
            
            }
        }
        return result;
        
    }
}
```

## [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/solution/)

### Analysis

- 比较height[i]和height[j]，去找寻最大值，形成最大的面积
- **Complexity Analysis**
  - Time complexity : O(n). Single pass.
  - Space complexity : O(1). Constant space is used.

### Solution

```java
class Solution {
    public int maxArea(int[] height) {
        int i=0,j=height.length-1;
        int result=0;
        while(i<j){
            int temp= (j-i)*Math.min(height[i],height[j]);
            result=Math.max(result,temp);
            if(height[i]<height[j]) i++;
            //if(height[i]<height[j]) 使用这个进行判断会导致time limit exceed，原因是相等的情况没有考虑到
            else j--;
        }
        return result;
        
    }
}
```

## [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

### Analysis

![image-20200226170658993](/photo/image-20200226170658993.png)

- 两个数组的指针从尾端开始扫描，并比较数组大小
- 考虑以下用例，从而构造逻辑
  - nums1所有数字都大于nums2的情况
  - nums1部分数字大于nums2的情况
  - nums1所有数字全小于nums2的情况
- **Complexity Analysis**
  - Time complexity: O(*n*+*m*).
  - Space complexity :O(1).

### Solution

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i=m-1,j=n-1,k=m+n-1;
        while(i>=0&&j>=0){
            if(nums1[i]>nums2[j]) nums1[k--]=nums1[i--];
            else nums1[k--]=nums2[j--];
        }
        while(j>=0) nums1[k--]=nums2[j--];
    }
}
```

### Reference

- [Java 三元运算符](https://www.w3cschool.cn/java/java-ternary-operator.html)
- [System.arraycopy() in Java](https://www.geeksforgeeks.org/system-arraycopy-in-java/)
- [Java Ternary Operator](http://tutorials.jenkov.com/java/ternary-operator.html)

## [\3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

### Analysis

- A **sliding window** is an abstract concept commonly used in array/string problems. A window is a range of elements in the array/string which usually defined by the start and end indices, i.e. [*i*,*j*) (left-closed, right-open). A sliding window is a window "slides" its two boundaries to the certain direction. For example, if we slide [i, j)[*i*,*j*) to the right by 11 element, then it becomes [*i*+1,*j*+1) (left-closed, right-open).
- 滑动窗口算法可以用以解决数组/字符串的子元素问题，它可以将嵌套的循环问题，转换为单循环问题，降低时间复杂度
- keep a hashmap which stores the characters in string as keys and their positions as values, and keep two pointers which define the max substring. move the right pointer to scan through the string , and meanwhile update the hashmap. If the character is already in the hashmap, then move the left pointer to original postition one more step
- **Complexity Analysis**
  - Time complexity: O(*n*).
  - Space complexity (HashMap) : O(min(m, n)). Same as the previous approach.

### Solution

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s.length()==0) return 0;
        Map<Character, Integer> map= new HashMap<>();
        int result=0;
        for(int i=0,j=0;i<s.length();++i){
            if(map.containsKey(s.charAt(i))){
                //move original position one more step
                 j = Math.max(j,map.get(s.charAt(i))+1);
            }
            map.put(s.charAt(i),i);
            result= Math.max(result,i-j+1);
        }
        return result;
    }
}
```

