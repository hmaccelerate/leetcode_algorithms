[TOC]



# 0.总结

解决双指针问题三种常用思想：

- 左右指针：需要两个指针，一个指向开头，一个指向末尾，然后向中间遍历，直到满足条件或者两个指针相遇
- 快慢指针：需要两个指针，开始都指向开头，根据条件不同，快指针走得快，慢指针走的慢，直到满足条件或者快指针走到结尾
- 后序指针：常规指针操作是从前向后便利，对于合并和替换类型题，防止之前的数据被覆盖，双指针需从后向前便利
- 记忆口诀：左右指针中间夹，快慢指针走到头，后序指针往回走

# 1.同向双指针

# 数组去重类

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

# Reverse类

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

# 窗口类

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

# 灌水类

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

# 链表类

链表中点

带环链表

# 2.相向双指针

# Two Sum类问题

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

# Partition类

## 总结

#### 算法思路I

> - 使用第一个数组元素作为枢轴点，即为pivot；
> - 使用一个指针去扫描整个数组，凡是小于pivot的全部放到数组左端；
> - 最后讲pivot放到数组中间的位置，pivot左边全部都是小于他的数字，右边反之，最后返回pivot的位置信息；

#### 代码

```java
int partition(vector<int> &nums, int begin, int end)
{
    int pivot = nums[begin];
    int pos = begin;
    for(int i = begin+1; i < end; ++i)
    {
        if(nums[i] <= pivot)
            swap(nums[++pos],nums[i]);
    }
    swap(nums[pos], nums[begin]);
    return pos;
}
```

### 思路II

#### 算法思路

> - 就如快速排序中最常使用的那样，使用两个指针分别从头部和尾部进行扫描，头部遇到大于pivot的数和尾部遇到小于pivot的数进行交换；(binary search那样从两边扫描)
> - 使用了两个指针，效率更高一点；

#### 代码

```java
int partition(vector<int> &nums, int begin, int end)
{
    int pivot = nums[begin];
    while(begin < end)
    {
        while(begin < end && nums[--end] >= pivot);
        nums[begin] = nums[end];
        while(begin < end && nums[++begin] <= pivot);
        nums[end] = nums[begin];
    }
    nums[begin] = pivot;
    return begin;
}
```

PS: partition类题目，有同向双指针的写法，也有相向的写法，目前暂时放在同向分类底下

### Reference

- [Partition算法剖析]([http://haoyuanliu.github.io/2016/12/18/Partition%E7%AE%97%E6%B3%95%E5%89%96%E6%9E%90/](http://haoyuanliu.github.io/2016/12/18/Partition算法剖析/))
- [被忽视的 partition 算法](https://selfboot.cn/2016/09/01/lost_partition/)

## [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/solution/)

### Analysis

#### Approach : Quickselect

- The approach is basically the same as for quicksort. For simplicity let's notice that `k`th largest element is the same as `N - k`th smallest element, hence one could implement `k`th smallest algorithm for this problem.
- First one chooses a pivot, and defines its position in a sorted array in a linear time. This could be done with the help of *partition algorithm*.
- Finally the overall algorithm is quite straightforward :
  - Choose a random pivot.
  - Use a partition algorithm to place the pivot into its perfect position `pos` in the sorted array, move smaller elements to the left of pivot, and larger or equal ones - to the right.
  - Compare `pos` and `N - k` to choose the side of array to proceed recursively.![quickselect](\photo\215_quickselect.png)
- Data structure: Array
- **Complexity Analysis**
  - Time complexity :O(*N*) in the average case, (O(N^2) in the worst case.
  - space complexity: o(1)

### Solution

```java
class Solution {
    int[] nums;
    public int findKthLargest(int[] nums, int k) {
        this.nums=nums;
        int size=nums.length;
        return quickSelect(0,size-1,size-k);

    }
    
        public void swap(int a,int b){
            int temp=this.nums[a];
            this.nums[a]=this.nums[b];
            this.nums[b]=temp;
        }
        public int partition(int left, int right, int pivot_index){
            int pivot= this.nums[pivot_index];
            // move pivot to the end
            swap(right,pivot_index);
            // move items smaller than pivot to the left
            int store_index=left;
            for(int i=left;i<=right;i++){
                if(this.nums[i]<pivot){
                    swap(i,store_index);
                    store_index++;
                }
            }
            swap(store_index,right);
            return store_index;
            
        }
        public int quickSelect(int left,int right,int k_smallest){
            if(left==right) return this.nums[right];
            // select a random pivot_index
            Random random_num=new Random();
            int pivot_index=left+random_num.nextInt(right-left);
            pivot_index= partition(left,right,pivot_index);
            // if pivot_index== k_smallest
            if(k_smallest==pivot_index) return this.nums[pivot_index];
            if(k_smallest<pivot_index) return quickSelect(left,pivot_index-1,k_smallest);
            return quickSelect(pivot_index+1,right,k_smallest);
        }
}
```



## [378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)

### Analysis

### Approach : Quickselect

- Data structure: Array
- **Complexity Analysis**
  - time complexity: o(n)
  - space complexity: o(1)

### Solution

```java
class Solution {
    public void swap(int[][] matrix,int a, int b){
        int rows=matrix.length;
        int temp=matrix[a/rows][a%rows];
        matrix[a/rows][a%rows]=matrix[b/rows][b%rows];
        matrix[b/rows][b%rows]=temp;
    }
            
    
    public int kthHelper(int[][] matrix, int start, int end, int k){
        int rows=matrix.length;
        int left=start;
        int right=end;
        int pivot=matrix[start/rows][start%rows];

        //partition 
        // move pivot to the end
        swap(matrix,right,start);
        // move items smaller than pivot to the left
        int store_index=left;
        for(int i=left;i<=right;i++){
                if(matrix[i/rows][i%rows]<pivot){
                    swap(matrix,i,store_index);
                    store_index++;
                }
            }  
        swap(matrix,store_index,right);
        
        if(store_index+1==k) return matrix[store_index/rows][store_index%rows];
        if(store_index+1<k) return kthHelper(matrix,store_index+1,end,k);
        return  kthHelper(matrix,start,store_index-1,k);
    }
    public int kthSmallest(int[][] matrix, int k) {
        if(matrix==null || matrix.length==0) return -1;
        int rows= matrix.length;
        int cols =matrix[0].length;
        return kthHelper(matrix,0,rows*cols-1,k);
    }
}
```

## [\75. Sort Colors](https://leetcode.com/problems/sort-colors/submissions/)

### Analysis

- Initialise the index of current element to consider : `curr = 0`.
- While `curr <= p2` :
  - If `nums[curr] = 0` : swap `curr`th and `p0`th elements and move both pointers to the right.
  - If `nums[curr] = 2` : swap `curr`th and `p2`th elements. Move pointer `p2` to the left.
  - If `nums[curr] = 1` : move pointer `curr` to the right.![image-20200301165647672](\photo\image-20200301165647672.png)
- Data structure: Array
- **Complexity Analysis**
  - Time complexity :O(*N*) since it's one pass along the array of length N*N*.
  - Space complexity :(1)O(1) since it's a constant space solution.

### Solution

```java
class Solution {
  /*
  Dutch National Flag problem solution.
  */
  public void sortColors(int[] nums) {
      int p0=0,curr=0,p1= nums.length-1;
      while(curr<=p1){
          if(nums[curr]==0){
              swap(nums,curr,p0);
              p0++;
              curr++;
          }else if(nums[curr]==2){
              swap(nums,curr,p1);
              p1--;
              //只有在和 right 换元素时，cur 指针的位置是不动的，因为下一轮还要看一下换过来的元素是不是要放到左边
          }else curr++;
      }
 
  }
    
 public void swap(int[] nums, int a, int b){
     int temp=nums[a];
     nums[a]=nums[b];
     nums[b]=temp;
 }
}
```



# Wiggle Sort类问题

[\280. Wiggle Sort](https://leetcode.com/problems/wiggle-sort/submissions/)

### Analysis

-  reorder it **in-place**  means you should use swap
- 排序数组的规律是 nums[0]<=nums[1]>=nums[2]<=nums[3]>=nums[4]
  - index是奇数的，大于两边的
  - 第一个小于第二个；第二个大于第三个；第三个小于第四个，第四个大于第五个
- Data structure: Array
- **Complexity Analysis**
  - Time complexity : O*(*n).]
  - Space complexity : O(1)*O*(1).

### Solution

```java
class Solution {
    public void wiggleSort(int[] nums) {
        boolean less= true;
        for(int i=0;i<nums.length-1;i++){
            if(less){
                if(nums[i]>nums[i+1]) swap(nums,i,i+1);
            }else{
                if(nums[i]<nums[i+1]) swap(nums,i,i+1);
            }
            less=!less;
        }
        
    }
    public void swap(int[] nums,int a, int b){
        int temp=nums[a];
        nums[a]=nums[b];
        nums[b]=temp;
    }
}
```



# 其他

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

