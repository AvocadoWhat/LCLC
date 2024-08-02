# Day 1 Array

## 1. Binary Search
### 704. Binary search $\color{green}{\textsf{EASY}}$

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

The key to set up the sliding window is to keep a consistent definition of the window and consider edge cases, which is the [**Loop Invariant Condition**](#head_loop_invariant). 



### 27. Remove element $\color{green}{\textsf{EASY}}$

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

This approach uses **slow-fast-pointers (two pointers)**, in which the `while` loop condition states `fast <= n-1 and 
slow <= fast`. Because as long as `slow` is not faster than `fast`, and fast doesn't exceed n, the loop should go on. 
Pointers update logics:
1. the slow pointer update logic is when there isn't a match between the fast pointer and val
2. the fast pointer update logic is when there is a match between the fast pointer and val
3. because when the fast is ahead of slow, an array update is needed: value at slow should be the non-val value in 
   history that the fast pointer visited (equivalent to remove the element that equals `val`)
4. the value update should happen before slow pointer update


### 977. Squares of a sorted array
> Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted 
> in non-decreasing order.
>
> Example 1:
> Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].

```
# 977. Squares of a sorted array
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        n = len(nums)
        i, j = 0, n-1

        res = [0] * n
        k = n-1
        while i <= j:
            if nums[i] ** 2 > nums[j] ** 2:
                res[k] = nums[i] ** 2
                i =+ 1
            else:
                res[k] = nums[j] ** 2
                j -= 1
            k -= 1
            
        return res
```
Time complexity: O(n); space complexity: O(1). 

**Two pointer** approach -> narrowing window. 
* The precondition is this is a sorted array, and the square is the largest either of the left most or the right most 
element. Therefore, the comparing is simplified as only between the left or right most element's square (equivalent 
to their abs values).
* Secondly, to construct a container before the loop, we can use `[float('inf')] * n` (in this problem, `[0] * n` also 
  serves the purpose as the smallest squared value is zero).


### <a name="head_loop_invariant"></a>Loop invariant
A loop invariant is a condition [among program variables] that is necessarily true immediately before and 
immediately after each iteration of a loop. (Note that this says nothing about its truth or falsity part way through 
an iteration.)
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
Loop invariant condition is a condition about the relationship between the variables of our program which is definitely
true immediately before and immediately after each iteration of the loop. 
