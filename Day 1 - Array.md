# Day 1 Array

## 1. Binary Search
204. Binary search $\color{green}{\textsf{EASY}}$

> Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.
You must write an algorithm with `O(log n)` runtime complexity.

```
//204. Binary Search
class Solution:
	def search(self, nums: List[int], target:int) -> int:
		n = len(nums)
		left, right = 0, n-1 # index -> interval
		while left <= right:
			mid = (left + right)//2
			if target < nums[mid]:
				right = mid - 1
			elif target > nums[mid]:
				left = mid + 1 
			else:
				return mid
		return -1
```

Time complexity: O(log n); space complexity: O(1). 

This approach uses **left-closed-right-closed interval**, which allows the target search to be equal to the left/right end value. As such, we need to 
1. Allow while loop condition as `left <= right` becase it needs to be exausted when `left = right`
2. When updating right between loops with if condition `target < nums[mid]`, right can be `mid - 1` as the current target can't be equal to right

The key to set up the sliding window is to keep a consistent definition of the window and consider edge cases, which is the [**Loop Invariant Condition**](https://gist.github.com/asabaylus/3071099#anchors-in-markdown). 



27. Remove element $\color{green}{\textsf{EASY}}$

> Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm). The order of the elements may be changed. Then return *the number of elements in* `nums` *which are not equal to* `val`.
Consider the number of elements in `nums` which are not equal to `val` be `k`, to get accepted, you need to do the following things:
> - Change the array `nums` such that the first `k` elements of `nums` contain the elements which are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
> - Return `k`.

```
//27. Remove element
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        n = len(nums)

        slow, fast = 0, 0
        while fast <= n-1 and slow <= fast:
            if nums[fast] != val:
                nums[slow] = nums[fast]
                slow += 1

            fast += 1
        return slow
```

Time complexity: O(n); space complexity: O(1). 






### [Loop invariant](https://gist.github.com/asabaylus/3071099#anchors-in-markdown)
A loop invariant is a condition [among program variables] that is necessarily true immediately before and immediately after each iteration of a loop. (Note that this says nothing about its truth or falsity part way through an iteration.)
A loop invariant is some predicate (condition) that holds for every iteration of the loop.

The loop invariant must be true:
1. before the loop starts
2. before each iteration of the loop
3. after the loop terminates
( although it can temporarily be false during the body of the loop ).
On the other hand the loop conditional must be false after the loop terminates, otherwise, the loop would never terminate.

A good loop invariant should satisfy three properties:

1. Initialization: The loop invariant must be true before the first execution of the loop.
2. Maintenance: If the invariant is true before an iteration of the loop, it should be true also after the iteration.
3. Termination: When the loop is terminated the invariant should tell us something useful, something that helps us understand the algorithm.

Loop Invariant Condition: 
Loop invariant condition is a condition about the relationship between the variables of our program which is definitely true immediately before and immediately after each iteration of the loop. 
