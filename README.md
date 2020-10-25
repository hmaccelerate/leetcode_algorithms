# leetcode algorithms
## Methodology

策略

- ​	第一遍：按照leetcode 的tag 类型进行刷题，由易到难，频率高到频率低，每个pattern或者类型至少刷10刀典型的题目，然后进行总结。
  - 做该类型的第一个题目，直接看答案，然后去理解套路和数据结构
  - 之后的题目，可以尝试第一个题目的套路解题，超过10分钟，直接看答案
- ​	第二遍：随机刷题
- 题目分类
  - 按照leetcode的tag进行分类
  - tag细分
    - 这个大分类底下，根据网上的总结，再细分这个tag的类型；
    - 选择做LeetCode submission建议的关联题目
- 题解
  - 建议去中文力扣网站搜索答案，然后再看英文答案
  - [LeetCode Solutions: A Record of My Problem Solving Journey](https://github.com/azl397985856/leetcode)

步骤

1. 先自己分析问题，思考一下解题思路。
   - 做相关类型的第一个题目，直接看答案，然后去理解套路和数据结构
   - 之后的题目，可以尝试第一个题目的套路解题
     - 5分钟后，套路不适用，就直接看答案。
     - 如果有部分思路，可以尝试写伪代码，但是过了5分钟，如果解不出来，就记下在哪里卡住了，难点在哪，看答案
2. 看答案
   - 如果对应的题目有`Solution`，就看`Solution`，没有的话就点`Discuss`，按`Most Votes`排序，看排名最高的解法。难以理解一些文章的细节时，去搜搜相关视频，视频的讲解可以帮助理解。
   - 如何理解代码具体细节？
     - 将具体的用例输入，按照代码过程计算各个变量并观察
   - 对比一下自己的解法与最优的解法的差别，总结一下为什么没想起来，记录下来这个算法的关键点。
3. 关掉别人的代码，开始自己Coding，Debug，Submit。
4. ps: 想到了思路，但是感觉思路不对，可以直接看别人思路，进行比对

思路

- 分析问题
  - 根据题干描述，分析这道题的pattern
    - 这道题能拆解为子问题，说明应该考虑递归
      - DFS
      - BFS
    - 这道题求最值，说明应该考虑贪心算法
    - 这道题求最值，并且有重复子问题，有最小优化结构，有状态转移，使用DP
    - 这道题的输入数据是数组，可以考虑对它进行排序
  - 根据这道题的pattern，分析要使用什么数据结构来存储中间数据和结果数据
    - DFS：stack
    - BFS：Queue
    - DP：数组(一维或者二维)
  - 写伪代码的时候，要学会构造不同的输入来模拟不同的情况或者边界条件，这样你才能写出考虑周全的代码

LeetCode 上的题大致分为三种类型：

- 考察数据结构，比如链表、栈、队列、哈希表、图、Trie、二叉树等
- 考察基础算法，比如深度优先、广度优先、二分查找、递归等
- 考察基本算法思想：递归、分治、回溯搜索、贪心、动态规划等

## Recording daily algorithms

|    Day     |                        Topic                        |
| :--------: | :-------------------------------------------------: |
| 2020/02/03 |                Valid Perfect Square                 |
| 2020/02/04 | Search Insert Position/Guess Number Higher or Lower |
| 2020/02/06 |                                                     |
|            |                                                     |
|            |                                                     |

## Template

## []()

### Analysis

- Data structure
- Complexity Analysis

### Solution

```java

```

### Reference

[]()

## Frequently used Git commands

- ​	git add .
- ​	git commit -m "update two pointers"
- ​	git push

## References

- [大家都是如何刷 LeetCode 的？](https://www.zhihu.com/question/280279208 )f
- [如何最快速的刷题（官方网站：cspiration.com）](https://www.youtube.com/watch?v=HlIu_kf_KH0)
  - 第一遍：直接看答案，学习数据结构，学习算法
  - 第二遍：自己想，背经典算法，背一些模板题，经典题
  - 第三遍：熟悉所以题目，大部分都要写出来了
  - 遍数：一遍不是一题一次，而是指这个一遍在这个半个小时，反复做了很多次

阿里 工作2年对应 p6 等级要求  2万3左右    1年13个月 

361制度   绩效 小组 10个左右  挑取一个人没有奖金，6个人 3个月，3个人 6个月：分你股份奖金

应届生 A评分：算法/系统设计/java/岗位相关知识 