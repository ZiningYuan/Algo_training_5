# Basics
https://programmercarl.com/数组理论基础.html

# Binary Search
Leetcode: [704 Binary Search](https://leetcode.com/problems/binary-search/)

### Attempts
**Approach**: counter and loop, split by half and counter +=1, try to find the exact match of the target with the remaining half. <br>
**What went wrong**: Very complicated loops, don't know how to add the original length to get the correct index. <br> Messed up when defining the range (open or closed).

### Solutions
这道题目的前提是数组为有序数组，同时题目还强调数组中无重复元素，因为一旦有重复元素，使用二分查找法返回的元素下标可能不是唯一的，这些都是使用二分法的前提条件。
二分查找涉及的很多的边界条件，逻辑比较简单，但就是写不好。例如到底是 while(left < right) 还是 while(left <= right)，到底是right = middle呢，还是要right = middle - 1呢？
大家写二分法经常写乱，主要是因为对区间的定义没有想清楚，区间的定义就是不变量。要在二分查找的过程中，保持不变量，就是在while寻找中每一次边界的处理都要坚持根据区间的定义来操作，这就是循环不变量规则。
写二分法，区间的定义一般为两种，左闭右闭即[left, right]，或者左闭右开即[left, right)。

### [left, right]
* while (left <= right) 要使用 <= ，因为left == right是有意义的，所以使用 <=
* if (nums[middle] > target) right 要赋值为 middle - 1，因为当前这个nums[middle]一定不是target，那么接下来要查找的左区间结束下标位置就是 middle - 1

```
class Solution:
  def search(self, nums: List[int], target: int) -> int:
      left = 0 
      right = len(nums)-1
      while left <= right:
          mid = int(left + ((right - left)/2))
          if nums[mid] > target:
              right  = mid - 1
          elif nums[mid] < target:
              left = mid + 1
          else:
              return mid
      return -1
```

Time Complexity：O(log n); Space Complexity：O(1)

### [left, right)
* while (left < right)，这里使用 < ,因为left == right在区间[left, right)是没有意义的
* if (nums[middle] > target) right 更新为 middle，因为当前nums[middle]不等于target，去左区间继续寻找，而寻找区间是左闭右开区间，所以right更新为middle，即：下一个查询区间不会去比较nums[middle]


Time Complexity：O(log n); Space Complexity：O(1)


### Ref:https://programmercarl.com/0704.二分查找.html#_704-二分查找




