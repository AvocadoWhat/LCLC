# Day 1 Array

## 1. Binary Search
204. Binary search

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
