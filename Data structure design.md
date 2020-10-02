## [ First Unique Number](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/3313/)

### Analysis

In my approach, I used queue and hashmap to design this data structure. For add method, I would store data into queue and  hashmap. For hashmap, key is number, value is count. if the element exists, increment the count in map alone.  if the element is not present then add it to the queue, put this element in the map and the count is 1

 For showFirstUnique method, I will use for loop to iterate all data from queue, and check count from hashmap. when count equals 1, it will return the value.

- Data structure: Queue/Hashmap
- Complexity Analysis
  - Time: O(n)
  - Space: O(n)

### Solution

```java
class FirstUnique {

   Queue<Integer> queue;
    HashMap<Integer, Integer> map;
    
    public FirstUnique(int[] nums) {
        queue = new LinkedList<Integer>();
        map = new HashMap<>();
        for(int item : nums)
            this.add(item); // adding elements to the queue
    }
    
    public int showFirstUnique() {
        if(!queue.isEmpty()){
            for(Integer q:queue){
                if(map.get(q)==1)
                    return q;
            }
        }
        return -1; // if every element in the queue is repeated
    }
    
    public void add(int key) {
        if(map.containsKey(key))
            map.put(key, map.get(key) + 1); // if the element exists increment the count in map alone
        else{
            queue.add(key); //if the element is not present then add it to the queue
            map.put(key, 1); // put this element in the map and the count is 1
        }
    }
}

/**
 * Your FirstUnique object will be instantiated and called as such:
 * FirstUnique obj = new FirstUnique(nums);
 * int param_1 = obj.showFirstUnique();
 * obj.add(value);
 */
```

### Reference



In my approach, I used 

















