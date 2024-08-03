# Day 2 Array

## 1. Sliding window
### 209. Binary search $\color{orange}{\textsf{MEDIUM}}$

> Given an array of positive integers nums and a positive integer target, return the minimal length of a subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

> Example 1:
> Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.

```
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        n = len(nums)
        i, j = 0, 0

        temp_sum = 0
        min_len = float('inf')

        for j in range(n):
            temp_sum += nums[j]

            while temp_sum >= target:
                min_len = min(min_len, j-i+1)
                temp_sum -= nums[i]

                i += 1

        return min_len if min_len != float('inf') else 0

```
- Time: O(n); space: O(1)

The approach is a sliding windows. 
High-level idea to solve this problem includes:
1. the goal is to sum the adjacent elements
2. constraint 1: `sum` is valid only when `sum >= target`
3. constraint 2: the length of these adjacent elements should be the smallest

In the sliding window, i (i.e., left bound) and j (i.e., right bound) form an interval just like the fast-slow 
   pointers. Because the adjacent elements have to be a sub-array and all elements are positive, we can rule out 
   negative value being summed. Therefore, the sliding machanism is:
1. expand the window from left to right -> start from right bound moving rightwards
2. when 'sum >= target', the left bound can be moved towards right -> to narrow the window
3. after narrowing the window, once `sum < target`, extend the right bound one more step rightwards
4. update `sum` accordingly



















