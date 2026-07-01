# DSA Question — Count Subarrays with Product Less Than K

Difficulty: Medium

## Problem
Given an array of positive integers nums and an integer k, return the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than k.

## Input
- nums: list of positive integers (1 <= len(nums) <= 10^5)
- k: integer (0 <= k <= 10^9)

## Output
- An integer representing the count of contiguous subarrays whose product is < k.

## Example
Input: nums = [10, 5, 2, 6], k = 100
Output: 8

Explanation: The 8 subarrays are: [10], [5], [2], [6], [10,5], [5,2], [2,6], [5,2,6]

## Constraints
- All numbers in nums are positive integers.
- Time complexity expected: O(n)
- Space complexity expected: O(1)

## Hint
Use a sliding window with two pointers and maintain the product of elements in the current window. When product >= k, move the left pointer to shrink the window.

## Solution Outline
1. If k <= 1, answer is 0 because product of positive integers is at least 1.
2. Initialize product = 1, left = 0, result = 0.
3. Iterate right from 0 to n-1:
   - Multiply product by nums[right].
   - While product >= k and left <= right:
       - Divide product by nums[left] and increment left.
   - All subarrays ending at `right` and starting between `left` and `right` (inclusive) have product < k. Add (right - left + 1) to result.
4. Return result.

## Sample Code (Python)
```python
def num_subarray_product_less_than_k(nums, k):
    if k <= 1:
        return 0
    prod = 1
    left = 0
    count = 0
    for right, val in enumerate(nums):
        prod *= val
        while prod >= k:
            prod //= nums[left]
            left += 1
        count += right - left + 1
    return count
```

Tags: sliding-window, two-pointers, arrays
